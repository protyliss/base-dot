# Date Modify Expression

String Expression for Modify Time

```regexp
([+-]\d+\s*(y(ear(s)?)|m(onth(s)?)|d(ate(s)?)|h(our(s)?)(i|minute(s)?)|s(ec(ond(s)?)?)?))+
```

## Units

* y
* year
* years
* m
* month
* months
* d
* date
* dates
* h
* hour
* hours
* i
* min
* minute
* minutes
* s
* sec
* second
* seconds

## Examples

__after 30 seconds__:

* `+30s`
* `+30sec`
* `+30second`
* `+30seconds`

__yesterday__:

* `-1d`
* `-1date`
* `-1dates`

__tomorrow__:

* `+1d`
* `+1date`
* `+1dates`

__previous month__:

* `-1m`
* `-1month`
* `-1months`

__next month__:

* `+1m`
* `+1month`
* `+1months`
