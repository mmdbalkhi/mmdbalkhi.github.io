Title:Git Cheat Sheet
Date:2021-3-31-11:00
Modified:2021-5-12-10:30
Category:tecnology
Tags:tecnology,programin,git
Slug:git cheat sheet
Authors:komeilParseh
description:Some important git commands

## List of git commands

`git init`

- Get started with git

`git add fileName`

- Add file to git

`git add -A`

- Add all files to git

`git log`

- Displays commits

`git commit -m "description"`

- commit changes with descriptions

`git status`

- Show status

`git reset fileName`

- Remove the file from the stage mode

`git diff HEAD`

- Show current status relative to last commit status

`git diff --staged`

- Display the current status relative to the stage status

`git checkout --fileName`

- Extract the file from the last commit and replaces the current file

`git branch`

- Show existing branches

`git branch branchName`

- Build a new branch with the specified name

`git checkout branchName`

- Switch from the current branch to the specified branch

`git merge branchName`

- Merges the branch with the current branch

`git rm fileName`

- Remove the file from git and from the system tray

`git branch -d branchName`

- Delete branch

`git push origin master`

- Sends the master directory to origin

`git pull origin master`

- Receives the master branch from origin

`git remote`

- Remote display

`git remote add origin url`

- Add remote with specified address and origin name

`git show commitID`

- Display commit details with specified ID

`git tag`

- Show tags

`git tag -a tagName -m "description"`

- Add tags with specified name and description

`git show tagName`

- Show tag details

`git blame fileName -L lineNumber`

- See who wrote from the line to the end of the file

`git blame fineName -L lineNumber, lineNumber`

- See who wrote the line

`git bisect`

- Used for debug

`git config`

- Used for tool settings. Like the author profile as well Proxy settings for clientgate
