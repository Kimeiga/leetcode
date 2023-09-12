# How this site was made

1. Make new repository
2. Check "Add README.md"
  a. Delete the header from the readme or else there will be two headers on / page
3. Add a post by clicking on "Add file"
  a. Name it "_posts/YYYY-MM-DD-post-title.md"
  b. Add front-matter
  ```
  ---
  layout: post # not sure if you need this for sure
  title: Title
  ---
  ```
  c. Write your post in markdown
  d. If you have ChatGPT text you want to use, click the "Copy" button at the top right of the post in lieu of copying manually to preserve the markdown
  e. Save and commit
4. Add _config.yml
  a. Add this:
  ```yml
  remote_theme: jekyll/minima
  minima:
    skin: dark
  plugins:
    - jekyll-feed
  ```
  You need the jekyll-feed plugin so the RSS link isn't broken. Not sure how to remove it entirely
5. Turn on Github Pages in settings
  a. Turn on Enforce HTTPS (it's free)
