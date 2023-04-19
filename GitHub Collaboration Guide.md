# GitHub Collaboration Guide

Below is a brief guide to help us all collaborate on our project and make sure we don't create unnecessary issues when working on our features. Two terms you'll see often are "local repo" and "remote repo". "Local repo" refers to the git repository on your local machine. "Remote repo" refers to the project repository housed on GitHub.

## 1. Navigate to the Folder You Want Your Cloned Repo to Be Housed Inside

Let's say you want to your local version of the project repo to be housed inside a folder called "Projects_and_Algorithms". `cd` into that folder in your command line:

![](Screenshot%202023-04-19%20at%209.19.50%20AM.png)

## 2. Make Sure This Folder Is Not Already a Part of a Local Git Repo

In order to avoid the headache of dealing with a nested git repo, check to make sure the folder you are cloning the remote repo into is not already a part of a git repo.

You can do this by entering  `git status` in the command line from inside the folder you want to clone the remote repo into. If things are good, you will see the following message:

`fatal: not a git repository (or any of the parent directories): .git`

If your folder is part of a parent directory that is being tracked in a git repo, you will see something like the following:

```
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

## 3. Clone the GitHub Project Repository to Your Local Machine

Once you have the URL for the remote repo, clone the remote repo to your local machine by entering the following command into your command line (minus the carrots): `git clone <project-url>` 

Once you enter the command, your command line should look something like the following:

![](Screenshot%202023-04-19%20at%209.23.38%20AM.png)

Now, when you run the `ls` command, you should see the cloned repo listed. Go ahead and `cd` into that directory.

Your command line should indicate that you are now in a local git repository, on branch "main".

![](Screenshot%202023-04-19%20at%209.28.58%20AM.png)

Now, when you run `git status` , you will see what local branch you are on as well as the remote branch you are connected to. The remote repository is called `origin` , and particular branches on that remote repository will be named following a forward slash:

![](Screenshot%202023-04-19%20at%209.33.18%20AM.png)

It is always a good idea to run `git status` to see an up-to-date report on the status of your local and remote repository.

## 4. Create a Descriptively-Named Local Branch and Switch Over To It

It is crucial that everyone do their developing on a feature branch rather than on the main branch. First of all, it ensures that we don't interfere with each other's work. Second, the main branch on the remote repo is protected, which means that you will receive an error message when you try to push your code up to the remote repo.

For example, let's say I create a file called "index.html" while I'm on the main branch of my local repo. Then I stage and commit that file using `git add .` and `git commit -m "added index.html file"` . When I try to run `git push` to push my commit up to the remote repo, I get an error message:

![](Screenshot%202023-04-19%20at%2010.23.38%20AM.png)

To avoid this, I need to create my own local branch before I start writing any of my own code. I can do this by entering `git branch -c <name-of-feature-branch>` (minus the carrots). **Please make sure you use a descriptive name for your branch.** Instead of calling it something like "my-branch", choose a name that more accurately represents the actual feature you are working on. 

For example, if I am working on creating html files for the project, I could create a branch called "html". I would do this by entering `git branch -c html` .

To make sure my branch was created, I can enter `git branch` . This will show a list of all the branches in my local repo and will show which branch I am currently on.

To switch over to my local feature branch, I should enter `git switch html` .

![](Screenshot%202023-04-19%20at%2010.55.22%20AM.png)

To simplify the process, you can both create a new branch and switch over to that new branch by entering `git checkout -b <name-of-feature-branch>` (minus the carrots).

![](Screenshot%202023-04-19%20at%2011.58.06%20AM.png)

## 5. Create a Feature Branch on the Remote Repo

After you have created and switched over to your local feature branch, you should create a branch in the remote repository to track this branch. You can do this by using the command `git push --set-upstream origin <name-of-remote-feature-branch`. Make sure the names of your local and remote feature branches are identical to avoid any confusion.

![](Screenshot%202023-04-19%20at%2012.41.41%20PM.png)

The bottom line in the screenshot above confirms that a new remote branch ('origin/html') has been created and that your local feature branch ('html') is now connected to it.

To view the change on GitHub, navigate to the project repository and click on the dropdown button that has a branch icon and says "main".

![](Screenshot%202023-04-19%20at%2012.57.25%20PM.png)

Here, you can see that the "html" remote branch has been created.

## 6. Make Sure Your Local Feature Branch Is Up To Date with 'origin/main' Before Adding Your Own Code

"origin/main" is the name of our code base on GitHub. It is the protected branch, the "main" branch, that we merge new features into. "origin" is a reference to our remote repository.

Let's say I'm on my local branch, called "html". I'm ready to add some HTML to our project. Before I do, I want to pull any updates to the main branch on our remote repo into my local branch so that my copy of the code base is up to date. To do this, I make sure, first, that I'm on my local feature branch, and then I run `git pull origin main` . This command fetches any new commits from the main remote branch into my local feature branch and merges those commits.

![](Screenshot%202023-04-19%20at%2012.55.53%20PM.png)

Since I hadn't added any code to my local feature branch yet, git simply performed a fast-forward merge and updated my local branch with a new file ("index.js") that had been added to the main branch in the remote repo.

## 7. Make Sure Your Local Feature Branch Is Up To Date with 'origin/main' Before Pushing Your Commits

Let's say I've added an "index.html" file to my local feature branch. I've staged and committed my changes and pushed my code up to my remote branch. 

![](Screenshot%202023-04-19%20at%201.10.12%20PM.png)

However, while that was going on, the remote main branch was updated. Because I didn't run `git pull origin main` to make sure my local branch is up to date with origin/main, my branch is out of sync. I can see this if I look at my remote branch on GitHub:

![](Screenshot%202023-04-19%20at%201.13.01%20PM.png)

My branch is one commit ahead of main because it has the index.html file that I wrote, which is not on the main branch. That's normal. The problem is that my branch is also one commit behind main, meaning that main has updated code that is not reflected in my branch.

If I try to run `git pull origin main` to fix this conflict, I will get the following message:

![](Screenshot%202023-04-19%20at%201.22.52%20PM.png)

I need to decide what git should do when it can't simply perform a fast-forward merge (i.e., when the merge is complicated by different files having different versions). In order to resolve merge conflicts my self, I can enter `git config pull.rebase false` :

![](Screenshot%202023-04-19%20at%201.26.16%20PM.png)

git will now open my default text editor (VS Code in my case) and have me resolve my merge conflicts there.

VS Code opens with a tab that shows a default commit message. I'll shorten it to keep it under the 50 character limit.

![](Screenshot%202023-04-19%20at%201.33.21%20PM.png)

In the sidebar on the left, VS Code shows me where the merge conflicts are. In my case, they are in the "index.js" file.

I click on the source control icon with the blue "1" badge, I can see what the differences are between my branch's version of origin/main and the actual code in origin/main.

By clicking on the "index.js" file in the source control sidebar, I see, thankfully, that my out-of-date version of origin/main is simply missing an additional line of code in "index.js".

![](Screenshot%202023-04-19%20at%201.49.32%20PM.png)

Now that I have reviewed the changes, I can finish the merge by clicking on the "Commit" button beneath the message that says "Merge branch 'main'..."

Then I click "Sync Changes", which effectively pushes my updated branch to my remote branch.

![](Screenshot%202023-04-19%20at%201.52.54%20PM.png)

Now, my remote branch is up to date with origin/main, and I can move forward with developing my feature branch.

![](Screenshot%202023-04-19%20at%201.57.30%20PM.png)

As a practice, try running `git pull origin main` from your local branch before adding new code to your branch. If your branch ends up somehow being out of sync with origin/main, the problem is fixable. It just requires an extra step or two.

## 8. Make a Pull Request When Your Feature Branch Is Ready

When you have finished *and tested* the code in your feature branch and made sure there are no bugs, you can request that your branch be merged into origin/main by creating a pull request.

If you visit your remote branch on GitHub, click on the dropdown menu next to the message saying how many commits ahead of main your branch is. Then click on the button that says "Open Pull Request".

![](Screenshot%202023-04-19%20at%202.03.26%20PM.png)

You will be prompted to write a message with a title. Write down anything you think is important for whoever will review the pull request to know.

**Important:** Your branch needs to be up to date with main before you open a pull request. In other words, your branch should not be behind main by any commits, as mine was in the example in the previous step.

![](Screenshot%202023-04-19%20at%202.17.48%20PM.png)

Click on the "Create pull request" button, and your pull request will be flagged for review.