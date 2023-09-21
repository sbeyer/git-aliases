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
[alias]
	get-tree-from = read-tree --reset -u
	s = status -uno
	who = shortlog -s --
	k = !gitk

	# find files using git
	find = "!f() { git ls-files '**'$1'**'; }; f"

	# list all ignored files
	ls-ignored = ls-files -o -i --exclude-standard

	# list all changed files
	ls-changed = "diff --name-only"

	# edit files using the editor used by git
	edit = "!`git config core.editor`"

	# handling git conflicts
	list-unmerged = "list-changed --diff-filter=U"
	edit-unmerged = "!git edit `git list-unmerged`"
	add-unmerged = "!git add `git list-unmerged`"
	reset-unmerged = "!uf=`git list-unmerged`; git reset HEAD $uf; git checkout -- $uf"

	# git svn stuff
	svn-commit = "!git svn-up && git svn dcommit"
	svn-stash-commit = "!git stash && git svn-commit && git stash pop"
	svn-stash-up = "!git stash && git svn-up && git stash pop"
	svn-up = svn rebase

	# the best way to show history in the terminal
	lg = log --graph --pretty='format:%C(auto)%h%d %s %C(blue)%an %C(green)%cr'

	# ...and with more infos per commit
	lgv = log --decorate --graph --stat

	# history if you want to see WHEN something happened
	timelog = log --date-order --pretty='format:%C(auto)%h %C(green)%cI %C(blue)%an %C(auto)%s%C(auto)%d'

	# a reminder what happened recently and you usually don't need to press q in the pager
	log3 = log HEAD~3..HEAD

	# git vi foo -> open all files containing foo in vim... didn't use it since fzf/Telescope, but still nice to have
	vi = "!f() { vim -o `git ls-files *$1*` ; } ; f"

	# git git git git --help
	git = !git

	# a shortcut for the most used submodule command
	sup = submodule update --recursive --init

	# cd `git root`
	root = rev-parse --show-toplevel

	# diff shortcuts
	d = diff
	dw = d --color-words
	di = diff --cached
	diw = di --color-words

	# switch branches using fzf
	sb = "!f() { branch=$(git branch -vva | fzf -e | sed -ne 's/^..\\([^ ]*\\) .*$/\\1/p') ; if [ -n \"$branch\" ] ; then if [[ \"$branch\" =~ ^remotes/ ]] ; then git switch -t \"$branch\" ; else git switch \"$branch\" ; fi ; fi ; test \"$#\" -gt 0 && echo \"Ignored arguments: $@\" ; } ; f"

	# detach HEAD (yea, I sometimes want that)
	detach = switch --detach
```
