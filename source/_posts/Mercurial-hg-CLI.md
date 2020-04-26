---
title: Mercurial hg CLI
date: 2016-12-04 16:57:39
tags: [Version Control, hg, CLI]
categories: [Dev, Version Control]
---

## Synopsis
```
hg command [option]... [argument]...
```

## add
add the specified files on the next commit:
```
hg add [OPTION]… [FILE]…
```

## addremove
add all new files, delete all missing files:

```
hg addremove [OPTION]... [FILE]...
```
Add all new files and remove all missing files from the repository.

## annotate
show changeset information by line for each file:
```
hg annotate [-r REV] [-f] [-a] [-u] [-d] [-n] [-c] [-l] FILE...
```
List changes in files, showing the revision id responsible for each line.

## archive
create an unversioned archive of a repository revision:

```
hg archive [OPTION]... DEST
```
By default, the revision used is the parent of the working directory; use -r/–rev to specify a different revision.

## backout
reverse effect of earlier changeset:
```
hg backout [OPTION]... [-r] REV
```
Prepare a new changeset with the effect of REV undone in the current working directory. If no conflicts were encountered, it will be committed immediately.

## branches
list repository named branches:

```
hg branches [-c]
```
List the repository’s named branches, indicating which ones are inactive. If -c/–closed is specified, also list branches which have been marked closed

## cat
output the current or given revision of files:
```
hg cat [OPTION]... FILE...
```
Print the specified files as they were at the given revision. If no revision is given, the parent of the working directory is used.

## clone
make a copy of an existing repository:

```
hg clone [OPTION]... SOURCE [DEST]
```
Create a copy of an existing repository in a new directory.

## commit
commit the specified files or all outstanding changes:

```
hg commit [OPTION]... [FILE]...
```
Commit changes to the given files into the repository. Unlike a centralized SCM, this operation is a local operation.

## config
show combined config settings from all hgrc files:
```
hg config [-u] [NAME]...
```
With no arguments, print names and values of all config items.
With one argument of the form section.name, print just the value of that config item.
With multiple arguments, print names and values of all config items with matching section names.

## copy
mark files as copied for the next commit:

```
hg copy [OPTION]... [SOURCE]... DEST
```
Mark dest as having copies of source files. If dest is a directory, copies are put in that directory. If dest is a file, the source must be a single file.

## diff
diff repository (or selected files):

```
hg diff [OPTION]... ([-c REV] | [-r REV1 [-r REV2]]) [FILE]...
```
Show differences between revisions for the specified files.
Differences between files are shown using the unified diff format.

## export
dump the header and diffs for one or more changesets:

```
hg export [OPTION]... [-o OUTFILESPEC] [-r] [REV]...
```
Print the changeset header and diffs for one or more revisions. If no revision is given, the parent of the working directory is used.

![mercurialhg](https://philsblog.b-cdn.net/images/mercurialhg.png "mercurialhg")