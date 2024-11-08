---
title : 'Notes on the Blowfish theme'
date : 2024-09-07T16:48:33+10:00
categories: ["hugo", "theme"]
author: "Brian Molinari"
draft : false
weight: 5
---


## Overview

This note outlines how the Blowfish theme works, with an aim to showing how some elements of the theme can be modified.


## Base template mechanism

There is a single `baseof.html` file, in `layouts/_default`.
This includes the declarations
```html
<body>
  {{ partial "partials/header/basic.html" . }}
  <div>
    <main id="main-content" class="grow">
      {{ block "main" . }}{{ end }}
    </main>
    {{- partial "footer.html" . -}}
  </div>
</body>
```
That is, the header and the footer are common to all pages, and are provided by partial templates. The body content of each page is provided by the `block` mechanism. The template for each page kind will thus have the following structure:
```html
{{ define "main" }}
  template code
{{ end }}
```

## Home Page

The content root directory `content` shows that the home page markup is provided by `_index.md`. All layout is provided by the theme, in the directory `themes/blowfish/layouts`. The matching template is `index.html`.


The template `index.html` can be quoted in full:
```html
{{ define "main" }}
  {{ $partial := print "partials/home/" .Site.Params.homepage.layout ".html" }}
  {{ if templates.Exists $partial }}
    {{ partial $partial . }}
  {{ else }}
    {{ partial "partials/home/profile.html" . }}
  {{ end }}
{{ end }}
```
If the parameter `homepage.layout` is defined in the `Hugo` configuration files, then a filename is constructed and this is used as a template.
Otherwise a default template is used.

## Content Style

In the Tailwind mechanism the stying is provided by adding the following classes to the `body` tag.

```html
<body
  class="flex flex-col h-screen px-6 m-auto text-lg leading-7
  max-w-7xl bg-neutral text-neutral-900 dark:bg-neutral-800
  dark:text-neutral sm:px-14 md:px-24 lg:px-32 scrollbar-thin
  scrollbar-track-neutral-200 scrollbar-thumb-neutral-400
  dark:scrollbar-track-neutral-800
  dark:scrollbar-thumb-neutral-600">
```
Some of the relevant tags are:


## CSS and JS Assets

The theme CSS declarations are to be found in `themes/blowfish/assets/css`. The line
```html
	{{- partial "head.html" . -}}
```
in `baseof.html` causes the the various files in this sub-directory to be concatenated (order is significant) and written to a file `public/css/xxx.css`. If there is a user-provided file 
`assets/css/custom.css` then this is included as the last component. Finally, the line
```html
 <link type="text/css" rel="stylesheet" href="/css/xxx.css"
```
is written in the generated html file, to provide the appropriate linkage.

Rather than the entire Tailwind library being included in `xxx.css`, the Tailwind system provides a utility that scans the website `content` and `layout` files to determine the subset of the library that is in fact used. For the theme as supplied, this subset is provided in the file `assets/css/compiled/main.sss`.

The Blowfish [documentation](https://blowfish.page/docs/advanced-customisation/) provides a discussion of what might be included in `custom.css`, and how to regenerate `compiled/main.css` if the use of tailwind classes is modified.

Similarly, the theme JS functions are to be found in the directory `themes/blowfish/assets/js`. The same partial template causes these files to be concatenated and written to a file `public/js/xxx.js`. The line
```html
 <script type="text/javascript" src="/js/xxx.js"
```
is written in the generated html file, to provide the appropriate linkage.

