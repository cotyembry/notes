# notes

I literally created this repo just for a place to put notes about, well.. code I suppose. And  help on some processes

#git help

To get a git repo set up the following things worked for me:

    git init
    git add .
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

-------
#tracked files, staged files, unstaged

when __changing__ files that are already tracked (i.e. already added to the project with the `git add <filename here>` command) the files become _unstaged_. Well, from there to _stage_ them (meaning, add the files that have been changed to the list of files to be pushed on the next commit - i.e. update these files in the repository with the code that is located locally) anyways..., if the files are not staged they cannot be pushed to github thus, the new code will not be updated to the project. So, to _stage_ the files do the following on the command line:

    git add <filename that is unstaged>
    
then you can say `git status` to check the new status of the project

finally you can push the new project to the repo, but first add a commit message that will be displayed next to the file name (i.e. when all said and done after this command is ran, on github.com/username/repoName the file will be viewable in a gui type environment. Well, to the far right side of the row, but still on the same row, where the file name is located, this message we are about to set will appear there __only__ for each file that has been altered in the local project)

    git commit -m "say some commit comment here; maybe say - Added code logic to format the routing of the application"

and finally actually do the push

    git push origin master
