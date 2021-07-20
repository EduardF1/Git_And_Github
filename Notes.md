# Git and Github

# Git and VCS locally (local machine)

1) VCS - what it is ?
- Let's say we have a file, at the moment of creation, the file is version 1 (<em>initial save point</em>).
- At a later point, we decide to change that files and make another <em>save point (version 2)</em>.
- In some situations (sometimes it happens), a file will be damaged/messed up to the point where it can no longer
be saved / savaged (<u>all hope lost...</u>). This can become a pretty difficult/inconvenient situation as we most likely will have inter-linked 
classes/files. 
- If such situations occur, we can do two things, <u><em>rollback our changes (return to a previous file version*)</em></u> or <u><em>compare file versions</em></u>.
`* - it can be any file version, initial, second etc. as long as we are aware of the version we choose.`.

2) Git using the CLI
- To navigate to where we want to set our project directory, we use `cd folderName`.
- Once we reach the directory, we can either create our needed files by using `touch fileName.fileExtension` or create the directory structure we want by using combinations of `cd` (navigation) and `mkdir directoryName` (to create our directories).
- To initialize Git within our project, we need to navigate to the root project directory and run `git init` (from this point on, this will be called our <em><u>working directory</u></em>).
- To verify that Git was successfully initialized, we can run `ls -a` (this will also show hidden files within the directory).
- To start tracking the files within the working directory for changes, we need to add the files to <em><b>the staging area </b></em>. The staging area is an intermediary location from which we can
choose which files inside the working directory we can commit.
- To see which files are located in the staging area, we can run `git status`. After running the command, files that are colored in red (and also under the `Untracked files` text/category) are files that are present in the working directory but which are
not tracked yet. 
- To start tracking the files (for changes) from the working directory and add them to the staging area, we need to run `git add`. We can either run `git add <fileName>` (add a specific file) or `git add .` (add all files/ multiple files). 
- Once the file(s) are added to the staging area, we can run `git commit -m "commitMessage"`. The commit message is quite important as it helps us to keep track of what changes we have made, these messages should be as explicit and short as possible (and answer the question `What is/are the change(s) since the last commit/save point ?`.
- Usually, the first commit message is "initial commit". Furthermore, these messages are written in the present tense. Ex.: `git commit -m "integrate Kafka"`.
- Commits can be seen after they're made by using the `git log` command. Each commit has a unique hash code.

3) Simplified model

| Working Directory                                       |          Staging Area                                                     |Local Repository |
| --------------------------------------------------------| --------------------------------------------------------------------------|---------------- |
| git add file (moves the <br> file to the Staging area   | git commit -m "commitMessage" <br>(file committed to the local repository)|---------------- |
|       file                                              |          file                                                             |    file         |

4) If for example we messed up a file which is not yet committed, we can see the differences between the previous version of the file and the current by running
`git diff fileName`.

5) To revert the changes to the file, we can run `git checkout fileName`. This will revert the specified file to the last committed version of the file in the local
repository.

# Git and VCS remotely

1) What do we mean by a remote repository ?
- A repository hosted on someone else's computer or server.

2) Github
- Log in / Be logged on to Github
- Press the `+` button in the upper right corner and select `New Repository`.
- Give the Repository a name and a description, choose either public or private.
- Then, be sure to be in the working directory locally (in the terminal).
- Copy the Repository URL, and run `git remote add origin repositoryURL`.
- Run `git branch -M main` to change to the main branch from master.
- Run `git push -u origin main` to push the local commits (local repository) to the remote repository. The `-u` flag links the local and remote repositories. The following parameters `origin main` are the name of the remote followed by the branch name. The `main` branch is the default branch of all commits.

