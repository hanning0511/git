# stash

The stash is a mechanism for capturing your work in progress, allowing you to save it and return to it later when convenient. The *git stash* command save your current working directory and index, then clear them out.

<div grid="~ cols-2 gap-8" class="justify-items-center">

<div>

1. Suppose you were working happily on a task. A very serious bug is reported to you and you have to stop current work to fix it.
   ```shell {monaco}
   git stash save "WIP: task xxx"
   ```

</div>

<div>

2. The bug has been fixed. Let's restore the task.
   ```shell {monaco}
   git stash pop
   ```

</div>

</div>

- Full git stash uages
   ```shell
   git stash list [<options>]
   git stash show [<options>] [<stash>]
   git stash drop [-q|--quiet] [<stash>]
   git stash ( pop | apply ) [--index] [-q|--quiet] [<stash>]
   git stash branch <branchname> [<stash>]
   git stash clear
   git stash [push [-p|--patch] [-k|--[no-]keep-index] [-q|--quiet]
      [-u|--include-untracked] [-a|--all] [-m|--message <message>]
      [--] [<pathspec>...]]
   git stash save [-p|--patch] [-k|--[no-]keep-index] [-q|--quiet]
      [-u|--include-untracked] [-a|--all] [<message>]
   ```