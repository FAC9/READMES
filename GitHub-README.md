Git versus GitHub
=================

Git and GitHub are two tools that work very well together to track your source code and make it easy to work with others. However, they don't have to be used together and have some important differences.

## Git

Git is a distributed version control system created by Linus Torvalds in 2005 to help manage the Linux kernel's development. Version control software is used to track and share changes (known as 'commits') to documents in a 'repository'. Using version control means that you have a full history of changes to your documents and always know what version is the most up-to-date. Here 'distributed' means that each developer working on the repository has a complete copy with the full change history on their computer, with no need to rely on a central server to track changes.

When using Git, you commit changes to a branch of the repository. Once you're finished with whatever you were working on the branch can be merged back into the central, master branch. This allows multiple people to be working on the same codebase at the same time.

Once you're made your changes you need to share them with your collaborators. If there's only a couple you could allow them to ssh into your local repository and pull any changes. But what if you don't necessarily know who your collaborators will be, or they need to access the repository when your computer is not available? You need to store the repository on a server accessible to everyone. This is where GitHub comes in.


## GitHub

GitHub is a hosting service for git repositories created in 2007. The main benefit of putting your repository on GitHub is to make collaboration easier.

Though you can use git without GitHub, it is difficult for other people to konw about your project and contribute to it. GitHub allows anyone to clone or fork your project and gives you an easy way to keep the public version up to date.

As well as the basic hosting service, GitHub offers additional tools to make collaborating easier. These include bug tracking, feature requests, pull requests and so on.
