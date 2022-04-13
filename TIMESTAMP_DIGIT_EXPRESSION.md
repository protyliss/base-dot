# Timestamp Digit

> Specification Version 2.0

Digit Expression for Timestamp and Timezone

## Expression

```regexp
[+-]?\d{4}\d{2}\d{2}(\d{2}(\d{2}(\d{2}(\d+)?)?)?)?(\.\d+)?
```

* yyyy
* yyyymm
* yyyymmdd
* yyyymmddhh
* yyyymmddhhii
* yyyymmddhhiiss
* yyyymmddhhiissu
* yyyymmddhhiissuuu
* yyyy.z
* yyyymm.z
* yyyymmdd.z
* yyyymmddhh.z
* yyyymmddhhii.z
* yyyymmddhhiiss.z
* yyyymmddhhiissu.z
* yyyymmddhhiissuuu.z
* -yyyy.z
* -yyyymm.z
* -yyyymmdd.z
* -yyyymmddhh.z
* -yyyymmddhhii.z
* -yyyymmddhhiiss.z
* -yyyymmddhhiissu.z
* -yyyymmddhhiissuuu.z

## Examples

### Year to Date as Default

1234-12-12T00:00:00.000+00:00:

```regexp
12341212
```

### Year to Hour

1234-12-12T12:00:00.000+00:00:

```regexp
1234121212
```

### Year to Microseconds

1234-12-12T12:12:12.123+00:00:

```regexp
123412121212123
```

### Year to Timezone

1234-12-12 12:12:12.123+09:00

```regexp
123412121212123.09
```

1234-12-12 12:12:12.123-09:00

```regexp
-123412121212123.09
```
