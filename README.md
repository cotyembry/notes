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
