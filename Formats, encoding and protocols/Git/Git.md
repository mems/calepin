## Libraries and implementations

- [isomorphic-git/isomorphic-git: A pure JavaScript implementation of git for node and browsers!](https://github.com/isomorphic-git/isomorphic-git)
- [petersalomonsen/wasm-git: GIT for nodejs and the browser using https://libgit2.org compiled to WebAssembly with https://emscripten.org](https://github.com/petersalomonsen/wasm-git)
- [~sircmpwn/shit - sourcehut git](https://git.sr.ht/~sircmpwn/shit) - An implementation of git in (almost) pure POSIX shell
- [nayuki/Git-library-Java: Low-level Java library to read/write Git repositories.](https://github.com/nayuki/Git-library-Java)
- [djanderson/aho: A git implementation in awk](https://github.com/djanderson/aho)

## How git works

- [git - Rebase local repo with remote whose history ha changed - Stack Overflow](https://stackoverflow.com/questions/42267566/rebase-local-repo-with-remote-whose-history-has-changed/42281702#42281702)
- [Git from the inside out](https://maryrosecook.com/blog/post/git-from-the-inside-out)
- [Git de l'intérieur](https://alm.developpez.com/tutoriel/fonctionnement-interne-de-git/)
- [The Architecture of Open Source Applications (Volume 2): Git](http://aosabook.org/en/git.html)
- [blob - How to DEFLATE with a command line tool to extract a git object? - Stack Overflow](https://stackoverflow.com/questions/3178566/how-to-deflate-with-a-command-line-tool-to-extract-a-git-object)
- [Some of git internals (updated)](https://web.archive.org/web/20201226115731/https://yurichev.com/news/20201220_git/)

### Hash of a file

Content of `blob FILE_SIZE\0FILE_CONTENT`

- [Git - finding the SHA1 of an individual file in the index - Stack Overflow](https://stackoverflow.com/questions/460297/git-finding-the-sha1-of-an-individual-file-in-the-index/24283352#24283352)
- [How is the git hash calculated? - Stack Overflow](https://stackoverflow.com/questions/35430584/how-is-the-git-hash-calculated)

## Implement a custom remote

For storage or transmition protocol

- https://github.com/git/git/blob/master/git-remote-testgit.sh https://github.com/git/git/blob/master/Documentation/git-remote-testgit.txt
- [Git - git-remote-helper Documentation](https://git-scm.com/docs/git-remote-helpers)
- [pull-git-remote-helper](https://www.npmjs.com/package/pull-git-remote-helper) and [clehner/abstract-pull-git-repo: abstract interface for git repo using pull streams](https://github.com/clehner/abstract-pull-git-repo)
- [peritus/git-remote-couch: a git-remote-helper that allow you to push source code into a CouchDB](https://github.com/peritus/git-remote-couch)
- [glandium/git-cinnabar: git remote helper to interact with mercurial repositories](https://github.com/glandium/git-cinnabar)
- [anishathalye/git-remote-dropbox: A transparent bridge between Git and Dropbox - use a Dropbox (shared) folder a a Git remote!](https://github.com/anishathalye/git-remote-dropbox)
	- [Dropbox a a True Git Server · cat /var/log/life](https://www.anishathalye.com/2016/04/25/dropbox-as-a-true-git-server/)
	- [git-remote-dropbox · cat /var/log/life](https://www.anishathalye.com/2015/08/19/git-remote-dropbox/)
	- [git-remote-dropbox/DESIGN.rst at master · anishathalye/git-remote-dropbox](https://github.com/anishathalye/git-remote-dropbox/blob/master/DESIGN.rst)
- [felipec/git-remote-bzr: Transparent bidirectional bridge between Git and Bazaar for Git](https://github.com/felipec/git-remote-bzr)
- `git remote -v`

- [Extend Git with Custom Command (Example)](https://coderwall.com/p/bt93ia/extend-git-with-custom-commands)

## Diff format

```diff
diff --git a/path/file-old.ext b/path/file.ext
similarity index 100%
rename from path/file-old.ext
rename to path/file.ext
```

```c
// https://github.com/git/git/blob/3bab5d56259722843359702bc27111475437ad2a/apply.c#L1329-L1345
optable[] = {
	{ "@@ -", gitdiff_hdrend },
	{ "--- ", gitdiff_oldname },
	{ "+++ ", gitdiff_newname },
	{ "old mode ", gitdiff_oldmode },
	{ "new mode ", gitdiff_newmode },
	{ "deleted file mode ", gitdiff_delete },
	{ "new file mode ", gitdiff_newfile },
	{ "copy from ", gitdiff_copysrc },
	{ "copy to ", gitdiff_copydst },
	{ "rename old ", gitdiff_renamesrc },
	{ "rename new ", gitdiff_renamedst },
	{ "rename from ", gitdiff_renamesrc },
	{ "rename to ", gitdiff_renamedst },
	{ "similarity index ", gitdiff_similarity },
	{ "dissimilarity index ", gitdiff_dissimilarity },
	{ "index ", gitdiff_index },
	{ "", gitdiff_unrecognized },
};
```

- [Git - diff-format Documentation](https://git-scm.com/docs/diff-format#_generating_patch_text_with_p)
- [`git-am` internaly use `git-apply`](https://github.com/git/git/blob/bbcefff/git-am.sh#L151)
- [patch - What is the difference between git am and git apply? - Stack Overflow](https://stackoverflow.com/questions/12240154/what-is-the-difference-between-git-am-and-git-apply)
