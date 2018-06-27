+++ 
draft = false
date = 2018-06-24T23:34:34-07:00
title = "Jekyll to Wordpress to Hugo"
slug = "" 
tags = []
categories = ["Hugo", "TravisCI"]
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

### Deploying on Github Pages Manually
Hugo has a [detailed guide](https://gohugo.io/hosting-and-deployment/hosting-on-github/) on deploying your website on Github Pages.

1. Delete *public/* directory from the project root directory if there is one.
2. Add your github.io repository as a submodule
3. Build your static website by running **hugo**.
4. cd into the newly created *public/* directory
5. Add changes, commit staged, and push to master branch of your github.io repo.

Once you have set a submodule in your root project directory, do not delete *public/* directory.

The reason why we deleted it at first place was simply to add a git submodule pointing to a directory named *public/* which will be populated by Hugo later.

Whenever you want to update your github.io page, simply go through steps #3 ~ #5.

### Deploying on Gibhub Pages with Travis CI
I have used blog posts by [Chris Hager](https://www.metachris.com/2017/04/continuous-deployment-hugo---travis-ci--github-pages/) and [Martin Kaptein](https://www.martinkaptein.com/blog/hugo-with-travis-ci-on-gh-pages/) to write up my Travis CI configuration file.

For people who are not familiar with Continuous Integration(CI) tool such as Jenkins and Travis CI, a CI tool automates testing, building, and deploying your projects.

For my personal use, I chose Travis CI to do this job due to Travis CI's great web-based GUI tool.

##### Create Travis CI config file
Firstly, you need to add **.travis.yml** file in your root directory of the repository.

```yaml
language: go

go:
  - master # This uses automatically the latest version of go

install:
  - go get github.com/spf13/hugo # This provides the latest version of Hugo to Travis CI
  - rm -rf public || exit 0

script:
  - hugo # This commands builds your website on travis

deploy:
  local_dir: public # Default static site output dir for Hugo
  repo: taeyeonkim90/taeyeonkim90.github.io # This is the slug of the repo you want to deploy your site to
  target_branch: master # GitHub pages branch to deploy to (in other cases it can be gh-pages)
  provider: pages
  skip_cleanup: true
  github_token: $GITHUB_TOKEN # This is the authentication which you will setup in the next step in travis-ci dashboard
  email: taeyeonkim90@gmail.com
  name: "Andrew Kim"
  on:
    branch: master
```

1. **go:** statement tells Travis CI to use an environment with go compiler pre-installed
2. **install:** statement tells Travis CI to install dependencies which is required for buliding this project
3. **script:** can be thought as the build step prior to the deployment
4. **deploy:** is executed when the build is successful. In this example, Travis CI already has a pre-configured deployment strategy set up for Github Pages. **provider: pages** states we will be deploying on Github Pages. The rest is self explanatory.

##### Generate Github Access Token
**$GITHUB_TOKEN** is what will be used by Travis CI to be able to push to your Github Pages repository.
Firstly, you need to generate this token on your Github.

Go into your *global settings > Developer settings > Personal access tokens*.

Your new access token should have all **repo** permissions checked and no more is required.

Save the token, then copy the generated access token.

##### Register Github Access Token on Travis CI
Move to the Travis CI homepage where you will be able to see your blogging repository.

In your blogging repository visible on Travis CI, go into *More options > Settings*.

Add an environnment variable named, **GITHUB_TOKEN** and add your previously generated Github access token.

You are almost done in this point.

##### Remove git submodules on /public/ directory
In my experience, leaving a git submodule for your /public/ directory caused permission problem when Travis CI was attempting to pull in the git submodules recursively due to SSH key not setup on Travis CI.

To by-pass this, my crude approach was simply to delete the submodule in your git cache, /public/ directory, and git modules.

Once I removed all submodules in my project, I pushed my updated project, Travis CI detected the push, Travis CI saw **.travis.yml** config, and Travis CI built and deployed the result onto my Github Pages