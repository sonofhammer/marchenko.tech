---
title: "How This Blog Is Made"
date: 2019-10-07
lastmod: 2020-02-27
author: Daniil Marchenko

---

*How to host a blog for one dollar a month.*

## 1. Register a Domain (~$12.00)

The most expensive part of hosting a personal static blog is buying a domain name. So bite the bullet, and spend those 12 bucks or so to get yourself a domain name. Get something memorable. Run it past a few friends of yours to see if its a good one.

Some Domain registrars to explore

* namecheap.com
* domains.google.com

## 2. Get the Tools Installed on Your System (free)

There are plenty of static site generators written in a variety of languages, from [C#](https://wyam.io/) to [Python](https://blog.getpelican.com/) to [Go](https://gohugo.io/). This site is created using Hugo, so the rest of the post will follow that.

To create a static site in Hugo, head on over to [GoHugo.io](https://gohugo.io/) and look over their docs to get an idea of how to install it on your operating system. The steps below are outlined for a Windows OS.

### Get Chocolatey

 [Chocolatey](https://chocolatey.org/) is a package management tool for Windows that makes downloading and installing applications a breeze. Go on over to [chocolatey.org/install](https://chocolatey.org/install) and run their one-liner as administrator in either cmd.exe or powerhsell.exe.

### Get Git

Using chocolatey, install [git](https://git-scm.com/) by running the following command: `choco install git`. You can read more about git [here](https://git-scm.com/).

### Get Hugo

Using Chocolatey, install Hugo by running the following command: `choco install hugo`. Verify that you have Hugo installed by running `hugo version`

## 3. Create a Local Version of the Site (free)

In the terminal, navigate to the parent folder where your site will live. Run the following `hugo new site sampleSite`

A new folder with the name of `sampleSite` will be created with site contents in it, but we'll need theme and some content before we can see it.

To make things easier to change directory (`cd`) to `sampleSite` and initialize a git repository by typing `git init`.

### Set a Theme

As of this post, this blog is using [Ghostwriter theme](https://themes.gohugo.io/ghostwriter/). However the directions for using the theme are not the best, since they instruct you to clone the repo directly. Instead of cloning the repository into the `/themes` directory in the site, setting it up as a git sub-module makes it a bit easier to manage separately from the rest of the site's content. 

To set up the theme as a submodule run `git submodule add https://github.com/jbub/ghostwriter themes/ghostwriter`

Add a line in `config.yml` to set the theme: `theme = "ghostwriter"`.

### Create a New Post

Create a new post: `hugo new post/mynewpost.md`

Serve the dev version of the site by running `hugo serve -D`.

Play around with Hugo and Theme settings to set it up just how you like it.

## 4. Host Your Site (free)

There are plenty of places where you can host a static site. GitHub Pages and GitLab are just two of many options.

This site uses Netlify.

To set up your own site on Netlify, push the git repo created in step 3 to one of the three (1) GitHub, (2) GitLab or (3) BitBucket.

Once the source code is in one of the places above, register an account with [Netlify](netlify.com).

Click the *New site from Git* button and follow the on-screen instructions. Be sure to set up your DNS correctly in both Netlify and whatever domain registrar you went with in step 1.

Because some themes are more special than others, Some of them require special build steps to function properly.

### Building your site

Ghostwriter theme requires to be built before it can be used. To build it, we need to run a few npm, and to do that, we need node on the build agent.

Netlify is clever enough to know that it needs to install node if you add a `.node_version` at the root of the repository. In this case, I created a file with `14.16.0` in it.

Netlify also needs instructions on how to build a site. To do that we can create a `netlify.toml` file at the root of the repository containing the instructions for building the site. 

The file for this site contains the following:

```toml
[build]
command = "cd themes/ghostwriter/ && npm ci && npm run build && cd ../../ && hugo --gc --minify -v"
publish = "public"

[build.environment]
HUGO_VERSION = "0.81.0"
```

The build command contains the following parts

`cd themes/ghostwriter/` = changes the current working directory\
`npm ci` = installs npm packages\
`npm run build` = builds the theme\
`cd ../../` = walks back up the directory structure\
`hugo --gc --minify -v` = builds hugo site\

The `publish` element specifies which directory to publish, and the `HUGO_VERSION` specifies which hugo version to use.

More information on how to build a hugo site on netlify can be found in [Netlify's](https://docs.netlify.com/configure-builds/common-configurations/hugo/) and [Hugo's](https://gohugo.io/hosting-and-deployment/hosting-on-netlify/) docs.

## 5. Configure Netlify to use Let's Encrypt SSL (free)

[Let's Encrypt](https://letsencrypt.org/) allows you to encrypt the website, allowing visitors to connect to it over https instead of http.

On Netlify, Under "Domain management" section of the site, select HTTPS and configure the SSL certificate from Let's Encrypt.

That's it! Your very own static blog should be up and running.
