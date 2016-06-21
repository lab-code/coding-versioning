# Rewriting R code
Have a look at the following simple code control.
```r
  d = 0
  wkd = 7
  w = 0
  nd = 0
  y = 0
  while(nd < 1000){
    d = d + 1
    if (d == wkd){
      d = 0
      w = w + 1
    }
    nd = nd + 1
    if (d == 365){
      y = y + 1
    }
  }
  print(w)
  print(y)
```

In the end you probably figured out what it does. It basically counts the number of days and weeks in the 1000 days that begin the statement. Well, the truth is, that you read it and have no idea what is happening. THat is bad. Nobody can fix if something goes wrong. There might be bug inside that you miss and you have no idea where - and there is a bug in the code. So what you happen if we just fix it with comments?

```r
  #day counter
  d = 0
  #days in a week
  wkd = 7
  #number of weeks
  w = 0
  #number of days
  nd = 0
  #number of years
  y = 0
  while(nd < 1000){
    d = d + 1 #add a day
    if (d == wkd){ #check if week
      d = 0
      w = w + 1 #add 1 to weeks
    }
    nd = nd + 1 #add counter
    if (d == 365){ #check if days equal number of days in a year
      y = y + 1 #add one to year
    }
  }
  print(w)
  print(y)
```
Did I solve something? No. I made thing worse, less readable and longer. So let's make it slightly better.
```r
  dayCounter = 0
  daysInWeek = 7
  nWeeks= 0
  nDays = 0
  nYears = 0
  while(nDays < 1000){
    dayCounter = dayCounter + 1
    if (dayCounter == daysInWeek){
      dayCounter = 0
      nWeeks = nWeeks + 1
    }
    nDays = nDays + 1
    if (dayCounter == 365){
      nYears = nYears + 1
    }
  }
  print(nWeeks)
  print(nDays)
```
Suddenly we don't need comments and also the bug is immediatelly clear.
```r
if (dayCounter == 365){
  nYears = nYears + 1
}
```
Should be
```r
if (nDays == 365){
  nYears = nYears + 1
}
```
But we can make things even better. Days in week is a constant, so we mark it as such. Also, days in week are variable but days in year are not. That is inconsistent. So following is more clear
```r
DAYS_IN_WEEK = 7
DAYS_IN_YEAR = 365
```
Rewrite one line if for shorter code (if the language allows it)
```r
if (dayCounter == 365) nYears = nYears + 1
```
And most importantly, put everything that does one thing into a function. Now the problem with R is that id doesn't allow two outputs from function, so we need to be smart about it. One option is to write two functions.
```r
function = WeeksInDays(nDays){
  DAYS_IN_WEEK = 7
  dayCounter = 0
  nWeeks = 0
  for(i in 1:nDays){
    dayCounter = dayCounter + 1
    if (dayCounter == DAYS_IN_WEEK){
      dayCounter = 0
      nWeeks = nWeeks + 1
    }
  }
  return(nWeeks);
}
function = YearsInDays(nDays){
  DAYS_IN_YEAR = 365
  dayCounter = 0
  nYears = 0
  for(i in 1:nDays){
    dayCounter = dayCounter + 1
    if (dayCounter == DAYS_IN_YEAR){
      dayCounter = 0
      nYears = nYears + 1
    }
  }
  return(nYears);
}
print(WeeksInDays(1000))
print(YearsInDays(1000))
```
Now that looks better but actually, for loop is crap to do such thing. Always try to thing if there is simple sollution that uses less lines of code. Formely it was paramount to write economic code, but now readibility is preffered. So what about modulo?
```r
function = WeeksInDays(nDays){
  DAYS_IN_WEEK = 7
  remainderDays = nDays %% DAYS_IN_WEEK
  nWeeks = (ndays - remainderDays) / DAYS_IN_WEEK
  return(nWeeks);
}
function = YearsInDays(nDays){
  DAYS_IN_YEAR = 365
  remainderDays = nDays %% DAYS_IN_YEAR
  nYears = (ndays - remainderDays) / DAYS_IN_YEAR
  return(nYears);
}
print(WeeksInDays(1000))
print(YearsInDays(1000))
```
And as a last touch, we see there is duplicit code, so let's deal with it right now.
```r
function = DivideWithoutRemainder(num1, num2){
  remainder = num1 %% num2
  return((num1 - remainder) / num2)
}
function = WeeksInDays(nDays){
  nWeeks = DivideWithoutRemainder(nDays, 7)
  return(nWeeks);
}
function = YearsInDays(nDays){
  nYears = DivideWithoutRemainder(nDays, 365)
  return(nYears);
}
print(WeeksInDays(1000))
print(YearsInDays(1000))
```
This created legible structured code that is easy to maintain as well as understand. Didn't we go quite a trip from the horrific start?
