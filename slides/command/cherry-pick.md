# cherry-pick

<div grid="~ cols-2 gap-4" class="justify-items-left">

<div>

- Suppose you had a series of commits on your development branch, dev, as shown in beow Figure, and you wanted to introduce them onto the master branch but in a substantially different order.
    ```shell
    git checkout master
    git cherry-pick dev^
    git cherry-pick dev~3
    git cherry-pick dev~2
    git cherry-pick dev
    ```

</div>

<div class="text-center mt-5">

<img src="/git-cherry-pick1.png" class="h-20">

Before cherry-pick

<img src="/git-cherry-pick2.png" class="h-20">

After cherry-pick

</div>

</div>

- *git cherry-pick* also allowed a range of commits to be selected and reapplied in a single command, for example:
    ```shell
    git cherry-pick X..Z
    ```