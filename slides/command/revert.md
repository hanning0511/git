# revert

<div grid="~ cols-2 gap-4" class="justify-items-left mt-10">

<div>

The *git revert* commit command is substantially similar to the command *git cherry-pick* commit with one important difference: it applies the inverse of the given commit. Thus, this command is used to introduce a new commit that reverses the effects of a given commit.

```shell {monaco}
git revert master~2
```

</div>

<div class="text-center mt-5">

<img src="/git-revert1.png" class="w-85">

Before revert

<br/>
<br/>

<img src="/git-revert2.png" class="w-100">

After revert

</div>

</div>