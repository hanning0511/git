# Tag

<div grid="~ cols-2 gap-4" class="justify-items-left mt-10">

<div>

![Local Image](/tag.png)

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

<div>

- assigns an arbitrary yet presumably human readable name to a specific object, usually a commit.

</div>

</div>
