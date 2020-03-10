Title: My end-to-end Git Workflow 
Date: 2020-03-10
Modified: 2020-03-10
Category: Git
Tags: engineering, devops, automation, sysadmin, development, git
Slug: end-to-end-git-workflow
Authors: JohnVonNeumann
Summary: My git flow, not git-flow.

From master branch, to make sure you have a clean copy of your codebase, first, ensure you're on master:

        git branch

The output should be similar to this, with the "*" next to *master*:

        aaa1-lint-makefiles
        \* master
        setup-terraform-automation
        test-yamllint-ci-step

If your asterisk is positioned next to a different branch, you can return to the *master branch* with:

        git checkout master

Now that you are on *master*, you can branch into a feature branch for local development:

        git checkout -b {project_code}{issue_number}-short-summary

You will be prompted with your new branch name, otherwise you can re-run the first step to ensure you're now on the correct branch. Now you can continue your development.

When you have made an edit to a file, you will need to *stage* the change, this indicates to *git* that you wish to package it into a *patch* and introduce it to the codebase. Firstly though, we can check what changes are available for staging by running:

        git status

This will give us output detailing the current state of our local environment, showing a potential combination of *tracked* and *untracked* files.

Untracked files are files which have not been *checked into* our version control system. For example, if you have just created a new file, and have not *committed* that file into the code base.

Tracked files are files that have been checked into the version control system.

In this scenario, as we have not added anything, the above command will return:

        On branch aaa-test-example-branch
        nothing to commit, working tree clean

Lets say we add a file to the repository, we wish to commit this file, first, we perform some work on the file.

        touch example_file.py

We now verify that the file is in the repository and git is aware of it.

        git status

The output of which is:

        On branch aaa-test-example-branch
        Untracked files:
        (use "git add <file>..." to include in what will be committed)

        example_file.py

Now that we've confirmed git is aware of our file, we can stage it. With the name of your file, run:

        git add example_file.py

We can now check whether the file has been staged with:

        git status

You will receive output similar to this, indicating that the file is now ready to be committed, if this is the first time you have committed a particular file, it will state that it is a *new file:*:

        Changes to be committed:
        (use "git reset HEAD <file>..." to unstage)

        new file:   example.py

You can now commit the change. Committing something is basically to package it into a change, and add it as a piece of work, consider it *git*'s primary data unit, repositories are built up of hundreds or thousands of commits, each telling part of a story of a project.

        git commit

This will spawn a new window in the text editor specified in your git settings, allowing you to leave a message to go along with the commit.

Commit messages should help tell a story, the *git log* will live for the length of the solution, and should enable other engineers to understand how the code was written and in some cases, why it was written the way it was. A good git log helps engineers create a better solution, by providing them with valuable context to utilise in their day to day engineering.

A good structure to use for commit messages is:

* {UPDATE, DELETE, CREATE} - A verb to describe at a high level what you are doing in this commit, for example you may be adding an entirely new file, so you may choose to start your message with "CREATE".
* The file name you are impacting - This should be the file name of the file being worked upon, we may be creating the new python file, *example_file.py* so we can set this to "example_file.py"
* A dash to separate the header of the message from the description to come.
* A short description to tell the reader from a high level what/why you are doing. For example, "example script for git how-to blog". Ideally, this should be kept to under 78 characters, otherwise it will wrap in the ggit log and be harder for engineers to read.
* Finally, underneath this, we add an extended explanation, after performing a double carriage return, this extended message will not show in the short log, only in the full log, so we can be more elaborate in our explanation of the change here, ultimately we wish to detail why we are performing the change, any interesting context around this change (Were their issues, Is this a workaround for a bug in a vendor software?), be detailed in your message. For example: "In order to explain the example git workflow in the how to guide, I had to create an example file with an add/commit workflow along with a simple way to understand the best way to set out a commit message. This change will illustrate an example that will assist developers craft better commit messages."

This leaves us with a final commit message of:

        CREATE example_file.py -  example for git how-to

        In order to explain the example git workflow in the how to guide, I
        had to create an example file with an add/commit workflow along with
        a simple way to understand the best way to set out a commit message.
        This change will illustrate an example that will assist developers
        craft better commit messages.

Type in your message, ensuring that you keep your subject line shorter than 50 characters and your body lines shorter than 72 characters otherwise the comments will not line wrap and people reading the git log will have an awkward time reading.

Now that we have written out our commit, we can save it:

        :wq

Our output will look something like this:

        [aaa-test-example-branch 6b20c8a] CREATE example_file.py -  example for git how-to
         1 file changed, 0 insertions(+), 0 deletions(-)
         create mode 100644 example_file.py

We can now check whether our commit was created with another call to status, if the commit has been created, we will not receive any additional output than we did from our original call to git status at the start of the guide:

        git status

However, if we check the git log, we will see our commit at the HEAD of the chain:

        git log

Returning:

        commit 6b20c8aada7ae3c97fed086ab00e86d0312224fe (HEAD -> aaa-test-example-branch)
        Author: JohnVonNeumann <louiswillcock@gmail.com>
        Date:   Thu Oct 17 14:31:50 2019 +1100

        CREATE example_file.py -  example for git how-to

        In order to explain the example git workflow in the how to guide, I
        had to create an example file with an add/commit workflow along with
        a simple way to understand the best way to set out a commit message.
        This change will illustrate an example that will assist developers
        craft better commit messages.

This shows that we have indeed committed our change, the only issue is that it only exists on our local repository, in order to tell our source of truth about it, the remote; we must *push* the code.

        git push origin branch-name

Now that our change is in our remote branch, in order to have this change integrated into the master branch we must issue a *merge request* or a *pull request* depending on the platform you're currently using to support git.

This will typically be done via the GUI, so we can navigate to there to issue the merge request, you can search online to find out how to do this.

By this stage, it will be assumed that you have received the correct number of approvals for your branch and new code, so you can proceed to get the thing merged.

We position ourselves onto the local branch we are working on, use the processes mentioned up above, in this example we are going to assume that inside the *master* branch there are commits that have been merged since we started developing our code, as this will be the trickiest situation to deal with.

Once you are located on the branch, you can *pull* the changes from master into your branch, which will add changes and place them onto your branch, effectively removing the need for dirty merge commits that clog up the git log.

        git pull --rebase origin master

We can assert that the changes have been pulled into our branch with our handy friend *git log*.

Finally, now that the changes from remote master are in your local branch, you can push them upto your remote branch, however, as you have pulled in changes from elsewhere and performed a rebase, your remote branch will complain that the tip of your local branch is *behind* the remote. This is incorrect, we are ahead, so we need to *force* the changes upon the remote.

        git push origin branch-name --force-with-lease

Finally, you can either migrate back to the GUI and use the button to merge the code, or you can do it from your terminal if you have the privileges to merge code.

        git fetch origin
        git checkout master
        git merge branch-name
        git push origin master
