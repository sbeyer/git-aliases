# git aliases

This is a collection of git aliases that people might find useful.

Git aliases are virtual git commands that call other (git) commands.
You have them in your Git configuration (e.g., `~/.gitconfig`), looking like this:
```gitconfig
[alias]
	some-alias-name = "what-it-does"
```

Here's a list of what I use:

```gitconfig
[alias]
	get-tree-from = read-tree --reset -u
	who = shortlog -s --

	# git k for consistency
	k = !gitk

	# git status shortcuts
	s = status -s
	st = s -uno

	# find files using git
	find = "!f() { git ls-files '**'$1'**'; }; f"

	# list all ignored files
	ls-ignored = ls-files -o -i --exclude-standard

	# list all changed files
	ls-changed = "diff --name-only"

	# edit files using the editor used by git
	edit = "!`git config core.editor`"

	# handling git conflicts
	ls-unmerged = "ls-changed --diff-filter=U"
	edit-unmerged = "!git edit `git ls-unmerged`"
	add-unmerged = "!git add `git ls-unmerged`"
	reset-unmerged = "!uf=`git ls-unmerged`; git reset HEAD $uf; git checkout -- $uf"

	# git svn stuff
	svn-commit = "!git svn-up && git svn dcommit"
	svn-stash-commit = "!git stash && git svn-commit && git stash pop"
	svn-stash-up = "!git stash && git svn-up && git stash pop"
	svn-up = svn rebase

	# the best way to show history in the terminal
	lg = log --graph --pretty='format:%C(auto)%h%d %s %C(blue)%an %C(green)%cr'
	lf = lg --first-parent

	# ...and with more infos per commit
	lgv = log --decorate --graph --stat
	lgp = log --decorate --graph -p

	# history if you want to see WHEN something happened
	lgt = log --date-order --pretty='format:%C(auto)%h %C(green)%cI %C(blue)%an %C(auto)%s%C(auto)%d'

	# a reminder what happened recently and you usually don't need to press q in the pager
	lg3 = log HEAD~3..HEAD

	# git vi foo -> open all files containing foo in vim... didn't use it since fzf/Telescope, but still nice to have
	vi = "!f() { vim -o `git ls-files *$1*` ; } ; f"

	# git git git git --help
	git = !git

	# shortcut for the most used submodule command
	sup = submodule update --recursive --init

	# cd `git root`
	root = rev-parse --show-toplevel

	# diff shortcuts
	d = diff
	dw = d --color-words
	di = diff --cached
	diw = di --color-words

	# stash shortcuts
	sl = stash list --pretty='format:%C(yellow)%gD %C(green)%cI %C(cyan)%s'
	slp = sl -p
	sls = sl --stat
	srm = stash drop
	sc = stash push --keep-index
	scc = stash push
	sccc = stash push --include-untracked
	scp = sc -p
	sg = stash pop
	sgg = sg --index

	# shortcut to review changes into index
	a = add -p
	af = add

	# shortcut to throw away changes
	aw = checkout -p
	awa = checkout -f

	# shortcut for cherry-pick
	cp = cherry-pick

	# shortcut for fetch/pull
	f = fetch -p
	ff = merge --ff-only @{u}
	p = pull -p
	pm = p --no-ff
	pr = p --rebase

	# shortcuts for merge
	m = merge
	mc = m --continue
	ma = m --abort

	# shortcuts for rebase
	r = rebase -i
	ri = r
	rc = rebase --continue
	rs = rebase --skip
	ra = rebase --abort

	# shortcuts for push
	u = push
	uf = push --force-with-lease

	# shortcuts for commit
	c = commit
	cm = commit -m
	ca = commit --amend

	# shortcut for branch stuff
	b =  branch -vv
	bd = branch -d
	bdf = branch -D
	br = branch -m
	bn = checkout -b

	# switch branches using fzf
	sb = "!f() { branch=$(git branch -vvl | fzf -e | sed -ne 's/^..\\([^ ]*\\) .*$/\\1/p') ; case \"$branch\" in \"\") echo Branch not changed. ;; *) git switch \"$branch\" ;; esac ; test \"$#\" -gt 0 && echo \"Ignored arguments: $@\" ; } ; f"
	sbr = "!f() { branch=$(git branch -vvr | fzf -e | sed -ne 's/^..\\([^ ]*\\) .*$/\\1/p') ; case \"$branch\" in \"\") echo Branch not changed. ;; *) git switch -t \"$branch\" ;; esac ; test \"$#\" -gt 0 && echo \"Ignored arguments: $@\" ; } ; f"
	sba = "!f() { branch=$(git branch -vva | fzf -e | sed -ne 's/^..\\([^ ]*\\) .*$/\\1/p') ; case \"$branch\" in remotes/*) git switch -t \"$branch\" ;; \"\") echo Branch not changed. ;; *) git switch \"$branch\" ;; esac ; test \"$#\" -gt 0 && echo \"Ignored arguments: $@\" ; } ; f"

	# detach HEAD (yea, I sometimes want that)
	detach = switch --detach

	# credit (or blame) authors
	cr = blame --color-lines -w
	crr = cr -C -C
	crrr = cr -C -C -C
```
