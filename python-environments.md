# Getting Python On Your Machine: Mamba :snake:!

---

## Overview

Mamba is an open-source, cross-platform, language-agnostic package manager and environment management system that allows you to quickly install, run, and update packages within your work environment(s).

Here we will cover:

1.  What are packages?
2.  Installing Mamba
3.  Creating a Mamba environment
4.  Useful Mamba commands

### Prerequisites

| Concepts                                                                                                  | Importance | Notes |
| --------------------------------------------------------------------------------------------------------- | ---------- | ----- |
| [Installing and Running Python](https://foundations.projectpythia.org/foundations/how-to-run-python.html) | Helpful    |       |

- **Time to learn**: 20 minutes


### Conda vs. Mamba

For the Cook-off we're recommending something a bit different than the [installation instructions in Pythia Foundations](https://foundations.projectpythia.org/foundations/how-to-run-python.html#installing-and-managing-python-with-conda)

You may have already used [conda](https://foundations.projectpythia.org/foundations/conda.html) to install Python and other packages on your machine. Maybe you've also gotten frustrated by extremely slow installations! [mamba](https://mamba.readthedocs.io/en/latest/) is basically a drop-in replacement for conda that is much faster!

Short story: follow these instructions to install mamba and use mamba for your Python package management, and you'll be happier!

### What are Packages?

A Python package is a collection of modules, which, in turn, are essentially Python scripts that contain published functionality. There are Python packages for data input, data analysis, data visualization, etc. Each package offers a unique toolset and may have its own unique syntax rules.

Package management is useful because you may want to update a package for one of your projects, but keep it at the same version in other projects to ensure that they continue to run as expected.

## Installing Mamba

We recommend you install mambaforge. You can do that by following the [mambaforge documentation](https://mamba.readthedocs.io/en/latest/installation.html).

You will need to download and install packages from their Github repository, selecting the installation suitable for your machine (ex. Macbook Pro with an M1 processor)
- [Link to downloads](https://github.com/conda-forge/miniforge#mambaforge)

Mambaforge only comes with the `mamba` package management system; it is a pared-down version of the full Anaconda Python distribution.

We recommend mambaforge for three reasons:

1. It's much faster than conda.
2. Takes up much less disk space than a full Anacaonda Python installation.
3. It encourages you to install only the packages you need in reproducible isolated environments for specific projects. This is generally a more robust way to work with open source tools.

Once you have `mamba` via the mambaforge installer, the next step is to create an environment and install packages.

## Creating and Managing Python Environments with Mamba

A *mamba* environment is an interoperable collection of specific versions of packages or libraries that you install and use for a specific workflow. Mamba's package manager takes care of dependencies so everything works together in a predictable way. One huge advantage of using environments is that any changes you make to one environment will not affect your other environments at all, so you are much less likely to "break" something!

### Creating a Python Environment 

To create a new mamba environment, type `mamba create --name` and the name of your environment in your terminal, and then specify any packages that you would like to have installed. For example, to install a Jupyter-ready environment called `sample_environment`, type

```
mamba create --name sample_environment python jupyterlab
```

The above invocation will install the *python* and *jupyterlab* packages and their dependencies into your *sample_environment*
.
Once that environment is created, you will be prompted to _activate_ it in your current terminal session:

```
mamba activate sample_environment
```

It is a good idea to create new environments for different projects because since Python is open source, new versions of the tools are released very frequently. Isolated environments help guarantee that your script will use the same versions of packages and libraries and should run the same as you expect it to. Similarly, it is best practice to NOT modify your `base` environment.

### Create a Python environment from an environment file

Many projects have lengthy lists of packages. Rather than listing each package individually in a `mamba create` command, it's common practice to list packages in a text file usually called `environment.yml`. For example, each Cookbook repository contains an `environment.yml` file at the root of the repository.

We recommend having a separate named environment for each Cookbook you are working on, and managing these through environment files. The *name* of the environment is usually specified in the `environment.yml` file as well.

To create and activate environment named `my-cookbook-env` (for example) from an `environment.yml` file, do the following:
```
mamba env create -f environment.yml
mamba activate my-cookbook-env
```

### Modifying Your Environment
When you are working with cookbooks, it is recommended that when you install new packages, you add those packages to your `environment.yml` file.

#### Adding New Packages to Your Environment

Here is a sample of what this `environment.yml` file looks like:
```yaml=
name: cookbook-dev
channels:
  - conda-forge
dependencies:
  - jupyter-book
  - jupyterlab
```

If you wanted to add another package, for example, `xarray`, which is useful when working with weather and climate datasets, your new file would look like the following:
```yaml=
name: cookbook-dev
channels:
  - conda-forge
dependencies:
  - jupyter-book
  - jupyterlab
  - xarray
```

You would update your environment using the `mamba env update` command, specifying the `environment.yml` file as the place to check to see if there are new packages to install!

```
mamba env update -f environment.yml
```

#### Creating a New Environment
You can also rename your environment using the `environment.yml` file. This is helpful when creating your own cookbook! For example, let's create a new environment `my-cookbook-dev`.

```yaml=
name: my-cookbook-dev
channels:
  - conda-forge
dependencies:
  - jupyter-book
  - jupyterlab
  - xarray
```

Following the steps outlined in the previous section, we would run

```
mamba env create -f environment.yml
mamba activate my-cookbook-dev
```



## Useful Mamba commands

Here are some commands that you will typically use:

- Activating a specific environment

```
mamba activate sample_environment
```

- Deactivating the current environment

```
mamba deactivate
```
Deactivating an environment will switch you back to your original, or *base* environment.

- Checking what packages/versions are installed in the current environment

```
mamba list
```

- Check if a particular package is available for install:

```
mamba repoquery search somepackage
```

- Installing a new package into the current environment

```
mamba install somepackage
```

- Installing a specific version of a package into the current environment

```
mamba install somepackage=0.17
```

- Updating all packages in the current environment to the latest versions

```
mamba update --all
```

- Checking what conda environments you have

```
mamba env list
```

- Deleting an environment

```
mamba env remove --name sample_environment
```

Remember, *mamba* is a variant of *conda*. While it is not a one-to-one replacement for *conda*, its usage is very similar, We therefore recommend you refer to [Conda's documentation](https://docs.conda.io/en/latest/) or this handy [Conda cheat sheet](https://docs.conda.io/projects/conda/en/latest/_downloads/843d9e0198f2a193a3484886fa28163c/conda-cheatsheet.pdf).


---

## Summary

Mamba is an optimized package and environment management system, based on conda, that allows you to quickly install, run, and update packages within your work environment(s). This is important for gathering all of the tools necessary for your workflow. Use the command line to manage your Python environments using Mamba.

### What's Next?

- [How to Run Python in the Terminal](terminal.md)
- [How to Run Python in a Jupyter Session](jupyter.md)

## Resources and References

- [Linux commands](https://cheatography.com/davechild/cheat-sheets/linux-command-line/)
- [Mamba](https://mamba.readthedocs.io/en/latest/index.html)
- [Mamba Concepts](https://mamba.readthedocs.io/en/latest/user_guide/concepts.html)
- [Mamba Troubleshooting](https://mamba.readthedocs.io/en/latest/user_guide/troubleshooting.html)
- [Conda documentation](https://docs.conda.io/en/latest/)
- [Conda cheat sheet](https://docs.conda.io/projects/conda/en/latest/_downloads/843d9e0198f2a193a3484886fa28163c/conda-cheatsheet.pdf)



