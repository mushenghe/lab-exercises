# lab-exercises

# Table of contents
1. [Git workflow](#lab-#1-introduction-to-git-workflow)

# Lab #1: Introduction to Git workflow

## Overview
This lab will provide a quick review of Git, what a typical release lifecycle may look like, and the workflow you will adopt during development. Git will be used heavily in this research lab, so the primary goal of this exercise is to familiarize yourself with the general workflow we use to maintain our repositories. This is extremely valuable for 

Keep in mind there are many workflows out there, each with their own set of advantages and disadvantages. By no means are we making any claims that *this* particular workflow is best or the only workflow that would serve our purposes or your own purposes in the future. However, it is important that as we work together as a team, we follow similar workflows as well as standards and conventions.

**Prerequisites:** 

**Pre-lab:** The goal here is simply to set your workspace in such a way that you can demonstrate all your work on your *own* private repository rather than on an argallab's repository. Generally, you will *not* be mirroring our repositories to develop code. This is strictly for bookkeeping reasons. Please contact a senior lab memeber if this is confusing.

**Verification:** After completion of this lab exercise, you will email screenshots of the certificate and a network graph of your progress to a senior lab member. 

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
git checkout -b feature-lab01-certificate
```
You can confirm this using the command `git branch` again. Notice, not only have you created a new branch, but you also switched to the new branch as well, indicated by the asterisk next to `feature-lab01-certificate-name` (this is a shortcut that will come in handy in the future). This is equivalent to
```
git branch feature-lab01-certificate
git checkout feature-lab01-certificate
```
It is important to note that, currently, the `feature-lab01-certificate-name` branch exists only on your local machine -- and is not reflected remotely. Thus, you can resolve this discrepancy by
```
git push origin feature-lab01-certificate-name
```
2. **Make local changes to your feature branch.** Go to your `images` folder and open `lab01_certificate.png` in your favorite photo editor (eg. Photoshop, Paint). (An application such as Preview or LibreOffice Draw will also suffice. For this exercise, the only tools you will need are textboxes and basic drawing tools.) Use a textbox to write your name in the designated area, and save it. You may have to export the changes and replace the old `lab01_certificate.png` file to accomplish this. You've done two things here: (a) made a change locally on your computer and (b) completed the feature you set out to accomplish (ie. added your name). 

3. **Update your remote repository with your local changes.** You can now update your remote repository to reflect the progress you've made. To complete part (a), you can go to your `lab-exercises` folder,
```
git add images/lab01_certificate.png
git commit -m "added my name to the lab01 certificate"
git push origin feature-lab01-certificate-name
```
This updates your feature branch `feature-lab01-certificate-name`.

4. **Update the development branch.** Recall, you've also completed your feature, part (b). Generally when you are working with other developers in a team and your feature is completed, you will have to test that your feature works with all the other features your team has developed since you created this feature branch in Step 1. Thus, you will need to `merge` those changes your colleagues have made to your code before updating the `devel` branch. 


```

```
5. Pull request to devel (from feature branch)
```

```
6. Merge release to devel
```

```