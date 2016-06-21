# Overview

# General guide

## Better coding
#### Self sustaining code
Functions and classes shoudl be, where possible, independent on other classes and inputs. If a function requires a special input that only another function provides, there is then a question whether it wouldn't be better to combine both. Exception is usually preprocessing.

Use default types where possible - don't pass classes or structs or lists into toher functions if not absolutely necessary. It makes code effective but also less understandable as you look at a function which accepts list of settings and its not clear what that list contains. Comments in the function with description of the list create useless texts, as the list is already defined elsewhere and makes everything bloated and hard to sustain. Imagine that you want to make change to the list structure, remove fields etc - then you need to look for all functions that used it and check, if they still work - boring and bothersome.
```matlab
settings = struct()
settings.channels = 64
settings.outcome = 'matrix'
selectmatrix(data, settings) % BAD style - doesn't raise errors and warning and needs high control on the selectmatrix function side. Also, can lead to settings definitions far away from the function which reduces reading flow. Also, it is LONG!

selectmatrix(data, 'channels', 64, 'outcome', 'matrix') % GOOD - clear what it does, can be easilly controlled in the function. One line as well.
```

Use defensive programming!
Defensive programming is writing code that reports errors and doesn't allow to fail in the middle just because. It is extremely important especially in languages as matlab, R, javascript etc. that allow non typed variables to be accepted - eg.g user can pass matrix instead of value by mistake and function will allow it. Defensive programming is also paramout in all cases where users directly interact with functions. It is not as important in functions that only other functions call.

defensive programming can be iumplemented by assertions as well as clearly stating what type of variable you expect and what you return
```matlab
% FUNCTION to return first character of given string
function[output] = rtrnfrstch(input) %BAD - not clear what shoudl go in and what to expect
  output = input(1) %BAD - what if input is a struct?
end

%GOOD
function [outputCharacter] = returnfirstletter(inputString)
  assert()
  if ~character(inputString)
    warning() %well defined matlab warning message
  end
  outputCharacter = inputString(1)
end
```

```matlab
function [character] = returnfirstletter(inputString)
end
```
### Flow
Don't use while unless you are a absolutely sure what you are doing.

### Comments
General rule is that every comment in flow points to poorly written code. If you use non standard naming conventions, non standard input types etc. then you need comments. But at that time it's important to ask a question, shouldn't I rather rewrite the code behind?

If you can't, or the functions do not make sense, then add comments.

### Functions
- Functions should be self sustained where possible. Should not depend on other functions or inputs that are not of basic types (integer, string, list etc.).
- functions should validate input where error can be expected
- function should not depend on specific input of other functions if possible - this can lead to confusion in complex functions as matlab or R doesn't well implement namespaces and classes

- naming should be preserved throughout functions if possible (if one function accepts "header" as parameter, the passing script should also pass in header variable)
- functions should be short (under 60 lines) and do a single thing

## Naming conventions
These are some of the naming conventions that deal with clarity of the text. Please refer to each individual programming language for specifics of naming.

### Variables
Things should be named clearly, uniquely.
```matlab
ch = 3 %BAD
channel = 3
selCh_i = [5:10]  %BAD
selectedChannelsIndices = [5:10] %GOOD
```
Namig should reflect what will reside inside, therefore keep plurals, indicate if it will be a number or string, etc.
```r
results = data.frame(id = c(1:100), height = seq())

carIndex = c(2,3,4) #BAD - should be carIndices
completeCases = c(1:54, 67:98) #SEMI-GOOD - better use of plural, but we don't know if it talks about rows, list indices, referencing table column
completeCasesRows =  c(1:54, 67:98) #GOOD
resultsTable[completeCaseRows, ] #simple selection

completeCasesId = c(1:54, 67:98) #GOOD
results[results$id %in% completeCasesId, ] #selection based on id
```
