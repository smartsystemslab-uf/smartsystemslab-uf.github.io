# Documentation

This page is meant help everyone understand GitHub and the setup of our new lab website as well as how to add/edit project and news pages.

## Main Points

- The first requirement is a GitHub account for accessing the git repository for the website. Please send Taylor Whitaker an email containing your GitHub username so that you can be added as a contributor.

- Once you are added to the repo, you will be able to write to the repo located at: [https://github.com/smartsystemslab-uf/smartsystemslab-uf.github.io](https://github.com/smartsystemslab-uf/smartsystemslab-uf.github.io)

- You can edit directly on the website or you can clone the repository to your own computer so that you can start to make and edit your own project pages. This requires either a command line interface or desktop client, like the [GitHub Desktop application](https://desktop.github.com)

- The master branch of the repo is locked and so everyone will have their own branch. If editing on the website, you can select your branch you wish to make changes to on the tool bar like below with "ExampleBranch." Otherwise, you will have to make commits to the appropriate branch with the command line or desktop client. Once added to the repo, you will have a branch named after you created for you.

<p align="center"> <img width="640" src="https://github.com/smartsystemslab-uf/smartsystemslab-uf.github.io/blob/master/Docs/ChangingBranchesWithOnlineEditor.png?raw=True"/> </p>

- Changes that are made to each branch will not show up on the website until a pull-request is submitted. You may do this yourself if you know how, or can send an email to Taylor Whitaker to finalize the changes.


## Repository Directories

There are a number directories in the website repo. These are the important ones:

- Docs
- News
- Projects

This website is automatically generated for us, we just have to provide the text and a little bit of text styling. These folders hold the content of the webpages that we will see. All pages require their own directories that contain a README.md file. The README.md files are built with the markdown language and will be automatically generated into a webpage. This page is an example of such. The source can be found in the docs folder [HERE](https://github.com/smartsystemslab-uf/smartsystemslab-uf.github.io/blob/master/Docs/). The actual webpage that is produced can be seen at [https://smartsystemslab-uf.github.io/Docs/](https://smartsystemslab-uf.github.io/Docs/). The URL of the webpage closely matches the directory path to the README.md file.


### Docs

This folder holds this README.md file and two folders, Template and MarkdownConventions.

The Template folder holds the template that should be used for your README.md files. [Source File](https://github.com/smartsystemslab-uf/smartsystemslab-uf.github.io/blob/master/Docs/Template/README.md) - [Generated Webpage](https://smartsystemslab-uf.github.io/Docs/Template/)

The MarkdownConventions folder holds a few examples of what styling you can use in a README.md file. [Source File](https://github.com/smartsystemslab-uf/smartsystemslab-uf.github.io/blob/master/Docs/MarkdownConventions/README.md) - [Generated Webpage](https://smartsystemslab-uf.github.io/Docs/MarkdownConventions/)


### Projects

This folder holds all the project pages. Every project needs its own directory that will contain a README.md file for the content and an images folder for any images used. Take a look at some of the existing project folders and the resulting pages. You can use [the template README.md](https://github.com/smartsystemslab-uf/smartsystemslab-uf.github.io/tree/master/Docs/Template) file to start writing your content.

Since changes are not immediately added to the actual website, you need to be able to see how it will end up looking. With all pages being written as a README.md, you can see how the page will look when accessing the repo via GitHub.com and navigating to your project folder.


### News

Coming soon...
