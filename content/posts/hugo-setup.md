---
title: "Blogging Setup With Hugo and GitHub Pages"
date: 2020-03-18T17:28:51+05:00
draft: false
---

If you want to share your thoughts with the world, starting an online blog is a good idea. You can use a static site generator and a free static hosting service to host your blog for free.

In this post, I will show you how I setup my blog using **Hugo** and **GitHub pages**.

## Workflow

1. Write posts in markdown.
2. Convert to a static website using hugo.
3. Commit and push to GitHub to deploy.

## Install Hugo

To build the site, hugo must be installed on your system. 

Use your package manager to install Hugo.

On macOS use [Homebrew](https://brew.sh/)

```
brew install hugo
```

On Arch linux

```
pacman -Syu hugo
```

For other distros and Windows, [this](https://gohugo.io/getting-started/installing/)

To check if hugo is installed, run

```
hugo version
```



## Create and Configure Site

Create a new site named 'blog'

```
hugo new site blog
```

Hugo will generate files required for a site in a new folder called blog.

Initialize an empty Git repository.

```
git init
```



A theme is required for a hugo site. Visit https://themes.gohugo.io/ and select a theme. For this tutorial, I am using notepadium. To use a theme, it should be in themes directory of hugo site. It is recommended to add theme as a [Git Submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules) because it makes easier to update themes.

```
git submodule add https://GitHub.com/cntrump/hugo-notepadium.git themes/hugo-notepadium
```

To use installed theme, add these lines to `config.toml`

```
theme = "hugo-notepadium"
```



## Write Some Content

To write a post, you can manually create a markdown file in content folder or use the Hugo cli.

```
hugo new posts/first-post.md
```

The above command will create a new file in `content/posts/` directory called `first-post.md`.

Open this file in your text editor of choice and write your first post.

Preview your site before deploying by running

```
hugo server
```

Your website will be available at http://localhost:1313/.

## Build and Deploy on GitHub Pages

Types of GitHub Pages:

- User Pages: [username].GitHub.io
- Project Pages: [username].GitHub.io/[project]

I recommend using Project Pages for blog.

In `config.toml`, add

```
publishDir = "docs"
```

This will output generated static files to docs folder. GitHub pages will deploy from this folder.

Also set `baseURL` and `title`.

Create a new repository in your GitHub account and copy its URL.

In your hugo site directory,  run

```
git remote add origin <URL-of-new-Repo>
```



Build your site by running

```
hugo
```

Then run following to deploy

```
git add .
git commit -m "First Post"
git push origin master
```

Go to GitHub repository Settings > GitHub pages. Select /docs in **Source**.

Navigate to your site at [username].GitHub.io/blog

Profit.



## To-Do

- [ ] Automate build and deploy.

