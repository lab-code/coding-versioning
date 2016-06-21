#Versioning

## Tutorials

## General rules for versioning
- Small commits of single files are preferable to large features. Large features should reside in feature branch.

### Branching
- Every large piece of code should reside in branch

#### Basic flow
- Never commit to master! Pull or merge to master.
- Master should optimally never fail or have bugs. If there are bugs in your code, fix them and them pull to master.
- Master doesn't need to have all the features. It needs to be stable.
- All coding should be done in feature branches and pulled to develop.
#### Merging your own repos
- When issues are resolved, develop will be pulled to master and released.

#### Pull requests
- before pull request, check if the target branch is updated in your repo
- before pull reuqest is issued, you should try rebasing on develop and check if it works
- Bugfix commits should be presented as such.

- No dependent code should be pulled into develop - all issues with file dependencies should be fixed in features before pull request.
