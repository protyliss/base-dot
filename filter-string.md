# Filter String

String Expression for Multiple Conditional Filtering of Data

* URL Safe with Search String
* Shorten as Possible

## Combination

* [Period String](period-string.md)
* [Digit Timestamp](timestamp-digit.md)

## Expression

```regexp
[TARGET]:[KEYWORD]([;/][TARGET]:[KEYWORD])*
```

* Next Condition Starts with `;` - AND
* Next Condition Starts with `/` - OR

### TARGET

```regexp
[_a-zA-Z][_a-zA-Z0-9]*
```

### KEYWORD

```regexp
!?'?[^,:;/]'?+([,:]!?'?[^,:;/]'?)*
```

* Starts with: `!` - NOT
* Next Keyword Starts with `,` - OR
* Next Keyword Starts with `:` - AND
* ` `(Space) Replace to `*`

#### BETWEEN

```regexp
[KEYWORD]~[KEYWORD]
```

#### GREATER THAN

```regexp
~[KEYWORD]
```

#### LESS_THEN

```regexp
[KEYWORD]~
```

---

### Examples

|Field|Type|
|---|---|
|foo|integer|
|bar|integer|
|baz|string|

#### `foo:1`:

```SQL
SELECT *
FROM TABLE
WHERE foo = 1  
```

#### `foo:1;bar:!2`:

```SQL
SELECT *
FROM TABLE
WHERE foo = 1
  AND bar <> 2
```

#### `foo:1,2/bar:3:4`:

```SQL
SELECT *
FROM TABLE
WHERE (foo = 1 OR bar = 2)
   OR (bar = 3 AND bar = 4)
```

#### `foo:1~10`

```SQL
SELECT *
FROM TABLE
WHERE foo BETWEEN 1 AND 10
```

#### `baz:1`

```SQL
SELECT *
FROM TABLE
WHERE foo like `%1%`
```

#### `baz:1*2`

```SQL
SELECT *
FROM TABLE
WHERE foo like `%1 2%`
```

#### `baz:'1*2*3'`

```SQL
SELECT *
FROM TABLE
WHERE foo like `1 2 3`
```
