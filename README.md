# [Parisod Lab Dry Guide](http://parisodlab.org/dry-guide/)

The Parisod lab [dry-lab computing guide](http://parisodlab.org/dry-guide/). The guide is built with [mkdocs](http://www.mkdocs.org/).

## Editing the site

1. Clone the repo

```
git clone https://github.com/ParisodLab/dry-guide.git
```

2. Install `mkdocs` and `mike=0.4.2`, with conda and pip

```
conda activate dry-guide

```

3. When edits are complete, use `cd ../parisodlab.github.io/; mkdocs gh-deploy --config-file ../dry-guide/mkdocs.yml --remote-branch master`.

If you are making minor changes, use the same version:

```bash
mike deploy [current date version] latest --update-aliases --ignore --push
```

The word `latest` here is an alias which will ensure that the new version is served.


If you have made substantial changes to the site, like adding new sections or removing or rewriting sections, create a new version with the current date.

```bash
mike deploy [today's date] latest --update-aliases --ignore --push
```