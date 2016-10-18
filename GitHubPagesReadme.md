# Hoisting websites on GitHub Pages

## Introduction
Gt is a version control system that you can use locally on your machine, while GitHub and GitHub Pages hoist projects that use git on their servers.
GitHub Pages host webpages for free through GitHub. GitHub pages can host websites for projects and every GitHub user is allowed to host one personal website. If your files follow a specific naming convention (more on that later) and the files inside use HTML or Markdown, you can view the files like any other website.

## Step-by-step tutorial for creating a website on GitHub Pages

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

[error](/images/github_pages_07.png)

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
```http://yourusername.github.com/repo-name```


## References
1.  [jmcglone.com](http://jmcglone.com/guides/github-pages/)
2.  [teamtreehouse tutorial](http://blog.teamtreehouse.com/using-github-pages-to-host-your-website)
3.  [opentechsvhool tutorial](http://opentechschool.github.io/social-coding/extras/pages.html)
