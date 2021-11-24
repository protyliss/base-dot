# Filter String

String Expression for Multiple Conditional Filtering of Data

* URL Safe with Search String
* Shorten as Possible

## Combination

* [Period String](period-string.md)
* [Digit Timestamp](timestamp-digit.md)

## Expression

### `;` - And:

```regexp
[CONDITION](;[CONDITION])*
```

* foo:1;bar:2

### `/` - Or:

```regexp
[CONDITION](/[CONDITION])*
```

* foo:1/bar:2

``

### CONDITION

```regexp
[TARGET]:[KEYWORD]
```

* foo:1

### TARGET

```regexp
[_a-zA-Z][_a-zA-Z0-9]*
```

* foo
* bar1
* _baz

### KEYWORD

```regexp
[^!',:*]+
```

* foo
* bar

#### `!` - Not:

```regexp
![KEYWORD]
```

* !foo
* !bar

#### `''` - Strong Equal:

```regexp
'[KEYWORD]'
```

* 'foo'
* 'bar'

#### `'` - Starts with:

```regexp
'[KEYWORD]
```

* 'foo
* 'bar

#### `'` - Ends with:

```regexp
[KEYWORD]'
```

* foo'
* bar'

#### `,` - Or:

```regexp
[KEYWORD]+(,[KEYWORD])?
```

* foo,bar

#### `:` - And:

```regexp
[KEYWORD]+(:[KEYWORD])?
```

* foo:bar

#### `~` - BETWEEN

```regexp
[KEYWORD]~[KEYWORD]
```

#### `~` - GREATER THAN

```regexp
~[KEYWORD]
```

#### `~` - LESS_THEN

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

---

## Dynamic Input KEYWORD

When keywords are entered by regular human, not a Developer. (Such as FORM)
Using readable, meaningful words rather than operator symbols.

If Keyword has Operator Symbols, will be escaped for to keep itself.

* `foo OR bar` => `foo,bar` :
* `foo AND bar` => `foo:bar`
* `NOT foo` => `!foo` :
* `!:;/,*` => `!!!:!;!/!,!*`
