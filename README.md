# daccs-tutorials

This repo is for holding the Jupyter Notebook tutorials from Ouranos PAVICS and other partners.  The Notebooks will then be converted into Jupyter Book format before being put online.

# Requirements

1. birdy kernal
2. Conda or Miniconda: [Miniconda](https://docs.conda.io/en/latest/miniconda.html)

# Create a Conda environment

Create a conda environment using the "birdy.txt" file in the "conda-files" folder

> conda create --name birdyenv --file conda-files/birdy.txt

If a PackageNotFound error is encountered try adding a channel from which to get the packages and run the create environment command again.

> conda config --append channels conda-forge  
> conda create --name birdyenv --file conda-files/birdy.txt

# Activate the environment and install the kernal

> conda activate birdyenv
> python -m ipykernel install --user --name=birdy

# Create a Jupyter Book

Create a Jupyter Book with the following command:

> jupyter-book create mynewbook/

Substitute the name of your book for "mynewbook".

This will create a "_build" folder, "requirements.txt", "_config.yml" and "_toc.yml" files and sample content files such as "markdown.md", "markdown-notebooks.md" and "notebooks.ipynb".

The sample content files can be deleted.



# Add files to the Jupyter Book

Before converting a Jupyter Notebook you need to specify where they are.

The "_toc.yml" file specifies the structure of the book and the table of contents.

Edit the "_toc.yml" file to include the Jupyter Notebook files needed.  Under "chapters" add your files

> - file: filename1
> - file: folder/filename2


# Build the Jupyter Book

Run the command:

> jupyter-book build mybookname/

HTML files will be generated and placed in the "mybookname/_build/html" folder
