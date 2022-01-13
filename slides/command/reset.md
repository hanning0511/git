# reset

---

The <kdb>git</kdb> reset command changes your repository and working directory to a known state. Specifically, git reset adjusts the **HEAD** ref to a given **commit** and, by default, updates the index to match that commit. If desired, git reset can also modify your working directory to mirror the revision of your project represented by the given commit.

The git reset command has three main options: --soft, --mixed, and --hard.

|     |     |     |     |
| --- | --- | --- | --- |
|Option|HEAD|Index|Working directory|
|<kbd>--soft</kbd>|YES|NO|NO|
|<kbd>--mixed</kbd>|YES|YES|NO|
|<kbd>--hard</kbd>|YES|YES|YES|