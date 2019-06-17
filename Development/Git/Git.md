- [Git - Documentation](https://git-scm.com/doc)
- [Version Control Best Practices](https://www.git-tower.com/blog/version-control-best-practices/)
- [Introducing Git Submodule in Tower](https://www.git-tower.com/blog/introducing-git-submodules-in-tower/)
- [version control - Git for beginners: The definitive practical guide - Stack Overflow](https://stackoverflow.com/questions/315911/git-for-beginners-the-definitive-practical-guide)
- [Gérez vo code source avec Git - OpenClassrooms](https://openclassrooms.com/courses/gerez-vos-codes-source-avec-git)
- List of commands in plain english: [Oh, shit, git!](http://ohshitgit.com/)

## User infos

	git config --global user.name John Doe
	git config --global user.email john@doe.name

## Merge and rebase

- [Bien utiliser Git merge et rebase • Git Attitude : formations Git qualitatives et sympathiques](http://www.git-attitude.fr/2014/05/04/bien-utiliser-git-merge-et-rebase/)
- [git merge v git rebase: Avoiding Rebase Hell - Jarrod Spillers](http://www.jarrodspillers.com/git/2009/08/19/git-merge-vs-git-rebase-avoiding-rebase-hell.html)
- [Why you should stop using Git rebase – Fredrik V. Mørken – Medium](https://medium.com/@fredrikmorken/why-you-should-stop-using-git-rebase-5552bee4fed1)

## Hooks

- [Meta Magic: Git Hooks](http://benjamin-meyer.blogspot.fr/2008/10/git-hooks.html)
- [githook - change default git hook - Stack Overflow](https://stackoverflow.com/questions/1977610/change-default-git-hooks)
- [Putting git hooks into repository - Stack Overflow](https://stackoverflow.com/questions/3462955/putting-git-hooks-into-repository/3464399#3464399)
- [Missing git hooks documentation | Mark's Blog](http://longair.net/blog/2011/04/09/missing-git-hooks-documentation/)

## Branching

Merge branch, not rebase

- [Merge and rebase](#merge-and-rebase)
- [What are some examples of commonly used practices for naming git branches? - Stack Overflow](https://stackoverflow.com/questions/273695/what-are-some-examples-of-commonly-used-practices-for-naming-git-branches#answer-6065944)

## Stash

Save a stash:

	git stash save

Remove tracked file inside an ignored folder:

	git rm --cached that_dir

Remove the lastest stash:

	git stash drop

## Gerrit

Push to `refs/for/<name>`

code review tool

1. Add `commit-msg` into `.git/hooks/`
2. Change to executable `chmod +x commit-msg`
3. Config local repository to pushref: `refs/heads/*:refs/for/*`
	Change inside: `[remote "origin"]` the line with `push = ` as:

		push = refs/heads/*:refs/for/*

Now all push with `git push` or in gittower push to `origin/<default>` (or use "Gerrit Push" in Git Tower 2)

- [Why i git push gerrit HEAD:refs/for/master used instead of git push origin master - Stack Overflow](https://stackoverflow.com/questions/10461214/why-is-git-push-gerrit-headrefs-for-master-used-instead-of-git-push-origin-mast)
- [Tower on Twitter: "@ritey Nothing Tower-specific. You should make sure to set a proper Push Refspec to make your life easier (a you'd do on the CLI, too)."](https://twitter.com/gittower/status/197977339534114816)
- [git - Push to gerrit using SourceTree - Stack Overflow](https://stackoverflow.com/questions/9917645/push-to-gerrit-using-sourcetree)
- [gerrit - git alia for HEAD:refs/for/master - Stack Overflow](https://stackoverflow.com/questions/7423893/git-alias-for-headrefs-for-master)
- [How to configure specific upstream push refspec for Git when used with Gerrit? - Stack Overflow](https://stackoverflow.com/questions/7101145/how-to-configure-specific-upstream-push-refspec-for-git-when-used-with-gerrit/7141743#7141743)

## Git diff for binary files

	git config --global core.attributesfile '~/.gitattributes'

Exemple to diff PNG files with EXIFtool

	echo '*.png diff=exif' >> .gitattributes
	git config diff.exif.textconv exiftool

	diff --git a/image.png b/image.png

- http://git-scm.com/book/ch7-2.html
- [Git - How to Get Better Diff for Image - Lar Tesmer' Blog](http://www.lars-tesmer.com/blog/2010/09/20/git---how-to-get-better-diffs-for-images/)

----

	echo "*.gif diff=image" >> ~/.gitattributes
	echo "*.jpg diff=image" >> ~/.gitattributes
	echo "*.png diff=image" >> ~/.gitattributes
	git config --global diff.image.command '~/bin/git-imgdiff'

`~/bin/git-imgdiff`:

	#!/bin/sh
	compare $2 $1 png:- | montage -geometry +4+4 $2 - $1 png:- | display -title "$1" -

----

	identify -verbose info: <image>

## Sparse checkout

Aka partial checkout

[Is there any way to clone a git repository's sub-directory only? - Stack Overflow](https://stackoverflow.com/questions/600079/is-there-any-way-to-clone-a-git-repositorys-sub-directory-only/13738951#13738951)

## Commit

- [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0-beta.4/)

### Don't commit generated files

- [Why I don’t commit generated files to master — Medium](https://medium.com/@kentcdodds/why-i-don-t-commit-generated-files-to-master-a4d76382564)

### Commit for other author

	--author=<author>

	From:

	git commit --amend --author="Author Name <email@address.com>"

- [git - Change commit author at one specific commit - Stack Overflow](https://stackoverflow.com/questions/3042437/change-commit-author-at-one-specific-commit)

### Update commit messages

Do it only for non pushed commits

- [How to Batch Update Git Commit Messages](https://davidwalsh.name/update-git-commit-messages)

## Removing a file from every commit

For pushed commit, **this change the history**

	git filter-branch --tree-filter 'rm -f passwords.txt' HEAD

- [Git - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History#_removing_file_every_commit)

## How git works

- [git - Rebase local repo with remote whose history ha changed - Stack Overflow](https://stackoverflow.com/questions/42267566/rebase-local-repo-with-remote-whose-history-has-changed/42281702#42281702)
- [Git from the inside out](https://maryrosecook.com/blog/post/git-from-the-inside-out)
- [Git de l'intérieur](https://alm.developpez.com/tutoriel/fonctionnement-interne-de-git/)
- [The Architecture of Open Source Applications (Volume 2): Git](http://aosabook.org/en/git.html)
- [blob - How to DEFLATE with a command line tool to extract a git object? - Stack Overflow](https://stackoverflow.com/questions/3178566/how-to-deflate-with-a-command-line-tool-to-extract-a-git-object)

### Hash of a file

Content of `blob FILE_SIZE\0FILE_CONTENT`

- [Git - finding the SHA1 of an individual file in the index - Stack Overflow](https://stackoverflow.com/questions/460297/git-finding-the-sha1-of-an-individual-file-in-the-index/24283352#24283352)
- [How is the git hash calculated? - Stack Overflow](https://stackoverflow.com/questions/35430584/how-is-the-git-hash-calculated)

## Ignore file in folder

`*`, `[`, `]`, space, `\` need to be escaped with `\`

Ignore `sites/*/files` but not `sites/default/files/favicon.ico`.

	*
	!.gitattributes
	!.gitignore
	!readme.md
	!.gitkeep
	!*.php
	!*/

You need to make exception for each subfolders:

	sites/*/files
	#
	!sites/default/files
	sites/default/files/*
	!sites/default/files/favicon.ico


Note `*` will also exclude folder, to exclude only files use `*.*`:

	*.*
	!*.c

- [Git - gitignore Documentation](https://git-scm.com/docs/gitignore)
- [git - gitignore - only allow certain extensions and files - Stack Overflow](https://stackoverflow.com/questions/11852558/gitignore-only-allow-certain-extensions-and-files/11853075#11853075)
- [gitignore - Is there a way to tell git to only include certain files instead of ignoring certain files? - Stack Overflow](https://stackoverflow.com/questions/1279533/is-there-a-way-to-tell-git-to-only-include-certain-files-instead-of-ignoring-cer/43438694#43438694)

## Commit empty folder

Add an empty file `.gitkeep`:

	touch .gitkeep

Or use a `.gitignore`:

	# Ignore everything in this directory
	*
	# Except this file
	!.gitignore

- [What is .gitkeep? Differences between .gitignore and .gitkeep - Apply Head](https://applyhead.com/gitkeep-vs-gitignore/)
- [How can I add an empty directory to a Git repository? - Stack Overflow](https://stackoverflow.com/questions/115983/how-can-i-add-an-empty-directory-to-a-git-repository)

## Include version

- [To put the prefix ?<revision-number> to codes by Git/Svn - Stack Overflow](https://stackoverflow.com/questions/1127177/to-put-the-prefix-revision-number-to-codes-by-git-svn/1127241#1127241)
- [How do I enable ident string for Git repos? - Stack Overflow](https://stackoverflow.com/questions/1792838/how-do-i-enable-ident-string-for-git-repos)

## Case sensitivity

	git mv hello.txt Hello.txt

- [rename - Changing capitalization of filename in Git - Stack Overflow](https://stackoverflow.com/questions/10523849/changing-capitalization-of-filenames-in-git)

## Character encoding

Unicode

	git config --global core.precomposeunicode true
	git config --global core.quotepath false

- [macos - Git and the Umlaut problem on Mac OS X - Stack Overflow](https://stackoverflow.com/questions/5581857/git-and-the-umlaut-problem-on-mac-os-x)
- [macos - How to handle Asian character in file name in Git on OS X - Stack Overflow](https://stackoverflow.com/questions/4144417/how-to-handle-asian-characters-in-file-names-in-git-on-os-x)
- [Tower Help - Files with unicode names are displayed as untracked.](https://www.git-tower.com/help/mac/faq-and-tips/faq/unicode-filenames)

## Search

```sh
git log --all --grep='<keywork in commit msg>'
```

## Undo

```sh
git reflog
```

Reset HEAD to log entry

```sh
git reset --hard "HEAD@{5}"
```

- [Undoing a git rebase - Stack Overflow](https://stackoverflow.com/questions/134882/undoing-a-git-rebase)
- [Git - git-reflog Documentation](https://git-scm.com/docs/git-reflog)

## Find a bug

```sh
git bisect run <yourtest.sh>
```

- [Git - git-bisect Documentation](https://git-scm.com/docs/git-bisect)

## Tools

- [samkelleher/conventional-github-releaser: Node utility to auto generate GitHub Release Notes from git commits using latest ECMAScript](https://github.com/samkelleher/conventional-github-releaser)
