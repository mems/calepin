- [Git - Documentation](https://git-scm.com/doc)
- [Git Explorer](https://gitexplorer.com/) - "Find the right commands you need without digging through the web"
- [Version Control Best Practices](https://www.git-tower.com/blog/version-control-best-practices/)
- [Introducing Git Submodule in Tower](https://www.git-tower.com/blog/introducing-git-submodules-in-tower/)
- [version control - Git for beginners: The definitive practical guide - Stack Overflow](https://stackoverflow.com/questions/315911/git-for-beginners-the-definitive-practical-guide)
- [Gérez vo code source avec Git - OpenClassrooms](https://openclassrooms.com/courses/gerez-vos-codes-source-avec-git)
- List of commands in plain english: [Oh Shit, Git!?!](https://ohshitgit.com/)
- [Explain Git with D3](https://onlywei.github.io/explain-git-with-d3/) - Visualizing Git Concepts
- [alaingilbert/git2graph: Generate a git graph structure from linear git history](https://github.com/alaingilbert/git2graph)
- [cecton/git-tools: Git subcommands to help with your workflow](https://github.com/cecton/git-tools/#git-try-merge) - "`git try-merge` does like a `git merge origin/main` but helps you resolve the conflicting commits one by one instead than having to solve them altogether like `git merge`"

```sh
# List files in commit
git diff-tree --no-commit-id --name-only -r <commit>

# List files in stash
git stash show -p stash@{0} --name-only

# Apply stach as a patch (if git stash apply fail)
#git stash show -p | git apply --apply --index --whitespace=fix --reject
git stash show -p | git am -3

# Export stash as patch file
git stash show "stash@{0}" -p > ~/Desktop/changes.patch
git archive "stash@{0}" | gzip >whatever.tgz

# Apply a patch file
#git apply --index --3way --binary --verbose /path/to/changes.patch
#git apply --index --3way --binary --whitespace=fix /path/to/changes.patch
git apply --apply --index --whitespace=fix --reject /path/to/changes.patch
# Then list rejected files
find -name *.rej

# Create a branch from stash
git stash branch stashed_changes_branch

# Get file stats (list files per number of commit change it)
git log --pretty=format: --name-only | sort | uniq -c | grep -vE '/path/to/ignore|/path/to/file/to/ignore' | sort -rg | head -40

# Rollback commit as patch
git diff --binary $COMMIT_HASH $COMMIT_HASH^ > /path/to/mypatch.patch

# Create a patch from staged changes
git diff --cached --binary > /path/to/mypatch.patch

# Create a patch from working directory (uncommitted modifications)
git diff --binary HEAD > /path/to/mypatch.patch

# Create an archive include files changes between 2 commits
LAST_COMMIT_HASH=<newest-commit-id-to-include>; FIRST_COMMIT_HASH=<oldest-commit-id-to-include>; git archive --prefix=some_path_prefix/ -o ~/Desktop/patch.zip $LAST_COMMIT_HASH:src_path $(git diff-tree -r --no-commit-id --name-only --diff-filter=ACMRT $FIRST_COMMIT_HASH^:src_path $LAST_COMMIT_HASH:src_path)
```

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
- [git - pre-receive hook on server-side that refuse any push to master which ha any non-linear history - Stack Overflow](https://stackoverflow.com/questions/5488442/pre-receive-hook-on-server-side-that-refuse-any-push-to-master-which-has-any-non)
- [githook - git server side hook - only specific branche will be pushed - Stack Overflow](https://stackoverflow.com/questions/47201157/git-server-side-hook-only-specific-branches-will-be-pushed)
- [Git - Git Hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks#_server_side_hooks)
- [Git - git-receive-pack Documentation](https://git-scm.com/docs/git-receive-pack#_pre_receive_hook)
- [Git - githook Documentation](https://git-scm.com/docs/githooks)
- [platform-samples/pre-receive-hook at master · github/platform-samples](https://github.com/github/platform-samples/tree/master/pre-receive-hooks)
- [platform-samples/commit-current-user-check.sh at master · github/platform-samples](https://github.com/github/platform-samples/blob/master/pre-receive-hooks/commit-current-user-check.sh)
- [githook - git: who pushed in post-receive hook - Stack Overflow](https://stackoverflow.com/questions/3762012/git-who-pushed-in-post-receive-hook)
- [git/hooks--update.sample at master · git/git](https://github.com/git/git/blob/master/templates/hooks--update.sample)
- [git/update-hook-example.txt at master · git/git](https://github.com/git/git/blob/master/Documentation/howto/update-hook-example.txt)
- bare repo hooks: `repo.git/hook/update`
- [Git post-receive hook not working? - Stack Overflow](https://stackoverflow.com/questions/49728213/git-post-receive-hook-not-working) - post-receive hook has no lock mecanism
- [How Not to Write Your Git Update Hooks - DZone DevOps](https://dzone.com/articles/how-not-to-write-your-git-update-hooks)
- https://schacon.github.io/git/howto/update-hook-example.txt
- [githooks - Git hook: add a new file to repo if a new branch is created - Stack Overflow](https://stackoverflow.com/questions/18323175/git-hook-add-a-new-file-to-repo-if-a-new-branch-is-created/18325201#18325201)
- [One-click App Deployment with Server-side Git Hooks — SitePoint](https://www.sitepoint.com/one-click-app-deployment-server-side-git-hooks/)
- [git - View commits on a new branch in the update hook - Stack Overflow](https://stackoverflow.com/questions/18723219/view-commits-on-a-new-branch-in-the-update-hook/18726025#18726025)
- [Git - An Example Git-Enforced Policy](https://git-scm.com/book/en/v2/Customizing-Git-An-Example-Git-Enforced-Policy)
- [I there a way to configure git repository to reject 'git push --force'? - Stack Overflow](https://stackoverflow.com/questions/1754491/is-there-a-way-to-configure-git-repository-to-reject-git-push-force)

How Git hooks works:

- [Are git pre-receive/update hook serialized? - DevOp Stack Exchange](https://devops.stackexchange.com/questions/431/are-git-pre-receive-update-hooks-serialized/439#439)
- [Git - git-receive-pack Documentation](https://git-scm.com/docs/git-receive-pack#_quarantine_environment)
- [How To Use Git Hooks To Automate Development and Deployment Tasks | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-use-git-hooks-to-automate-development-and-deployment-tasks)

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

### JSON diff

```sh
jq -c . input.json
```

- [tomnomnom/gron: Make JSON greppable!](https://github.com/tomnomnom/gron)

### Image diff

Exemple to diff PNG files with EXIFtool

```sh
echo '*.png diff=exif' >> .gitattributes
git config diff.exif.textconv exiftool

diff --git a/image.png b/image.png
```

```sh
identify -verbose info: <image>
```

- [Git - How to Get Better Diffs for Images - Lars Tesmer's Blog](https://web.archive.org/web/20200805133545/http://www.lars-tesmer.com/blog/2010/09/20/git---how-to-get-better-diffs-for-images/)

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

### SQLite diff

```
[diff "sqlite3"]
    textconv = sqlite3 $1 .dump
```

- [sqldiff.exe: Database Difference Utility](https://sqlite.org/sqldiff.html)
- [simonw/sqlite-diffable: Tools for dumping/loading a SQLite database to diffable directory structure](https://github.com/simonw/sqlite-diffable)

## Sparse checkout

Aka partial checkout

[Is there any way to clone a git repository's sub-directory only? - Stack Overflow](https://stackoverflow.com/questions/600079/is-there-any-way-to-clone-a-git-repositorys-sub-directory-only/13738951#13738951)

## Commit

### Commit as other author

```

--author=<author>
```

```
From:
```

```sh
git commit --amend --author="Author Name <email@address.com>"
```

- [git - Change commit author at one specific commit - Stack Overflow](https://stackoverflow.com/questions/3042437/change-commit-author-at-one-specific-commit)

### Update commit messages

Do it only for non pushed commits

- [How to Batch Update Git Commit Messages](https://davidwalsh.name/update-git-commit-messages)

### Removing a file from every commit

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

```sh
# by default it's $XDG_CONFIG_HOME/git/ignore or ~/.config/git/ignore
git config --global core.excludesFile '~/.gitignore'
```

- [Git - gitignore Documentation](https://git-scm.com/docs/gitignore)
- [Global Git ignore - Stack Overflow](https://stackoverflow.com/questions/7335420/global-git-ignore)
- [git - gitignore - only allow certain extensions and files - Stack Overflow](https://stackoverflow.com/questions/11852558/gitignore-only-allow-certain-extensions-and-files/11853075#11853075)
- [gitignore - Is there a way to tell git to only include certain files instead of ignoring certain files? - Stack Overflow](https://stackoverflow.com/questions/1279533/is-there-a-way-to-tell-git-to-only-include-certain-files-instead-of-ignoring-cer/43438694#43438694)
- [github/gitignore: A collection of useful .gitignore templates](https://github.com/github/gitignore)
- https://www.gitignore.io/

## Commit empty directory

Use an empty `.gitignore` in the empty directory, or with a list of files that should be ignored:

```gitignore
# Ignore everything in this directory
*
# Except this file
!.gitignore
```

Or create a file like `.keep` or `.gitkeep` (the name is not important, it's not a feature of Git) in the empty directory.

- [What is .gitkeep? Differences between .gitignore and .gitkeep - Apply Head](https://applyhead.com/gitkeep-vs-gitignore/)
- [How can I add an empty directory to a Git repository? - Stack Overflow](https://stackoverflow.com/questions/115983/how-can-i-add-an-empty-directory-to-a-git-repository)
- [Git FAQ - Git SCM Wiki](https://git.wiki.kernel.org/index.php/Git_FAQ#Can_I_add_empty_directories.3F)
- [What is .gitkeep? How to Track and Push Empty Folders in Git](https://web.archive.org/web/20211218035743/https://www.freecodecamp.org/news/what-is-gitkeep/)
- [git - What are the differences between .gitignore and .gitkeep? - Stack Overflow](https://stackoverflow.com/questions/7229885/what-are-the-differences-between-gitignore-and-gitkeep)

## Include version

- [To put the prefix ?<revision-number> to codes by Git/Svn - Stack Overflow](https://stackoverflow.com/questions/1127177/to-put-the-prefix-revision-number-to-codes-by-git-svn/1127241#1127241)
- [How do I enable ident string for Git repos? - Stack Overflow](https://stackoverflow.com/questions/1792838/how-do-i-enable-ident-string-for-git-repos)

## Case sensitivity

```sh
git mv hello.txt Hello.txt
```

- [rename - Changing capitalization of filename in Git - Stack Overflow](https://stackoverflow.com/questions/10523849/changing-capitalization-of-filenames-in-git)

If a remove branch doesn't appears because it use a different naming (ext `origin/Feature/branchA` vs `origin/feature/branchA`) update path name in `/.git/modules/submodules/<submodule>/refs/remotes/origin/feature`

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

## Restore delete file

```sh
# Get the commit hash that delete the file
git rev-list -n 1 HEAD -- <file_path>

# List all commits that involved that file path
git log --all -- <file_path>

# List all deleted files
git ls-files -d
git log --diff-filter=D --summary | grep delete

# Restore the
git checkout $(git rev-list -n 1 HEAD -- "$file")^ -- "$file"
```

- [How to find and restore a deleted file in a Git repository - Stack Overflow](https://stackoverflow.com/questions/953481/how-to-find-and-restore-a-deleted-file-in-a-git-repository)

## Worktree

- Git 2.5+
- [How to clone a specific Git branch? - Stack Overflow](https://stackoverflow.com/questions/1911109/how-to-clone-a-specific-git-branch)
- [Multiple working directorie with Git? - Stack Overflow](https://stackoverflow.com/questions/6270193/multiple-working-directories-with-git/30185564#30185564)
- [Git - git-worktree Documentation](https://git-scm.com/docs/git-worktree)
- [Parallelize Development Using Git Worktrees](https://spin.atomicobject.com/2016/06/26/parallelize-development-git-worktrees/)
