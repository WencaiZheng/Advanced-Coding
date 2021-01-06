# Git Command

Golden rule: never change the shared history; never rebase the shared commits.

## Basic

1. check the status

   ``` bash
   git status
   ```

2. track all the local change

   ```bash
   git add/rm .
   ```

3. commit the changes

   ```bash
   git commit -am "comments"
   ```

4. push to a branch

   ```bash
   git push origin master
   ```

5. stash data in working area, store the working area data to stashed space and replace it with HEAD repo

   ```bash
   git stash --include-untracked
   ```

6. check diff

   ```bash
   git diff HEAD HEAD~2
   git diff branch1 branch2
   ```

## LOG

1. get git commit graph

   ```bash
   git log --graph --decorate --oneline
   ```

2. get one branch to other branch log

   ```bash
   git log branch1..master --oneline
   ```

3. get one commit to other commit

   ```bash
   git log HEAD~5..HEAD^ --oneline
   ```

   

4. get the commit messages that contains theString

   ```bash
   git log –grep theString –oneline
   git log –GtheString --patch #which line
   ```

   

## Branch 

1. check how many branches are there

   ```bash
   git branch
   ```

2. create a new branch

   ```bash
   git branch develop
   ```

3. create a new branch named develop2 if there is no one named it

   ```bash
   git checkout -b develop2
   ```

3. push to new branch

   ```bash
   git push origin develop
   ```

## Merge and delete

1. merge branches, first stand at develop branch, this automatically merge the changes in develop2 to develop

   ```bash
   git checkout develop
   git merge develop2
   ```

2. check the log file and see details

   ```bash
   git log
   git show <first 8 digits of hash code of log>
   ```

3. then delete the develop2 branch, when you stand at other branch and make sure your changes are committed already

   ```bash	git branch -d develop2
   git branch -d develop2
   ```

4. remotely delete branch

   ``` bash
   git branch origin --delete develop2
   ```


5. fetch to see if any change in the remote repo

   ```bash
   git fetch
   ```

6. pull the remote repo to local if there is no change in local and there is change in remote repo

   ```bash
   git pull origin/master
   ```

7. if both change in remote and local repo, merge if you don't have merge conflicts

   fast-forwarding vs. 3-way merge: whether the master branch has diverges.

   ```bash
   git merge mybranch
   ```

8. if there is same line same file change in remote and local repos, solve conflicts by modifying the file manually

   ```bash
   both modified: filename
   ```

## Revert to history - Reset

1. show history commit

   ```bash
   git show HEAD~3
   ```

   ```bash
   git show HEAD^^^
   ```

   ```bash
   git show HEAD@{"1 month ago"}
   ```

2. Track one file across all commits

   ```bash
   git blame filename
   ```

1. Return to the previous commit

   ```bash
   git reset --hard SHA-1 # get this commit and cover the stage and wd with it
   ```

   ```bash
   git reset --mixed SHA-1 # get this commit and cover the stage with it only
   ```

   ```bash
   git reset --soft SHA-1 # get Head and master point to this commit only
   ```

2. Un-stage files

   ```bash
   git rm --cached # untracked
   ```

   ```bash
   git reset HEAD # DEFAULT --mixed reset, resulting latest repo override staged file like above 1.2 line, HEAD points to the latest commit
   ```

   

## Modify history

1. modify latest commit

   ```bash
   git commit --amend
   ```

2. interactive rebase

   ```bash
   git rebase -i
   ```

3. fix seemingly irrecoverable mistakes

   ```bash
   git reflog
   ```

4. rewrite entire bunch of commit history

   ```bash
   git filter-repo
   ```

5. create new commit revert changes to previous commit

   ```bash
   git revert
   ```

   

# Git workflow

good reference: https://nvie.com/posts/a-successful-git-branching-model/

1. Peer to peer model
2. centralized model
3. mixed ones

4. pull request model
5. 