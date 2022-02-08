# Filter Expression

> Specification Version 2.1

String Expression for Multiple Conditional Filtering of Data

## Combination with

* [Timestamp Expression](TIMESTAMP_EXPRESSION.md)
  * [Period Expression](PERIOD_EXPRESSION.md)

---

## Condition

| Character |         Meaning         |
|:---------:|:-----------------------:|
|     :     | Target and Keyword Glue |

Condition is a pair of Target and Keyword.

```regexp
([^:]):([^;/]+)
```

> Group 1 is named as Target, Group 2 is named as Keyword

* `foo:a`: `foo` value includes `a`
* `bar:b`: `bar` value includes `b`

### Multiple Condition

| Character | Meaning |
|:---------:|:-------:|
|     ;     |   And   |
|     /     |   Or    |

Single Condition are combined with `And` and `Or`

```regexp

([^:]):([^;/]+)([;/]([^:]):([^;/]+))*
```

* `foo:a;bar:b`: `foo` value includes `a` __AND__ `bar` value includes `b`
* `foo:a/bar:b`: `foo`value includes `a` __OR__ `bar` value includes `b`

### Condition Grouping

| Character |   Meaning   |
|:---------:|:-----------:|
|     (     | Group Start |
|     )     |  Group End  |

Using parenthesis to make Detail Condition

```regexp
(([^:]):([^;/]+)([;/]([^:]):([^;/]+))*)([;/](([^:]):([^;/]+)([;/]([^:]):([^;/]+))*))*
```

* `(foo:a;bar:b);(baz:c/qux:d)`: `foo` value is 'a' AND `bar` value is 'b' __AND__ `baz` value is 'c' OR __qux__ value
  is 'd'
* `(foo:b;bar:b)/(baz:c/qux:d)`: `foo` value is 'a' AND bar value is 'b' __OR__ `baz` value is 'c' OR `qux` value is 'd'

## Target Expression

* Database Column(Field)
* Control Name(ID)
* Variable Name
* ...

```regexp
[_a-zA-Z][_a-zA-Z0-9](\.[_a-zA-Z][_a-zA-Z0-9])*
```

## Keyword Expression

```regexp
[^;/]
```

### Operators

#### Anywhere

| Character | Meaning |
|:---------:|:-------:|
|     *     |  Space  |

* `foo:a*b:`: `foo` value includes 'a b'

#### Starts with

| Character |   Meaning    |
|:---------:|:------------:|
|     !     |     Not      |
|     '     | Starts With  |
|     ~     | Greater than |

* `foo:!a`: `foo` value not includes 'a'
* `foo:b`: `foo` value starts with 'b'
* `foo:!'c`: `foo` value not starts with 'c'

#### Between with

| Character | Meaning |
|:---------:|:-------:|
|     ~     |  Range  |

* `foo:1~10:`: `foo` value is greater than '0' and less than '11'

#### Ends with

| Character |  Meaning  |
|:---------:|:---------:|
|     '     | Ends With |
|     ~     | Less Than |

* `foo:a'`: `foo` value ends with 'a'

### Multiple Keyword

| Character | Meaning |
|:---------:|:-------:|
|     :     |   And   |
|     ,     |   Or    |

* `foo:a:!b`: `foo` value includes 'a' and not includes 'b'
  - aa
  - ac
  - ad
  - ae
  - ...
* `foo:'a:b'`: `foo` starts with 'a' and ends with 'b'
  - ab
  - a1b
  - a2b
* `foo:1,2` `foo` value is '1' or '2'

### Keyword Grouping

| Character |   Meaning   |
|:---------:|:-----------:|
|     (     | Group Start |
|     )     |  Group End  |

* `foo:('a,'b):(a':b')`: `foo` value (starts with 'a' or 'b') and (ends with 'a' or 'b')
  - aa
  - ab
  - ba
  - bb
  - a1
  - b2
  - ~~c3~~
  - 1a
  - 2b
  - ~~3c~~
* `foo:(a,('b,'c);(d,(e',f'))`: `foo` values (includes 'a' or (starts with 'b' or 'c')) or (includes 'd' or (ends with 'e' or 'f'))
  - a
  - b
  - c
  - d
  - e
  - f
  - ~~g~~
  - ~~h~~
  - b1
  - c2
  - ~~e3~~
  - ~~f4~~
  - ~~1b~~
  - ~~1c~~
  - 1e
  - 1f

## Example with SQL

```text
foo:a
```

> ```sql
> SELECT * FROM table WHERE foo = '%a%'
> ```

```text
foo:a;bar:b
```

> ```sql
> SELECT * FROM table WHERE foo = '%a%' AND bar = '%b%'
> ```

```text
foo:a/bar:b
```

> ```sql
> SELECT * FROM table WHERE foo = '%a%' OR bar = '%b%'
> ```
>

```text
(foo:a;bar:b);(baz:c)
```

> ```sql
> SELECT * FROM table WHERE (foo = '%a%' AND bar = '%b%') OR (baz = '%c%')
> ```
