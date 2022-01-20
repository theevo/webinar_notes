# Undoing Mistakes with Git

host: Tobias Gunther at Tower.app
date: 2022-01-06 6:00 PM UTC

## discard all changes to this file

`git restore <filename>`


## restore a deleted file

`git restore <filename>`

yup, same command will bring the file out of the trash

## discard chunks/lines in a file

`git restore -p <filename>`

## TIP: SEMANTIC COMMITS

- don't mix commits from different topics
- be thoughtful with your commits

## Undo all local changes

"Bloody hell! Let's start over!"

`git restore .`

## Fixing the last commit message

"Whoops. Typo in the commit message."

`git commit --amend -m "Typos are indeed embarassing"`

can also use `amend` to add a file that belongs to that commit

## Reverting a commit

- you made a commit earlier that is wrong and want to undo it
- make a new commit that reverses changes made by a previous commit
- makes "opposite" changes of the previous commit

`git revert <commit hash>`

## resetting to an old revision

go back in time to a previous point in time

`git reset --hard <commit hash>`

## HARD vs MIXED reset

- mixed will keep the changes
- changes will appear in staged files
- hard will just drop all changes

## 8. restting a file to an old revision

"Yikes! I know this file was correct sometime before"

`git restore --source <commit hash> <filename>`

## intermezzo: reflog

logs movement of the HEAD pointer

## 9. Recovering deleted commits

you want to undo `git reset --hard`

`git reflog` and copy the hash to which you want to return
`git branch restore <commit hash>`

## 10. Recovering a deleted branch

HEAD moves everytime you switch branches

`git reflog`
`git branch <branch name> <commit hash>`

## 11. Moving a commit to a new branch

you accidentally commited to main

start off on main branch

`git branch <branch name>`
`git reset HEAD~1 --hard`

## 12. Moving a commit to a different branch

the destination branch already exists

`git checkout <destination branch>`
`git cherry-pick <commit id>`

reset main to HEAD~1

## INTERACTIVE REBASE 

- swiss army knife of git tools
- you can cut yourself

## 13. Editing Old commit message

1. How far back do you want to go? What should be the base commit?
2. `git rebase -i HEAD~3` pick # just before the commit you want to fix
3. fix it in the text editor

replace "pick" with "reword". don't rename it yet... that's on the next screen. save and close.

## 14. Delete old commits

same as #13. replace "pick" with "drop"

## 15. Squashing multiple commits into one

commits are maybe too small. let's combine them into one

same as #13. replace "pick" with "squash". but only need it once for 2 commits. think of "squash" as a "+" symbol

```
pick blah blah
squash blah blah blah
pick wah wah
```

## 16. Adding a change to an old commit

maybe this commit is incomplete or incorrect

this cleans up original commit + bandaid commit pattern

add the files to staging area

`git commit --fixup <commit hash>`
`git rebase -i --autosquash HEAD~4`

text editor will mark the line with your new commit with fixup

warning: this will change the commit dates on GitHub for all commits between HEAD and old commit. it looks fine in Terminal.

## 17. Splitting / Editing an old commit

Maybe this old commit was just too big

