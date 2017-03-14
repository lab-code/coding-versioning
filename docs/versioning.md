#Versioning
To illustrate, what versioning is and what it does, versioning is the whole idea behind google docs rewind features and revisions in any modern text editors. Rather than overwriting each version with a new one and resaving the former with hyperbolic name such as `final_version3.4_february_name.docx`, we save everything in a single file and keep the history of that file in a versioning system. We can then see who changed what and when, reload working code if it suddenly breaks, trace errors to incompetent people and all that jazz. So it is nothing short of amazing. Let's get started.

## Tutorials
There are many already well done tutorials on the subject and I recommend to go through them before you go any further. Information in this section should be used as a general tips, rather than teach you how to do things. You should be familiar with staging, committing, pushing, pulling and branching, before you check these tips.

- [Interactive from github](https://try.github.io/levels/1/challenges/1)
- [No deep shit!](http://rogerdudler.github.io/git-guide/)
- [Slightly deeper](https://www.atlassian.com/git/tutorials)
- [And a last one](http://rypress.com/tutorials/git/index)

### On git software
There are many amazing git GUIs, such as [GitKraken](https://www.gitkraken.com/) or [SourceTree](https://www.sourcetreeapp.com/) and I wholeheartedly recommend using them. But learn git from the scratch. If you need help and will search for it online, nobody will direct you towards what button to push. People will tell you what commands to run, so it is good to know those basics.

### What commands you shoudl know
Before getting deep into git, you shoudl be familiar with these commands
```
git add [--all] 
git commit [-a -m] 
git branch [-a -l -d -D] 
git log [<sha>]
git checkout [<branch>] [<commit>]
git remote [add set-url]
git clone [<what>] [<where>]
git push [<remote> <branch>]
git reset [<what>][--hard]
git fetch [<remote>] 
git pull [<remote/branch>]
git merge [<branch>]
git help [<something>]
```

## Committing
One thing to keep in mind at all times is, that **"Commits are not just saves".**

Unlike save, they are non stationary in time. They allow insight into code development, reasoning behind many not so obvious design steps and allow to debug and pinpoint possible errors better than any save would. Do not use commits as saves. For saving purposes, use [releases](#releases).

- [Commit messages should be descriptive and clearly stated](#commit-messages)
- [Each commit should be localised to a single issue or a problem](#commit-problem)
- [Small commits of single files are preferable to large features](#commit-size)
- [Imports of plugins or new packages should be done in a single commit](#committing-imports)

### Commit messages
_Each commit should convey its purpose clearly._

Same as issues with naming presented in [coding-style](coding-style.md#naming-conventions), messages in commit history such as "Better charts" can be contextually relevant, but are usually useless. If possible, it should be obvious what that commit does. In personal projects, this is quite common to forget and disregard, but in major collaborative projects, necessary to abide by.

> I have many times sinned when doing personal projects and committed pieces of code with simply "it works" or "finally fixed?" "maybe fixed" "now fixed" or "need to go home, not time to describe what this does but its awesome" Messages. These were simply reactions to my frustrations or time pressure. It is at those times that I violated my own principles, commits are not saves.

### Commit content
_Each commit should be localised to a single issue or a problem._

This is often difficult to do, as we figure out why some piece of code isn't working by finding out, that many other parts of the code aren't working. Or the  change we need to do requires to change much more than just a single file. In such cases, it is recommended to stash, checkout a new branch and work on this  rewrite separately. As a general rule of thumb, if you follow the previous rule of commit messages well, and your message contains a word AND, you should think whether it is not better to separate into two separate commits.

> Again, I have sinned many times in personal project and committed multiple files without any meaningful message at once. This is usually because of time pressure and necessity to commit before I leave. In such circumstances, I recommend checking out a new branch, and rebasing the next dat.

### Commit size
_Small commits of single files are preferable to large features. Large features should reside in feature branch._

This is closely related to the previous rule, but its so important it is necessary to rephrase and state again. It doesn't mean to checkout a branch and then do a massive commit. This means, that development of larger features might take longer time and therefore it is good to keep it clean and separate from the master not to break or detriment the general flow of the project.

### Committing imports
_Imports of plugins or new packages SHOULD be done in a single commit._

Sometimes people misinterpret previous rules and import packages file by file, commenting every time a new file is added. This is not a good approach because it bloats the log as well as possibly BREAKS the branch. If separate files in the package depend on other files, these commits, when checked out, will be logically broken. Therefore large unmodified packages should be imported as one.

Now when you import some code, it usually happens that this code needs changing. It is genuinely good idea to separate imported original code from the changes you made, so people may see what was different before you started tweaking it.

## Branching
Branching is a must do in effective git use. It allows separation of non functional, experimental code from the working core, it allows effective collaboration, merge requests, easy switching between problems and much more. There isn't anything world changing in how you branch, just follow the main rules of committing and have these simple rules in mind.

- [Branches are used for experimenting or modifying the code](#branch-content)
- [If possible, branches should be kept in sync with master](#branch-updating)

### Branch content
_Branches are used for experimenting or modifying the code._

This seems more like a description, but it is important to state. Branches are not for keeping different releases and or project versions. I know some people who use branches to keep Python and C controllers of their hardware in one project. I strongly recommend against such practices. Although your code might have some similar libraries and structure, it is better to use [submodules](#submodules) for such work then branches. It gets messy over time and although it can be done, usually you are just safer in starting two projects and keeping such a different code separate. I know google does it differently, but leave it to them :)

> There are many reasons why to do this, but the most common issue you run into if you mix multiple languages and projects, is the gitignore file. Remember, that .asv file are not kept in Matlab commits, therefore when you switch branches, they remain, because they are not versioned. So if you don't ignore them in your python .gitinore, you might inadvertantly commit them to repo.

### Branch updating
_If possible, branches should be kept in sync with master_

While you are working on a feature or restructuring old code, you should still keep in touch what is happening on master. Once you create a branch and overrite parts of master branch code, you don't have to worry about merging. Git know that you hve changed those pieces of code and will merge any master update appropriately. Just merge master from time to time to your branch or check conflicts with it. You will have to do so when creating pull requests anyway and this will save you a lot of trouble, as two weeks later merges can get really huge and messy.

### Branch logic
There are several standard ways of how branching can work. Two the most known are something I am going to refer to as [Feature](https://www.atlassian.com/git/tutorials/comparing-workflows#feature-branch-workflow) style and the other is [GitFlow](https://www.atlassian.com/git/tutorials/comparing-workflows#gitflow-workflow).
Personally I tried the GitFlow few years ago and it was too convoluted and complicated for any small team projects, so I do not recommend it in research environment.

Feature approach is quite simple and made even easier by GitHub, Bitbucket and others. It follows the general idea that each feature shoudl be in its own branch, just as GitFlow presumes. These branches has to be keep in synch with the master branch as it gets updated and when they are ready, user merges the branch into master. This merge HAS to be without conflicts. Any conflicts with the master need to be resolved on the feature branch before merge is done. Git will take care of the rest afterwards.

## Pushing and fetching
Pushing and fetching is usually without any issues if you work on your own project and remember what you are working on. There are only few caveats, but the main things to keep in mind are in section about [collaborating](#collaborating).

- [How to use pull and fetch properly](#pull-vs-fetch)
### Pull vs fetch
As you might know, git has two commands for getting stuff from the remote repository. Fetch only "fetches" repositry state from the remote, whereas pull does fetch and then immediatelly merges it to current branch - if the remote local connection is known.

General recommendation is to do fetch and then merge. Generally it doesn't matter as long as you don't expect any merge issues or you are sure you can resolve thm quickly. It is a good practice to do fetch and merge if you are working on larger public repositories.

## Merging
Merging goes quite differently when you work on your own private project without anybody interfering or when you work on project with multiple people. This section is dedicated only to good practices how to deal with your own repositories. For Collaboration, see [below](#collaborating).

Despite it is debatable, I won't include the intricacies of gt rebase. More about git rebase can be found [here](https://www.atlassian.com/git/tutorials/merging-vs-rebasing). 

Also, have in mind the difference between `git merge` and `git merge --no-ff`. If you are workign on a single project by yourself or a small team, you will probably be able to pull just by moving the HEAD forward. But it is up to personal or team preference, if those merges shoudl be done as a mere sequential changes (similar to `git rebase`) or if you want a new merged commit to be created. Remember that pull requests create new commits regardless even when the commits have same history.

### Merging your own repos
Mergin yor own repos is usually the least problematic thing to do. You can usually get it done by a simple fast-forward commit, if you are not working on several branches at once and keep fogetting the changes you do to each one.

If you cannot do simple non-conflicting merges in your own repo, maybe its time to think about a new approach.

Remeber that you can do do pull requests in personal repos as well. It is a good practice to push to remote branchs, do and close a pull request online on that branch and then pull the resulting master back home. 

## Rebasing
Rebasing can be useful tool and it comes into play when there are tens to hundreds of people working on a single project. Despite that, I don't rebase too often. Sometimes I do rebase on master branch if many changes have been made, but overall I generally only use interactive rebase to clean up history before pulling. Checkout `git rebase -i`

## Collaborating

- [How the common flow goes](#basic-flow)
- [Never commit to master!](#never-commit-to-master)
- [Master never fails](#master-never-fails)
- [How to handle pull requests](#handling-pull-requests)

### Basic flow
Basic flow of most projects would be as follows:

1. Checkout new branch from the tip of master
2. Make changes
3. Merge master to your branch
4. Solve any issues and commit
6. Merge branch to master

The situation is quite more clear with the use of pull requests (Github) or merge requests (Gitlab). In those, the branch is flagged for merge and remote repo tells us, if there are any issues with the merge and doesn't allow us to merge the code until they are solved in the branch. If using any of these major remote repositories, it is advisable that the merge is done online, not locally - although both ways are naturally possible. More about merging [later](#handling-pull-requests).

### Never commit to master
It is paramount that this becomes your second nature in collaborative projects. Any direct commits to master WILL trip somebody off. If somebody commits bug into master, everybody will HAVE to merge that bug into their code to keep history linear (although there are debates in how linear should git history really be).

All coding should be done in feature branches and pulled to master or merged by the lead programmer.

### Master never fails
Master should optimally never fail or have bugs. Master doesn't need to have all the features. It needs to be stable. If there are bugs in your code (which there shouldn't, if you were following this rule :), fix them and them pull to master. That way, there is always a commit to revert to which works.

> In reality, especially in the beginning, master will fail. If you don't include some CIs for tests, or your tests suck (or you don't write tests because you are badass), then master will be buggy. But you should try to avoid it at all costs.


### Handling pull requests
Important information to keep in mind is, that you initiate pull request on the entire branch, not only a certain commit or state. So if the branch is updated or changed, the pull request will be changed as well. This is quite useful, because you can fix problems with merging or other issues on the same pull request before it is closed.

Overall, pull requests should be kept to the minimal size or precise desciption. More small self contained pull requests are better than on HUGE which changes the entire codebase. This is good for clearity of review as well as nice towards other people who are workign on the project and don't know about theese massive changes comming. Keep it clear and to the minimum.

Remember, that pull requests can have extensive messages and comments. Be even more descriptive in the message thaan usual with your commits.

Before the request is initiated, keep the following in mind:

- Check if the target branch is updated in your repo and not behind the tip of a master branch
> This is non requried, but will save you the trouble and public shame of making a pull request on a repo that can't be merged. Don't do it kid.

- If you are using GitFlow style, You code shoudl check not only vs master but vs develop as well.
> Remember, that in GitFlow develop is sorta master, so check, check, check.

- No dependent code is pulled. If your code depends on something else being fixed, fix it first.
> It happens more than often that during fixing some part of the code you realise, others parts are so broken you cannot fix this until you fix those. It is good idea to do dependencies separtely and than add those features. Believe me.

- Importance of the pull request is clear. Mesage is well laid out and code is simple and small.
> The best pull requests are usually issue fixes, where you can simply add _closes #5 by changing var time from int to float_ message. It will link to the issue and everything is dandy.

- Each pull request commit should be self sustained so they can be cherry-picked.
> Sometimes not everyting in your pull request will be wated. But if it has easy changes that are actually good, they can be picked - if they don't depend on commits that are unwanted. If you end up with a long list of commits with their fixes, i is time to rebase before you initiate the pull request.

- Pull request shoudl have limited amout of commits, hopefuly to a maximum of 5
> This is simmilar to the previous commits. In large proffesional repos, nobody wants to ahve thousands of amended or back fixed commits. If you made 12 commits out of which 7 are fixes of typos and such, rebase to 5 before you pull.

If you didn't folllow the rules above of you did but something went wrong anyway and you cannot merge the branch online(Github screams that they can't be merged), you can easilly do the following:
1. Checkout the branch locally
2. Merge master to it
3. Fix any conflicts (this will teach git how to fix them online)
4. Push to the branch on the remote
5. Merge and close pull request

## Git features

### Releases

### Tags

### Submodules

## Tips and tricks
### Multiple remotes
Remember, that you can have as many remotes as you wish in one project. Remotes are local, so remember that
