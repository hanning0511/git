---
theme: default
background: https://source.unsplash.com/collection/94734566/1920x1080
class: 'text-center'
highlighter: shiki
lineNumbers: false
info: |
  ## Re-Introduce to Git
drawings:
  persist: false

---

# **Re**-Introduce to Git

### Han Ning

---

# Birth of Git (1)

<v-clicks>

- Before the birth of Git, the Linux kernel was developed using the commercial BitKeeper[1] VCS
- The company that owned BitKeeper placed additional restrictions on its “free as in beer” version in the spring of 2005, the Linux community realized that BitKeeper was no longer a viable solution
- Torvalds looked for alternatives. Failed. He set out to write his own, the Git
- Key events of Git
  - Development began on **3 April 2005**
  - Torvalds announced the project on **6 April 2005**
  - Git became self-hosted on **7 April 2005**
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

# Basic Concepts - Repository

- ### Repository

  - A complete working copy of all the files.
  - A copy of the repository itself.
    - configurations
    - **object store**
    - **index**
    - ...

```shell
# ls .git        
branches  COMMIT_EDITMSG  config  description  HEAD  hooks  index  info  logs  objects  refs
```

---

# Basic Concepts / object store

Git places only four types of objects in object store. These four atomic objects form the foundation of Git’s higher level data structures.
The object store locates at **.git/objects**

<div grid="~ cols-2 gap-2" m="-t-2" class="justify-items-center text-center">

<v-click>

![Local Image](/blob.png)
**Blob**

</v-click>

<v-click>

![Local Image](/tree.png)
**Tree**

</v-click>

<v-click>

![Local Image](/commit.png)
**Commit**

</v-click>

<v-click>

![Local Image](/tag.png)
**Tag**

</v-click>

</div>

---

# Basic Concepts / Object Store / Blob

<div grid="~ cols-2" class="justify-items-center text-center">

<div>

![Local Image](/blob.png)
**Blob**

</div>

<div class="text-left">

```c {1-3|5-10|12-15}
struct blob {
	struct object object;
};

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

- contraction of "binary large object".
- each version of a file is represented as a blob.
- a blob holds a file's data, but does not contain any metadata, such as file name.

---

# Basic Concepts / Object Store / Tree

<div grid="~ cols-2" class="justify-items-center text-center">

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

# Basic Concepts / Object Store / Commit

<div grid="~ cols-2" class="justify-items-center text-center">

<div>

![Local Image](/commit.png)
**Commit**

</div>

<div class="text-left">

```c{1-8|10-13}
struct commit {
	struct object object;
	timestamp_t date;
	struct commit_list *parents;

	struct tree *maybe_tree;
	unsigned int index;
};

struct commit_list {
	struct commit *item;
	struct commit_list *next;
};
```

</div>

</div>

- holds metadata for each change introduced into the repository, including the author, committer, commit date, and log message.
- points to a tree object that captures, in one complete snapshot, the state of the repository at the time the commit was performed.
- Most commits have one commit parent. The root commit has no parent.

---

# Basic Concepts / Object Store / Tag

<div grid="~ cols-2" class="justify-items-center text-center">

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

# Basic Concepts / Object Store

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