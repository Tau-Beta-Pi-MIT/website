# HTML MIT-hosted Website for MIT Tau Beta Pi

## Overview
This repository contains html and css code along with images for our website, hosted [here](tbp.mit.edu/www).  This code can be edited and pushed to our Athena server by individuals with appropriate credentials.  

## Installation/Requirements
The only capabilities you'll need on your machine are `ssh` and `git`.  Once you have these set up, you'll be ready to make modifications to the site as you see fit!

## Navigating to our code on the Athena server
Our codebase is hosted on MIT's athena server, which is accessible through remote login via `ssh`.  You can navigate to our codebase on the Athena server by following these instructions:

1. Make sure you’re on the mailing list tbp-officers@mit.edu.

2. `ssh` into the Athena server: 

`ssh <kerb>@athena.dialup.mit.edu`

**PW**: your kerb password + Duo Authentication (1 for Duo Push)

3. Navigate to our directory where our codebase is hosted:

`cd /mit/tbp/www`

## Suggested workflow for making changes ([feature/branch workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow)):
1. Create a branch on the GitHub repository for the feature you’d like to add (e.g. a button for logging tutoring hours):

`git checkout -b name_of_your_branch`

2. Make changes to this codebase on the new branch on your local machine.  Once you're ready to commit and push your changes:

`git add .`

`git commit -m "your_commit_statement"`

`git push -u origin name_of_your_branch`

3. Now navigate to the repository on the Athena server, by following the instructions in the section above ("Navigating to our code on the Athena server").  Once there, fetch the new branch using a git fetch of this syntax: `git fetch <remote-repo> <remote-branch>:<local-branch>` (give it the same name for simplicity):

`git fetch origin name_of_your_branch:name_of_your_branch`

4. Now checkout the new branch on the Athena server:

`git checkout name_of_your_branch`

5. Next, inspect the website at tbp.mit.edu/www to make sure your changes appear as you'd expect and are free of bugs.  **NOTE**: Changes don't always appear immediately, so you noticed that nothing has changed on tbp.mit.edu/www, give it a little more time to wait for the changes to be visible.  

6. Once you're satisfied with how everything looks, perform a merge pull request on the GitHub repo (this is accomplished most effectively by just doing this through [GitHub online](https://github.com/)).  Integrate your new changes with the master branch, and then (on both your local machine and the Athena server), switch back to the master branch and pull:

`git checkout master`

`git pull`

7. Finally, after you pull again on both your local computer and the remote Athena server, verify that the website looks as you'd expect it to and is free of bugs!

Feel free to email rmsander1026@gmail.com with any questions about this workflow or the website.
