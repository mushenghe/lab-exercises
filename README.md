# lab-exercises

# Table of contents
1. [Git workflow](#lab-1-introduction-to-git-workflow)

# Lab 1: Introduction to Git workflow

## Overview
This lab will provide a quick review of Git, what a typical release lifecycle may look like, and the workflow you will adopt during development. Git will be used heavily in this research lab, so the primary goal of this exercise is to familiarize yourself with the general workflow we use to maintain our repositories.

Keep in mind there are many workflows out there, each with their own set of advantages and disadvantages. By no means are we making any claims that *this* particular workflow is best or the only workflow that would serve our purposes or your own purposes in the future. However, it is important that as we work together as a team, we follow similar workflows as well as standards and conventions.

**Pre-lab:** The goal here is simply to set your workspace in such a way that you can demonstrate all your work on your *own* private repository rather than on an argallab's repository. Generally, you will *not* be mirroring our repositories to develop code. This is strictly for bookkeeping reasons. Please contact a senior lab memeber if this is confusing.

**Verification:** After completion of this lab exercise, you will email your certificate and a screen capture of the network graph, of your progress, to a senior lab member. 

## Instructions
### Pre-lab: Getting started
We want you to essentially create a copy of this repository and place it your own private repository. Git calls this mirroring. This is so that you can track your own progress of this exercise in your repository. Please read these instructions carefully to get started.

1. **Create a new private repository.** Click on this [link](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-new-repository) and follow the instructions to create a new repository on your own account. Name this repository, `lab-exercises`.

2. **Set up your workspace.** Open your Terminal, and create a catkin workspace:
```
mkdir -p ~/lab01_ws/src
```
3. **Mirror this repository.** Clone a bare copy of this [repository](https://github.com/argallab/lab-exercises.git) on your local machine:
```
cd ~/lab01_ws/src
git clone --bare https://github.com/argallab/lab-exercises.git
```
Then, mirror-push this to your private repository:
```
cd lab-exercises.git
git push --mirror https://github.com/<your_github_handle>/lab-exercises.git
```
Note, alternatively, the web url after `--mirror` can be copy-pasted directly from your private repository webpage by clicking on the "Clone or download" button and the clipboard icon.
4. **Clean up your workspace.** Lastly, now that the mirroring step is complete, you no longer need the cloned bare copy. You can remove this by
```
cd ..
rm -rf lab-exercises.git
```
The only thing left in your `src` folder should be the `lab-exercises` folder.

### Exercise
1. **Create a new feature branch.** In your Terminal, go to the `lab-exercises` folder.  
```
cd ~/lab01_ws/src/lab-exercises
```
Everything in this folder represents the contents of the git repository you created in the pre-lab, and, currently, the contents contained locally are synchronized with the contents that are contained remotely. You can confirm this by
```
git status
```
You can also examine the current branch structure by
```
git branch
```
Switch your branch to `devel` and create your first feature branch by
```
git checkout devel
git checkout -b feature-lab01-certificate-name
```
or
```
git checkout -b feature-lab01-certificate-name devel
```
You can confirm this using the command `git branch` again. Notice, not only have you created a new branch, but you also switched to the new branch as well, indicated by the asterisk next to `feature-lab01-certificate-name` (this is a shortcut that will come in handy in the future). This is equivalent to
```
git branch feature-lab01-certificate-name
git checkout feature-lab01-certificate-name
```
It is important to note that, currently, the `feature-lab01-certificate-name` branch exists only on your local machine -- and is *not* reflected remotely. Thus, you can resolve this discrepancy by
```
git push origin feature-lab01-certificate-name
```

2. **Make local changes to your feature branch.** Go to your `images` folder and open `lab01_certificate.png` in your favorite photo editor (eg. Photoshop, Paint). (An application such as Preview or LibreOffice Draw will also suffice. For this exercise, the only tools you will need are textboxes and basic drawing tools.) Use a textbox to write your name in the designated area, and save it. You may have to export the changes and replace the old `lab01_certificate.png` file to accomplish this. You've done two things here: (a) made a change locally on your computer and (b) completed the feature you set out to accomplish (ie. added your name to the certificate). 

3. **Update your remote repository with your local changes.** You can now update your remote repository to reflect the progress you've made. To address part 2(a), you can go to your `lab-exercises` folder,
```
git add images/lab01_certificate.png
git commit -m "added my name to the lab01 certificate"
git push -u origin feature-lab01-certificate-name
```
where the `-u` flag allows for remote tracking of this branch and ensures that future `git pull`s will behave seemlessly. These commands will update your remote feature branch `feature-lab01-certificate-name` with the changes you made locally. 

4. **Update the development branch using a pull request.** Recall, you've also completed your feature (step 2(b)), adding your name to the certificate. Generally when you are working in a team and your feature is completed, you will have to test that your feature works with all the other features your team has developed since you created this feature branch in step 1. Thus, you would need to `fetch` and `merge` those changes your colleagues have made to your code -- without endangering your work from being overwritten -- *before* testing or updating the `devel` branch. 
```
git checkout feature-lab01-certificate-name
git fetch origin
git merge devel
```
At times, `git merge` will indicate what are called merge conflicts. This generally means that you and your team members have been working on the same files and requires you to execute a separate set of instructions to resolve any conflicts between you and your team members' work. This is beyond the scope of this lab exercise, but if you are curious, you can read about resolving merge conflicts [here](https://www.atlassian.com/git/tutorials/using-branches/merge-conflicts).

If you are thinking, why not just simply `git pull` in these scenarios? Well, we'd like to caution you from getting in the habit of relying on this command for this scenario. This is simply because you generally don't know what changes others have been making, and a `git pull` may very well overwrite hours/days of your work in a blink of an eye. By taking these conservative steps, you will guarantee full control over these situations. To read more about this, we recommend this quick [article](https://medium.com/@sabbirhossain_70520/git-fetch-vs-git-pull-691823ed4239). There is also debate over whether to use `rebase` instead of `merge`; again, this is beyond the scope of this exercise, but we recommend this (article)[https://www.atlassian.com/git/tutorials/merging-vs-rebasing] if you are interested in reading more about this discussion.

Once the integration of others' code with your feature branch is completed and tested, you can now safely update your remote repository by
```
git push -u origin feature-lab01-certificate-name
```
Now, you can make a pull request. A pull request allows your supervisor or other colleagues an opportunity provide you with another set of eyes and ensure it is indeed safe to incorporate your feature into more stable branches, such as `devel` or `master`. Since this is an exercise that currently lives on your own private account, you will act as both the developer making a pull request and as the reviewer. The simplest way to make a pull request is to:
	1. Go to your private `lab-exercises` repository using a web browser (`https://github.com/<your_github_handle>/lab-exercises`)
	2. Switch your branch to your feature branch, by clicking on the "Branch: master" button and selecting "feature-lab01-certificate-name" under "Branches"
	3. Click on "New pull request" (next to "Branch: feature-lab01-certificate-name")
	4. Check that "base" is set to "devel" and "compare" is set to "feature-lab01-certificate-name"
	5. Click on the green button, "Create pull request"

In order to accept a pull request, 
	1. Go to the "Pull requests" tab
	2. Select this particular pull request
	3. Click on "Merge pull request" and again on "Confirm merge"
	4. Click on "Delete branch"

The last task in this step is to create a drawing of yourself (or something that you identify with) in the certificate. Have fun with it. You will create another branch (from `devel`) called `feature-lab01-certificate-drawing` and follow similar steps as you did above. Once your feature branch is integrated with the `devel` branch, you are ready to move to the next step.

5. **Create a release branch and integrate features to the master branch.** The lifecycle wouldn't be complete without a release. Typically, your team will develop many exciting features (more interesting than the features in this exercise, we hope) that will warrant a stable, more official version of the project. This may mean more senior members will get involved and actively engage in the review process -- to ultimately ensure that the released product meets our high standards. A significant portion of time here may be spent on editing/writing clean `README` files, finalizing which features to include, or running automatic documentation generators (eg. Doxygen) on the codebase. The process will look very similar to steps you saw in step 4.

First, you will create a release branch (from devel)
```
git checkout -b release/1.0 devel
```
This is where you and others may spend time preparing the code to be released (eg. documentation) and determine when it is ready for primetime.

Open your `README.md` file in a text editor (eg. vim, Sublime Text). Next to "Lab #1: Introduction to Git workflow", type "This is ready for primetime!" and save it.

Let's just imagine your team has reviewed everything and agrees with your declaration. Make a pull request, where this time, "base" is set to "master" and "compare" is set to "release/1.0". Accept the pull request. 

6. **Update your development branch with changes made in the release branch.** In the process of preparing a release version of the code, the `release/1.0` branch has diverted slightly from the `devel` branch. It is important to note that while some have been part of the release process, others in your team may have continued developing new features. Therefore, `release/1.0` has to be integrated back into the `devel` branch. In order to do this, you can
```
git checkout devel
git merge release/1.0
git push -u origin devel
```
Since the `release/1.0` branch has served its purposes, you can now remove it. You can do this by removing it locally:
```
git branch -d release/1.0
```
and remotely:
```
git push origin --delete release/1.0
```

## Verification
Email your certificate and a screenshot of your network graph to a senior lab member. One way to do the latter is to go to your `lab-exercises` repository using a web browser, clicking on the "Insights" tab, and then selecting on "Network". You should be able to this similarly usings tools such as `gitk`.

