---
title: "How to Create a Custom Git Commands on Windows"
date: 2024-10-01
---

## Intruduction
[`Git`](https://git-scm.com/) is one of the most popular version control systems, widely used by developers to manage and track changes in their code. While `Git` comes with built-in commands that handle most tasks, sometimes you may want to create custom commands to simplify repetitive tasks or enhance your workflow.

### Why Create Custom Git Commands?
Before diving into the technical details, it's important to understand why creating custom Git commands can be useful:

* **Automation:** Save time on repetitive tasks by wrapping multiple `Git` commands into one.
* **Simplification:** Reduce complex command sequences into a single, easy-to-remember command.
* **Consistency:** Ensure that your team follows the same workflow by creating shared commands.
* **Personalization:** Tailor Git’s behavior to match your specific workflow needs.

In this article, we’ll walk through how to create a custom Git command.

## Fast Push Command

Let’s create a command called `fpush` for quickly pushing changes. This command will perform the following steps:

1. Pull data from the current branch
2. Stage all unstaged changes
3. Commit these changes
4. Push the commit to the server

## 1. Create the Command File

* Create a new folder to hold files with custom commands _(for example, "E:/git-custom-commands")_.
* Inside this folder, create a new command file named `git-fastpush.cmd`.
* Add the following content to the file:

    ```bash
    git pull
    git add .
    git commit -m %1
    git push
    ```

### Explanation of Commands:
- **`git pull`:** Fetch changes from a remote repository into the current branch.
- **`git add .`:** Stage all unstaged changes.
- `git commit -m %1`: Commit changes, where `%1` is the first argument passed to the command (e.g., `git fpush "this_is_commit_message"`).
- `git push`: Push the local commit to the server.

## 2. Add a New Alias to the Git Config

Next, we need to add the new `alias` to the **Git configuration** with reference to our file. Run the following command in the console:

```bash
git config --global alias.fpush "!E:/git-custom-commands/git-fastpush.cmd"
```

## 2. Run the New Command
You're all set! Now you can execute your new Git command:
```
git fpush "your_comment"
```

Here we go. Feel free to create your own custom commands!