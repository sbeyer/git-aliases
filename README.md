# git aliases

This is a collection of git aliases that people might find useful.

Git aliases are virtual git commands that call other (git) commands.
You have them in your Git configuration (e.g., `~/.gitconfig`), looking like this:
```gitconfig
[alias]
	some-alias-name = "what-it-does"
```

You are encouraged to share your aliases as an issue (preferred), pull request, or via [Twitter](http://twitter.com/_sbeyer_).

For now I only list my used aliases.
Later, I will make the list more accessible by categorizing the aliases, giving descriptions, use-cases, and examples.

```gitconfig
	edit = "!`git config core.editor`"
	diff-words = "diff --color-words"
	list-changed = "diff --name-only"
	list-unmerged = "list-changed --diff-filter=U"
	edit-unmerged = "!git edit `git list-unmerged`"
	add-unmerged = "!git add `git list-unmerged`"
	reset-unmerged = "!uf=`git list-unmerged`; git reset HEAD $uf; git checkout -- $uf"
	lg = log --graph --pretty='format:%C(auto)%h%d %s %C(blue)%an %C(green)%cr'
	timelog = log --date-order --pretty='format:%C(auto)%h %C(green)%cI %C(blue)%an %C(auto)%s%C(auto)%d'
	get-tree-from = read-tree --reset -u
	k = !gitk
	log3 = log HEAD~3..HEAD
	logv = log --decorate --graph --stat
	find = "!f() { git ls-files '**'$1'**'; }; f"
	ls-ignored = ls-files -i --exclude-standard
	svn-commit = "!git svn-up && git svn dcommit"
	svn-stash-commit = "!git stash && git svn-commit && git stash pop"
	svn-stash-up = "!git stash && git svn-up && git stash pop"
	svn-up = svn rebase
	s = status -uno
	vi = "!f() { vim -o `git ls-files *$1*` ; } ; f"
	who = shortlog -s --
	git = !git
```
