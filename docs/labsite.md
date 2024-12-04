# parisodlab.github.io

[TOC]

## Getting Started

The Parisod Lab website was built using [jekyll](https://jekyllrb.com/) and runs using the [Github Pages](https://pages.github.com/) service.

#### Software-Dependencies

Several software packages are required for editing/maintaining the Parisod Lab site. They can be installed using [Homebrew](https://brew.sh):

```
# For first time user, run these two commands in your terminal to add Homebrew to your PATH:
    (echo; echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"') >> $HOME/.bashrc
    eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
# Next follow the instructions below to install the required software packages.
brew install ruby imagemagick exiftool python ghostscript
brew upgrade ruby # If Ruby has not been updated in a while, you may need to do this.
sudo gem install jekyll -v 3.6.0
# If you get an error when trying to run pip, try:
# brew link --overwrite python
pip install metapub pyyaml
```

* __Ruby__ - Is used to run jekyll, which is the software that builds the site.
* __Jekyll__ - As stated earlier, jekyll builds the static site and is written in Ruby.
* __Imagemagick__ - Handles thumbnail generation and scaling photos. Imagemagick is used in the `build.sh` script.
* __exiftool__ Extract data about photos as part of the `build.sh` script for use in scaling images.
* __Python__ Retrieves information about publications and updates `_data/pubs_data.yaml`.

#### Cloning the repo

To get started editing, clone the repo:

```
git clone https://github.com/parisodlab/parisodlab.github.io
```

This repo contains documents that get compiled into the Parisod Lab website. When you make changes to this repo and push them to GitHub, Github will trigger a 'build' of the labsite and update it. This usually takes less than a minute. Instructions for changing various aspects of the site are listed below.

You can also use [Github Desktop](https://desktop.github.com) to manage changes to the site. 

If you want to edit the site locally and preview changes, run the following in the __root__ directory of the git repo:

```
jekyll serve
```

The site should become available at `localhost:4000` and any changes you make will be reflected at that local url.

#### Updating the site

In order for any change to become visible, you need to use git. Any subsequent directions that suggest modifying, adding, or removing files assumes you will be __committing__ these changes to the repo and __pushing__ the commit to GitHub.com. See [Git-SCM](http://www.git-scm.com) for a basic introduction to git.


## Parisodlab.github.io

The structure of the Parisod Lab repo looks like this:

```
CNAME
LICENSE
README.md
build.sh
index.html
_config.yml
_data/
_includes/
_layouts/
_posts/
_site/
assets/
feeds/
files/
pages/
people/
publications/
scripts/
protocols/
funding/
```

The folders prefixed with


## Announcements

Announcements are stored in the `_posts` folder. Posts are organized into folders by year. There is also a `_photo_albums` folder that you can ignore (more on this below). Two types of announcements can be made. A 'general' announcement regarding anything, or a new publication.

#### General Announcements

To add a new post create a new text file with the following naming scheme:

```
YYYY-MM-DD-title.md
```

For example:

```
2017-09-24-A new post.md
```

The contents of the file should correspond to the following structure:

```
---
title: "The title of the post"
layout: post
tags: news
published: true
---

The post content goes here!
```

The top part surrounded by `---` is known as the __header__ and has to define a number of variables:

`layout: post`, `tags: news`, and `published: true` should always be set and should not change. The only thing you will change is the `title`. Set a title, and add content below.

Because we used a `*.md` extension when naming the file, we can use markdown in the post to create headings, links, images, and more.

### Publication Post

New publication posts can be created. These posts embed a publication summary identical to what you see on the publication page. They follow the same paradigm as above except they require two additional lines in the header:

* `subtitle:` - Usually the title of the paper; Appears on homepage.
* `PMID:` - The pubmed identifier

__Example__:

```
---
title: "Sandra's paper accepted at <em>G3</em>!"
subtitle: "Ice age-driven range shifts of diploids and expanding autotetraploids of <em>Biscutella laevigata</em> within a conserved niche."
layout: post
tags: news
published: true
PMID: 39253771
---

Congratulations to Sandra for her paper accepted at G3!
```

## Lab members

### Adding new lab members:

* __(1)__ - Add a photo of the individual to the `people/` folder.
* __(2)__ - Edit the `_data/people.yaml` file, and add the information about that individual.

Each individual should have - at a minimum, the following:

```
- first_name: <first name>
  last_name: <last name>
  title:  <The job title of the individual; e.g. Graduate Student; Research Associate; Undergrad; Postdoctoral Researcher; Lab technician>
  photo: <filename of the photo located in the people/ directory>
```

Additional fields can also be added:

```
- first_name: <first name>
  last_name: <last name>
  title: <The job title of the individual; e.g. Graduate Student; Research Associate; Undergrad; Postdoctoral Researcher; Lab technician>
  pub_names: ["<an array>", "<of possible>", "<publication>", "<names>"]
  photo: <base filename of the photo located in the people/ directory; e.g. 'dan.jpg'>
  website: <website>
  description: <a description of research>
  email: <email>
  github: <github username>
```

!!! Note
    `pub_names` is a list of possible ways an individual is referenced in the author list of a publication. This creates links from the publications page back to lab members on the people page.

### Set Status to Former

Lab members can be moved to the bottom of the people page under the 'former member' area. To do this add a `former: true` line for that individual and a `current_status:` line indicating what they are up to.

For example:

```
- first_name: Manuel
  pub_names: 
    - Poretti M
  last_name: Poretti
  description: My research broadly spans... I am currently working to uncover... and to develop ....
  title: Postdoctoral Researcher, 2021-2024
  photo: manuel.jpg
  former: true
  github: mporetti
  email: manuel.poretti@unifr.ch
  current_status: Postdoc at University of Melbourne -- <a href='https://ch.linkedin.com/in/manuelporetti'>Manuel's Linkedin Profile</a>
```

### Remove lab members

Remove the persons information from `_data/people.yaml`; Optionally delete their photo.

## Funding

Funding is managed using the `funding/` folder in the root directory and the data file `_data/funding_links.yaml`. The `funding/` folder has two subfolders: `past/` and `current/` for past funding and current funding. Rename the logo file to be lowercase and simple.

To update funding simply place the logo of the institution providing funding in one of these folders and it will appear on the funding page under the heading corresponding to the subfolder in which it was placed. If you would like to add a link for the funding of that organization you can edit the `_data/funding_links.yaml` file.

This file is structured as a set of `basename: url` pairs:

```
veluxstiftung: https://veluxstiftung.ch
snf: http://www.snf.ch/en/Pages/default.aspx
```

Each acronym above corresponds with an image file in the `current/` or `past/` folder. Notice that the extension (e.g. jpeg/png, etc) does not matter. Just use the basename of the file and its associated link here.

## Protocols

Protocols are stored in the `protocols/` folder and their titles and pdfs are managed in `_data/protocols.yaml`. To add a new protocol, add the PDF to the `protocols/` folder. Then add these lines to the `_data/protocols.yaml` file:

```
- Name: Title of Protocol
  file: filename_of_protocol_in_protocols_folder.pdf
  group: <em>Biscutella</em> Phenotyping methods
```

* `name` - The name of the protocol
* `file` - The filename of the protocol within the `protocols/` folder.
* `group` - The grouping of the protocol; It will be nested under this grouping on the protocols page.

```
- name: Semi-Quantitative Biomass Assay
  file: SemiQuantitativeBiomassAssay.pdf
  group: <em>Biscutella</em> Phenotyping Methods
- name: Crab Spider Culture</a>
  file: CrabSpiderCultureprotocol.pdf
  group: <em>Biscutella</em> Phenotyping Methods
```

To remove a protocol, delete the pdf and remove the corresponding lines.

## Research

The research portion of the site is structured as a set of sections - each devoted to a project/area. Navigate to `/pages/research` and you will see a set of files:

* `research.html` - This page controls the content at the top of the research page. It's an overview of research in the Parisod lab. You can edit the top portion between the `<p>[content]</p>` tags freely to modify the top of the research page.
* `research-*.md` - These are the individual projects. These files look like this:

```
---
title: Description of the project
image: project_image.jpg
order: 1
---

Research content goes here.
```

The page includes a header (the items located between `---`) which includes a number of important items.

* `title` - the title to display for the research area.
* `image` - An image for that research area/project. This is the base name of the image placed in `/assets/img/research/`
* `order` - A number indicating the order you would like the page ot appear in. Order is descending and any set of numbers can be used to determine sort order (e.g. 1, 2, 5, 8, 1000). 

## Publications

Elements used to construct the publications page of the website are stored in two places:

1. `_data/pubs_data.yaml` - The publications data stores authors, pub date, journal, etc.
2. `publications/` - The publications folder for PDFs, thumbnails, and supplementary files.

__(1) Download a PDF of the publication__

To download automatically, you would need  to installhttps://github.com/billgreenwald/Pubmed-Batch-Download.git

Then you can run the script with:
python pubmed_batch_download.py -pmf publications/publications_list.txt -out publications/
This will download the PDFs to the `publications/` folder.

You will want to remove any additional PDF pages (e.g. cover sheets) if there are any present in the PDF. See [this guide](https://support.apple.com/kb/PH20221?locale=en_US&viewlocale=en_US) for information on removing pages from a PDF.

Save the PDF to `/publications/[year][tag]`

Where `tag` is a unique identifier for the publication. In general, these have been the first author or the journal or a combination of both.

__(Optional) PMID Known__

If the PubMed Identifier (PMID) is known for the publication, you can add it to the file `publications/publications_list.txt`.

__(2) Run `build.sh`__

The `build.sh` script does a variety of tasks for the website. For publications - it will generate thumbnails. It will also fetch information for publications and add it to the `_data/pubs_data.yaml` file __if__ a PMID has been provided. If you did not add a PMID, you will have to manually add authors, journal, etc. to the `_data/pubs_data.yaml` file.

__(3) Edit `_data/pubs_data.yaml`__

The publication should now be added either manually or automatically to `_data/pubs_data.yaml` and should look something like this:

```
- Authors:
  - "Gr\xFCnig S"
  - Patsiou T
  - Parisod C
  DOI: 10.1111/nph.20103
  Journal: New Phytol
  PMC: null
  PMID: '39253771'
  Title: Ice age-driven range shifts of diploids and expanding autotetraploids of
    Biscutella laevigata within a conserved niche

```

You will need to add a few things:
  - Add a `PDF:` line to associate the publication with the correct PDF and its thumbnail. This is the same `tag` you used above.
  - If there is no `Date_Published:` line you will want to add that. The format is `YYYY-month_abbr-DD` (e.g. `2017 Aug 17`).
  - Add `<em>` tags around items you want to italicize: `<em>Biscutella laevigata</em>`

Final result:

```
- Authors:
  - "Gr\xFCnig S"
  - Patsiou T
  - Parisod C
  DOI: 10.1111/nph.20103
  Date_Published: 2024 September 16
  Journal: New Phytol
  PMC: null
  PMID: '39253771'
  Title: Ice age-driven range shifts of diploids and expanding autotetraploids of
    <em>Biscutella laevigata</em> within a conserved niche
  PDF: 2024BiscutellaNewPhytol.pdf
```

__(4) Add supplementary data__

Supplemental data and figures are stored in `publications/[pdf_name]`. For example, `2024BiscutellaNewPhytol` has an associated folder in `publications/` where supplemental data and figures are stored: `publications/2024BiscutellaNewPhytol/<supplemental files>`

Once you have added supplemental files, you'll need to add some information to `_data/pubs_data.yaml` to describe them. These are the lines that were added for `2024BiscutellaNewPhytol`:

```
  pub_data:
    files:
      Supplemental_Figures.pdf: {title: Supplemental Figures}
      Supplemental_Files.zip: {title: Supplemental Files}
      Supplemental_Tables.zip: {title: Supplemental Tables}\
      ...
      <name of file>: {title: <title to display>}
```

The last line above illustrates the format. The name of the file must match exactly what is in the `publications/[pdf_name]` folder. Resulting supplemental data will be listed under publications and on the data page.

## Photo Albums

Photo albums can be added to the Parisod Labsite. Adding albums requires two utilities to be installed on your computer:

* (a) Image Magick
* (b) exiftool

These can easily be installed with [homebrew](https://brew.sh/). should have been installed during Setup (above), but if not you can install them using the following:

```
brew install imagemagick
brew install exiftool
```

__(1) Place images in a folder and name it according to the following schema:__

`YYYY-MM-DD-title`

For example, `2024-06-05-Manuel-Farewell`.

__(2) Move that folder to `/people/albums/`__

__(3) Run the `build.sh` script in the root of the `Parisodlab.github.io` repo.__

The `build.sh` script will do the following:

* (a) Construct pages for the album being published.
* (b) Decrease the size of the images in the album (max width=1200). 

!!! Note

    The `build.sh` script also performs other maintenance-related tasks. It is fine to run this script at anytime.

You can run the script using:

```
bash build.sh
```

__(4) Add the images using git and push to GitHub__

You can easily add all images using:

```
git add *.jpg
```

__(5) Push changes to github__

```
git push
```

## Software

If you can write software you should be able to figure out how to update this section. It's markdown/html and not overly complicated.

