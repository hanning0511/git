---
theme: default
background: https://source.unsplash.com/collection/94734566/1920x1080
class: 'text-center'
highlighter: shiki
lineNumbers: false
info: |
  ## Git
drawings:
  persist: false

---

# Git

### Han Ning

---

# Birth of Git (1)

<v-clicks>

- Before the birth of Git, the Linux kernel was developed using the commercial BitKeeper[1] VCS.
- The company that owned BitKeeper placed additional restrictions on its “free as in beer” version in the spring of 2005, the Linux community realized that BitKeeper was no longer a viable solution.
- Torvalds looked for alternatives. Failed. He set out to write his own, the Git.
- Key events of Git:
  - Development began on **3 April 2005**.
  - Torvalds announced the project on **6 April 2005**.
  - Git became self-hosted on **7 April 2005**.
    ```
    commit e83c5163316f89bfbde7d9ab23ca2e25604af29
    Author: Linus Torvalds <torvalds@ppc970.osdl.org>
    Date:   Thu Apr 7 15:13:13 2005 -0700

    Initial revision of "git", the information manager from hell
    ```

</v-clicks>

[1] <a href="http://www.bitkeeper.org/">BitKeeper</a>

---

# Birth of Git (2)

<v-click>

- key events of Git.
  - First Linux commit was maded on 16 April 2005
    ```
    commit 1da177e4c3f41524e886b7f1b8a0c1fc7321cac2
    Author: Linus Torvalds <torvalds@ppc970.osdl.org>
    Date:   Sat Apr 16 15:20:36 2005 -0700

    Linux-2.6.12-rc2

    Initial git repository build. I'm not bothering with the full history,
    even though we have it. We can create a separate "historical" git
    archive of that later if we want to, and in the meantime it's about
    3.2GB when imported into git - space that would just make the early
    git days unnecessarily complicated, when we don't have a lot of good
    infrastructure for it.

    Let it rip!
    ```

    ```
    17291 files changed, 6718755 insertions(+), 0 deletions(-)
    ```

</v-click>
---

# Birth of Git (3)

- Naming
  - "unpleasant person" in British English slang
  - Global information tracker
  - Goddamn idiotic truckload of sh*t

---

# Repository

- A complete working copy of all the files.
- A copy of the repository itself.
  - configurations
  - **object store**
  - **index**
  - ...

<div class="mt-10">

```shell
# ls .git        
branches  COMMIT_EDITMSG  config  description  HEAD  hooks  index  info  logs  objects  refs
```

</div>

---

# Object Store (1)

<div class="mt-10">

### Object store is at the heart of Git's repository implementation. It contains original data files and all the log messages, author information, dates, and other information required to rebuild any version or branch of the project.

</div>

<div grid="~ cols-2 gap-2" class="justify-items-center text-center mt-10">

<div>

```shell
.git/objects/f1/38820097c8ef62a012205db0b1701df516f6d5
.git/objects/f4/e5a3565665973603222e2fc71bbbaf76969eaa
.git/objects/a1/f08a707c39c1d4b539f198b7d5b5ddc1afbb83
.git/objects/0d/de9ae0b8c4ab9d228f208e8f7d30662c90df96
.git/objects/ec/9b39b0dc59091bbefb65e2ec17952a092e3fd7
.git/objects/d7/ab7c6d324521ee35af57953e4e33684484e692
.git/objects/43/3eb172726bc7b6d60e8d68efb0f0ef4e67a667
.git/objects/8d/31680a3407185b3ec01edfcd0c352cca6a8f02
.git/objects/91/20ce65c97c4bd43857fba9f49363e0c966af91
.git/objects/80/550805d8e2d9630ecd0b6124800dca90b24e33
```

</div>

<div class="text-left">

```c
struct object {
	unsigned parsed : 1;
	unsigned type : TYPE_BITS;
	unsigned flags : FLAG_BITS;
	struct object_id oid;
};

struct object_id {
	unsigned char hash[GIT_MAX_RAWSZ];
	int algo;	/* XXX requires 4-byte alignment */
};
```

</div>

</div>

---

