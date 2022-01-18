# Tree

<div grid="~ cols-2 gap-4" class="justify-items-left mt-10">

<div>

![Local Image](/tree.png)

<br/>
<br/>

<div>

```c
struct tree {
	struct object object;
	void *buffer;
	unsigned long size;
};
```

</div>

</div>

<div class="text-2xl">

- represents one level of directory information.
- records blob identifiers, path names, and a bit of metadata for all the files in one directory.
- recursively reference other (sub)tree objects.

</div>

</div>