Frequently committing WIP code can be managed by:
1. **Squashing Commits:** Before merging into main, squash the WIP commits. This condenses multiple commits into one, making the history cleaner.
	- Create and work on a feature branch (commit changes as usual):
	  ```
	  git checkout -b feature
		```
	- Squash and merge into the main branch once the work is complete:
	  ```
		git checkout main 
		git merge --squash feature 
		git commit -m "Add new feature"
		```
	- This combines all commits from `feature` into a single commit on `main`. 
2. **Interactive Rebase:** Use `git rebase -i` to clean up the commit history. It allows to combine, reorder, or remove commits before pushing them to main.
	- This opens your default text editor with a list of the last 5 commits. Each commit is prefixed with `pick`.
		```
		git rebase -i HEAD~5
		```
	- **Squashing Commits:** Squash a commit into the previous one by changing its command from `pick` to `squash` (or simply `s`). 
	  ```
		pick 1234567 First commit
		squash 89abcde Second commit
		squash fedcba9 Third commit
		pick 13579bd Fourth commit
		pick 2468ace Fifth commit
		```
	- **Reordering, Editing, or Dropping Commits:** The lines can be reordered to change the commit order, change `pick` to `edit` if you want to modify the commit content, or delete a line entirely to drop a commit.
	- **Force-Push (if necessary):** If you’ve already pushed these commits to a remote branch, you’ll need to force-push to update the remote:
	  ```
		git push --force origin your-branch
		```
3. **WIP Branch:** Keep the WIP commits on a dedicated branch. When the work is ready, merge a cleaned-up version into your main branch.
