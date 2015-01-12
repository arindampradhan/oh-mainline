================
Working with git
================

+-------------------------------+--------------------------------------------------------------------------------------+
| Git Commands                  |                What it does                                                          |
+===============================+======================================================================================+
| git **clone**  <repo>         | Used to clone the repo ``git clone <repo> | <name>``                                 |
+-------------------------------+--------------------------------------------------------------------------------------+
| git **commit**                |  **Commit** an applied change on the given branch                                    |
+-------------------------------+--------------------------------------------------------------------------------------+
| git **remote**                | `track <https://help.github.com/articles/configuring-a-remote-for-a-fork/>`_         |
|                               | remote branch                                                                        |
+-------------------------------+--------------------------------------------------------------------------------------+
| ``git revert <commit-SHA-1>`` |`Revert <http://git-scm.com/docs/git-revert>`_ changes in a commit                    |
+-------------------------------+--------------------------------------------------------------------------------------+
|``git fetch <remote> <branch>``| The git `fetch <https://www.atlassian.com/git/tutorials/syncing/git-fetch/>`_ command|
|                               | imports commits or `tags <http://git-scm.com/book/en/v2/Git-Basics-Tagging>`_        |
|                               | from a remote repository into your local repo.                                       |
+-------------------------------+--------------------------------------------------------------------------------------+
| **git pull**                  | **Updates** your repo. Shorthand for ``git fetch`` followed by                       |
|                               | ``git merge FETCH_HEAD``. Recommended                                                |
|                               | to use it with `- -rebase <http://bit.ly/1yAi5bf>`_.                                 |
+-------------------------------+--------------------------------------------------------------------------------------+
| **git log**                   | Lists commits made in the current **branch** of the                                  |
|                               | repo. **Hacks**: ``git log --pretty=oneline``.                                       |
|                               | Also check `this <https://coderwall.com/p/euwpig/a-better-git-log>`_.                |
+-------------------------------+--------------------------------------------------------------------------------------+
| **git rebase** :              |  - Rebasing is the process of moving a **branch**                                    |
|  - ``git rebase <base>``      |    to a new **base commit**                                                          |
|  - ``git rebase -i <base>``   |  - Interactive `rebase <https://help.github.com/articles/using-git-rebase/>`_        |
|  - ``git rebase -i HEAD~NUM`` |  - Modifying to a `head <https://help.github.com/articles/about-git-rebase/>`_       |
|  - ``git rebase -i bbc643cd^``|  - Modify to specified commit bbc643cd                                               |
|  - ``git rebase --abort``     |  - Abort a rebase                                                                    |
|  - ``git reflog``             |  - Tracks the changesets to the tip of branch                                        |
+-------------------------------+--------------------------------------------------------------------------------------+

Issues with Pull Requests
=========================

Problems new contributors face
-------------------------------

1. Get into `OpenHatch workflow <https://openhatch.org/wiki/OpenHatch_git_workflow>`_ .

#. | **Understand** your `problem <https://sethrobertson.github.io/GitFixUm/fixup.html>`_ 
     first.

#. Learn to **go to a certain commit**.

   * | **Soln:** Each commits has a hash value(SHA-1) which is fixed. 
       `Switch <http://stackoverflow.com/questions/4940054/how-can-i-switch-my-git-repository-to-a-particular-commit>`_ 
       to a commit.

#. | If you need to **modify a single commit** as per requested by the 
     maintainer in the pull request 
     **revert the old commit with a new commit and push it** 
     mentioning the changes you have made:

   * | **Soln:** Please **understand** `reset and revert <http://stackoverflow.com/questions/2530060/can-you-explain-what-git-reset-does-in-plain-english>`_ . 
       The ideal solution is to `revert previous commit <http://stackoverflow.com/questions/4114095/revert-to-a-previous-git-commit>`_ , 
       edit it and ``push it`` for changes that are **not published** or 
       ``force push`` it for changes that **are published**. 
       you can also `undo <http://stackoverflow.com/questions/927358/undo-the-last-git-commit>`_ 
       a commit and ``force push`` the changes made.

   * | **Note:** Commits **do not** technically **change** when we force push 
       the commit, reset or modify them. But the **hash gets updated**, and the 
       new hashed commit gets tagged to that branch. You can easily find you 
       previous **commit on github** too just by adding ``/commit/<branch>`` 
       to the repo address. It will show you the **remote git log**. See the 
       hash get changed after rewriting the commit.

