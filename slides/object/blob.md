# Blob

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