# notes

I literally created this repo just for a place to put notes about, well.. code I suppose. And  help on some processes

# git help

drop the last stashed item

    git stash drop
    

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
    

# create and checkout new branch

    git checkout -b newBranchName
    

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
# tracked files, staged files, unstaged

when __changing__ files that are already tracked (i.e. already added to the project with the `git add <filename here>` command) the files become _unstaged_. Well, from there to _stage_ them (meaning, add the files that have been changed to the list of files to be pushed on the next commit - i.e. update these files in the repository with the code that is located locally) anyways..., if the files are not staged they cannot be pushed to github thus, the new code will not be updated to the project. So, to _stage_ the files do the following on the command line:

    git add <filename that is unstaged>
    
then you can say `git status` to check the new status of the project

finally you can push the new project to the repo, but first add a commit message that will be displayed next to the file name (i.e. when all said and done after this command is ran, on github.com/username/repoName the file will be viewable in a gui type environment. Well, to the far right side of the row, but still on the same row, where the file name is located, this message we are about to set will appear there __only__ for each file that has been altered in the local project)

    git commit -m "say some commit comment here; maybe say - Added code logic to format the routing of the application"

and finally actually do the push

    git push origin master

-------

# branches

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

# pull request

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

# commiting deleted files

    git ls-files --deleted -z | xargs -0 git rm 

# Resetting files that are staged to be commited
I accidentally did `git add <filename>` and it somehow added all of the files..? Anyways, I wanted to undo this hiccup so I found out that doing the following can fix the issue and rollback the staged files to nothing to be commited

    git reset HEAD -- .

see http://stackoverflow.com/questions/19730565/how-to-remove-files-from-git-staging-area for more info on this command.

It might take a little while to run as well so be prepared to wait...

# Reverting to a previous commit

    git revert HEAD~1..HEAD

or you can revert the last two commits

    git revert HEAD~2..HEAD

# Rollback a git pull
see the following for the answer
http://stackoverflow.com/questions/1223354/undo-git-pull-how-to-bring-repos-to-old-state

# Git keeps prompting me for password
you can get rid of this on the command line by doing the following:

    git config --global credential.helper wincred

# Error message issues
When trying to git add ... files, or in general, if you get the error that says something like:
    
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

