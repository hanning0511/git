# Blob

<div grid="~ cols-2 gap-4" class="justify-items-left mt-10">

<div>

![Local Image](/blob.png)

<br/>
<br/>

<div>

```c
struct blob {
	struct object object;
};
```

</div>

</div>

<div class="text-2xl">

- contraction of "binary large object".
- each version of a file is represented as a blob.
- a blob holds a file's data, but does not contain any metadata, such as file name.

</div>

</div>

