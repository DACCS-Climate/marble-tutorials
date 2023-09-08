# Marble Tutorials

Tutorials for the Marble Software stack organized as a [jupyter book](https://jupyterbook.org).

## Build the book

To convert the files contained in the `tutorials/` directory to HTML:

1. install the requirements:

```shell
python3 -m pip install -r tutorials/requirements.txt
```

2. build the HTML files:

```shell
jupyter-book build tutorials/
```

This will create a `tutorials/_build` directory. The tutorials jupyter book can now be viewed by opening the 
`tutorials/_build/html/index.html` file.

## Contributing

To contribute to this project, please create a new branch off of the `main` branch, make your changes there and then 
create a pull request to merge your branch back into `main`.

If you do not have sufficient permissions to create a new branch in this repository, please fork this repository first.

### Updating Tutorials

When creating or updating jupyter notebook formatted tutorials, please commit a version of the notebook that includes 
the output cells. The [build procedure](#build-the-book) does not execute the notebooks by default and so only the cells
that are already visible in the notebooks will be shown.

When creating, deleting, or renaming tutorial files, make sure that you have also updated the relevant entries in the 
table-of-contents file that can be found at [`tutorials/_toc.yml`](tutorials/_toc.yml).
