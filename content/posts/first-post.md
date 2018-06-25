+++ 
draft = false
date = 2018-06-24T23:34:34-07:00
title = "Jekyll to Wordpress to Hugo"
slug = "" 
tags = []
categories = ["Hugo", "Draft", "Test"]
+++
---
### Why I ditched Jekyll and Wordpress
When I first created my personal blog about 3 years ago, I chose to use [Jekyll](https://jekyllrb.com/) hosted on [Github Pages](https://pages.github.com/). 

At the time, I was not confident enough to modify my Jekyll theme to fit into my needs, and I decided to move to [dockerized Wordpress](https://hub.docker.com/_/wordpress/) hosted on my own AWS EC2 server.

Wordpress was easy to use due to the out-of-box web interface for blog administration. Its export/import feature was also beneficial for backups and migrations. However, hosting my own Wordpress site started to cost me once my AWS free trial was over.

While thinking about going back to Jekyll, I found about [Hugo](https://gohugo.io/). I was interested in Hugo due to its fast growth and started looking into the documentations.

Now that I have learnt a lot on front-end development ever since my first Jekyll project, I was confident that I could modify a Hugo theme to satisfy the following personal requirements.


### Requirements
1. Simple and readable Hugo theme
2. Ability to categorize blog posts
3. Ability to customize the about page

While going through Hugo Themes, I found [Coder theme](https://github.com/luizdepra/hugo-coder). It had pagination feature of blog posts, but it was lacking my requirement #2 and #3.

I decided to create my own theme based on Coder, and this is how I have done it.

### Modifying Hugo Theme
To enable categorized blog posts, we need to talk about Hugo's [Taxonomy system](https://gohugo.io/content-management/taxonomies/). 

Hugo already has built-in taxonomy feature for categorization of blog posts, and you can enable it by adding following lines to your **config.toml** file.

```toml
[taxonomies]
  category = "categories"
  tag = "tags"
```

After enabling taxonomies, you need to create view templates for categories.

In **themes/coder/layouts/** directory, create a new directory named **categories** with *list.html* and *category.html*.

*list.html* is for listing all categories, and *category.html* is used for listing blog posts for a single category.

Once you are done, you may add a link to /categories/ in your navigation bar by modifying the **config.toml** like following example.

```toml
# Menu links
[[menu.main]]
    name = "Blog"
    weight = 1
    url  = "/posts/"
[[menu.main]]
    name = "Categories"
    weight = 2
    url = "/categories/"
[[menu.main]]
    name = "About"
    weight = 3
    url = "/about/"
```

I have also modified the blog post template to list categories of each post. However, I will leave a link to my repository rather than going into the details.

### Deploying on Github Pages
Hugo has a [detailed guide](https://gohugo.io/hosting-and-deployment/hosting-on-github/) on deploying your website on Github Pages.

1. Delete *public/* directory from the project root directory if there is one.
2. Add your github.io repository as a submodule
3. Build your static website by running **hugo**.
4. cd into the newly created *public/* directory
5. Add changes, commit staged, and push to master branch of your github.io repo.

Once you have set a submodule in your root project directory, do not delete *public/* directory.

The reason why we deleted it at first place was simply to add a git submodule pointing to a directory named *public/* which will be populated by Hugo later.

Whenever you want to update your github.io page, simply go through steps #3 ~ #5.