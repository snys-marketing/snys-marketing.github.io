---
layout: post
title: "How to Track Your GitHub Pages Blog with Google Analytics 4"
description: "A step-by-step guide to adding Google Analytics 4 to a Jekyll blog on GitHub Pages, so you can see how many people read each post."
categories: analytics
---

Once my first post was live, I wanted to know whether anyone was reading it. GitHub Pages has no built-in stats, so I connected the blog to Google Analytics 4 (GA4). The standard version is free, and the whole thing took about 15 minutes, including one detour that I'll point out below.

## What you need

- A blog on GitHub Pages that uses the default minima theme
- A Google account
- About 15 minutes

## Step 1: Create a GA4 account and property

1. Go to analytics.google.com and sign in.
2. Click **Admin** (the gear icon at the bottom left), then **Create**, then **Account**. The **Property** option stays greyed out until an account exists.
3. Name the account and click **Next**.
4. Name the property, set your time zone and currency, and click **Next**. Answer the short business questions and click **Create**.
5. When asked for a platform, choose **Web**. Enter your blog address without `https://` (for example `yourname.github.io`) and give the stream a name. Leave **Enhanced measurement** on and click **Create stream**.
6. Copy the **Measurement ID**. It looks like `G-XXXXXXXXXX`.

## Step 2: Add the tag to your blog

Google asks you to paste a snippet into the `<head>` of every page. In Jekyll, the head is built from a file called `head.html`, so that's the file to override.

My first attempt was `_includes/custom-head.html`, which some minima guides mention. On my site it was ignored, and Google reported that the tag wasn't detected. Overriding `head.html` worked.

In your repository, click **Add file**, then **Create new file**, and name it `_includes/head.html`. Paste this, replacing both `G-XXXXXXXXXX` with your own Measurement ID:

{% raw %}

```html
<head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  {%- seo -%}
  <link rel="stylesheet" href="{{ "/assets/main.css" | relative_url }}">
  {%- feed_meta -%}

  <!-- Google tag (gtag.js) -->
  <script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
  <script>
    window.dataLayer = window.dataLayer || [];
    function gtag(){dataLayer.push(arguments);}
    gtag('js', new Date());

    gtag('config', 'G-XXXXXXXXXX');
  </script>
</head>
```

{% endraw %}

The lines above the Google snippet are the standard head that minima uses, so your styling and SEO tags stay the same. They rely on the `jekyll-seo-tag` and `jekyll-feed` plugins, which should already be listed in your `_config.yml`.

Click **Commit changes** once. Each commit triggers a new build, so avoid committing again until this one finishes.

## Step 3: Wait for the build

Open the **Actions** tab in your repository. When the latest run shows a green tick, the change is live. This usually takes one to two minutes.

## Step 4: Check that the tag is installed

There are two ways to check

- Open your blog, press Ctrl+U to view the page source, and search for `googletagmanager`. If you find it, the tag is on the page.
- In GA4, click **Test installation** on the setup screen. When it works you'll see a message that the tag was detected on your site.

## Step 5: See your first visitor

Open your blog in a private window, then go to **Reports**, then **Realtime** in GA4. If you see one active user, you're set. The other reports take up to about a day to fill in, so an empty dashboard on day one is normal.

## Where to find your numbers

- **Reports, Engagement, Pages and screens:** which posts get read the most
- **Reports, Acquisition, Traffic acquisition:** where readers come from, such as LinkedIn or Google Search

## Two settings worth changing

**Data retention.** GA4 keeps detailed data for only 2 months by default. Go to **Admin**, then **Data collection and modification**, then **Data retention**, choose **14 months**, and save.

**UTM links.** When you share a post, add UTM parameters so GA4 can tell you which post on which platform sent the reader. For example:

```
https://yourname.github.io/your-post/?utm_source=linkedin&utm_medium=social&utm_campaign=my-post
```

## Things to know

- Your own visits are counted unless you set up an internal traffic filter.
- Ad blockers stop some readers from being counted, so the real number is a bit higher than what you see.
- GA4 uses cookies. If you expect readers from the EU, look into adding a consent banner.

## If Google says the tag isn't detected

- Check that the file is named exactly `_includes/head.html` and sits in the root of the repository, not inside another folder.
- Check that the latest run in **Actions** has a green tick.
- View the page source and search for `googletagmanager`. If it's missing, open the file again and make sure there are no stray backticks or extra lines at the top.
- Press Ctrl+F5 on your blog before testing again.