| Working Directory                                       |          Staging Area                                                     |Local Repository <br> (master/main branch)                      |
| --------------------------------------------------------| --------------------------------------------------------------------------|----------------------------------------------------------------|
| git add file (moves the <br> file to the Staging area   | git commit -m "commitMessage" <br>(file committed to the local repository)|here, the commits are done sequentially: C1, C2, C3 and so on.. |
|       file(s)                                           |          file(s)                                                          |    file(s)                                                        |

- We can have our <em><u>Local Repository</u></em> in parallel/in sync with our <em><u>Remote Repository</u></em>.
- Commits are done locally and remain present in the local repository (.git) and are moved/synced on the remote when we run `git push`.  
- The local repository is the .git file inside our <em><u>Local Repository</u></em> and the <em><u>Remote Repository</u></em> is the one
hosted on Github/Bitbucket etc.

# Git .ignore
- prevent certain files from being committed to either the local or remote repository.
- Stuff that shouldn't be hosted on an open platform (Github/Bitbucket), these should be added to the `.gitignore` file:
    - secret passwords.
    - api keys.
    - AWS keys.
    - files for user settings/preferences (ex.: DS_Store).
    - files for local setup
   
- To create a gitignore file, run `touch .gitignore` in the project/working directory.
- To remove all files from the staging area, run `git rm --cached -r .`. This command removes all `.` the cached files `--cached` recursively `-r`.

# Git clone
- Cloning is pulling down all the commits/files from a remote repository into the local working directory (local machine).
- Run `git clone repositoryURL` where repositoryURL is the URL of the repository which can be obtained from github.
- After the repository is cloned locally, we can run `cd` to enter the directory of that cloned project and run `git log` to
see previous (the history) of the commits.

# Git - Branching and Merging

- Working on the main branch but trying out different stuff/experiments on the experimental branch, both branches existing at the same time (parallelized).
```
main branch: [C1] -- [C2] -- [C3]
                      |
experimental branch: [C3] -- [C4]
```

- If the experimental branch has resulted in some resourceful outcome, we can simply merge it into the main branch and bring the changes into it.
- If there are any merge conflicts, some editing might be necessary but after those are solved, the changes should be present in the main working branch.
```
main branch: [C1] -- [C2] -- [C3] -- [C4] --
                      |                |
                      |                |
experimental branch: [C3] -- [C4]------*                                       
```  
- For any given large project, there will be multiple branches being worked on in parallel. That is because needed work might imply bugfixes, feature development
  (adding new features), improvements etc. and these different activities could result in breaking the main branch (hence, the project). In order to avoid this, parallel
  branches are made, each for a specific purpose and the work done on them should be merged to the main branch only once the changes are working (not breaking anything else),
  tested and are verified.
  
- To create a new branch, we can run `git branch branchName` where `branchName` can be something like `story1-implementation` or `defect1231-fix`.
- If we afterwards run `git branch`, we will be able to see the available branches.
```
Ex.: 
1) create a new branch: git branch alien-plot
2) run git branch
3) the terminal will show the available branches for the current working directory:
    alien-plot
  * main
  
Note: The * denotes the currently selected branch (the branch that we're on).  
```

- To switch between branches, we can run `git checkout branchName`.
- To a merge a branch into the current branch, we can run `git merge branchName`.
- To push the changes to the remote, we can run `git push orgin remoteBranchName -u`.
- On Github, we can merge changes from different branches (of the same project) from one to another by using the `Compare & pull request` option:
1) Click the `Compare & pull request` option, scroll down a bit and see the changes, additions are highlighted in green and deletions are highlighted in red.
2) Check the branches, `base: branchToMergeInto <- compare:branchToCompareWith`.
3) Select the `Create Pull Request` option and wait for the Github server to finish its analysis (takes a couple of seconds).
4) Enter a merge commit message for example `Merge experimental branch to main`.
5) Click `Confirm merge`.
6) The changes (previous operations) can be seen/checked in the Github Network tab `Network/Network Graph`.

# Project collaboration
- Collaboration: a person sets up the repository and then gives permissions to the others (read/write).
- Forking is copying a Github repository and adding it under our own name on Github.  
- Forking, clone a repository on the remote (Github), changes to the repository are possible through PRs (pull requests).
- Forking means that a person will own a copy of a Github repository and from that point on, the person can clone it locally and work on it.
- After the person is satisfied with the made changes, the person can push the changes to the remote repository. Once on the remote repository, the
only way that the cloned project's changes could be incorporated in the initial/original project is through PRs (if the person does not have write access).
- It is a PR as the owner of the initial/original repository will review (Code review) the changes to the project and if these are OK, that person can merge (pull) them in the 
project with a new commit, otherwise not.
  
# NPM Modules
- Usually NPM Modules (node modules) are excluded from projects as they occupy a lot of space (memory) and contain a lot of packages.
- Reference: `https://github.com/contentful/the-example-app.nodejs`.