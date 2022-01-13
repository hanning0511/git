# diff

- ### There are three basic sources for tree or treelike objects to use with git diff:
    - Any tree object anywhere within the entire commit graph
    - Working directory
    - The index

<br>

- ### Usages

| | |
| --- | --- |
| *git diff* | working directory and index |
| *git diff* <kbd>commit</kbd> | working directory and specific tree |
| *git diff --cached* <kbd>commit</kbd> | index and specific tree |
| *git diff* <kbd>commit1</kbd> <kbd>commit2</kbd> <br/><br/> *git diff* <kbd>commit1</kbd>\.\.<kbd>commit2</kbd> | two trees |
| *git diff* ... <kbd>PATH</kbd> | limit the output to a subset of the repository |
