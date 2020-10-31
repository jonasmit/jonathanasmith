---
title: "Host your blog free with Hugo and Netlify"
subtitle: "free"

date: 2020-10-30T11:01:07-04:00

tags: ['Hugo', 'Blog']
categories: ['Blog']
author: "Jon"
noSummary: true

resizeImages: false

draft: true
---
There are, quite literally, dozens of options for building and hosting your own site or blog. However, if you are building a personal site - where no revenue is being generated - the most important requirement is price. And **Free (as in Beer)** is the best price!

In this article, I will describe a method for building a blog using a static site generator technology, hugo. Static sites are great because of their simplicity - there is no database or application server code to maintain - only a web server. Hugo allows you to build complex sites even without these technologies by generating the final static site from pre-built components and themes.

__Steps:__
- Domain Name (Optional)
- Register for Github
- Install Tools
- Set up Hugo and Theme
- Build Content
- Push code to Github
- Register and Configure Netlify

### Domain Name (Optional)
To make your site easy to access, you most likely will want to purchase a domain name. Personally, I like __[Google Domains](https://domains.google.com/)__ because it is simple and easy to track using a service that I use every day (gmail account). 

Once you have obtained the domain name, no additional setup is required until you are ready to point Google's domain name servers at your new site.

### Register for Github
More than likely you already have a __[Github](https://www.github.com/)__ account but if not, go ahead and get that set up so you can have a source code repository to store your site content.

If you do not know what Github is, check out the following helpful material:
  - __[Getting Started with GitHub](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/quickstart)__
  -  __[Hello World](https://guides.github.com/activities/hello-world/)__

### Install Tools
The steps I show in this article use the command line versus the user interface, so to follow along, go ahead and set up git and authenticate to GitHub. I also recommend installing a project from GitHub called hub which makes it easy to create and manage repositories from the command line.

To simplify management of software on your local machine use a package management tool like __[homebrew](https://brew.sh/)__ on Mac __[chocolatey](https://chocolatey.org/)__ for Windows. I'll show Mac setup since that is the platform I use.  

- Install Git:

```plaintext
git --version
```
On Mac, if you don't have git installed you will be prompted to install via XCode which is a simple options so just follow the instructions.

- Install Hub:

```plaintext
brew install hub
```
- Install Hugo:

```plaintext
brew install hugo
```
- Verify Hugo:

```plaintext
hugo version
```

### Create Hugo Site and Theme

- Create a directory and navigate to the directory:

```plaintext
mkdir github_repositories && cd github repositories
```

- Create a new site and navigate to the site directory:

```plaintext
hugo new site my-new-blog && cd my-new-blog
```

- Create a git repository:

```plaintext
echo "# my-new-blog" >> README.md
git init
git add .
git commit -a -m "initial commit"
```

- Create a GitHub repository:

```plaintext
hub create 
```

- Push code GitHub

```plaintext
git push -u origin HEAD
```

- Install a Hugo theme:

Hugo needs a theme to display your content, so go ahead select a __[theme](https://themes.gohugo.io/)__ and install it. For demonstration purposes I will use the __[hello-world-ng](https://themes.gohugo.io/hugo-theme-hello-friend-ng/)__ theme. 

Now we need to let Git know about our code so we can 

```plaintext
git submodule add https://github.com/rhazdon/hugo-theme-hello-friend-ng.git themes/hello-friend-ng
```

If you want to change the theme, you can fork the theme first in Github and then add it as a submodule (changign the url to your own copy of the theme). Either way, it is best to use a submodule so your Github repository for your site is aware of how to get new versions of the theme when it changes (original or your own forked copy).

- Copy Example Site Content

```plaintext
cp -r themes/hello-friend-ng/exampleSite/* .
```

- Run Locally (with drafts)


```plaintext
hugo serve
```

Now you should have a site that looks like the below image:

