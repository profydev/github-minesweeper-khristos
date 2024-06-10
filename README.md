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
## [Overview](https://profy.dev/project/github-minesweeper/feature-lifecycle-overview)

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

## What just happened? A look at the commit history

To get a better understanding of what just happened let's have a quick look at the commit history of the main branch.

To open it navigate back to the main page of the repository.

Then click on the commits.

Now you can see the list of all commits on the main branch.

As you can see we have two commits:

1. the initial commit when the repository was created and
2. the commit that we just created by merging the PR.

Note that the title we entered when we created the PR became the commit message Move 1 ( #1 ).

As promised, the #1 turned into a link to the Pull Request. This comes in very handy when you have to investigate the commit history of a larger project e.g. while tracking down a bug. Once you find the responsible commit you can look at the PR to understand the larger context. Assuming that the PR has a good description of course.



### Round 2: Continuous integration

## Overview

We're ready to make our second Minesweeper move. We will basically repeat the steps from the last round. This time I won't describe these steps in much detail anymore so you can start practicing for yourself.

But there will be something new to learn as well:

1. A quick introduction to Continuous Integration and GitHub Actions
2. An explanation of "Squash merging"


## Syncing the local main branch

What does the commit history on our local machine look like?

Let's see. Head back to your terminal and run

```sh
git checkout main
```

To get an overview of the commit history we can run the **git log** command. I like the **oneline** option because it gives a more concise overview of the commits.

```sh
git log --oneline
```

>*If you ever see a : in the last line (see screenshot below) and don't know what to do anymore: You just opened the VIM editor. You can hit the **return** key to show the next line or **q** to exit the editor.*

Interesting. Unlike on GitHub we only see the initial commit on our machine.

But that makes sense. We clicked the "Merge" button on GitHub. So our local repository is not yet aware of the second commit on the main branch. We need to sync the repositories first.

To sync our local branch with the remote repository we use the **git pull** command. Note that it's important that we're on the main branch.

```sh
git pull origin main
```

Alternatively, you can use the short-hand command **git pull**. The difference is that this will pull all the tracked branches instead of only **main**.

>*If you see a yellow hint about "Pulling without specifying how to reconcile divergent branches" you can simply use one of the suggested commands to get rid of it the next time (e.g. **git config pull.rebase false**).*

Let's look at the commit history again to verify that everything worked fine.

```sh
git log --oneline
```

Now you should see both commits exactly as you did on GitHub.



## [Adding the second move](https://profy.dev/project/github-minesweeper/second-move)

For the second move, we again need to create a new branch from the **main** branch.

```sh
git checkout -b move-1-2
```

Replace the content of **commands.json** with this:

```json
{
  "commands": [
    "clear A8",
    "flag C3",
    "flag D2"
  ]
}
```

Now commit the file changes. Instead of using the **git add .** command to stage the file before committing we can commit it directly with the **--all** or **-a** option.

```sh
git commit -a -m "Flag fields with mines"
```

>*You can already push the commit to GitHub if you like. In real-world projects with larger feature PRs you would push from time to time just to backup your code. You might also ask your teammates for early feedback with a "Draft PR" just to make sure you're heading in the right direction. This can be very valuable especially for Junior devs.*


Now let's clear the next field. We'll simply add the next line to **commands.json** and commit it again.

>**Note: The file content below is invalid. That's on purpose. It's important that you copy & paste the exact content to your repo.**

```json
{
  "commands": [
    "clear A8",
    "flag C3",
    "flag D2",
    "clear H9
  ]
}
```

Next, commit and push the changes.

```sh
git commit -a -m "Clear H9"
git push origin move-1-2
```

>*Note: The link to create a PR in the output of the **git push** command only appears when you push the branch for the first time. If you don't see it you can create PR in the GitHub UI.*

Finally, create the PR on GitHub. **This time try it on your own.**

Here are the steps you need to open a PR:

* open the repository on GitHub
* click the **"Compare & pull request"** button (see screenshot below)
* enter the title "Move 2"
* enter a description
* click the **"Create pull request"** button

Once you created the PR head to the next section.


## Continuous Integration pipeline

By now you opened the PR for our second move. After waiting for a short while you should see this:

What a happy message: "All checks have failed." But what does that mean exactly? **This is the Continuous Integration pipeline in action.**

Let's have a closer look and click on the "Details" link.

You should now see the logs of the CI scripts.

We'll see in a bit how this works. But for now, let's fix the errors.

The error message states **The commands.json file contains a syntax error: Unexpected token in JSON.**

So the JSON in **commands.json** is invalid. My editor actually told me so from the beginning.

The last command needs a closing double-quote. Ok, no problem. Head back to your local repository and replace the content in **commands.json** with the following:

```json
{
  "commands": [
    "clear A8",
    "flag C3",
    "flag D2",
    "clear H9"
  ]
}
```

Commit and push again.

```sh
git commit -a -m "Fix JSON format"
git push origin move-1-2
```

Great. Now the CI scripts will run again. Let's head back to GitHub and see what we get.

>*Note: you have to go back to the Pull Request's main page e.g. via the **"Conversation"** tab. You may need to refresh that page to see the updated CI checks.*

Damn, the checks failed again. This time try and find the problem yourself first.


The problem is that we added the command **clear H9** but the field **H9** doesn't exist. Let's rename it to **H8**.

```json
{
  "commands": [
    "clear A8",
    "flag C3",
    "flag D2",
    "clear H8"
  ]
}
```

**Once you're done commit and push again.** Now the CI checks should turn green.

Before we continue with the PR, let's get a quick overview of what just happened.


## [Detour: GitHub Actions and CI](https://profy.dev/project/github-minesweeper/github-actions)

On the last page, we saw the Continuous Integration pipeline (or short CI pipeline) in action. We pushed invalid code to the remote repository on GitHub. That caused the CI pipeline to fail. And that again prevented us from merging a broken JSON file and a non-existent field.

In a real-world project, CI pipelines work pretty much the same. They run automated tests, type checks, a linter, or other tools like Prettier. This helps to keep the codebase consistent and prevents bugs.

### To clarify, let's paint a realistic scenario

Imagine you're working on a new feature for a large application. You write the code, commit and push it to GitHub. Then you open a PR and request a review from your teammates. Exactly as we did here. Your teammates review the code and test the feature.

Everything seems to work. So they approve the PR.

But of course, their time is limited. They can't test every feature in the whole application. So they miss something important. To build the new feature you had to adjust a piece of code that is used in different places of the app. And unfortunately, you broke it.

Without a CI pipeline, you could just go ahead and merge the PR. You would introduce a bug into seemingly unrelated features. This bug would end up in the production application which is used by real users. That can be costly.

With a CI pipeline that runs automated tests, this bug can easily be prevented. The pipeline fails and you can't merge the PR. Even if your teammates think the code works.

### Great. But how does our CI pipeline work?

Our project uses a native GitHub feature called GitHub Actions. With GitHub Actions, we can run scripts and code in a virtual machine within GitHub. The same scripts that we can also run in the terminal on our local machine (e.g. **npm start**).

The actions are defined in the file **.github/workflows/main.yml** in the repository. You can check it in your editor. This is what it looks like:

```yaml
# name of the workflow
name: CI

# event that triggers the workflow
on:
  pull_request:
    branches: [ main ]

jobs:
  # this is the only job of our workflow
  validate:
    # the docker image that is used (a virtual Ubuntu machine)
    runs-on: ubuntu-latest

    steps:
    # checkout the code from the repository
    - uses: actions/checkout@v2

    # runs a node script to validate the json file
    - name: Validate Commands JSON structure
      run: node ./internal/validate-commands-json.js
    
    # runs a node script to validate the commands 
    - name: Validate Commands
      run: node ./internal/validate-commands.js
```

This may look like Gibberish to you. But what it means is basically that it

1. starts a virtual Ubuntu machine
2. checks out the code from the repository
3. runs a Node.js script that checks the JSON format of the **commands.json** file
4. runs another Node.js script that checks if all commands in that file are valid.

These steps are triggered whenever new changes are pushed to a PR. In a real-world project, they typically run commands like **npm run build** or **npm run test** instead of the command **node ./internal/validate-commands-json.js** in our project.

This might still feel a bit abstract so let's see how the YAML file relates to the error messages that we saw on GitHub on the last page.


Here you can see where each part of the YAML file is shown in the GitHub UI. The error message in the logs ("The commands.json file contains a syntax error") is the output of the **node ./internal/validate-commands-json.js** command.

As mentioned, the workflow is defined in a YAML file. This file and the two Node.js scripts mentioned above are stored inside our repository as you can see below.

Of course, this CI pipeline is very basic. You can do a lot more with GitHub Actions. As a foundation, this should be sufficient though.

After this detour into Continuous Integration and GitHub Actions, we're ready to finish our second move in our GitHub Minesweeper game. Along the way, we'll take a closer look at squash merging.

## Further Reading

1. [CI/CD: Continuous Integration & Delivery](https://semaphoreci.com/cicd)
2. [Learn more about GitHub Actions](https://docs.github.com/en/actions/learn-github-actions)


## Merge the PR

At this point, you should have a PR for our second move and the CI checks at the bottom should have turned green.

Only one step left: At this point, the "Merge" button is still disabled because we need to get a review.

So go ahead and request another review by our teammate Tara. She'll leave this comment in a bit:

Yay, we again didn't hit a mine! Finally, merge the PR and we're done with our second move.

Before we continue with the next move, let's understand why the button says "Squash and merge" instead of simply "Merge".


## Squash & Merge

I kept you wondering about the "Squash and merge" button for a while now. Finally, it's time to reveal the secret: What's the difference between a "normal" merge and a squash merge?

First, let's quickly remember what we did on the previous pages: We created a PR with 4 commits in total. This is the commit history of the PR on GitHub:

With a "normal" merge (also called fast-forward merge) all of these commits would end up in the main branch.

Note that commits like "Fix JSON format" or "Rename field H9 to H8" don't add a lot of value but just fix small problems that were introduced within the PR. In real-world teams, you can often see similar commits like "Address review comments" or "Fix tests".

**The question is: Do we really want all these commits on the main branch?**

Commits like these are irrelevant outside the PR and would just add clutter to the history of the main branch. The history would become hard to read and understand.

That's where the **"squash and merge"** button comes into play. Let's see how that improves the readability of our main branch. Since we already squash merged the "Move 2" PR we can simply look at the history of the main branch on GitHub to see what happened.

Instead of the 4 commits that we saw in the PR we only have one new commit "Move 2 (#2)" on the main branch. The commits from the **move-1-2** branch have been combined (or squashed) into a single commit on **main**.

**So by using squash merge the history of the main branch contains only one commit per PR.** That makes the history of the main branch much more readable and easy to understand in the long run. And since the commit on the main branch links directly to the PR we don't even lose all the details and context.

Two quick notes:

1. Squash merging is not a requirement in Trunk-Based Development. It's just my experience, that many companies use it nowadays.
2. There is another advantage to squash merging: The history of the main branch stays "linear". It would require a deeper dive into Git to correctly explain this. If you're interested have a look at the link in the "Further Reading" section below.

Great, we successfully finished the second round of GitHub Minesweeper. It's time for our final move.

## Further Reading

1. [Different merge strategies and advantages of squash merge](https://blog.dnsimple.com/2019/01/two-years-of-squash-merge/)


### Round 3: Being the reviewer
## [Overview](https://profy.dev/project/github-minesweeper/overview-reviewer)

Spoiler alert: After two successful rounds of Minesweeper it'll be "game over" soon.

>*Don't worry. To practice Trunk-Based Development you can start a new game as often as you like. The goal is to build up muscle memory, right?*

Until now, we created Pull Requests and our bot-friend Tara approved them. In this chapter, you will learn how the review process looks from the other side. This time you'll review a PR.

Let's start by adding the next move.


## The final move

Before we edit the commands file **remember to sync our local repository with the remote one**.

These are the Git commands you need to run on your local machine to sync the **main** branch:

```sh
git checkout main
git pull origin main
git log --oneline
```

The last line isn't really necessary. But why not double-check that everything looks fine?!

Now it's time for the final move. Try the next steps for yourself.

* create and checkout a new branch called **move-1-3**
* add command "clear H7" to the array in the file **commands.json**
* commit and push the changes
* open a PR on GitHub
* wait for the CI checks to finish and request a review.

These are the Git commands you need:

* Create and check out the new branch: **git checkout -b move-1-3**
* Commit the file changes: **git commit -a -m "Clear H7"**
* Push the changes: **git push origin move-1-3**

You saw it coming. H7 wasn't a great choice. The game is over because we uncovered a mine.

**Great news though: Tara created a PR that lets you start a new game.** That's what we'll do in the next section.

But before we get there, let's close this PR to keep the repository tidy.

Again, you can delete the branch since it's not needed anymore.

Now it's time for you to become the reviewer.


## [Review & Approve a PR](https://profy.dev/project/github-minesweeper/review-and-approve)

To recap: The game is over because we hit a mine. But Tara opened a PR that allows us to restart the game. We only need to merge it.

Let's have a look at that PR (Restart Game). First, navigate to the Pull Request list.

You should see a single PR (if you closed the previous one). You might see a green check instead of the red cross in the screenshot below. That's fine.

Now open the PR.

Tara shared the new empty board in the comment so you can select your first field to be cleared.

As you can see at the bottom, all checks passed. But we can't merge the PR yet because it's missing an approving review.

Since Tara opened the PR we can't request a review from her. After all, she's not allowed to approve her own PR. This time the review is our responsibility.

Go ahead and open the **"Files changed"** tab.

Now you should see a list of all the code changes like this:

In a real project, you would thoroughly review the code. You would step through each file and add comments to the code where you think an improvement was required. Ideally, you'd check out the code on your local machine, run, and test it.

To add comments you hover a line in one of the files. You'll see a **"+"** sign as you can see in the screenshot. Go ahead and give it a try.

If you want to publish the comment directly you can click on the "Add single comment" button. The author of the PR is notified right away. This makes sense if you only have minor remarks.

If you use the **"Start a review"** button the comment is not published directly but marked as "pending". You can add more comments and publish them together once you finish the review process. This is very handy when you have to review multiple files. Here an example:

Imagine you go through a long list of code changes. You might not understand a part of the code immediately so you add a comment asking for clarification. You then continue reading the other code changes and suddenly you get the bigger context. Now you can go back and edit or delete the comment without the author of the PR being notified.

So go ahead and click the **"Start a review"** button. You should see your comment embedded in the code now as shown in the screenshot below.

Finally, click on the **"Finish your review"** button.

We don't need to request changes but can directly approve the PR. You can enter a nice message if you want to make Tara happy. Then select the **"Approve"** option and click the button.

You should then be redirected to the bottom of the PR page.

Merge the PR as usual and you're ready to start a new game.


## [Overview](https://profy.dev/project/github-minesweeper/quick-reference-overview)

This is the end of the guided part of this course. We covered in more or less detail

* The Trunk-Based Development Git workflow
* Working with a team on a remote repository
* Squash merging
* Continuous Integration and GitHub Actions
* The review process from the reviewer's perspective

Now it's time for you to practice Trunk-Based Development on your own. No more hand-holding.

**First, if you liked the course I would really appreciate it if you could share it with your friends or [mention it on Twitter](https://twitter.com/intent/tweet?url=https://profy.dev/project/github-minesweeper&text=This%20course%20by%20@j_kettmann%20helped%20me%20get%20comfortable%20with%20Git%20and%20GitHub).**

**Second, I recommend playing a few more rounds of GitHub Minesweeper** to build up some muscle memory. You can find a cheat sheet with all the relevant commands on the next page.

**Third, you can start using Continuous Integration and GitHub Actions as well as Trunk-Based Development in your own projects.** This will prepare you for the real dev world. It may even impress a hiring manager and help you get a job.

You can get two guides to setting up GitHub Actions and branch protection in your own projects similar to the repo in this course. Just fill out the form below and I'll send them to you via email.


## Cheat sheet

Now it's time for you to practice Trunk-Based Development on your own. By playing a few more rounds of GitHub Minesweeper you have the chance to build up muscle memory. It might feel cumbersome at first. But believe me, it'll get better soon and it'll come in handy once you start working on a team of developers.

Since you might not remember all the commands here is a quick overview.

## GitHub Minesweeper rules

**Goal of the game:** flag all mines

Available commands to add to **commands.json**:

* **clear [field]**: e.g. "clear A9", clears the selected field
* **flag [field]**: e.g. "flag A9", flags the selected field. Should be used when you think this field is a mine.
* **unflag [field]**: e.g. "unflag A9", removes a flag from the selected field. Should be used if you mistakenly flagged a field.
* **end**: once you flagged all mines you can end the game with this command. Tara will reveal the board and create a new PR to restart the game.

## Trunk-Based Development

1. Sync the local **main** branch.
2. Check out a new branch from **main**.
3. Add new commands to **commands.json**.
4. Commit and push the changes.
5. Open a Pull Request.
6. Wait for the CI checks to pass.
7. Request a review by Tara.
8. Merge the PR if it was approved. If you hit a mine, restart the game by approving and merging the PR created by Tara.

## Git Cheat Sheet

Here is a list of Git commands in the order you need them for Trunk-Based Development:

1. Check out the main branch: **git checkout main**
2. Sync the local and remote main branches: **git pull origin main**
3. Create and check out a new branch: **git checkout -b YOUR_BRANCH_NAME**
4. Commit all file changes: **git commit -a -m "YOUR_COMMIT_MESSAGE"**
5. Push the changes to the remote repo on GitHub: **git push origin YOUR_BRANCH_NAME**

