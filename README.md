# notes

I literally created this repo just for a place to put notes about, well.. code I suppose. And  help on some processes

#git help

To get a git repo set up the following things worked for me:

    git init
    git add -A
    git commit -m "First commit"
    
Then I created a repository on github.com under my profile. After that I copied the url that was produced for the repo
Then I ran the following to set the origin (I think is how they say it in the git community?)
    
    git remote add origin https://github.com/cotyembry/PROJECT_NAME.git

And to check that it was added okay:
  
    git remote -v
    
You can add multiple remotes

This acutally makes the mystery go away for setting up different servers repos to push to. You can just add another 'remote' I suppose you would say.

    git remote add server1 https://github.com/cotyembry/SOME_PROJECT1.git
    git remote add server2 https://github.com/cotyembry/SOME_PROJECT2.git

and boom, now you can push to multiple places/repos (more on this later when the section starts about pushing the project)

If you have problems and added the wrong remote or something, you can also remove the remote you setup.

as an example, here is a sample snippet:

    git remote -v

which yeilds the following output:

    origin  https://github.com/OWNER/REPOSITORY.git (fetch)
    origin  https://github.com/OWNER/REPOSITORY.git (push)
    destination  https://github.com/FORKER/REPOSITORY.git (fetch)
    destination  https://github.com/FORKER/REPOSITORY.git (push)

# Remove remote

and to remove one, for instance, do the following

    git remote rm destination

then to verify it is gone

    git remote -v

    origin  https://github.com/OWNER/REPOSITORY.git (fetch)
    origin  https://github.com/OWNER/REPOSITORY.git (push)
    
