# Pack File

<div grid="~ cols-2 gap-4" class="justify-items-center">

<div class="mt-5">

### Storing the complete content of every version of every file is incredibly inefficient. So Git uses a more efficient storage mechanism called a pack file. It only stores the first version of file and deltas.

<br/>

```shell
host~: git gc
Enumerating objects: 10, done.
Counting objects: 100% (10/10), done.
Delta compression using up to 36 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (10/10), done.
Total 10 (delta 0), reused 0 (delta 0)
```

</div>

<div class="mt-5">

<img src="https://stefan.saasen.me/articles/git-clone-in-haskell-from-the-bottom-up/images/pack-client-server.png" class="h-100">

</div>

</div>