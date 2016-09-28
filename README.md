# notes

I literally created this repo just for a place to put notes about, well.. code I suppose.

To get a git repo set up the following things worked for me:

    git init
    git add .
Then I created a repository on github.com under my profile. After that I copied the url that was produced for the repo
Then I ran the following to set the origin (I think is how they say it in the git community?)
    git remote add github https://github.com/cotyembry/PROJECT_NAME.git
Then to make sure that both the local version (on the actual computer your sitting at) and the version on github are synced up
    git pull git remote add github https://github.com/cotyembry/PROJECT_NAME.git
And finally to  push the  project
    git push -u origin master
    
Or something like that

Oh yeah,

If you need to remove the hidden .git file, you can use
    rm -rf .git
When in the home directory of the project
