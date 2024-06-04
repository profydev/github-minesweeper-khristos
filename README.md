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
