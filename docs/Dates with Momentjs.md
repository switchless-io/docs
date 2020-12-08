# Date operations with moment
Keyowrds :[[dates]][[moment]][[patterns]]



## Creating a date object
```
// Current date-time
var date1=moment()
// Moment<2020-12-08T10:28:26+05:30>

// Create date from string
var date1=moment('2020-12-08')
// Moment<2020-12-08T00:00:00+05:30>

// Cloning
var date2=moment(date1) 
// Moment<2020-12-08T10:28:26+05:30>

```

## Can I use moment date object for creating a date entry for postgres timestamptz type?
Yes. It'll come out exactly as expected:
![[Pasted image 20201208105725.png]]


## Beginning / end of a period oprations
```//Start of day
date2.startOf('day')
// date1: Moment<2020-12-08T10:30:16+05:30>
// date2: Moment<2020-12-08T00:00:00+05:30>


// End of day
date2.endOf('day')
// Moment<2020-12-08T23:59:59+05:30>


//similar operation for months
```

## Difference between dates 
```
// 1. Same day from start to end
date1=date1.startOf('day')
date2=date2.endOf('day')
diff=date2.diff(date1,'days')
// = 0


// 2. Month beginning to end

date1=date1.startOf('month').startOf('day')
//Moment<2020-12-01T00:00:00+05:30>

date2=date2.endOf('month').endOf('day')
//Moment<2020-12-31T23:59:59+05:30>


diff=date2.diff(date1,'months')
// = 0
diff=date2.diff(date1,'days')
// = 30

```