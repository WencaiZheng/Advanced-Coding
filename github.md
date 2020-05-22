# GitHub learn

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

## Branch control

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

   

