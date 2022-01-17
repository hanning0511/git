# Object

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