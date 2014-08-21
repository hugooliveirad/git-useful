# git-useful
> a collection of incredibly useful git commands

## Table of Contents
- [Add](#add)
    - [add files interactively](#add-files-interactively)
- [Log](#log)
    - [shows commit frequency for each user in the repo](#shows-commit-frequency-for-each-user-in-the-repo)
    - [pretty log (one line with graphic and colors)](#pretty-log-one-line-with-graphic-and-colors)
    - [logs commits that added or removed a certain keyword](#logs-commits-that-added-or-removed-a-certain-keyword)
- [Diff](#diff)
    - [diff word-by-word](#diff-word-by-word)
    - [short infos about changes in a commit](#short-infos-about-changes-in-a-commit)
    - [show changed files in a commit](#show-changed-files-in-a-commit)
    - [list every changed file between two commits](#list-every-changed-file-between-two-commits)
    - [show modifications in a file in a commit](#show-modifications-in-a-file-in-a-commit)
    - [show files with conflicts](#show-files-with-conflicts)
- [Misc](#misc)
    - [sync fork](#sync-fork)
    - [assume file as unchanged](#assume-file-as-unchanged)
    - [undo assume file as unchanged](#undo-assume-file-as-unchanged)
    - [list files assumed as unchanged](#list-files-assumed-as-unchanged)
- [Others](#others)

## Add

#### add files interactively
```bash
git add <file> --patch

# working example
git add . --patch
```
Very useful when you need to commit different lines of a file. See more at the docs for [Interactive Mode](http://git-scm.com/docs/git-add#_interactive_mode).

## Log

#### shows commit frequency for each user in the repo
```bash
git log --format='%an' . | \
    sort | uniq -c | sort -rn | head
```
source: http://mislav.uniqpath.com/2014/02/hidden-documentation/

#### pretty log (one line with graphic and colors)
```bash
git log \
  --graph \
  --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'
```

#### logs commits that added or removed a certain keyword
```bash
git log -S '<keyword>'
```
source: http://mislav.uniqpath.com/2014/02/hidden-documentation/

## Diff

#### diff word-by-word
```bash
git diff --word-diff
```

source: http://idnotfound.wordpress.com/2009/05/09/word-by-word-diffs-in-git/

#### short infos about changes in a commit
```bash
git diff-tree --no-commit-id --shortstat -r <commit-hash>

# working example
git diff-tree --no-commit-id --shortstat -r HEAD
```

#### show changed files in a commit
```bash
git diff-tree --no-commit-id --name-only -r <commit-hash>

# working example
git diff-tree --no-commit-id --name-only -r HEAD
```

If you want a more detailed version, run with the `--stat`, or `--numstat` or `--dirstat` flags instead of `--name-only`.

source: http://stackoverflow.com/questions/424071/list-all-the-files-for-a-commit-in-git

#### list every changed file between two commits
```bash
git diff --name-only <commit-hash> <commit-hash>

# working example
git diff --name-only HEAD~3 HEAD
```

source: http://stackoverflow.com/questions/1552340/git-show-all-changed-files-between-two-commits

#### show modifications in a file in a commit
```bash
git diff <commit-hash>~1..<commit-hash> [<file>]

# working example
git diff HEAD~1..HEAD
```

You can optionally add a file name to show only changes in a specific file.

#### show files with conflicts
```bash
git diff --name-only --diff-filter=U
```

source: http://stackoverflow.com/questions/3065650/whats-the-simplest-way-to-git-a-list-of-conflicted-files

## Misc

#### sync fork
```bash
# Requires an "upstream" remote, pointing to original repo
# e.g. `git remote add upstream git@github.com:user/repo.git`
git fetch upstream; git checkout master; git rebase upstream/master
```
source: https://help.github.com/articles/syncing-a-fork

#### assume file as unchanged
```bash
git update-index --assume-unchanged <file>

# working example
git update-index --assume-unchanged .
```

#### undo assume file as unchanged
```bash
git update-index --no-assume-unchanged <file>

# working example
git update-index --no-assume-unchanged .
```

source: http://stackoverflow.com/questions/17195861/undo-a-git-update-index-assume-unchanged-file

#### list files assumed as unchanged
```bash
git ls-files -v|grep '^h'
```

source: http://stackoverflow.com/questions/17195861/undo-a-git-update-index-assume-unchanged-file

## Others
More than one line command useful things

- [Git cheat sheet](https://github.com/tiimgreen/github-cheat-sheet)
- [Git ahead and behind info](https://gist.github.com/hugobessaa/8788821)
- [git-overwritten](https://github.com/mislav/dotfiles/blob/7ac8cbfcd56cfa6c39b5719ea183e87878ea6ed5/bin/git-overwritten)