-------
Okay now lets talk about pushing the project, but first we have to do one thing and it might resolve an issue (let this be magic for now if you don't understand, but still type in the command)

To make sure that both the local version (on the actual computer your sitting at) and the version on github are synced up (in terms of files) do the following

    git pull

# Push

And finally to  push the  project to the master branch of the particular remote that was set up (in the following case it is the remote I named 'origin' .. and I'm pushing the project/code to the master branch)

    git push -u origin master

And if that doesn't work (sometimes an error is thrown (this is what the `pull` command was trying to avoid btw), to force the push you can do:

    git push -u -f origin master

...something like that...and that should work (pretty much...) you should probably read more about the pull command later though when you have time to know what you're actually doing.

Oh yeah,

If you need to remove the hidden .git file (to restart the whole git repo process - i.e. before you said the very first command `git init`), you can use the following command for help ut make sure that you are in the home directory of your project since that is where the .git file is located:

    rm -rf .git

#remove commited changes that have not been pushed

    git reset

this will stop any changes that have been set to be pushed

-------
#tracked files, staged files, unstaged

when __changing__ files that are already tracked (i.e. already added to the project with the `git add <filename here>` command) the files become _unstaged_. Well, from there to _stage_ them (meaning, add the files that have been changed to the list of files to be pushed on the next commit - i.e. update these files in the repository with the code that is located locally) anyways..., if the files are not staged they cannot be pushed to github thus, the new code will not be updated to the project. So, to _stage_ the files do the following on the command line:

    git add <filename that is unstaged>
    
then you can say `git status` to check the new status of the project

finally you can push the new project to the repo, but first add a commit message that will be displayed next to the file name (i.e. when all said and done after this command is ran, on github.com/username/repoName the file will be viewable in a gui type environment. Well, to the far right side of the row, but still on the same row, where the file name is located, this message we are about to set will appear there __only__ for each file that has been altered in the local project)

    git commit -m "say some commit comment here; maybe say - Added code logic to format the routing of the application"

and finally actually do the push

    git push origin master

-------

#branches

Ok, so now that a project is set up, its time to go over branching

To see what branches exist, in the root directory enter:

    git branch
    
This will list all the branches that exist

To create a branch (a complete copy of all the code from master)

    git branch feature1
    
and to switch to it to start working on the new code do:

    git checkout feature1

where feature1 can be any name you wish (that is unique to the branches)

This will actually change into the feature1 branch for you (you don't need to do like a `cd ./feature1` type of command)

now any changes in this new project (technically speaking its a "new branch") will not effect master

now act like this current branch (feature1) is master and write some code! (We will go over commands in a second to create a pull request and merge this later back to master)

#pull request

first since currently the branch that is being worked on is feature1 and we want to do a pull request to get the feature1 branch merged into master we need to get back into the master branch to make sure there weren't any code updates to the master branch while working on the feature1 branch

    git checkout master
    
this will switch back to the master branch

now before doing anything else, to make sure that get any updates that may have been made to master

    git pull
 
and now time to go back to the feature1 branch

    git checkout feature1

now that we are confident the project is up to date, push the changes to the feature1 branch

    git commit -m "say your custom commit message here"

if you do `git push` here it will probably give some type of error or warning. This is because it doesn't know where to push the code to. You can then do the following to resolve this:

    git push --set-upstream origin feature1
    

now to try to merge the whole feature1 branch to master do:

    git merge master

now go to github.com and go to the repo where master is

and you can create a pull request to finally delete the branch



you might not have to do this next step, but just for extra info:

sometimes there will be file conflicts here after trying to merge the branches. To fix them, you will have to manually look at the code and the lines that were having the conflicts and manually fix the issues.

Once done with that, try it again

    git merge master

and hopefully its all set up and has been successfully merged!

#delete branch

remember to see the branches:

    git branch
    
and again to delete it:
    
    git branch -d the_local_branch_name

#Resetting files that are staged to be commited
I accidentally did `git add <filename>` and it somehow added all of the files..? Anyways, I wanted to undo this hiccup so I found out that doing the following can fix the issue and rollback the staged files to nothing to be commited

    git reset HEAD -- .

see http://stackoverflow.com/questions/19730565/how-to-remove-files-from-git-staging-area for more info on this command.

It might take a little while to run as well so be prepared to wait...

#Rollback a git pull
see the following for the answer
http://stackoverflow.com/questions/1223354/undo-git-pull-how-to-bring-repos-to-old-state

#Error message issues
When tryihg to git add ... files, or in general, if you get the error that says something like:
    
    Another git process seems to be running in this repository, e.g.
    an editor opened by 'git commit'. Please make sure all processes
    are terminated then try again. If it still fails, a git process
    may have crashed in this repository earlier:
    remove the file manually to continue.
    
To resolve it you can do:

    rm -f ./.git/index.lock

If you still have problems you can refer to
http://stackoverflow.com/questions/38004148/another-git-process-seems-to-be-running-in-this-repository
for more help

    You have not concluded your merge (MERGE_HEAD exists).
    Please, commit your changes before you can merge.
    
To resolve this you can fix the files manually that it says are wrong or do

    git merge --abort
    
#mapped drives
Sometimes I use a mapped drive to access the git repo and its files and other times I remotely log into the server. When I remotely logg in, .git has it setup that the top level directory is `/y/` (i.e. `Y:/`) so when I do `git status` the command fails saying

    fatal: Could not switch to 'Y:/': No such file or directory
    
So to fix this I have to explicitly set the project directory and the working directory. In my case (with respect to the paths I had to add to get this to work) I put the following command down that worked

    git --git-dir=/d/CACHESYS/CSP/cah/.git --work-tree=/d/CACHESYS/CSP/cah/ status
    
To make things easier on me I set the environment variable up to be

    gitCustom="git --git-dir=/d/CACHESYS/CSP/cah/.git --work-tree=/d/CACHESYS/CSP/cah/"
    
And to use the command and do a normal `git status` for instance you would do

    $gitCustom status

#extra help

go to the following and watch the 11 minute video for more help
https://www.youtube.com/watch?v=oFYyTZwMyAg

if you want to see the introduction one to it you can see
https://www.youtube.com/watch?v=0fKg7e37bQE
