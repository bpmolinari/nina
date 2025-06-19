---
title: "Site documentation"
date : 2024-07-25T15:04:26+10:00
draft: false
weight: 7

---

## Site Documentation ##

### Content architecture ###

specify sections

### Style ###

specify configuration

### Home Page ###

In this description, all filenames are relative to the `content` directory.

The direct content is provided by the `_index.md` file.

The direct templates are provided by

- the `layouts/_index.html` file, and

- the `layouts/_default/baseof.html`files

The output is the `index.html` file in the `public` directory.

### Docs directory ###

This is a classic section (leaf bundle). The directory contains a `_index.md` file and a number of `xxx.md` files, each providing the markup for a particular topic.

The `_index.md` file is used to generate the `public/docs/index.html` file. The templates `layouts/_default/list.html` and `baseof.html` are used.

Each topic file `xxx.md` is processed into an `xxx` subdirectory, which contains an `index.html` file. That is generated from the content file `xxx.hlml` and the template file `layouts/_default/single.html` (as well as the `baseof.html` file.

### Family directory ###

This is a full section, and has the complexity of a website in its own right.

The page content is provided by `_index.html`

There are page bundles provided by a number of directories, each corresponding to a ancestor family.

Finally there is a resources directory `guides`, which details a number of aspects of collecting  this information. Again, it is structured as an intellectual journey from naivety through to reasonable competence. What I would have liked to have read.


### menu Notes

[nested notes](https://hugocodex.org/blog/creating-a-menu-with-nested-pages/)

[menu notes](https://harrycresswell.com/writing/menus-in-hugo/)
