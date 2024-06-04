# GitHub Minesweeper

Gain hands-on experience with a professional Git workflow used in many real-world teams with the help of a bot teammate. Find more information at [Profy.dev](https://profy.dev/project/github-minesweeper).


```sh
$ git clone https://github.com/profydev/github-minesweeper-khristos.git
$ cd github-minesweeper-khristos
```

## Further Reading

* [Protecting Git branches](https://spectralops.io/blog/how-to-set-up-git-branch-protection-rules/)
* [Connecting to GitHub with SSH](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh)
* [Forking Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/forking-workflow)

### Round 1: Trunk-Based Development
## Overview

Here's a quick overview of the steps required for our first move in the first GitHub Minesweeper game:

1. We create a new branch on our local machine
2. We edit the file commands.json
3. We commit and push the changes to the remote repo
4. We open a Pull Request on GitHub
5. We request a review by our bot-friend Tara on GitHub
6. We merge the PR

We'll start on our local machines with steps 1-3 and move to GitHub for steps 4-6.

## Steps on your local machine: Branch, Commit & Push

This repository has similar settings to real-world projects. One important part is that you can't push commits directly to the **main** branch.

Thus our first step is to create a new branch. We can use the **-b** option to create and check out a branch at the same time. Since this will be the first move of the first game let's use the name **move-1-1**.

```sh
$ git checkout -b move-1-1
$ git status
```

Let's start by clearing the field at the bottom left. Open the file **commands.json** and change the content to this:

```json
{
  "commands": [
    "clear A8"
  ]
}
```

Next, we stage the changes. In this case, we can simply stage all files.

```sh
$ git add .
$ git status
```

Finally, let's commit and push the changes to the remote repository on GitHub.

```sh
git commit -m "Clear A8"
git push origin move-1-1
```

## Further Reading

1. [How to write good commit messages](https://chris.beams.io/posts/git-commit/)
2. [The .gitignore file](https://www.atlassian.com/git/tutorials/saving-changes/gitignore)


## Create a Pull Request on GitHub

Now that we pushed the branch to GitHub it's time to create our first Pull Request. There are two options:

The first option is to click the link in the output of the **git push** command.

The second option is to open the repository on GitHub. You'll see a button [Compare & pull request] to create a PR if you pushed any branches recently.

Once you click either the link or the button, you should see a form to create the PR.

For branches with a single commit, the PR title is prefilled with the commit message. For branches with more commits, the title is created using the name of the branch.

In our case, the default title is "Clear A8". I'd rather call this PR "Move 1" and mention the field in the description.



## Request a Review

We created our first PR but can't merge it yet. We still need at least one approval from another developer.

We don't have a real developer at our disposal but our bot teammate Tara will help us out. Either select her from the suggested reviewers or click the gear icon to open the dropdown menu.

To send the review request you have to click outside the dropdown menu. Wait for a few seconds and Tara should leave a comment.

Great, we were lucky and didn't hit a mine. We can see the current state of the board to plan our next move. But before we continue with the next move, we should merge the PR so the file changes are available in the main branch.


## Merge the Pull Request

We created our first PR and got it approved. Now it's time to merge it to the main branch.

At the bottom of the page, you can see that the **"Squash and merge"** button turned green.

You might wonder why the button says "Squash and merge" and not only "Merge". We'll see what that means later.

For now, go ahead and click the button.

You should see a form that asks for a title and a description. The title is again prefilled with the commit message (similar to the PR title). I again replace it with "Move 1".

The text "#1" is the number of the Pull Request and will turn into a link in the commit history as we'll see in a bit.

To clean up you can delete the branch now. The good thing: you can recover it again. In theory, this should be possible indefinitely.
=======



