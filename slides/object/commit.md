# Commit

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