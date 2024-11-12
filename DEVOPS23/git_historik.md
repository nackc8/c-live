# Amend

```
❯ git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        entillfil.txt
        minfil.txt

nothing added to commit but untracked files present (use "git add" to track)
```

```
ignored-tempgit main*​
❯ git add minfil.txt

ignored-tempgit main*​​
❯  git commit -m 'ofijhoi'
[main (root-commit) d39f8e1] ofijhoi
 1 file changed, 5 insertions(+)
 create mode 100644 minfil.txt
 ```

Ändra senaste committen med amend:

git commit --amend # ändrar meddelandet

Oops! Glömde en fil!

❯ git add entillfil.txt  ^C

ignored-tempgit main
❯ git commit --amend   ^C

Glömde innehåll i en fil, vill inte ändra commit-meddelande

git add .
git commit --amend --no-edit

# Rebase
