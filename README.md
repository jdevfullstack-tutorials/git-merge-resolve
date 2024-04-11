# Git Workflow with Merge Conflicts

## Without Using Branches
### Git Pull Only
git pull when no changes made in local

### Git Fetch & Merge
1. edit files locally
2. `git add -A` or specific conflict file only
3. `git commit -m "<your message>"`
4. `git fetch`
5. then `git status` to see if you don't know
the merge conflicts yet
6. `git merge` but will fail, only
for purpose of prompting it in VSCode
then, I usually accept both changes and fix manually
7. `git add -A` or specific conflict file only
8. `git commit -m "<your message>"`
9. `git push`

2 commits are in remote main history,
local commit + merge commit

### Git Rebase
1. edit files locally
2. `git add -A` or specific conflict file only
3. `git commit -m "<your message>"`
4. `git fetch`
5. then `git status` to see if you don't know
the merge conflicts yet
6. `git rebase` but will fail, only to automatically
promp you to VSCode, I usually
accept both changes and fix manually
7. `git add -A` or specific conflict file only
8.  `git commit -m "<your message>"`
9. `git rebase --continue`, if that is the
last conflict to be edited, this will be 
successful
10. `git push`

1 commit only in remote main history

## Using Branches ( The Typical Way )

### Create A Branch First
My typical workflow is I will start
in `main` editing the files, but
I will not commit in there

`git switch -c 'new-branch-name'`

then 

`git add -A`

`git commit -m '<your message>'`

then `git push` once your branch
is ready 

`git push -u origin <same-branch-name-as-local>`

### Git Pull Origin Main To A Local Branch
use this when there are no changes in
your local branch but remote main has
commits and your branch is outdated

the long way 

1. `git checkout main`
2. `git pull`
3. `git checkout <the-target-branch>`
4. `git pull origin main`
5. `git push`

the short way

exactly in your branch
( no need to switch branches )

1. `git pull origin main`
2. `git push`

`git pull origin main` fetches commits from 
the remote main ( the GitHub repo main )
then it merges local main into the branch 
you are currently in

please do note that your local main
is still behind but that's not a problem
when your main branch is stale,

to update the local main,

`git checkout main`
`git pull`

all will be up to date

finally, the remote branch will be updated,
no commits behind master

### Git Fetch Then Merge
when you are actively editing your branch, 
then another developer pushed in remote main
you need to update yours too, save
your changes first in your active local
branch

1. `git add -A`
2. `git commit -m '<your message>'`
3. `git checkout main`
4. `git fetch -p origin`
5. `git merge origin`
6. `git checkout <target-branch>`
7. `git merge main`
8. settle the conflict if there is any
then `git add -A` then `git commit -m 'your message'`
9. `git push`

the short way, in your active branch

1. `git fetch origin main`
2. `git merge origin/main`
3. settle the conflict if there is any
then `git add -A` then `git commit -m 'your message'`
4. `git push`

### Git Fetch Then Rebase
when you are actively editing your branch, 
then another developer pushed in remote main
you need to update yours too, save
your changes first in your active local
branch

1. `git add -A`
2. `git commit -m '<your message>'`
3. `git checkout main`
4. `git fetch -p origin`
5. `git rebase origin`
6. `git checkout <target-branch>`
7. `git rebase main`
8. settle the conflict if there is any
then `git add -A` then `git commit -m 'your message'`
9. `git rebase --continue`
10. if there are no conflicts left,
the rebase will be completed then `git push`

the short way, in your active branch

1. `git fetch origin main`
2. `git rebase origin main`
3. settle the conflict if there is any
then `git add -A` then `git commit -m 'your message'`
4. `git rebase --continue`
5. if there are no conflicts left,
the rebase will be completed then `git push`
