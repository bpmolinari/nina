---
title: "Notes on the the Hugo system"
meta_title: ""
description: "this is meta description"
date: 2024-07-08T05:00:00Z
image: "/images/image-placeholder.png"
categories: ["Software"]
author: "Brian Molinari"
tags: ["software", "tailwind"]
draft: false
weight: 3
---

## Overview ##

![hello](img/HAM01.svg "wibble")

The Hugo processor is a stand-alone application written in Go, and is downloaded as an executable. It processes a site specification into a website.

The site specification consists of

- configuration files (in YAML or TOML format)

- Go template files (in augmented HTML format)

- content files (in Markdown format)

The website consists, as we have seen, of HTML, CSS and JS resources. In general terms, the HTML resources are specified by the template and content files. In general terms, the CSS and JS resources (if derived from libraries) are specified by the configuration files.

There are many themes available that provide a simple complete website. This can be customised by the user by modifying text fragments in the configuration and content files, and extended by the provision of additional content files.

In the simplest case, the Hugo system is a black box and the templating is a black art. The naive user can get away without an understanding of either. Until suddenly they can't.

## Syntax of the site specification ##

We will consider the simplest case, that of no theme and no assets such as image files. 

### Configuration ###

The basic configuration file is hugo.toml. Additionally, a directory /config can be used to place files of the format xxx.toml.

### Content ###

The directory ` /content ` contains a hierarchy of subdeictories and Markdown files, in the format `xxx.md`.

### Template ###

Template files (which have the format `xxx.html`) are placed in the directory `/layout`. In general this directory can have sub-directories that match the sub-directories in `/content`, which allows templates to be associated with content files in a sub-directory of the same name. Generally this fine association is not needed, and fallback layout files are placed in the `/layout/_default` directory.

## Syntax of the Website ##

The generated website is placed in the `/public` directory. The internal sub-directory structure matches that of the `/content` sub-directory.

## Hugo Semantics ##

The approach we take to specifying what the Hugo system does is to consider the Hugo abstract machine. That is, we describe the internal data structures that are created and modified during processing, and how this data is processed into into the system output.

The HAM has an object store consisting of

- A hugo object. The method .hugo.version returns the version number of the system. The range of methods is specified here.

- A site object. The method .Site.Title returns the site title (specified by the configuration data). The range of methods is specified here.

- A tree of Page objects. The internal data of a Page object contains the text of a Makdown file. The method .Page.Contents returns the this text, less the front matter, rendered into HTML. The range of methods is specified here.

The behaviour of the HAM involves the following steps.

- The customisation input files are read, and processed into the Site object. This data is accessed during subsequent processing.

- The content files are processed into an equivalent tree structure of Page objects. The front matter is processed into the internal data, to be accessed during subsequent processing.

- The Page tree is now traversed. Each Page object is processed, causing a corresponding HTML file to be written to the website file structure. 

Given a Page object (equivalently, a content file) there is a systematic process of determining a template file (specified here). A Go template has to applied to a context. Here the context is clearly the Page object being processed. The semantics of the templating language now determines what happens. The output can involve

- explicit HTML specified in the template,

- rendered content of the page, given by .Page.Contents, and

- data from the Page object and the Site object (set bu front-matter and configuration processing respectively.

It is important to realise that in processing a Page P, a template is not restricted to P alone. Methods on P allow other page objects to be referenced (and their content to be selectively mined). All pages in the tree could be automatically built into a home-page menu, for example.

The traversal order of the Page tree is not specified, and no particular order can be relied on.
