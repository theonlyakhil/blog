# Blog
This repository contains my blog. This blog runs on jekyll.

# How to install

1. Clone this repository
2. Make changes to config.yml to make it personal.
3. Add posts to in _posts.
4. Compile the site using command.
```bash
jekyll build
```
5. Push code to git.

# Add links to Navigation

1. Goto _data/navigation.yml
2. Edit navigation.yml
3. To add links
```
main:
  - title: "title"
    url: link
```
# Add blog posts

The blog posts are written using markdown.
1. Create a md file and name it using 'year-month-day-blog-post-title.md'
2. Add the following lines at the top.
```markdown
---
title:  "Things to do after installing Fedora 28"
search: true
categories: 
  - Linux
  - Fedora
last_modified_at: 2018-09-27T08:05:34-05:00
header:
  teaser: /assets/images/blog/things-to-do-after-installing-fedora-28.jpeg
---
```