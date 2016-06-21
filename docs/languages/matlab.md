## Matlab
### General overview
### Naming conventions
Functions in matlab are for some reason written as smallcase only, but let's keep it that way
```matlab
getMeSandwich('tuna with egg') %BAD - c# style
get_me_sandwich('tuna with egg') %BAD - php style
getmesandwich('tuna with egg') %GOOD - matlab style
```
Variables can vary uppercase and lowercase letters. Global should start with uppercase, local with lowercase
```matlab
channel_number %BAD - r style, php style - not a good style
channelnumber %BAD - this means I am looking at a function
channelNumber %GOOD
```
Variables starting with n or i mean number of or index of only
```matlab
nChannel = 8 %BAD - if this is number of channels, it should be in plural
channelIndex = [5:6] %BAD - shoudl be in plural channelIndices
iChannel = 5
iChannels = [4] %GOOD as well as we might add channels to arary
iChannels = [4 5]
channelIndex = 7
nChannels = 64
```
### Folder structure and dependencies
Matlab doesn't have forced folder structure but as it uses single files for each function, its structure is more important than in R or Python.
There aren't any strict conventions. Just try to separate functions that do the think package wants to do and those that only support its functionality. For example, functions that extract strings or search for the smallest common denominator in a package that deasl with EEG synchronising can easilly reside in a separate folder. I personally try to keep number of matlab files in each folder under 10.
