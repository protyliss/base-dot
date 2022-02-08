# Period Expression

> Specification Version 2.0

String Expression for Date Period with Timezone

## Combination with

* [Timestamp Expression](TIMESTAMP_EXPRESSION.md)

---

## Condition

### Between

| Character |           Meaning            |
|:---------:|:----------------------------:|
|     ~     | Begin Time and End Time Glue |

```regexp
([0-9]{6,})~([0-9]{6,})
```

> Group 1 is named as Begin Time, Group 2 is named as End Time


### After Begin Time

```regexp
[0-9]{6,}~
```

### Before End Time

```regexp
~[0-9]{6,}
```
