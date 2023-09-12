---
layout: page
title: About
---

## How this site was made

1. Make new repository

2. Check "Add README.md"

   a. Delete the header from the readme or else there will be two headers on / page
   
4. Add a post by clicking on "Add file"
   
    a. Name it "_posts/YYYY-MM-DD-post-title.md"
   
    b. Add front-matter
    ```yaml
    ---
    layout: post # not sure if you need this for sure
    title: Title
    ---
    ```
    
    c. Write your post in markdown
   
    d. If you have ChatGPT text you want to use, click the "Copy" button at the top right of the post in lieu of copying manually to preserve the markdown
   
    e. Save and commit

5. If it's a page instead (which will make it appear in the header at the top of the website), do this instead

   a. Name it page.md, doesn't have to be in a folder

   b. Add front-matter
   ```yaml
   ---
   layout: page
   title: Title
   ---
   ```
   Still not sure if you need the layout directive

   c. Write it in markdown

   d. Save and commit
   
7. Add _config.yml
   
    a. Add this:
    ```yaml
    remote_theme: jekyll/minima
    minima:
      skin: dark
    plugins:
      - jekyll-feed
    ```
    You need the jekyll-feed plugin so the RSS link isn't broken. Not sure how to remove it entirely
   
8. Turn on Github Pages in settings
   
    a. Turn on Enforce HTTPS (it's free)
