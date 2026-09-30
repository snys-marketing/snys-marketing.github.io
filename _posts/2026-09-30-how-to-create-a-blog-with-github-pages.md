---
layout: post
title: "How to Create a Free Blog on GitHub Pages (Step by Step)"
description: "A beginner-friendly guide to launching a free blog on GitHub Pages with Jekyll, using only your browser. No software to install."
categories: guides
image: /assets/images/github-pages-steps.png
---

I wanted a simple place to keep the marketing notes I learn along the way...

I wanted a simple place to keep the marketing notes I learn along the way, and to share them with other people. I chose GitHub Pages because hosting is free, pages load fast, and I can write everything in Markdown.

This guide walks through exactly how I set it up. You only need a web browser and about 20 minutes.

![Infographic: six steps to launch a free blog on GitHub Pages](/assets/images/github-pages-steps.png)

## What you need

- A free GitHub account
- A browser (no software to install)
- A few minutes to type or paste small text files

## Step 1: Create a GitHub account

Go to github.com and choose **Sign up**. Your **username** becomes your blog address, so pick something short, lowercase, and easy to remember.

For example, the username `snys-marketing` gives the blog address `snys-marketing.github.io`.

## Step 2: Create a repository

1. Click the **+** icon at the top right and choose **New repository**.
2. Name it exactly like your username, plus `.github.io`. For example: `snys-marketing.github.io`.
3. Set visibility to **Public**.
4. Switch on **Add README**.
5. Click **Create repository**.

The name must match your username exactly. One wrong character and the site will not load.

## Step 3: Add the `_config.yml` file

This file holds your site settings.

1. In your repository, click **Add file**, then **Create new file**.
2. Name the file `_config.yml`.
3. Paste this in and edit the title and description:

```yaml
title: Marketing Notes
description: What I learn about SEO, content, email and social media marketing
lang: en
theme: minima
plugins:
  - jekyll-seo-tag
  - jekyll-sitemap
  - jekyll-feed
```

4. Click **Commit changes**, then confirm.

What the settings do:

- `theme: minima` is the default Jekyll blog theme.
- `jekyll-seo-tag` adds title and description tags that search engines read.
- `jekyll-sitemap` creates a sitemap so Google can find your posts.
- `jekyll-feed` creates an RSS feed.

Keep the indentation exactly as shown, and use spaces, not tabs.

## Step 4: Add the `index.md` file

This is your home page. Create a new file named `index.md` and paste:

```
---
layout: home
---
```

With this layout, your home page lists all your posts automatically.

## Step 5: Turn on GitHub Pages

1. Open the **Settings** tab of your repository.
2. Click **Pages** in the left menu.
3. Under **Source**, choose **Deploy from a branch**.
4. Choose the **main** branch and the **/ (root)** folder, then click **Save**.

To check progress, open the **Actions** tab. When the latest run shows a green tick, your site is live. Open `https://your-username.github.io` and press Ctrl+F5 to refresh.

## Step 6: Publish your first post

1. Click **Add file**, then **Create new file**.
2. Name it like this: `_posts/2026-09-30-my-first-post.md`. Typing the `/` after `_posts` creates the folder for you.
3. Paste this and replace it with your own writing:

```
---
layout: post
title: "My First Post"
description: "A short summary of what this post covers."
categories: notes
---

Write your post here in Markdown.

## A subheading

- A point
- Another point
```

4. Click **Commit changes**.

After one or two minutes, your post appears on the home page.

The file name must follow the pattern `YEAR-MONTH-DAY-title.md`, in lowercase, without accents, joined by hyphens. If the name does not start with a date, the post will not show up.

## If something goes wrong

- **The page shows a 404 error.** Check that the repository name matches your username exactly, and that Pages is set to the `main` branch and `/ (root)`.
- **The post does not appear.** Make sure the file is inside the `_posts` folder and starts with a date. Jekyll skips posts dated in the future, and GitHub uses UTC time, so try setting the date one day earlier.
- **The build fails in Actions.** Click the failed run to read the error. The usual cause is wrong indentation in `_config.yml` or a missing `---` line at the top of a post.

## Next steps

Once your blog is running, three small upgrades make a big difference:

1. Add an **About** page so readers know who writes the blog.
2. Register the site in **Google Search Console** and submit `sitemap.xml` so Google indexes your posts.
3. Add images to your posts. Upload them to an `assets/images` folder and link them with `![description](/assets/images/file.png)`.

That is the whole setup: free hosting, your own address, and every post stored as a simple text file you can take anywhere.