#. | Sometimes you have **two or more commit on your pull request**, which is 
     usually not desired by maintainers. The solution is to do an 
     **interactive rebase** and squash the previous **N** commits on the 
     particular branch to which the pull request represents:

   * | **Soln:** Please **understand** `interactive rebase <https://help.github.com/articles/about-git-rebase/>`_. 
       Checkout the branch the pull request represents, count the **number[N]** 
       of commits you need to `squash <http://stackoverflow.com/questions/2563632/how-can-i-merge-two-commits-into-one>`_ 
       from the pull requests or ``git log`` on that branch, then 
       ``git rebase -i HEAD~N``. N (**number of commits before**) is usually 2 
       if you want to **squash 2 commits**. Change the pick to squash. 
       Save the configuration. Then force push the new commit 
       ``git push -f origin <branch>``.

#. | If you have **unwanted commits** attached to the pull request or 
     **history is broken** then you need to do an **interactive rebase** :

   * | **Soln:** It is better to tell others that you are having such problem 
       as it needs `rewriting history <http://git-scm.com/book/en/v2/Git-Tools-Rewriting-History>`_. 
       Please **understand** `rebasing <https://github.com/edx/edx-platform/wiki/How-to-Rebase-a-Pull-Request>`_ 
       and please see your `logs <http://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History>`_. 
       The **solution** is an `interactive rebase <https://help.github.com/articles/about-git-rebase/>`_ 
       **Command**: ``git rebase -i HEAD~N`` (N gives the number of the 
       revisions up in that branch). Try to pick N carefully count the commits 
       as maintainers will ask you to give the finalized result in a single 
       commit.

   * | The **interactive rebase** on that branch will show the commands that 
       runs on that branch and finally shows on the pull request. Delete the 
       commits you don't need and keep the ones you need. Squash the needed 
       commits to a single commit.

   * | **Note:** Branches are technically a **tagging system** to commits that 
       have a **hash value**, they are **relative**, even the master branch. 
       It can operate with commands like squash, pick and many others. The 
       commands are played from **top to bottom** on each commit and finally 
       shown in the pull request. See the `options <https://help.github.com/articles/about-git-rebase/>`_.

Resolving merge conflicts
-------------------------
| Conflicts are essentially two or more commits from different branches which 
  **overlap** because they have **different content** on the same revision. 
  Understanding `Merge conflict <https://www.youtube.com/watch?v=zz7NuSCH6II>`_, 
  you can manually resolve it with git.

| Tools like `kdiff3 <https://www.kde.org/applications/development/kdiff3/>`_ 
  helps you pick that **content of the commit** which you want to get merged in 
  the final commit. A `tutorial <https://www.youtube.com/watch?v=-CkqiIPAzgQ>`_ 
  on using **kdiff3**. Kdiff3 can be configured for all types of version 
  control ranging from **git,svn or mercurial**.

Installation
~~~~~~~~~~~~

**Ubuntu:**

	``$ sudo apt-get install kdiff3``

**Mac:**
	
	``$ brew install kdiff3``


**Configure kdiff3:**

Recent Git versions have built-in support for kdiff3.
	
	``$ git config --global merge.tool kdiff3``

This makes ``git mergetool`` launch kdiff3.


**Note:** The problem can also be resolved with an interactive rebase.

Become a git Expert
===================

| If you like git a lot and use it often, use tools like **git-extras** and 
  **aliases** to increase your **productivity**.

Alias
-----
| **Save you Keystrokes**. These scripts are added to your ``.bashrc`` , 
  ``.zshrc`` or ``any file you want to source``.Open ``.bashrc`` on your 
  favorite text editor. Follow the instructions.

**Examples** ::

	alias gc="git commit -m "$1"

	alias shortform="the longer version of the command"

Handy aliases for your bashrc ::

	$ gedit .bashrc

	alias gs="git status"
	alias ga="git add"
	alias gb="git branch"
	alias gc="git commit -m "$1""
	alias gp="git push $1 $2" # gp OR gp [remote] [branch]
	alias pull="git pull"
	alias co="git checkout"
  alias gt="git tag "$1""
  alias gtp="git push --tags"
	alias gl="git log --pretty=oneline"
	alias gcl="git clone"
	alias djports="fuser -k 8000/tcp"

`git-extras <https://github.com/tj/git-extras>`_
-------------------------------------------------
| Get **40 extra commands** that you find very necessary but are missing in 
  git, **i.e git-undo, git-summary, git-changelog, git-effort.**

`Installation <https://github.com/tj/git-extras/wiki/Installation>`_
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Ubuntu:**

	``$ sudo apt-get install git-extras``

**Mac:**

	``$ brew install git-extras``

`Usage <http://vimeo.com/45506445>`_
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* | ``git-summary`` # gives the status of the 
    **hours and duration you are actually working on a git project**.

* ``git-effort`` # shows the **file stats** you have mostly worked on a project.

* ``git-undo`` # undo a git commit.

* ``git-extras`` # shows the list of commands.