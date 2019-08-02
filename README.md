[![Build Status](https://travis-ci.org/ahjumma/hugo-blog.svg?branch=master)](https://travis-ci.org/ahjumma/hugo-blog)

# Summary
This is a Hugo-based blogging project for my personal blogging posts.

I am utilizing a theme based on [Coder](https://github.com/luizdepra/hugo-coder), and I have modified it to suit my needs such as categorization and displaying categories for each post.

Currently, Travis CI is being used to build and deploy my static web site on Github Pages.


## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

#### Prerequisites

Even though Hugo is written in Go, Hugo is a single executable binary file which **does not require Go**.

If you need to modify *css* files, the current theme is based on *less*, and you would need **npm** for compiling *less* files into *css*.


#### Installing

1. install Hugo executable from [here](https://gohugo.io/getting-started/quick-start/)

If you want to modify *less* file in the */themes/coder/static/less/style.less*, you need to install following npm libraries

2. sudo npm install -g less uglifycss


#### Compiling css from less

Compiling css file can be done by executing **make build** located in */themes/coder* directory.


## Deployment

Deployment guide can be found on my blogging post [here](https://taeyeonkim90.github.io/posts/first-post/).

The blogging post covers manual deployment strategy and TravisCI-based automated deployment on Github Pages.

## Built With

* [Hugo](https://gohugo.io/) - Static site generator
* [npm](https://www.npmjs.com/) - JS dependency management
* [Coder](https://github.com/luizdepra/hugo-coder) - Hugo theme created by [Luiz](https://github.com/luizdepra)
* [Travis CI](https://travis-ci.org/) - Continuous Integration tool for building and deploying this project

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* [Luiz](https://github.com/luizdepra): creator of the Hugo Coder theme