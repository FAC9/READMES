# Using GitHub

This README introduces GitHub. It covers the distinction between Git and GitHub, the use of labels and milestones on GitHub, how to document a project and how to host a website on GitHub Pages.

## Git versus GitHub

Git and GitHub are two tools that work very well together to track your source code and make it easy to work with others. However, they don't have to be used together and have some important differences.

### Git

Git is a distributed version control system created by Linus Torvalds in 2005 to help manage the Linux kernel's development. Version control software is used to track and share snapshots (known as 'commits') of documents in a 'repository'. Using version control means that you have a full history of changes to your documents and always know what version is the most up-to-date. Here 'distributed' means that each developer working on the repository has a complete copy with the full change history on their computer, with no need to rely on a central server to track changes.

When using Git, you **commit** changes to a branch of the repository. Once you're finished with whatever you were working on the branch can be **merged** back into the central, master branch. This allows multiple people to be working on the same codebase at the same time.

Once you're made your changes you need to share them with your collaborators. They get your updates by **pulling** the changes into their copies of the repository. If there's only a couple you could allow them to ssh into your local repository and pull any changes. But what if you don't know who your collaborators are, or they need to access the repository when your computer is not available? You need to store the repository on a server accessible to everyone. This is where GitHub comes in.

### GitHub

GitHub is a hosting service for Git repositories. By putting your repository on GitHub you enable anyone to access your repository, making it much easier to collaborate with others.

Using GitHub centralises your version control. Each developer **pushes** their changes to the GitHub repository, so that it is always the most up-to-date. Everyone can get the latest changes simply by pulling them from the GitHub repository into their local repo.

Beyond the public hosting service, GitHub's other substantial benefit is that it provides many tools to make it easier to collaborate with other developers. You can easily track bugs and progress, discuss development decisions, raise issues and so on.

A particularly useful addition to the Git workflow is the pull request. A developer commits some code and requests that it is pulled into the main branch. This enables you to review proposed changes and decide whether to accept them.

## Milestones and Labels

### Milestones
Essentially milestones are a way of organising a number of github issues
which need to be resolved by a certain deadline. Once a milestone has been
created, issues can be assigned to it. The idea being that once all these
issues have been resolved, then milestone has been reached.

This is an effective way of tracking progress on a project, and seeing which
issues need to be prioritised for upcoming deadlines.

Milestones could be used for Alpha, Beta, Release etc. Milestones could be
created in a more or less granular fashion as you see fit.

### Labels
Labels are applied to issues, and are fundamentally a categorisation tool. While there are pre-existing labels provided by GitHub, you can create custom labels to fit your needs.

![labels](/images/labelsexample.png)

Labels are extremely simple to create, are prominently displayed on github and can be easily and powerfully filtered. This makes them a very useful tool for developers  working in a team.

### Creating Milestones and Labels
Both Milestones and Labels can be managed under your repo's issues tab.

To create a milestone click on milestone, then on new milestone.

  ![Where to find Milestones](/images/milestones.png)

  Once you have created a milestone and assigned issues to it you will see a
   progress tracker like this.

  ![Progress](/images/milestoneinaction.png)

  As issues are resolved this progress bar will start to fill up. You can click
  on the milestone to see the issues in greater detail


Labels can be created in a similar way, and then added to individual issues.

### An example agile workflow using Milestones and Labels

For each sprint we can create a milestone, which contains the issues that are to be resolved in that sprint.
These issues can be assigned to different developers, and can be labeled with relevant information to help in the easy management of the project.

At the end of the sprint, any unresolved issues can be transfered to a new milestone, and labeled to show their level of priority


## Documenting projects in github
Good documentation is key to the success of any project.
Making documentation accessible enables people to learn about a project;
making it easy to update ensures that documentation stays relevant.

Two common ways to document a project are README files and wikis:

README files are a quick and simple way for other users to learn more about
your work.

Wikis on GitHub help you present in-depth information about your project
in a useful way.

It’s a good idea to at least have a README on your project, because
it’s the first thing many people will read when they first find your
work.

### Creating your README
When you create a new repository though GitHub, select “Initialize this
repository with a README” unless you plan to import an existing repository.
Screenshot of initializing a README

Your README.md file is now available for editing in your brand-new repository.
Your project’s name is at the top, followed by any description you chose to
include when creating the repository. READMEs are easy to modify, both on
GitHub or locally. Check out the Mastering Markdown guide to learn more about
how to modify the text within the file after you’ve made it.

### Creating your wiki
Every repository on GitHub comes with a wiki. After you’ve created a
repository, you can set up the included wiki through the sidebar navigation.
Starting your wiki is simply a matter of clicking the wiki button and
creating your first page.

## Hoisting websites on GitHub Pages

### Introduction
Gt is a version control system that you can use locally on your machine, while GitHub and GitHub Pages hoist projects that use git on their servers.
GitHub Pages host webpages for free through GitHub. GitHub pages can host websites for projects and every GitHub user is allowed to host one personal website. If your files follow a specific naming convention (more on that later) and the files inside use HTML or Markdown, you can view the files like any other website.

### Step-by-step tutorial for creating a website on GitHub Pages

All the files that build up your site need to be stored on your GitHub account. All we have to do is to push your repository to the ```gh-pages``` branch then GitHub automatically handles the publishing of your site.

### Automatic page genaration

1. Create a new repository with any name.

 ![create a new repo](/images/github_pages_01.png)

2. Go to ```Settings```. Scroll down and choose ```Automatic Page Generator```. It will automatically generate a front page for your site.
  ![launch autmoatic page generator](/images/github_pages_02.png)

3.  ![new project site](/images/github_pages_03.png)

4.   ![continue to layouts](/images/github_pages_04.png)

5. You can choose from sevveral layyouts.

 ![layouts](/images/github_pages_05.png)

6. Look you site online at ```http://yourusername.github.com/repo-name```

![github repo](/images/github_pages_06.png)

7.   Bear in mind, that for the first launch it might not work inadvance!

![error](/images/github_pages_07.png)

8. It is live!

![working page](/images/github_pages_08.png)

### Manual page generation

>Remember to save  your site on your ```gh-pages``` branch. If you add your site to the ```master``` branch GitHub will smiply ignore it. The ```gh-pages```  branch name is a sign for GitHub to start searching for a website.

1. Create a new repository on GitHub.
![create a new repo](/images/github_pages_01.png)

2. Clone the repo to your computer
```
$ git clone https://github.com/denesnori/test-page2
Cloning into 'test-page2'...
warning: You appear to have cloned an empty repository.
Checking connectivity... done.
```

3. Create a new branch for your site  
```
$ git checkout -b gh-pages
Switched to a new branch 'gh-pages'
$ git status
On branch gh-pages
Initial commit
nothing to commit (create/copy files and use
   'git add' to track)
```

4. You have to manually add all the files for your site. There is page where you can download
[minimal site sources](https://github.com/stevenfarlie/blank/zipball/gh-pages)
```
$ git add index.html site.css site.js
$ git commit -m 'test-page2 for GitHub Pages'
[gh-pages (root-commit) 41f0a06] test-page2 for GitHub Pages
 3 files changed, 46 insertions(+)
 create mode 100644 index.html
 create mode 100644 site.css
 create mode 100644 site.js
```

5. push your branch to GitHub.
```
$ git push origin gh-pages
Counting objects: 5, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 987 bytes | 0 bytes/s, done.
Total 5 (delta 0), reused 0 (delta 0)
```

6.  Visit you website on GitHub pages.
```http://yourusername.github.io/repo-name```


## References

1.  [jmcglone.com](http://jmcglone.com/guides/github-pages/)
2.  [teamtreehouse tutorial](http://blog.teamtreehouse.com/using-github-pages-to-host-your-website)
3.  [opentechsvhool tutorial](http://opentechschool.github.io/social-coding/extras/pages.html)
