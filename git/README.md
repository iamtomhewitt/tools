# Git

Other useful things are in the folder above.

### Rewrite the author of commits
* Open a terminal
* Paste: 
```bash
#!/bin/sh

git filter-branch --env-filter '
OLD_EMAIL="your-old-email@example.com"
CORRECT_NAME="Your Correct Name"
CORRECT_EMAIL="your-correct-email@example.com"
if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```
* Press enter
* Run `git update-ref -d refs/original/refs/heads/master`
* Run `git push --force --tags origin HEAD:master` 🎉

### Reset tags to align with remote
```bash
git tag -l | xargs git tag -d
git fetch --tags
```
