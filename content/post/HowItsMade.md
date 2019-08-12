---
title: "How This Blog Is Made"
date: 2019-08-11
draft: true
author: Daniil Marchenko

---

*How to host a blog for one dollar a month.*

## 1. Register a Domain (~$12.00)

The most expensive part in hosting a personal static blog is buying a domain name. So bite the bullet, and  spend those 12 bucks or so to get yourself a domain name. Get something memorable. Run it past a few friends of yours to see if its a good one.

Some Domain registrars to explore

* namecheap.com
* domains.google.com

Or, if you're feeling extra stingy, you can skip this part for now and head right on over to step two.

## 2. Get the Tools Installed on Your System (free)

There are plenty of static site generators written in a variety of languages, from [C#](https://wyam.io/) to [Python](https://blog.getpelican.com/) to [Go](https://gohugo.io/). This site is created using Hugo, so the rest of the post will follow that.

To create a static site in Hugo head on over to [GoHugo.io](https://gohugo.io/) and look over their docs to get an idea idea of how to install it on your particular system. The steps below are outlined for a Windows OS

### Get Chocolatey

 [Chocolatey](https://chocolatey.org/) is a package management tool for Windows that makes downloading and installing applications a breeze. Go on over to [chocolatey.org/install](https://chocolatey.org/install) and run their one-liner as administrator in either cmd.exe or powerhsell.exe.

### Get Git

Using chocolatey, install [git](https://git-scm.com/) by running the following command: `choco install git`. You can read more about git [here](https://git-scm.com/).

### Get Hugo

Using Chocolatey, install Hugo by running the following command: `choco install hugo`. Verify that you have Hugo installed by running `hugo version`

## 3. Create a Local Version of the Site (free)

In the terminal, navigate to the parent folder where your site will live. Run the following `hugo new site sampleSite`

A new folder with the name of `sampleSite` will be created with site contents in it, but we'll need theme and some content before we can see it.

To make things easier to `cd` to `sampleSite` and initialize a git repository by typing `git init`.

### Set a Theme

As of this post, this blog is using [Ghostwriter theme](https://themes.gohugo.io/ghostwriter/). However the directions for using the theme are not the best, since they instruct you to clone the repo directly. Instead of cloning the repository into the `/themes` directory in the site, setting it up as a git sub-module makes it a bit more easier to manage.

To set up the theme as a submodule run `git submodule add https://github.com/jbub/ghostwriter themes/ghostwriter`

Add a line in `config.toml` to set the theme: `theme = "ghostwriter"`.

### Create a New Post

Create a new post: `hugo new post/mynewpost.md`

Serve the dev version of the site by running `hugo serve -D`.

Play around with Hugo and Theme settings to set it up just how you like it.

## 4. Host Your Site (free)

There are plenty of places where you can host a static site. GitHub Pages and GitLab are just two of many options.

This site uses Netlify.

To set up your own site on Netlify, push the git repo created in step 3 to one of the three (1) GitHub, (2) GitLab or (3) BitBucket

Once the source code is in one of the places above, register an account with [Netlify](netlify.com). 

Click the `New site from Git` button and follow the on-screen instructions. Be sure to set up your DNS correctly in both Netlify and whatever domain registrar you went with in step 1.

Because some themes are more special than others, Some of them require special build steps to function properly.

### Some Build Troubleshooting

Ghostwriter theme in particular was a bit of a pain. It uses yarn packages and Netlify didn't want to build it at first. To build it, we need to restore yarn packages, and to do that, we need yarn on the build machine.

Head on over to the "Environment" section of the build definition in Netlify and create a `HUGO_VERSION` and `YARN_VERSION` variables containing appropriate version numbers ( `0.53` and `1.17.3` as of this publication)

in the build command type the following `cd themes/ghostwriter/ && yarn && yarn run build && cd ../../ && hugo -v`

`cd themes/ghostwriter/` = changes the current  working directory </br>
`yarn` = installs yarn packages </br>
`yarn run build` = build the yarn packages </br>
`cd ../../` = walks back up the directory structure </br>
`hugo -v` = builds hugo site using verbose logging verbose logging </br>

## 5. Configure Netlify to use Let's Encrypt SSL (free)

[Let's Encrypt](https://letsencrypt.org/) allows you to encrypt your website, allowing your visitors to connect to it over https instead of http.

On Netlify, Under "Domain management" section of your site, select HTTPS and configure the SSL certificate from Let's Encrypt.
