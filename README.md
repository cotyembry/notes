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
    
Then to make sure that both the local version (on the actual computer your sitting at) and the version on github are synced up

    git pull

And finally to  push the  project

    git push -u origin master

And if that doesn't work, to force the push you can do:

    git push -u -f origin master

...something like that

Oh yeah,

If you need to remove the hidden .git file, you can use

    rm -rf .git
    
When in the home directory of the project

-------

when __changing__ files that are already tracked (i.e. already added to the project with the `git add <filename here>` command) the files become _unstaged_. Well, from there to _stage_ them (meaning, add the files that have been changed to the list of files to be pushed on the next commit - i.e. update these files in the repository with the code that is located locally) anyways..., if the files are not staged they cannot be pushed to github thus, the new code will not be updated to the project. So, to _stage_ the files do the following on the command line:

    git add <filename that is unstaged>
    
then you can say `git status` to check the new status of the project

finally you can push the new project to the repo, but first add a commit message that will be displayed next to the file name (i.e. when all said and done after this command is ran, on github.com/username/repoName the file will be viewable in a gui type environment. Well, to the far right side of the row, but still on the same row, where the file name is located, this message we are about to set will appear there __only__ for each file that has been altered in the local project)

    git commit -m "say some commit comment here; maybe say - Added code logic to format the routing of the application"

and finally actually do the push

    git push origin master
