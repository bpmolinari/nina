---
title: "My journey with Web technology"
meta_title: ""
description: "this is meta description"
date: 2022-07-02T05:00:00Z
image: "/images/image-placeholder.png"
categories: ["Architecture"]
author: "Brian Molinari"
tags: ["silicon", "technology"]
draft: false
weight: 1
---

## Introduction ##

This records the resources that I discovered and used in getting a website constructed and deployed. The project was motivated by acquiring an nice domain name.

My starting point was that I was computer literate. I have experience in running a home Ubuntu environment. I have a strong preference for the markup Latex ecosystem, rather than the WYSIWYG Microsoft Word ecosystem. I have written moderate size programs (in a teaching environment) in a range a languages (including FORTRAN, Simula-67, Pascal, Modula, Miranda, Perl, Python).
  
I realised I had NOT maintained or developed any websites. I was familiar with the words (HTML, CSS, and so on) but had not worked with them.

## At The Browser

  A web-page, downloaded from a server, is a collection of text files consisting of
- HTML (Hypertext Markup Language) resources (content in a markup format)
- CSS (Cascading Style Sheets) resources (specifying layout attributes of the content)
- JS (JavaScript) programs 

The browser parses the HTML resources and constructs anDOM tree (Document Object Model). The tree is then rendered to the browser window, according to the CSS resources. The JS resources can access and modify any of the objects in the DOM tree, thus modifying the displayed page.

A convenient resource (among many) is the [World Wide Web Schools](https://www.w3schools.com) site. This provides both tutorial as well as reference documentation. Mozilla also provides a [starting point](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web) for complete beginners.

A modern browser is a complex software system. The code-base for Firefox is [21 million lines](https://hacks.mozilla.org/2020/04/code-quality-tools-at-mozilla/). The [Firefox Developer Tools](https://firefox-source-docs.mozilla.org/devtools-user/) provide a detailed debug interface into the working browser.

## CSS and JavaScript Resources ##

In principle a complete website can be written ab initio and placed on the server. In practice a great deal of the CSS and JavaScript resources for a website can be obtained from libraries. Typically all the resources needed for a website are collected in one place. The collection is often referred to (rather imprecisely) as a framework.

CSS frameworks include the following:

- [W3.CSS](https://www.w3schools.com/w3css/default.asp)
- [Tailwind](https://tailwindcss.com/)

JavaScript frameworks include the following
- [W3.JS](https://www.w3schools.com/w3js/default.asp)

Combined frameworks include the following
- [Bootstrap]( https://www.w3schools.com/bootstrap5/index.php)

## Simple Websites ##

Given a CSS framework and a JavaScript framework it is a short step to provide a complete website for a simple use-case. Such a website is often referred to (somewhat imprecisely) as a theme or a template.

A theme can be downloaded as a collection of resources. It can naively customised by searching the HTML resources for text strings that are evident in the web-page, and changing them to new values. The user then has a rather fragile website, to their requirements.

The World Wide Web School environment provides some templates [here](
https://www.w3schools.com/w3css/w3css_templates.asp).
The Bootstrap environment provides some themes [here](https://themes.getbootstrap.com/). There is a substantial ecosystem to support customisation and maintenance. These themes are typically premium. 

## At The Server: LAMP and WordPress ##

The [Wikipedia article](https://en.wikipedia.org/wiki/LAMP_(software_bundle)) is as good a starting place as any.

A raw web-site can simply use the first two layers of the stack, namely, Linux and Apache. The LAMP approach adopts content management using a database (MySQL) and a scripting language (originally PHP) to extract the content from the database and to then construct the web-site resources. The web-site construction can of course utilise CSS and JavaScript library resources as just discussed above.

To accommodate the situation where the content is dynamic, the web-site resources are generated anew for each user visit.

The generation of the web-site resources from the content can be automated by a web-site generator system, the dominant example being [WordPress](https://wordpress.org/). A complete starter web-site can be obtained by loading a theme (there are thousands of free and premium themes available). The designer is provided with an interface where content can be created and maintained using a WYSIWYG editor. The publisher sees the content as it will appear in the browser window. The content is maintained in a MySQL database. In the best case the entire HTML/CSS/JavaScript world is hidden from the designer.

## At The Server: JAM and Hugo ##

JAMstack is a software pattern for web-site development and architecture. In brief:

- There is no server-side processing. The client simply provides static web-site resources generated from content in Markup form (together with CSS and JS resources primarily from libraries)

- Client-side interactions (such as form submission) are directed to the API economy of specialised service providers, through the execution of JS scripts on the client browser.

This has positive security and efficiency outcomes. It allows simple scaling via Content Delivery Networks. A downside is that the pattern applies to many, but not to all, usecases.

This approach is automated by a static site generator, which processes the content (together with CSS and JS resources) into the web-site files (which are then uploaded to the server. As before, the notion of a theme means that a simple complete web-site is directly available. Content is typically managed by simple version control such as git. An example site generator is [Hugo](https://gohugo.io/), though there are 354 other competitors listed on the [Jamstack site](https://jamstack.org/). In contrast to WordPress, the Hugo processor does not reside on the server.


## My Choice of Technology

I ran some experiments with WordPress, but found it was not a good fit for me. I was uncomfortable with the WYSIWYG editor, and found that the basic themes all looked like blogs. I did not want a simple blog website.

In the JAMstack ecosystem I ran some experiments with Jeckyl and with Hugo, and settled on the latter. Reasons included

- it is a standalone executable (written in Go)

- it was actively maintained, with a good (and improving) documantation.
