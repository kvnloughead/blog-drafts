Idea for a blog on a helpful yet relatively simple git pattern. Two parts.

## Part 1 -- using `git commit` to act as reminders to future self.

When I am stopping work on a project in the middle of a task, I like to commit my changes as a "draft" commit. 

```
$ git commit -m "draft: make foo do bar"
```

If I think I'm likely to be confused by that message, I'll add additional information. When I return to the project, I can pick up where I left off. I'll use `git commit --amend` when I am finished with the task. A word of warning, don't push your draft commits to GitHub, you'll get a mismatched history error when you try push an amended commit. 