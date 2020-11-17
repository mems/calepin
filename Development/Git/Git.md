- [Git - Documentation](https://git-scm.com/doc)
- [Version Control Best Practices](https://www.git-tower.com/blog/version-control-best-practices/)
- [Introducing Git Submodule in Tower](https://www.git-tower.com/blog/introducing-git-submodules-in-tower/)
- [version control - Git for beginners: The definitive practical guide - Stack Overflow](https://stackoverflow.com/questions/315911/git-for-beginners-the-definitive-practical-guide)
- [Gérez vo code source avec Git - OpenClassrooms](https://openclassrooms.com/courses/gerez-vos-codes-source-avec-git)
- List of commands in plain english: [Oh Shit, Git!?!](https://ohshitgit.com/)
- [Explain Git with D3](https://onlywei.github.io/explain-git-with-d3/) - Visualizing Git Concepts

## User infos

Aka author, identity (or identities), accounts

```sh
git config --global user.name John Doe
git config --global user.email john@doe.name
```

- [Eric Williams - Conditional Includes For Git Config](https://web.archive.org/web/20201105224149/https://www.motowilliams.com/conditional-includes-for-git-config)

## Merge and rebase

- [Bien utiliser Git merge et rebase • Git Attitude : formations Git qualitatives et sympathiques](http://www.git-attitude.fr/2014/05/04/bien-utiliser-git-merge-et-rebase/)
- [git merge v git rebase: Avoiding Rebase Hell - Jarrod Spillers](http://www.jarrodspillers.com/git/2009/08/19/git-merge-vs-git-rebase-avoiding-rebase-hell.html)
- [Why you should stop using Git rebase – Fredrik V. Mørken – Medium](https://medium.com/@fredrikmorken/why-you-should-stop-using-git-rebase-5552bee4fed1)

## Reset

```sh
# Reset tracked files and remove untracked files
git reset --hard origin/master && git clean -f -d
```

- [git reset --hard HEAD leaves untracked files behind - Stack Overflow](https://stackoverflow.com/questions/4327708/git-reset-hard-head-leaves-untracked-files-behind/4327720#4327720)

## Hooks

- [Meta Magic: Git Hooks](http://benjamin-meyer.blogspot.fr/2008/10/git-hooks.html)
- [githook - change default git hook - Stack Overflow](https://stackoverflow.com/questions/1977610/change-default-git-hooks)
- [Putting git hooks into repository - Stack Overflow](https://stackoverflow.com/questions/3462955/putting-git-hooks-into-repository/3464399#3464399)
- [Missing git hooks documentation | Mark's Blog](http://longair.net/blog/2011/04/09/missing-git-hooks-documentation/)

## Branching

Merge branch, not rebase

- [Merge and rebase](#merge-and-rebase)
- [Git branch naming conventions - DeepSource](https://deepsource.io/blog/git-branch-naming-conventions/)
- [Trunk Based Development](https://trunkbaseddevelopment.com/)
- [What are some examples of commonly used practices for naming git branches? - Stack Overflow](https://stackoverflow.com/questions/273695/what-are-some-examples-of-commonly-used-practices-for-naming-git-branches#answer-6065944)

## Gitflow

```sh
# Per project
#git config --add gitflow.multi-hotfix true
git flow config multi-hotfix true

# Or globally
#git config --global --add gitflow.multi-hotfix true
git flow config --global multi-hotfix true
```

## Stash

Save a stash:

```sh
git stash save
```

Remove tracked file inside an ignored folder:

```sh
git rm --cached that_dir
```

Remove the lastest stash:

```sh
git stash drop
```

## Gerrit

Push to `refs/for/<name>`

code review tool

1. Add `commit-msg` into `.git/hooks/`
2. Change to executable `chmod +x commit-msg`
3. Config local repository to pushref: `refs/heads/*:refs/for/*`
	Change inside: `[remote "origin"]` the line with `push = ` as:

	```
	push = refs/heads/*:refs/for/*
	```

Now all push with `git push` or in gittower push to `origin/<default>` (or use "Gerrit Push" in Git Tower 2)

- [Why i git push gerrit HEAD:refs/for/master used instead of git push origin master - Stack Overflow](https://stackoverflow.com/questions/10461214/why-is-git-push-gerrit-headrefs-for-master-used-instead-of-git-push-origin-mast)
- [Tower on Twitter: "@ritey Nothing Tower-specific. You should make sure to set a proper Push Refspec to make your life easier (a you'd do on the CLI, too)."](https://twitter.com/gittower/status/197977339534114816)
- [git - Push to gerrit using SourceTree - Stack Overflow](https://stackoverflow.com/questions/9917645/push-to-gerrit-using-sourcetree)
- [gerrit - git alia for HEAD:refs/for/master - Stack Overflow](https://stackoverflow.com/questions/7423893/git-alias-for-headrefs-for-master)
- [How to configure specific upstream push refspec for Git when used with Gerrit? - Stack Overflow](https://stackoverflow.com/questions/7101145/how-to-configure-specific-upstream-push-refspec-for-git-when-used-with-gerrit/7141743#7141743)

## Git diff for binary files

```sh
git config --global core.attributesfile '~/.gitattributes'
```

Exemple to diff PNG files with EXIFtool

```sh
echo '*.png diff=exif' >> .gitattributes
git config diff.exif.textconv exiftool
```

```sh
diff --git a/image.png b/image.png
```

- http://git-scm.com/book/ch7-2.html
- [Git - How to Get Better Diff for Image - Lar Tesmer' Blog](http://www.lars-tesmer.com/blog/2010/09/20/git---how-to-get-better-diffs-for-images/)

----

```sh
echo "*.gif diff=image" >> ~/.gitattributes
echo "*.jpg diff=image" >> ~/.gitattributes
echo "*.png diff=image" >> ~/.gitattributes
git config --global diff.image.command '~/bin/git-imgdiff'
```

`~/bin/git-imgdiff`:

```sh
#!/bin/sh
compare $2 $1 png:- | montage -geometry +4+4 $2 - $1 png:- | display -title "$1" -
```

----

```sh
identify -verbose info: <image>
```

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

```sh
git commit --amend --author="Author Name <email@address.com>"
```

- [git - Change commit author at one specific commit - Stack Overflow](https://stackoverflow.com/questions/3042437/change-commit-author-at-one-specific-commit)

### Update commit messages

Do it only for non pushed commits

- [How to Batch Update Git Commit Messages](https://davidwalsh.name/update-git-commit-messages)

## Removing a file from every commit

For pushed commit, **this change the history**

```sh
git filter-branch --tree-filter 'rm -f passwords.txt' HEAD
```

- [Git - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History#_removing_file_every_commit)

## Ignore file in folder

`*`, `[`, `]`, space, `\` need to be escaped with `\`

Ignore `sites/*/files` but not `sites/default/files/favicon.ico`.

```gitignore
*
!.gitattributes
!.gitignore
!readme.md
!.gitkeep
!*.php
!*/
```

You need to make exception for each subfolders:

```gitignore
sites/*/files
#
!sites/default/files
sites/default/files/*
!sites/default/files/favicon.ico
```

Note `*` will also exclude folder, to exclude only files use `*.*`:

```gitignore
*.*
!*.c
```

- [Git - gitignore Documentation](https://git-scm.com/docs/gitignore)
- [git - gitignore - only allow certain extensions and files - Stack Overflow](https://stackoverflow.com/questions/11852558/gitignore-only-allow-certain-extensions-and-files/11853075#11853075)
- [gitignore - Is there a way to tell git to only include certain files instead of ignoring certain files? - Stack Overflow](https://stackoverflow.com/questions/1279533/is-there-a-way-to-tell-git-to-only-include-certain-files-instead-of-ignoring-cer/43438694#43438694)

## Commit empty folder

Add an empty file `.gitkeep`:

```sh
touch .gitkeep
```

Or use a `.gitignore`:

```gitignore
# Ignore everything in this directory
*
# Except this file
!.gitignore
```

- [What is .gitkeep? Differences between .gitignore and .gitkeep - Apply Head](https://applyhead.com/gitkeep-vs-gitignore/)
- [How can I add an empty directory to a Git repository? - Stack Overflow](https://stackoverflow.com/questions/115983/how-can-i-add-an-empty-directory-to-a-git-repository)

## Include version

- [To put the prefix ?<revision-number> to codes by Git/Svn - Stack Overflow](https://stackoverflow.com/questions/1127177/to-put-the-prefix-revision-number-to-codes-by-git-svn/1127241#1127241)
- [How do I enable ident string for Git repos? - Stack Overflow](https://stackoverflow.com/questions/1792838/how-do-i-enable-ident-string-for-git-repos)

## Case sensitivity

```sh
git mv hello.txt Hello.txt
```

- [rename - Changing capitalization of filename in Git - Stack Overflow](https://stackoverflow.com/questions/10523849/changing-capitalization-of-filenames-in-git)

## Character encoding

Unicode

```sh
git config --global core.precomposeunicode true
git config --global core.quotepath false
```

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

## Export changed files

```sh
git archive -o patch.zip $COMMIT_HASH $(git diff-tree -r --no-commit-id --name-only --diff-filter=ACMRT $COMMIT_HASH)
git archive -o patch.zip $COMMIT_TO_HASH $(git diff-tree -r --no-commit-id --name-only --diff-filter=ACMRT $COMMIT_FROM_HASH^ $COMMIT_TO_HASH)
```

rollback

```sh
git archive -o patch.zip $COMMIT_HASH^ $(git diff-tree -r --no-commit-id --name-only --diff-filter=ACMRT $COMMIT_HASH)
git archive -o patch.zip $COMMIT_FROM_HASH^ $(git diff-tree -r --no-commit-id --name-only --diff-filter=ACMRT $COMMIT_TO_HASH $COMMIT_FROM_HASH^)
```

- [git diff - Export only modified and added file with folder structure in Git - Stack Overflow](https://stackoverflow.com/questions/4541300/export-only-modified-and-added-files-with-folder-structure-in-git)

## Git light local copy

```sh
git clone --depth 1 http://DOMAIN\USERNAME@host/path.git
```

Then when sync:

```sh
# Force to refresh origin remote URL of include the current user
#git remote set-url origin "http://DOMAIN\$($env:USERNAME)@host/path.git"
# Fetch with no history
# use fetch insteaf of pull because pull do fetch and merge (that don't work because it try to merge unrelated histories)
git fetch --depth=1
# Reset the local repo (shouldn't have any changes for tracked files)
git reset --hard origin/master
```

- [How to keep the prod cloned repo naked/bare when updating it from the dev repo? : git](https://www.reddit.com/r/git/comments/9rlyhk/how_to_keep_the_prod_cloned_repo_nakedbare_when/)

## Git on Windows

See also [Bash shell on Windows](../../Operating%20Systems/Windows/Windows.md#bash-shell-on-windows)

### Credentials helper

Use the native Windows credentials manager (saved as generic credentials like "git:https://mygitrepo"):

```sh
git config --global credential.helper manager
```

- `explorer shell:::{1206F5F1-0569-412C-8FEC-3204630DFB70}` - access to Credential Manager, then go to "Windows Credentials"
- [Accessing Credential Manager](https://support.microsoft.com/en-us/help/4026814/windows-accessing-credential-manager) - In control panel
- [windows - Remove credentials from Git - Stack Overflow](https://stackoverflow.com/questions/15381198/remove-credentials-from-git/15382950#15382950)

About Explorer CLSIDs:

- [CLSID Key (GUID) Shortcuts List for Windows 10 | Tutorials](https://www.tenforums.com/tutorials/3123-clsid-key-guid-shortcuts-list-windows-10-a.html)
- [Control Panel (Windows) - Wikipedia](https://en.wikipedia.org/wiki/Control_Panel_%28Windows%29)
- [List of Control Panel Command Line Commands](https://www.lifewire.com/command-line-commands-for-control-panel-applets-2626060)

## Diff and merge tools

For Windows, in `%USERPROFILE%.git_config`:

```
[diff]
	tool = bc4
[difftool "bc4"]
	cmd = \"C:\\Program Files\\Beyond Compare 4\\BComp.exe\" \"$LOCAL\" \"$REMOTE\"
[merge]
	tool = bc4
[mergetool "bc4"]
	cmd = \"C:\\Program Files\\Beyond Compare 4\\BComp.exe\" \"$LOCAL\" \"$REMOTE\" \"$BASE\" \"$MERGED\"
	trustExitCode = true
```

```sh
git difftool --no-prompt FILEPATH FILEPATH
git mergetool --no-prompt FILEPATH
```

- [Git - git-mergetool Documentation](https://git-scm.com/docs/git-mergetool)
- [Git - git-difftool Documentation](https://git-scm.com/docs/git-difftool)
- [Beyond Compare Technical Support](http://www.scootersoftware.com/support.php?zz=kb_vcs)

## Remove branches no longer on remote

```sh
git branch --merged | egrep -v "(^\*|main|master|develop)" | xargs git branch -d
```

- [git - Remove tracking branches no longer on remote - Stack Overflow](https://stackoverflow.com/questions/7726949/remove-tracking-branches-no-longer-on-remote)
- [github - git - how to get default branch? - Stack Overflow](https://stackoverflow.com/questions/28666357/git-how-to-get-default-branch)
