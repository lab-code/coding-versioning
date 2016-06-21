# Overview

# General guide

## Better coding

### Flow
 Don't use while unless you are a absolutely sure what you are doing.

### Comments
General rule is that every comment in flow points to poorly written code. If you use non standard naming conventions, non standard input types etc. then you need comments. But at that time it's important to ask a question, shouldn't I rather rewrite the code behind?

If you can't, or the functions do not make sense, then add comments.

### Functions
- Functions should be self sustained where possible. Should not depend on other functions or inputs that are not of basic types (integer, string, list etc.).
- functions should validate input where error can be expected
- function should not depend on specific input of other functions if possible - this can lead to confusion in complex functions as matlab or R doesn't well implement namespaces and classes
```matlab
settings = struct()
settings.channels = 64
settings.outcome = 'matrix'
selectmatrix(data, settings) % BAD style - doesn't raise errors and warning and needs high control on the selectmatrix function side. Also, can lead to settings definitions far away from the function which reduces reading flow. Also, it is LONG!

selectmatrix(data, 'channels', 64, 'outcome', 'matrix') % GOOD - clear what it does, can be easilly controlled in the function. One line as well.
```
- naming should be preserved throughout functions if possible (if one function accepts "header" as parameter, the passing script should also pass in header variable)
- functions should be short (under 60 lines) and do a single thing

## Naming conventions
These are some of the naming conventions that deal with clarity of the text. Please refer to each individual programming language for specifics of naming.

### Variables
Things should be named clearly, uniquely
```matlab
  ch = 3 %BAD
  channel = 3
  selCh_i = [5:10]  %BAD
  selectedChannelsIndices = [5:10] %GOOD
```
# Language dependent styles

## Matlab
### Naming conventions
- functions in matlab are for some reason written as smallcase only, but let's keep it that way
```matlab
getMeSandwich('tuna with egg') %BAD - c# style
get_me_sandwich('tuna with egg') %BAD - php style
getmesandwich('tuna with egg') %GOOD - matlab style
```
- variables can vary uppercase and lowercase letters. Global should start with uppercase, local with lowercase
```matlab
channel_number %BAD - r style, php style - not a good style
channelnumber %BAD - this means I am looking at a function
channelNumber %GOOD
```
- variables should respect if they are an array of a single value and use plural or singular
- variables starting with n or i mean number of or index of only
```matlab
nChannel = 8 %BAD - if this is number of channels, it should be in plural
channelIndex = [5:6] %BAD - shoudl be in plural channelIndices
iChannel = 5
iChannels = [4] %GOOD as well as we might add channels to arary
iChannels = [4 5]
channelIndex = 7
nChannels = 64
```
## Python
## R