# Object Store (2)

<div class="mt-10">

### Git places only four types of objects in object store. These four atomic objects form the foundation of Git’s higher level data structures.

</div>

<div grid="~ cols-2 gap-2" class="justify-items-center text-center">

<div>

![Local Image](/blob.png)
**Blob**

</div>

<div>

![Local Image](/tree.png)
**Tree**

</div>

<div>

![Local Image](/commit.png)
**Commit**

</div>

<div>

![Local Image](/tag.png)
**Tag**

</div>

</div>

---

# Object Store (3)

<div grid="~ cols-2" class="justify-items-center text-center items-center mt-10">

<div>

![Local Image](/blob.png)
**Blob**

</div>

<div class="text-left">

```c
struct blob {
	struct object object;
};


```

</div>

</div>

- contraction of "binary large object".
- each version of a file is represented as a blob.
- a blob holds a file's data, but does not contain any metadata, such as file name.

---

# Object Store (4)

<div grid="~ cols-2" class="justify-items-center text-center items-center mt-10">

<div>

![Local Image](/tree.png)
**Tree**

</div>

<div class="text-left">

```c
struct tree {
	struct object object;
	void *buffer;
	unsigned long size;
};
```

</div>

</div>

- represents one level of directory information.
- records blob identifiers, path names, and a bit of metadata for all the files in one directory.
- recursively reference other (sub)tree objects.

---

# Object Store (5)

<div grid="~ cols-2" class="justify-items-center text-center items-center mt-10">

<div>

![Local Image](/commit.png)
**Commit**

</div>

<div class="text-left">

```c
struct commit {
	struct object object;
	timestamp_t date;
	struct commit_list *parents;

	struct tree *maybe_tree;
	unsigned int index;
};
```

</div>

</div>

- holds metadata for each change introduced into the repository, including the author, committer, commit date, and log message.
- points to a tree object that captures, in one complete snapshot, the state of the repository at the time the commit was performed.
- Most commits have one commit parent. The root commit has no parent.

---

# Object Store (6)

<div grid="~ cols-2" class="justify-items-center text-center items-center mt-10">

<div>

![Local Image](/tag.png)
**Tag**

</div>

<div class="text-left">

```c
struct tag {
	struct object object;
	struct object *tagged;
	char *tag;
	timestamp_t date;
};
```

</div>

</div>

- assigns an arbitrary yet presumably human readable name to a specific object, usually a commit.

---

# Object Store (7)

How Git's objects fit and work together to form the complete system?

<div grid="~ cols-2" class="justify-items-center text-center mt-10">

  <div>
    <img src="/1commit.png" class="h-85" />

  **initial commit**
  </div>

  <div>
    <img src="/2commits.png" class="h-85" />
  
  **second commit**
  </div>

</div>

---

# Object Store (8)

<div class="mt-10">

### Storing the complete content of every version of every file is incredibly inefficient. So Git uses a more efficient storage mechanism called a pack file. It only stores the first version of file and deltas.

</div>

<div class="mt-10">

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

---

# Index (1)

<div class="mt-10">

### Linux Torvalds said, "You can’t grasp and fully appreciate the power of Git without first understanding the purpose of the index".

</div>

<div class="mt-10">

- *.git/index*
- index captures a version of the project’s overall structure at some moment in time.
- index doesn’t contain any file content; it simply tracks what you want to commit.

</div>

---

# Index (2)

### Init a empty repository, create two files, create a commit.

<div grid="~ col-1" class="justify-items-center">

<img src="/index1.png" class="h-90 mt-10">

</div>

---

# Index (3)

### edit fil1, append ", modified" to the file

<div grid="~ col-1" class="justify-items-center">

<img src="/index2.png" class="h-90 mt-10">

</div>

---

# Index (4)

### *git add file1*.

<div grid="~ col-1" class="justify-items-center">

<img src="/index3.png" class="h-90 mt-10">

</div>

---

# Index (5)

### *git commit -s -m "modify file1"*.

<div grid="~ col-1" class="justify-items-center">

<img src="/index4.png" class="h-90 mt-10">

</div>