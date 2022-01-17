# Tag

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