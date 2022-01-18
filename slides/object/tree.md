# Tree

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