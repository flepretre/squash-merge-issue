# Squash merge issue example

This repository is there to expose a dangerouse behavior on the `squash and merge` action.

Let's say you started a branch **B** based on the work of someone else branch **A**.

In your branch **B** you remove some code that was introduced in branch **A**.

Now banch **A** is *squash merged* in **master** before the branch **B**, without modifications.

You have no conflict with **master**, the diff in github shows only the work of the branch **B**, but it shows 2 commits.

Now if you *squash merge* the branch **B**, here is what happen:
- all commits from the branch **A** (that are still in branch **B**) and all commit of the branch **B** are squashed together
- due to the fact they were related to **master** before the merge of the branch **A**, the fusion off the code from **A** and its removal from **B** will result in a empty diff
- the empty diff is now part of the squashed commit
- the rebase apply the diff of the squash commit on **master**, so it apply the empty diff
So once your branch is *squash merged* on **master**, the code you remove from **A** will remain on **master**.

:warning: This is not a bug from github, this is a bad usage of git, you can do this mistake with or without github.

## commits

You can see in the repository an example of the issue.

The `foo.txt` file contains the 4 lines, the removal from the line 2 has been lost during the `squash and merge` action.
