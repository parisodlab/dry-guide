---
runme:
  id: 01JN61R4BVS38SRW3EXS44G0BX
  version: v3
---

# [Parisod Lab Dry Guide](https://parisodlab.github.io/dry-guide/latest/)

The Parisod lab [dry-lab computing guide](https://parisodlab.github.io/dry-guide/latest/). The guide is built with [mkdocs](http://www.mkdocs.org/).

## Editing the site

1. Clone the repo

```sh {"id":"01JN61R4BVS38SRW3EXE73R62A"}
git clone https://github.com/ParisodLab/dry-guide.git
```

2. Install `mkdocs` and `mike=0.4.2`, with conda and pip (both)

```sh {"id":"01JN61R4BVS38SRW3EXGNP9D8A"}
conda activate dry-guide

```

3. When edits are complete, use `mike deploy [current date version] latest --update-aliases --ignore --push`.
   e.g. `mike deploy 2024-07-25 latest --update-aliases --ignore --push`

If you are making minor changes, use the same version:

```bash {"id":"01JN61R4BVS38SRW3EXHX79SKZ"}
mike deploy [current date version] latest --update-aliases --ignore --push
```

The word `latest` here is an alias which will ensure that the new version is served.

If you have made substantial changes to the site, like adding new sections or removing or rewriting sections, create a new version with the current date.

Get today's date with `date +%Y-%m-%d`.

```bash {"id":"01JN61SBMWNGADK7AKSFTRSYPP","interactive":"true"}
conda activate dry-guide
TODAY=$(date +%Y-%m-%d)
echo $TODAY
mike deploy $TODAY latest --update-aliases --ignore --push
```

If errors occur, try to reload vscode (shift-control-P to open the Command Palette then find Developer: Reload Window and press Enter).