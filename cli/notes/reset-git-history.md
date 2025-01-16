To rollback the repository to the initial commit, first find the SHA1 of the first commit:
```
$ git rev-list --max-parents=0 HEAD
00507b809baafb9ddf66c62e714ea712f718c2ab

$ git rev-list --max-parents=0 --abbrev-commit HEAD
00507b8
```

Then run either command depending on whether you want to preserve or discard all the changes made since that initial commit.
```
$ git reset 00507b8
$ git reset --hard 00507b8
```

Finally update the remote repository:
```
$ git push origin --force
```

Sources:
- https://stackoverflow.com/a/16500248/13910414
- https://calincrist.com/how-to-reset-the-git-history-back-to-initial-commit
- https://www.datacamp.com/tutorial/git-reset-revert-tutorial
