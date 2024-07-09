---
author: "Yang Lyu"
date: 2024-05-28
title: Quick tutorial on blog web with hugo and netlify
weight: 10
---

# How to Create a Blog with Hugo and Deploy on Netlify

Creating a blog with Hugo and deploying it on Netlify is a streamlined and efficient process. Hugo is a powerful static site generator that allows for quick and easy website development. Netlify provides seamless deployment and hosting for static sites. Here's a step-by-step guide to get your blog up and running.

## Prerequisites
- Install Hugo by following the [installation guide](https://gohugo.io/getting-started/installing/).
- Start from the root folder of a github repo, such as `yangblog`

## Step 1: Create a New Hugo Site
Start by creating a new Hugo site:
```
hugo new site yanglyublog --format yaml
```

## Step 2: Add a Theme
Choose a theme from the [Hugo Themes](https://themes.gohugo.io/) site. For example, to add the Ananke theme:

```bash
git init
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
echo 'theme = "ananke"' >> hugo.yaml
```

## Step 3: Create Content
Generate your first post:

```
hugo new posts/my-first-post.md
```

- Edit the content of the post by opening the `content/posts/my-first-post.md` file in a text editor. Change the `draft` status to `false`.
- You can also just create any `.md` file under `content/posts/`

## Step 4: Build the Site
To see your site locally, run:

```bash
hugo server --minify --theme hugo-book
```

Visit `http://localhost:1313` in your browser to preview the site.

## Step 5: Prepare for Deployment

- Update the `hugo.yaml` file, update as follows:

```yaml
baseURL: https://yanglyublog.netlify.app/
languageCode: en-us
title: Yang's Blog
theme: hugo-book
```

- Push your Hugo site to your repository.
- Read this blog [here](https://gohugo.io/hosting-and-deployment/hosting-on-netlify/) to understand the steps needed.

## Step 6: Deploy to Netlify

Go to [Netlify](https://www.netlify.com/) and sign up or log in. Click on “New site from Git” and select your repository.

Configure the build settings:
- **Build Command**: `hugo --gc --minify`
- **Publish Directory**: `public`

Set Env Var: 
- **HUGO_VERSION**: `0.128.2`

Click “Deploy site.” Netlify will build and deploy your site. Once the process is complete, you will have a live URL for your new blog.

## Step 7: Continuous Deployment
Every time you push changes to your GitHub repository, Netlify will automatically rebuild and deploy your site. This ensures your blog is always up-to-date with the latest changes.

## Conclusion
Creating and deploying a blog with Hugo and Netlify is straightforward. Hugo's speed and flexibility combined with Netlify's ease of use for deployment make it a powerful combination for bloggers and developers alike.

Enjoy your new blog!

