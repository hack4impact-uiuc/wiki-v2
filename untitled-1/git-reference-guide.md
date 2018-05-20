# Git Reference Guide

### Add and commit files

* Try to add files every now and then. If anything bad happens \(e.g. accidentally deleted file\), you will have a local saved copy in your local Git.
* Avoid adding files \(`git add`\) that: are not important / not useful to push to master, are dynamically generated, contain private information \(e.g. a secret key\), or don’t belong in the repo.
* Commit after you reach a good checkpoint, e.g. any subfeature of your feature. Try to commit often \(but meaningfully\) — this will help you take advantage of version control and use it effectively. Avoid committing broken code, but having stubs is okay as long as you fill them out in later commits before merging your PR.

```text
# Check before adding and committing
$ git branch  # make sure you’re on the right branch
$ git status  # view which files were changed
$ git diff  # view the changes

# Add and commit your code
$ git add <changed files you want to add> 
$ git commit <files you want to commit> -m “Commit message here”
```

In the last command, `git commit -m`, the `-m` flag allows for an in-line message that directly follows. This is really convenient and much faster!

If you don’t want to use the `-m` flag in that last command for whatever reason, you can alternatively do: `$ git commit <files you want to commit>` This will open vim, a text editor.

* Press `i` to enter “Insert mode” — this will allow you to type text like you would expect.
* Type in your commit message
* Hit `esc` key on your keyboard
* Type `:w` to write \(save\), then `:q` to quit. Alternatively,`:wq` and `:x` are both commands to write and quit at once.

#### Other vim basics:

* When not in “Insert mode”, you can navigate by using `j` and `k` to scroll up and down, and `h` and `l` for left and right.
* When in doubt, hit `esc`!

Yay, you’ve committed your code! Let’s check we added and committed everything we meant to, with `$ git status`.

### Merging `master` branch into your current branch and resolving merge conflicts

* Always do this before you start developing your feature. Try to do this before pushing up your branch. _Must do this before opening a PR._
* Do this occasionally throughout working on your feature if it’s been a while since you’ve pulled. Other people may have pushed changes that involve the same files you have worked on. I advise you to do this often and keep your local branches up-to-date — can save you from running into merge conflicts later from building off of outdated code. I usually do this at the start of every work session.

```text
# Merge master branch into your current branch
$ git branch  # view current branches
$ git checkout master
$ git pull
$ git checkout <branch-you-were-working on>
$ git merge master

# Resolve merge conflicts
< Resolve merge conflicts in your text editor >

$ git add <edited files>
$ git commit  # this will open vim
```

In vim, just type `:x` to save the commit and exit vim. Would advise checking the `$ git status`after merging.

### Pushing to your remote branch \(AKA the one on Github\)

* You can push up your branch to Github whenever! Pushing to your branch is not the same thing as opening a PR. You should push to your remote \(Github\) branch whenever you feel you want a copy saved on Github. Unless you plan on changing your commit history while you develop \(e.g. if you use `git rebase` often\), I advise you to push after every few commits to save a remote copy.

```text
$ git push
```

### Opening a Pull Request \(PR\) on Github

* Go to Github, find your branch, click on “New pull request”.
* Make sure you have resolved all merge commits. You should see green and the message, "This branch has no conflicts with the base branch."
* You can continue to push to your branch while your pull request is open, just make sure your branch is up-to-date and all merge conflicts are resolved before you push. For this reason, I generally would not open a PR until your code is ready for review. \(But feel free to push to your remote branch as often as you want!\)
* When you are ready to have your PR reviewed, assign someone by clicking on the grey gear icon next to “Assignees” to review your code.
* When they finish their code review, address all of their comments by responding and discussing on Github, or by fixing or cleaning up your code and pushing again.
* When your code is ready to be merged, your PM or TL will merge the pull request and delete your branch. It’s up to you whether or not you want to keep your old branch. I’d suggest keeping it to be safe, but if you’re sure you won’t need it anymore, feel free to delete it! `$ git branch -D <name-of-branch-you-are-tryna-delete>`

### More Git

* [Basic Git commands](https://confluence.atlassian.com/bitbucketserver/basic-git-commands-776639767.html)
* Fun game for [visualizing how Git works](http://learngitbranching.js.org/)
  * If you are new to using Git, I recommend trying the “Introduction Sequence” under the ‘Main’ tab and "Push & Pull -- Git Remotes!” under the ‘Remote’ tab.
  * If you are not new to Git, want to brush up, or want to learn more advanced Git commands, I’d still recommend giving some of these a try!

