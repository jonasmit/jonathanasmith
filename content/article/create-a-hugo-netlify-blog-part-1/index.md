---
title: "Host your blog free with Hugo and Netlify - Part 1"
subtitle: "free"

date: 2020-11-01T11:01:07-04:00

tags: ['Hugo', 'Netlify', 'Blogging']
categories: ['Hugo']
author: "Jon"
noSummary: false

resizeImages: false

draft: false
---
There are, quite literally, dozens of options for building and hosting your own site or blog. However, if you are building a personal site - where no revenue is being generated - the most important requirement is price. And **Free (as in Beer)** is the best price!

In this article, I will describe a method for building a blog using a static site generator technology, __[Hugo](https://gohugo.io/)__, and run it locally on your machine. In Part 2, I will hook up the site to Netlify to make your blog public. 

<!--More -->

Static sites are great because of their simplicity - there is no database or application server code to maintain - only a web server (and with Netlify, you won't even need to think about the web server). Hugo allows you to build complex sites even without database and application server technologies by generating the final static site from pre-built components and themes. You simply place your Markdown content in specific directories, use a pre-built theme, and your site is generated at build time. The result is a compelling site with very fast load times and features that closely resemble dynamic sites built with more moving parts. 

Hugo is extremely configurable and you can have a professional site with minimal effort. Most Hugo configuration follows the convention over configuration pattern but Hugo also provides a __config.toml__ file as well for global configurations and complex options. 

### Process Architecture
The overall process architecture is defined in the following diagram. As a developer, you will use Hugo on your local workstation to build and test your site. All local changes on your machine will be pushed to your remote GitHub repository. Netlify will then pick up the changes made in GitHub and build and publish the site. Finally, once published, visitors will be able to access your site. Best of all, these steps are automated, except the content development :).

![Process Architecture](https://docs.google.com/drawings/d/e/2PACX-1vTbcOcHb3s-wLoJ_Fx-0-8vH90O5qZPFKn6jp1qbOqghzR7s10fXe8VbKCi1_4kCEBvina99CdRbAjO/pub?w=960&amp;h=720)

### Steps
Next, I will guide you through the following steps:

![Hugo](https://docs.google.com/drawings/d/e/2PACX-1vSa7BPOztmrlGUc67D-0stJ0vdb-JauNviuuPvuR-yICrqR0E1S_mNBtp_DKCDNuD45OnLU2WbZ7bhX/pub?w=960&amp;h=720)

### Register a Domain Name (Optional)
To make your site easy to access, you most likely will want to purchase a domain name. Personally, I like __[Google Domains](https://domains.google.com/)__ because it is simple and easy to track using a service that I use every day. Also, when you are ready it will be easy to turn on Google Workspace (formerly GSuite) for a professional email for your domain.

Once you have obtained the domain name, no additional setup is required until you are ready to point Google's domain name servers at your new site.

### Register for GitHub
More than likely you already have a __[GitHub](https://www.github.com/)__ account but if not, go ahead and get that set up so you can have a source code repository to store your site content.

If you do not know what GitHub is, check out the following helpful material to learn more and get started with GitHub:

  - __[Getting Started with GitHub](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/quickstart)__
  -  __[Hello World](https://guides.github.com/activities/hello-world/)__

### Install Tools:
The steps I show in this article use the command line versus the user interface, so to follow along, go ahead and set up git and authenticate to GitHub via the command line (which will require generating and ssh key and uploading to GitHub). I also recommend installing a project from GitHub called __[hub](https://hub.github.com/)__ which makes it easy to create and manage repositories from the command line.

To simplify management of software on your local machine use a package management tool like __[homebrew](https://brew.sh/)__ on Mac __[chocolatey](https://chocolatey.org/)__ for Windows. I'll show Mac setup since that is the platform I use.  

#### Verify/Install Git:

```plaintext
git --version
```
On Mac, if you don't have git installed you will be prompted to install via XCode which is the simplest option - so just follow the instructions.

Otherwise, Google for the available options for your system.  Once you get a version printed out from the above command, you are ready to move on to the next step.

#### Install Homebrew (Mac):

```plaintext
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
````
Now that you have homebrew, you can install software packages on your local machine.

#### Install Hub:
Hub is a tool provided by GitHub, that allows you to interact with GitHub from the command line. You can accomplish the same actions in the GitHub web user interface, but I prefer to use the command line.

```plaintext
brew install hub
```
#### Install Hugo:
Now, let's install Hugo so we can create a blog!

```plaintext
brew install hugo
```
#### Verify Hugo:
Type the following command on your terminal to verify hugo is installed. At the time of this writing, v0.76.5 is the latest stable version.

```plaintext
hugo version
```

### Create Hugo Site and Theme
Now that you have the necessary tools installed, let's create a directory and generate the initial site. 

#### Create a directory and navigate to the directory:
In this command we will create a directory for your GitHub repositories (or you can use any directory you like) and navigating to that directory.

```plaintext
mkdir github_repositories && cd github repositories
```

#### Create a new site and navigate to the site directory:
The following command creates a new site named *my-new-blog* and navigates to the directory created for the site.

```plaintext
hugo new site my-new-blog && cd my-new-blog
```

#### Create a git repository:
In order to publish our content to GitHub, we must first put it in version control in git (locally). The following commands will create a README markdown file, initialize the current directory as a git repository, add, and commit all contents to version control. At this stage, everything is still managed locally on your machine.

```plaintext
echo "# my-new-blog" >> README.md
git init
git add .
git commit -a -m "initial commit"
```

#### Create a GitHub repository:
To publish our content, we need to leverage a remote repository provided by GitHub.  Let's use *hub*, to create our current directory as a GitHub remote repository.

```plaintext
hub create 
```

#### Push code GitHub
Now that you have a remote repository, we need to push the current commits you have made to the local git repository to our GitHub cloud repository.

```plaintext
git push -u origin HEAD
```

#### Install a Hugo theme:

Hugo needs a theme to display your content, so go ahead select a __[theme](https://themes.gohugo.io/)__ and install it. For demonstration purposes I will use the __[hello-world-ng](https://themes.gohugo.io/hugo-theme-hello-friend-ng/)__ theme. 

Now that you have picked a theeme, we will want to add the theme as a submodule using standard git commands.  This allows git to refer to the repository for your theme of choice. 

```plaintext
git submodule add https://github.com/rhazdon/hugo-theme-hello-friend-ng.git themes/hello-friend-ng
```

If you want to change the theme, you can fork the theme first in Github and then add it as a submodule (changign the url to your own copy of the theme). Either way, it is best to use a submodule so your Github repository for your site is aware of how to get new versions of the theme when it changes (original or your own forked copy).

#### Copy Example Site Content
Most themes will provide example content, to get started quickly let's copy all of that content into the current directory which will include content and a config.toml file.

```plaintext
cp -r themes/hello-friend-ng/exampleSite/* .
```

### Build Content
Hugo understands content types in your theme, so let's create a post for this blog theme using the following command.

```plaintext
hugo new posts/hello-world.md
```

Open up the hello-world.md file in a text editor and add the following text below the generated lines (between --- blocks):

```plaintext
Howdy, this is my first hugo blog. __Hello World!__
```

Notice, Hugo uses a configuration format called frontmatter to configure various elements in your posts - some of which are automatically generated for you based on the type of content you are creating with Hugo. All the configurations are beyond the scope of this article but the key is that by default draft: true is on for new content. This content is only displayed when Hugo is run in draft mode (-D flag). 

Check out this gist to see what it should look like when you are done:

{{<gist jonasmit 3c21da7e88481a8a43306c75b726f71a>}}

#### Run Locally (with drafts)
In order to run a webserver locally to display the blog, execute the following in your terminal.

```plaintext
hugo serve -D
```

The command will produce the url for you to use to see the blog. If you don't have anything else running on the default port (1313), you can browse to your new blog via http://localhost:1313/. 

If successful, you should see a fully functioning site! Remember, some of that content is from the example content from the theme but your Hello World post should also be visible.

![Hello World NG](/hello-world-md.png)

![Hello World NG](/hello-world-posts-md.png)

![Hello World NG](/hello-world-post-md.png)

If you made it this far, Congrats! You now have a fully functioning Hugo blog running locally. 

#### Remove Draft Status
By default, new posts you create are in draft mode. If you publish the content right now, anything with draft:true will not be visible publicly even if you publish your blog to the cloud.  

Stop the web server (Ctrl+C).

Open up your text editor and change the draft status to false.

Now, let's run the hugo web server again without the drafts flag.
```plaintext
hugo serve
```
Check your browser to confirm, but you should see your content in the browser. It is now ready to publish.

#### Push code to GitHub
To get ready to publish your blog to the cloud, let's go ahead and push changes to GitHub.

Stop the web server (Ctrl+C). Now execute the following commands to add new content, commit locally and push to the remote GitHub server.

```plaintext
git add .
git commit -a -m "new post"
git push -u origin HEAD
```

At this stage you have completed almost all the steps in this article:
![Completed Steps](https://docs.google.com/drawings/d/e/2PACX-1vT7tZsQL_bGQDJynRPDF0_yDiK9bhJ2jlhOv2Sma8bElRaP4thLCF-7Xiw7WR6XLYHZKhf6gY5aesSO/pub?w=597&amp;h=201)

In Part 2, I will demonstrate how to wire this blog up to Netlify and publish your blog using the domain name that you registered!