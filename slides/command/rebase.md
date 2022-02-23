# rebase

<div grid="~ cols-2 gap-4" class="justify-items-left">

<div>

1. Suppose you had been working on a topic branch, meanwhile new commits were applied on master branch. Before creating pull request based on the topic branch, you need to rebase to the tip-of-master.

    ```shell {monaco}
    git checkout topic
    git rebase master
    ```

</div>

<div class="text-center mt-5">

<img src="/git-rebase1.png" class="h-20">

before rebase

<img src="/git-rebase2.png" class="h-20">

after rebase

</div>

</div>

2. Reordering, editing, removing, squashing multiple commits into one, and splitting a commit into several are all easily performed by the git rebase command using the -i or --interactive option.
    ```shell {monaco}
    git rebase -i HEAD~2
    pick 7fa6096 hello tom
    pick dcc7a3b hello jack
    ...
    ```