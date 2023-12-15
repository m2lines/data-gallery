[![pre-commit.ci status](https://results.pre-commit.ci/badge/github/m2lines/data-gallery/main.svg)](https://results.pre-commit.ci/latest/github/m2lines/data-gallery/main)

# data-gallery

## Installation
```
git clone git@github.com:m2lines/data-gallery.git
cd data-gallery
conda env create -f environment.yml
```

### To update the existing environment
> :warning: Manually add any new packages to the `environment.yml` either as pip or conda dependencies. Using the default conda environment export causes sub-dependencies to be listed which slows down the `conda-lock` generation process.

To speed up the continuous integration, we also generated a [conda lock](https://conda.github.io/conda-lock/) file for linux as follows.
```
conda-lock lock --mamba -f environment.yml -p linux-64 --kind explicit
```
This file lives in `conda-linux-64.lock` and should be regenerated whenever the `environment.yml` is updated.

## Building the book
To build the book locally, you should first create and activate your environment, as described above. Then run
```
jupyter book build .
```
When you run this command, the notebooks will be executed. The built html will be placed in '_build/html`. To preview the book, run
```
cd _build/html
python -m http.server
```
The build process can take a long time, so we have configured the setup to use [jupyter-cache](https://jupyter-cache.readthedocs.io/en/latest/). If you re-run the build command, it will only re-execute notebooks that have been changed. The cache files live in `_build/.jupyter_cache`.

To check the status of the cache, run

```bash
$ jcache cache list -p _build/.jupyter_cache
```

To remove cached notebooks, run

```bash
$ jcache cache remove -p _build/.jupyter_cache
```

## Contributing

### Pre-commit

We use [pre-commit](https://pre-commit.com/) to keep the notebooks clean.
In order to use pre-commit, run the following command in the repo top-level directory:

```bash
$ pre-commit install
```

At this point, pre-commit will automatically be run every time you make a commit.

### Pull Requests and Feature Branches

In order to contribute a PR, you should start from a new feature branch.

```bash
$ git checkout -b my_new_feature
```

(Replace `my_new_feature` with a descriptive name of the feature you're working on.)

Make your changes and then make a new commit:

```bash
$ git add changed_file_1.ipynb changed_file_2.ipynb
$ git commit -m "message about my new feature"
```

You can also automatically commit changes to existing files as:

```bash
$ git commit -am "message about my new feature"
```

Then push your changes to your remote on GitHub (usually call `origin`

```bash
$ git push origin my_new_feature
```

Then navigate to https://github.com/m2lines/data-gallery to open your pull request.

### Synchronizing from upstream

To synchronize your local branch with upstream changes, first make sure you have the upstream remote configured.
To check your remotes, run

```bash
$ git remote -v
origin	git@github.com:rabernat/data-gallery.git (fetch)
origin	git@github.com:rabernat/data-gallery.git (push)
upstream	git@github.com:m2lines/data-gallery.git (fetch)
upstream	git@github.com:m2lines/data-gallery.git (push)
```

If you don't have `upstream`, you need to add it as follows

```bash
$ git remote add upstream git@github.com:m2lines/data-gallery.git
```

Then, make sure you are on the main branch locally:

```bash
$ git checkout main
```

And then run

```bash
$ git fetch upstream
$ git merge upstream/main
```

Ideally you will not have any merge conflicts.
You are now ready to make a new feature branch.

## References
