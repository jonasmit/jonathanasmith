---
title: "Host your blog free with Hugo and Netlify - Part 1"
subtitle: "free"

date: 2020-11-01T11:01:07-04:00

tags: ['Hugo', 'Blog']
categories: ['Blog']
author: "Jon"
noSummary: true

resizeImages: false

draft: true
---
There are, quite literally, dozens of options for building and hosting your own site or blog. However, if you are building a personal site - where no revenue is being generated - the most important requirement is price. And **Free (as in Beer)** is the best price!

In this article, I will describe a method for building a blog using a static site generator technology, Hugo. Static sites are great because of their simplicity - there is no database or application server code to maintain - only a web server. Hugo allows you to build complex sites even without these technologies by generating the final static site from pre-built components and themes.

Hugo is extremely configurable and you can have a professional site or blog with after learning how to configure Hugo to define your site and Netlify to build and host your content. There is likely some assumed knowledge in the brief instructions below, so be prepared to research Hugo and Netlify further as you progress.

__Steps:__
- Domain Name (Optional)
- Register for Github
- Install Tools
- Set up Hugo and Theme
- Build Content
- Push code to Github
- Register and Configure Netlify

### Domain Name (Optional)
To make your site easy to access, you most likely will want to purchase a domain name. Personally, I like __[Google Domains](https://domains.google.com/)__ because it is simple and easy to track using a service that I use every day (gmail account). That is one less login to remember and if you want an email address that corresponds with the domain, you will have less to configure when setting up Google Workspace (formerly GSuite).

Once you have obtained the domain name, no additional setup is required until you are ready to point Google's domain name servers at your new site (hosted by Netlify).

### Register for Github
More than likely you already have a __[GitHub](https://www.github.com/)__ account but if not, go ahead and get that set up so you can have a source code repository to store your site content.

If you do not know what Github is, check out the following helpful material:
  - __[Getting Started with GitHub](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/quickstart)__
  -  __[Hello World](https://guides.github.com/activities/hello-world/)__

### Install Tools:
The steps I show in this article use the command line versus the user interface, so to follow along, go ahead and set up git and authenticate to GitHub via the command line (which will require generating and ssh key and uploading to GitHub). I also recommend installing a project from GitHub called __[hub](https://hub.github.com/)__ which makes it easy to create and manage repositories from the command line.

To simplify management of software on your local machine use a package management tool like __[homebrew](https://brew.sh/)__ on Mac __[chocolatey](https://chocolatey.org/)__ for Windows. I'll show Mac setup since that is the platform I use.  

#### Install Git:

```plaintext
git --version
```
On Mac, if you don't have git installed you will be prompted to install via XCode which is the simplest option - so just follow the instructions.

Otherwise, Google for the available options for your system.  Once you get a version printed out from the above command, you are ready to move on to the next step.

#### Install Hub:

```plaintext
brew install hub
```
#### Install Hugo:

```plaintext
brew install hugo
```
#### Verify Hugo:

```plaintext
hugo version
```

### Create Hugo Site and Theme

#### Create a directory and navigate to the directory:

```plaintext
mkdir github_repositories && cd github repositories
```

#### Create a new site and navigate to the site directory:

```plaintext
hugo new site my-new-blog && cd my-new-blog
```

#### Create a git repository:

```plaintext
echo "# my-new-blog" >> README.md
git init
git add .
git commit -a -m "initial commit"
```

#### Create a GitHub repository:

```plaintext
hub create 
```

#### Push code GitHub

```plaintext
git push -u origin HEAD
```

#### Install a Hugo theme:

Hugo needs a theme to display your content, so go ahead select a __[theme](https://themes.gohugo.io/)__ and install it. For demonstration purposes I will use the __[hello-world-ng](https://themes.gohugo.io/hugo-theme-hello-friend-ng/)__ theme. 

Now we need to let Git know about our code so we can 

```plaintext
git submodule add https://github.com/rhazdon/hugo-theme-hello-friend-ng.git themes/hello-friend-ng
```

If you want to change the theme, you can fork the theme first in Github and then add it as a submodule (changign the url to your own copy of the theme). Either way, it is best to use a submodule so your Github repository for your site is aware of how to get new versions of the theme when it changes (original or your own forked copy).

#### Copy Example Site Content

```plaintext
cp -r themes/hello-friend-ng/exampleSite/* .
```

#### Create content for your post

```plaintext
hugo new posts/hello-world.md
```

Hugo uses a configuration format called frontmatter to configure various elements in your posts - some of which are automatically generated for you based on the type of content you are creating with Hugo. 

Open up the hello-world.md file and add the following statement below the front matter:

```plaintext
Howdy, this is my first hugo blog. __Hello World!__
```

Check out this gist to see what it should look like when you are done:

{{<gist jonasmit 3c21da7e88481a8a43306c75b726f71a>}}

#### Run Locally (with drafts)
In order to run a webserver locally to display the blog, execute the following in your terminal. 

```plaintext
hugo serve -D
```

If you don't have anything else running on the default port (1313), you can browse to your new blog via http://localhost:1313/

You should see a site that looks like the below image:

![Hello World NG](/hello-world-md.png)

In Part 2, I will demonstrate how to wire this blog up to Netlify and publish your blog!