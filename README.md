# Jekyll Tutorial

The objective of this tutorial is to introduce [Jekyll](https://jekyllrb.com/) and show you how to build a website that you can host on GitHub for free.

[<img src="https://jekyllrb.com/img/logo-2x.png" width="200">](https://jekyllrb.com/)

## Contents

- [Requirements](#Requirements)
- [Installation](#Installation)
- [An example website in under 10 min](#An-example-website-in-under-10-min)
- [Jekyll structure](#Jekyll-structure)
- [Jekyll themes](#Jekyll-themes)
- [Customising your website](#Customising-your-website)

## Requirements

To follow all of the steps in this tutorial you will need a [GitHub](https://github.com/) account. It is possible to run everything locally and deploy your website on a different server, but everything will presented under the assumption that you already have a GitHub account.

You will also need to install Jekyll (see the [next section](#installation)) for local development and testing. It is also possible to build your website entirely on GitHub, but you will save yourself a lot of time if you are able to test things locally before deployment.

## Installation

Before starting you will have to install Jekyll. Jekyll is written in [Ruby](https://www.ruby-lang.org/en/downloads/) and therefore your system must have Ruby installed in order to build Jekyll. With Ruby installed the installation of Jekyll should simply be:

```bash
gem install jekyll bundler
```

Please see the [installation instructions](https://jekyllrb.com/docs/installation/) on the Jekyll website for more details.

## An example website in under 10 min

Now that you have Jekyll installed let's make a quick website to see how easy it is. We we will go through everything in more detail afterwards.

### Step 1 - Create a new repository

On your GitHub account either [fork](https://help.github.com/en/github/getting-started-with-github/fork-a-repo) this repository or create a new one.

> If you choose to create a new repository be sure to click the `Add .gitignore` button at the bottom and scroll down to `Jekyll`.

Now clone your repository. *e.g.*

```bash
git clone https://github.com/<USERNAME>/jekyll_tutorial.git
```

and `cd` to the repository name. *e.g.*

```bash
cd jekyll_tutorial
```

### Step 2 - Create a gh-pages branch

If you forked this repository then you can simply checkout the `gh-pages` branch.

```bash
git checkout gh-pages
```

Otherwise, create and checkout a new branch called `gh-pages`.

```bash
git checkout -b gh-pages
```

> `gh-pages` is a special branch name used to idetify [GitHub Pages](https://pages.github.com/) content. It is also possible to host GitHub pages on the `master` branch.

### Step 3 - Jekyll quickstart

Next we will run through the [Jekyll quickstart](https://jekyllrb.com/docs/) instructions with some minor changes.

You will need run these commands in your local repository directory.

> Otherwise, you can run the standard quickstart commands and copy the outputs to this directory. Be careful to copy all hidden files!

First, we create a new Jekyll site in the current directory.

```bash
jekyll new . --force
```

Then, we will launch the Jekyll local server.

```bash
bundle exec jekyll serve
```

You can view the website at the address specified by `Server address`.

Play around a bit then close the server by typing `ctrl+c`.

### Step 4 - Basic configuration

We need to add some basic information about our website, in particular where it will be deployed.

Open the `_config.yml` file and update update the entries `url` and `baseurl` (repository name) to those of your GitHub repository. *e.g.* If you forked this repository they will be:

```yaml
baseurl: /jekyll_tutorial
url: https://<USERNAME>.github.io/
```

> You can update the other entries if you want, just leave `theme` alone for now.

Here is the content I will use for this demonstration.

```yaml
title: Yoda's House
email: yoda@force.com
description: >-
  Very good my site is!
baseurl: /jekyll_tutorial
url: https://sfarrens.github.io/
twitter_username: yoda
github_username:  yoda

# Build settings
theme: minima
plugins:
  - jekyll-feed
```

Now relaunch the Jekyll server and you can keep it running for the next step.

```bash
bundle exec jekyll serve
```

You can see where some of the information is displayed.

### Step 5 - Basic content

To start making this look like a website lets add some example content.

Open `index.markdown` and add some content below the header.

Open `about.markdown` and replace the default content below the header.

Create new markdown file called `cv.md` and add the following header.

```html
---
layout: page
title: CV
permalink: /cv/
---
```

Add any content you like below the header.

Finally, in the directory `_posts` create a new post with the following file name format: `year-month-day-post-title.md`.

Add the following header to the post.

```html
---
layout: post
title:  <Post Title>
date:   <year-month-day>
categories: news
---
```

Add any content you like below the header.

Play around a bit then close the server by typing `ctrl+c`.

### Step 6 - Deploy the example site

Now that we have something that looks like a website we can deploy it on GitHub.

Stage the files generated by Jekyll.

```bash
git add .
```

> Note that the contents of `_site` and `.jekyll-cache` should be ignored by git.

Commit the changes.

```bash
git commit -m "upload jekyll content"
```

Finally, push the commits to your remote GitHub repository.

```bash
git push --set-upstream origin gh-pages
```

Now you should be able to view your example site at `https://<USERNAME>.github.io/<REPOSITORY>/`.

> If you forked this repository it will be `https://<USERNAME>.github.io/jekyll_tutorial/`. Note it may take a few minutes before the website is available.

## Jekyll structure

If you made it through the first part of this tutorial you should be able to make a very basic website, but you probably don't know how everything works.

Jekyll sites generally have the following structure:

```bash
├── _config.yml
├── _data
│   └── navigation.yml
├── _includes
│   ├── footer.html
│   └── header.html
├── _layouts
│   ├── default.html
│   └── post.html
├── _posts
│   └── 2020-03-07-my-first-post.md
├── _sass
│   ├── _base.scss
│   └── _layout.scss
├── _site
├── assets
│   ├── css
│   └── images
├── Gemfile
└── index.html
```

Here is a very brief rundown of what each of these components do.

- `_config.yml:` The configuration file for your site. Here you define some variables, list plugins and set the corresponding parameter values.
- `_data:` In this directory you can create yaml files to define additional variables.
- `_includes:` This is simply a place for defining HTML snippets that can be used in your layouts. *e.g.* Define behaviour for the header/footer for your site.
- `_layouts:` This is where you define *layouts* for your site pages. In other words, these are HTML files that define how a given page is laid out.
- `_posts:` This one is pretty clear, it's a directory where you store your *posts*. The best part being that they can be markdown files!
- `_sass:` This is the most important section if you want to customise the look of your website. In this directory you define all your style sheets using Sass.
- `_site:` This is where the final static HTML files generated by Jekyll are stored. In general you won't need to touch anything here, but it can be useful to see what's going on as you are building your website.
- `assets:` In this directory you can store *e.g.* images, CSS files and java scripts.
- `Gemfile:` The [Gemfile](https://jekyllrb.com/docs/step-by-step/10-deployment/#gemfile) is used to fix package versions and dependencies for your website.
- `index.html:` This is where you set the content for your home page. It can be defined in either HTML or markdown. Other static pages are similarly defined in the root directory.

> To get a more in depth understanding of each of these components I recommend following the Jekyll [Step by Step tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/).

You will probably notice that in the earlier example site many of these files and directories were missing. This is because much of this content is often hidden in the Jekyll template you are using.

## Jekyll themes

The default theme in Jekyll is [Minima](https://github.com/jekyll/minima) (which was used for the first example), but there are huge number of [Jekyll themes](http://jekyllthemes.org/) available online.

### Changing theme offline

If you want to try out a different theme locally you need to update the value of `theme` in `_config.yml`. You also need to update your `Gemfile` to download the theme by adding `gem <THEME_NAME>`.

*e.g.* To use the [Cayman theme](https://pages-themes.github.io/cayman/) you would add `theme: jekyll-theme-cayman` to `_config.yml` and `gem "jekyll-theme-cayman"` to `Gemfile`.

Then update your *bundle* before launching the Jekyll server.

```bash
bundle update
bundle exec jekyll serve
```

> Be sure to read the warnings and errors as not all themes use the same *layouts*. So pages will need to updated to fit the theme requirements.

### Changing theme on GitHub

Changing a theme on GitHub is even simpler. In your repository, click on "Settings" and scroll down to "GitHub Pages". There is a button labelled "Change Theme" that will take you to a selection of themes you can use.

This will simply update the value of `theme` in `_config.yml`.


## Customising your website

If you have decided that none of the Jekyll themes really offer what you are looking for you, you can make your own or simply modify an existing theme.

### Making your own theme

It is possible to create your own Jekyll theme that you can share as a template for others to use.

There plenty of [blog posts](https://www.siteleaf.com/blog/making-your-first-jekyll-theme-part-1/) that explain how to do this in more detail.

### Sass

Most of the work of getting your site to look the way you want it to is in defining the style sheets. This means learning how to write Cascading Style Sheets (CSS). Jekyll uses [Syntactically Awesome Style Sheets (Sass)](https://sass-lang.com/).

[<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/96/Sass_Logo_Color.svg/1920px-Sass_Logo_Color.svg.png" width="200">](https://sass-lang.com/)

> To get started with SASS check out their [guide](https://sass-lang.com/guide).

Sass has several very cool features including nesting and *mixins*. Mixins allow you define reusable pieces of CSS that you can include in your Sass files (`.scss`).

Here is a quick example of how to add a shadow to a container (something I used extensively on my own site).

```sass
@mixin shadow {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.post-container {
  @include shadow;
}
```

Once you get comfortable with Sass, the rest is just patience. You will define the layouts for each type of page. In my opinion this is made easier by breaking your HTML into pieces (that you keep in `_includes`). Similarly, you can break your Sass files into pieces that can import each other.