# .gitignore help to deal with the following: Untracked files, Staged files, and Committed files
.gitignore will only ignore files that are `untracked` meaning they have never been commit (or if they have been commited the files need to be changed from `tracked` to `untracked`

to do this do the following

    git rm --cached <pathToFileOrTheFileName>
    
This will untrack the file specified. Now what you can do once the file is untracked is add it to the .gitignore file. Once its added to the .gitignore file, do `git status` again and the file that was specified to be untracked should no longer show up

# mapped drives
Sometimes I use a mapped drive to access the git repo and its files and other times I remotely log into the server. When I remotely logg in, .git has it setup that the top level directory is `/y/` (i.e. `Y:/`) so when I do `git status` the command fails saying

    fatal: Could not switch to 'Y:/': No such file or directory
    
So to fix this I have to explicitly set the project directory and the working directory. In my case (with respect to the paths I had to add to get this to work) I put the following command down that worked

    git --git-dir=/d/CACHESYS/CSP/cah/.git --work-tree=/d/CACHESYS/CSP/cah/ status
    
To make things easier on me I set the environment variable up to be (gitc == gitCustom)

    gitc="git --git-dir=/d/CACHESYS/CSP/cah/.git --work-tree=/d/CACHESYS/CSP/cah/"; cd /d/CACHESYS/CSP/cah/
    
And to use the command and do a normal `git status` for instance you would do

    $gitc status

# submodules
So if you want to have the master/ git repo and also have it include submodules (i.e. a git repo that is a child of the master/ branch), from scratch you can be inside the master/ repo and do

    git submodule add https://github.com/cotyembry/someRepo.git
    
this will clode the submodule to the master/ repo sort of like doing a `git clone ...` would
Now when making changes to the submodule, you need to `cd` into the submodules root folder and do

    git add -A
    git commit -m "committing submodule changes"
    git push origin master #or whatever the branch and remote names are for the repo
    
YOUR NOT DONE YET
What that did was push all the changes to the .git repo of the submodule (as if it was an independent .git repo that was created with `git init` or `git clone https://github.com/...`

Now `cd` up to the master's git repo and do

    git status
    
this should let you know that there are things ready to be committed to the master branch (i.e. the submodule has commits that need to be added to the master branches history)
So to commit the changes that were done to the submodule to master do (inside the main master repo that is the parent of the submodule):

    git add -A
    git commit -m "committing the changes to the master branch that were done and pushed in the submodule repo"
    git push origin master #or whatever the branch and remote names are for the repo
    

# extra help

go to the following and watch the 11 minute video for more help
https://www.youtube.com/watch?v=oFYyTZwMyAg

if you want to see the introduction one to it you can see
https://www.youtube.com/watch?v=0fKg7e37bQE




# Mischelaneous(sp)



# webpack - css stylesheet loader

    npm install style-loader css-loader --save-dev
    
    {
        // ...
        module: {
            loaders: [
                { test: /\.css$/, loader: "style-loader!css-loader" }
            ]
        }
    }


# cd to a mapped drive

cd is primarily for changing to directories, you're trying to change drives.
from the command prompt type

    z: 

or

    cd /D z:

# RDP from the command line
mstsc.exe {ConnectionFile | /v:ServerName[:Port]} [/console] [/f] [/w:Width/h:Height] 




# Pull in one file with git

git fetch <remote>

git checkout FETCH_HEAD - - <file>
    
    
# Compare/Diff two different git branches

        git diff branch_1..branch_2

That will produce the diff between the tips of the two branches. If you'd prefer to find the diff from their common ancestor to test, you can use three dots instead of two:

        git diff branch_1...branch_2
  
    
# Trigger custom event with custom object with jquery in the browser
	$(this.parentReference).on('addedClassName', (e) => {
		console.log('in on part of trigger with: ', e);
	})
	$(this.props.parentReference).trigger({
		type: 'addedClassName',
		trReference: tr
	});	//send event up to parent component to add this tr into a variable array
						
	
# css keyframes syntax


        .fadeIn {
            animation: fadeIn 2s;
        }
        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }

        .buttonHover:hover {
            background-color: rgb(194, 185, 185);
        }

        .buttonHover:active {
            background-color: rgb(146, 145, 145);
        }
        .button {
            background-color: white;
        }


# Visual Studio Code
for windows cmd terminal

    "terminal.integrated.shell.windows": "C:\\WINDOWS\\System32\\cmd.exe",
    "terminal.integrated.shellArgs.windows": [
        "/K",
        "D:\\Developer\\CustomTools\\logonCommands.cmd"
    ]
    
for powershell

    "terminal.integrated.shell.windows": "C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe",
    "terminal.integrated.shellArgs.windows": [
        "-NoExit",
        "C:\\Users\\johnembry\\Developer\\CustomTools\\logonCommands.cmd"
    ]
  
  so the powershell one will kind of work, but the .cmd file's `DOSKEY c=cls` logic doesn't work in the powershell environment. I have to use `Set-Alias c cls` but the whole point of passing in the arguments was to have a custom script to generate the aliases for me...powershell has a file much like a `.bashprofile` or `.bashrc` file in Linux so to generate one if never setup before you can check if one already exists:
  
    Test-Path $profile
    
if `False` make a new profile

    New-Item -path $profile -type file –force
    
and it creates the file `New-Item -path $profile -type file –force` and stores it in:

    C:\Users\{USERNAME}\Documents\WindowsPowerShell
    

# AutoHotkey text replacer script
basically start AutoHotKey, go down to the notification area on the Windows toolbar/taskbar and right click the AutoHotKey logo and choose something like "edit this script" (that's what it currently shows me) and you can I guess add the following the what is currently defined in your file that pops up (or completely replace everything you have in yours with what is below...I say that because its what mine currently is and its working great)

        ;
        ; AutoHotkey Version: 1.x
        ; Language:       English
        ; Author:         Lowell Heddings | geek@howtogeek.com
        ;
        ; Script Function:
        ;	enable paste in the Windows command prompt
        ;

        #NoEnv  ; Recommended for performance and compatibility with future AutoHotkey releases.
        SendMode Input  ; Recommended for new scripts due to its superior speed and reliability.
        SetWorkingDir %A_ScriptDir%  ; Ensures a consistent starting directory.

        #IfWinActive ahk_class ConsoleWindowClass
        ^V::
        SendInput {Raw}%clipboard%
        return
        #IfWinActive

        ;jce start adding custom commands
        ::btw::by the way

        ::cmo::
        ;cmo === commented out
        FormatTime, CurrentDateTime,, yyyy
        mYear = %CurrentDateTime%
        mYear := mYear - 1700
        FormatTime, CurrentDateTime,, M
        mMonth = %CurrentDateTime%
        StringLen, monthLength, mMonth
        if(monthLength = 1) {
            mMonth = 0%mMonth%
        }
        FormatTime, CurrentDateTime,, d
        mDay = %CurrentDateTime%
        StringLen, dayLength, mDay
        if(dayLength = 1) {
            mDay = 0%mDay%
        }
        SendInput jce %mYear%%mMonth%%mDay% commented out
        return

        ::jcea::
        ;jcea === jceadded
        FormatTime, CurrentDateTime,, yyyy
        mYear = %CurrentDateTime%
        mYear := mYear - 1700
        FormatTime, CurrentDateTime,, M
        mMonth = %CurrentDateTime%
        StringLen, monthLength, mMonth
        if(monthLength = 1) {
            mMonth = 0%mMonth%
        }
        FormatTime, CurrentDateTime,, d
        mDay = %CurrentDateTime%
        StringLen, dayLength, mDay
        if(dayLength = 1) {
            mDay = 0%mDay%
        }
        SendInput jce %mYear%%mMonth%%mDay% added
        return

        ::jcec::
        ;jcec === jcechanged
        FormatTime, CurrentDateTime,, yyyy
        mYear = %CurrentDateTime%
        mYear := mYear - 1700
        FormatTime, CurrentDateTime,, M
        mMonth = %CurrentDateTime%
        StringLen, monthLength, mMonth
        if(monthLength = 1) {
            mMonth = 0%mMonth%
        }
        FormatTime, CurrentDateTime,, d
        mDay = %CurrentDateTime%
        StringLen, dayLength, mDay
        if(dayLength = 1) {
            mDay = 0%mDay%
        }
        SendInput jce %mYear%%mMonth%%mDay% changed
        return




        ::jcech::
        ;jcec === jcechanged
        FormatTime, CurrentDateTime,, yyyy
        mYear = %CurrentDateTime%
        mYear := mYear - 1700
        FormatTime, CurrentDateTime,, M
        mMonth = %CurrentDateTime%
        StringLen, monthLength, mMonth
        if(monthLength = 1) {
            mMonth = 0%mMonth%
        }
        FormatTime, CurrentDateTime,, d
        mDay = %CurrentDateTime%
        StringLen, dayLength, mDay
        if(dayLength = 1) {
            mDay = 0%mDay%
        }
        htmlCommentStart = <{!}--
        htmlCommentEnd = -->
        SendInput %htmlCommentStart% jce %mYear%%mMonth%%mDay% changed %htmlCommentEnd%
        return



        ::jcecj::
        ;jcec === jcechanged
        FormatTime, CurrentDateTime,, yyyy
        mYear = %CurrentDateTime%
        mYear := mYear - 1700
        FormatTime, CurrentDateTime,, M
        mMonth = %CurrentDateTime%
        StringLen, monthLength, mMonth
        if(monthLength = 1) {
            mMonth = 0%mMonth%
        }
        FormatTime, CurrentDateTime,, d
        mDay = %CurrentDateTime%
        StringLen, dayLength, mDay
        if(dayLength = 1) {
            mDay = 0%mDay%
        }
        SendInput //jce %mYear%%mMonth%%mDay% changed
        return

        ::jceaj::
        ;jceaj === jceaddedjavascript
        FormatTime, CurrentDateTime,, yyyy
        mYear = %CurrentDateTime%
        mYear := mYear - 1700
        FormatTime, CurrentDateTime,, M
        mMonth = %CurrentDateTime%
        StringLen, monthLength, mMonth
        if(monthLength = 1) {
            mMonth = 0%mMonth%
        }
        FormatTime, CurrentDateTime,, d
        mDay = %CurrentDateTime%
        StringLen, dayLength, mDay
        if(dayLength = 1) {
            mDay = 0%mDay%
        }
        SendInput //jce %mYear%%mMonth%%mDay% added
        return

        ::jcecc::
        ;jcec === jcechanged
        FormatTime, CurrentDateTime,, yyyy
        mYear = %CurrentDateTime%
        mYear := mYear - 1700
        FormatTime, CurrentDateTime,, M
        mMonth = %CurrentDateTime%
        StringLen, monthLength, mMonth
        if(monthLength = 1) {
            mMonth = 0%mMonth%
        }
        FormatTime, CurrentDateTime,, d
        mDay = %CurrentDateTime%
        StringLen, dayLength, mDay
        if(dayLength = 1) {
            mDay = 0%mDay%
        }
        SendInput /* jce %mYear%%mMonth%%mDay% changed */
        return

        ::jceac::
        ;jceac === jceaddedcss
        FormatTime, CurrentDateTime,, yyyy
        mYear = %CurrentDateTime%
        mYear := mYear - 1700
        FormatTime, CurrentDateTime,, M
        mMonth = %CurrentDateTime%
        StringLen, monthLength, mMonth
        if(monthLength = 1) {
            mMonth = 0%mMonth%
        }
        FormatTime, CurrentDateTime,, d
        mDay = %CurrentDateTime%
        StringLen, dayLength, mDay
        if(dayLength = 1) {
            mDay = 0%mDay%
        }
        SendInput /* jce %mYear%%mMonth%%mDay% added */
        return

        ::jceah::
        ;jceah === jceaddedhtml
        FormatTime, CurrentDateTime,, yyyy
        mYear = %CurrentDateTime%
        mYear := mYear - 1700
        FormatTime, CurrentDateTime,, M
        mMonth = %CurrentDateTime%
        StringLen, monthLength, mMonth
        if(monthLength = 1) {
            mMonth = 0%mMonth%
        }
        FormatTime, CurrentDateTime,, d
        mDay = %CurrentDateTime%
        StringLen, dayLength, mDay
        if(dayLength = 1) {
            mDay = 0%mDay%
        }
        htmlCommentStart = <{!}--
        htmlCommentEnd = -->
        SendInput %htmlCommentStart% jce %mYear%%mMonth%%mDay% added %htmlCommentEnd%
        return

        ;jce end adding custom commands
	
	
# css media query example

        @media (max-width: 1400px) {
	        #pageHeaderTabs {
		        font-size: 16px;
	        }
        }
	
# Perl

# get length of array

        $numberOfArguments = scalar @ARGV;
	
# push onto an array

        push @filesToPullIn, $_;
	
# RDP for command line access and other things about it

start from command line

    mstsc RDP_filename
   
launch with only terminal
   
    mstsc RDP_filename /console
   
specify a remote computer name `/f` for full screen
   
    mstsc RDP_filename /v:computername
    
you should be able to make an "RDPfile" that would store your login session by launching the GUI manually and pressing the save as option
