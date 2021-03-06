posh-git-bash
========

This my first venture into bash scripting, so I decided to make a port of
posh-git, which, in my humble opinion, is fantastic (and can be found at found
at https://github.com/dahlbyk/posh-git).

I based my work off of
https://github.com/git/git/blob/master/contrib/completion/git-prompt.sh

This is distributed under the GNU GPL v2.0. I hope that you may find some use of
it. Please do not hesitate to contact me about any issues or requests.


INSTALLATION INSTRUCTIONS
========================
1. Copy this file to somewhere (e.g. `~/git-prompt.sh`).
2. Add the following line to your `.bashrc`:

        source ~/git-prompt.sh

3.  a. If you are using bash, `__git_ps1` can be used for
    `PROMPT_COMMAND` with two parameters, `<pre>` and `<post>`, which are
    strings you would put in `$PS1` before and after the status string generated
    by the git-prompt machinery. For example, the following

        PROMPT_COMMAND='__git_ps1 "\u@\h:\w" "\\\$ "'

    will show username, at-sign, host, colon, cwd, then various status strings,
    followed by dollar and space, as your prompt. Optionally, you can supply a
    third argument with a printf format string to fine-tune the output of the
    branch status.


The Prompt
----------
By default, the status summary has the following format:

    [{HEAD-name} +A ~B -C !D | +E ~F -G !H]

* `{HEAD-name}` is the current branch, or the SHA of a detached HEAD
 * Cyan means the branch matches its remote
 * Green means the branch is ahead of its remote (green light to push)
 * Red means the branch is behind its remote
 * Yellow means the branch is both ahead of and behind its remote
* ABCD represent the index; EFGH represent the working directory
 * `+` = Added files
 * `~` = Modified files
 * `-` = Removed files
 * `!` = Conflicted files
 * As in `git status`, index status is dark green and working directory status
 is dark red

For example, a status of `[master +0 ~2 -1 | +1 ~1 -0]` corresponds to the
following `git status`:

    # On branch master
    #
    # Changes to be committed:
    #   (use "git reset HEAD <file>..." to unstage)
    #
    #        modified:   this-changed.txt
    #        modified:   this-too.txt
    #        deleted:    gone.ps1
    #
    # Changed but not updated:
    #   (use "git add <file>..." to update what will be committed)
    #   (use "git checkout -- <file>..." to discard changes in working directory)
    #
    #        modified:   not-staged.ps1
    #
    # Untracked files:
    #   (use "git add <file>..." to include in what will be committed)
    #
    #        new.file



CONFIG OPTIONS
==============

This should work out of the box, but there are some options available, mostly
setting things in the local git config for
per-repository options.
```
bash.enableFileStatus
bash.enableGitStatus
bash.showStatusWhenZero
bash.showUpstream
```

bash.enableFileStatus
---------------------

    * true      Default. The script will query for all file indicators every
                time.

    * false     No file indicators will be displayed. The script will not query
                upstream for differences. Branch color- coding information is
                still displayed.

bash.enableGitStatus
--------------------

    * true      Default. Color coding and indicators will be shown.

    * false     The script will not run.

bash.showStashState
-------------------

    * true      Default. An indicator will display if the stash is not empty.

    * false     An indicator will not display the stash status.

bash.showStatusWhenZero
-----------------------

    * false     Default. No file change indicators will be shown if there are no
                changes to the index or working tree.

    * true      Indicators will be shown even if there are no updates to the
                index or working tree.

bash.showUpstream
-----------------
By default, `__git_ps1` will compare `HEAD` to your `SVN` upstream if it can
find one, or `@{upstream}` otherwise.

    * legacy    don't use the '--count' option available in recent versions of
                `git-rev-list`
                
    * git       always compare `HEAD` to `@{upstream}`
    
    * svn       always compare `HEAD` to your `SVN` upstream
