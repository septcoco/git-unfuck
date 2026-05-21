# git unfuck

A friendly recovery tool for git disasters. Run `git unfuck` when you've lost commits, deleted the wrong branch, got stuck mid-rebase, or have no idea what just happened.

It reads your reflog and dangling objects, figures out the most likely scenarios, and walks you through fixing them. Every destructive operation creates a backup branch first so you can always undo the undo.

## Install

```sh
mkdir -p ~/bin
curl -fsSL https://raw.githubusercontent.com/septcoco/git-unfuck/main/git-unfuck -o ~/bin/git-unfuck
chmod +x ~/bin/git-unfuck
```

Then add `~/bin` to your PATH if it isn't already. On macOS with zsh:

```sh
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

Now `git unfuck` works inside any repo.

## Use

```
$ git unfuck
```

That's it. It scans the repo and offers options.

## What it handles

- commits lost after a reset or rebase
- branches you deleted by accident
- detached HEAD (you're not on a branch and don't know how you got there)
- stashes you dropped
- merges, rebases, or cherry-picks you're stuck in
- "I don't even know what happened, just tell me" — plain English summary of recent activity

## Safety

Any operation that could lose work creates a backup branch named `unfuck-backup/<timestamp>` before doing anything. If something goes wrong, `git reset --hard unfuck-backup/<timestamp>` brings you back.

The tool never touches anything that isn't already in git's history. If you ran `git gc --prune=now` after the disaster, the data is genuinely gone and nothing can recover it.

## Requirements

- git
- Python 3.8+ (already installed on macOS and most Linux distros)

## License

MIT
