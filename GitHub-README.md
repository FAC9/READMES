Git versus GitHub
=================

Git and GitHub are two tools that work very well together to track your source code and make it easy to work with others. However, they don't have to be used together and have some important differences.

## Git

Git is a distributed version control system created by Linus Torvalds in 2005 to help manage the Linux kernel's development. Version control software is used to track and share snapshots (known as 'commits') of documents in a 'repository'. Using version control means that you have a full history of changes to your documents and always know what version is the most up-to-date. Here 'distributed' means that each developer working on the repository has a complete copy with the full change history on their computer, with no need to rely on a central server to track changes.

When using Git, you **commit** changes to a branch of the repository. Once you're finished with whatever you were working on the branch can be **merged** back into the central, master branch. This allows multiple people to be working on the same codebase at the same time.

Once you're made your changes you need to share them with your collaborators. They get your updates by **pulling** the changes into their copies of the repository. If there's only a couple you could allow them to ssh into your local repository and pull any changes. But what if you don't know who your collaborators are, or they need to access the repository when your computer is not available? You need to store the repository on a server accessible to everyone. This is where GitHub comes in.

## GitHub

GitHub is a hosting service for Git repositories. By putting your repository on GitHub you enable anyone to access your repository, making it much easier to collaborate with others.

Using GitHub centralises your version control. Each developer **pushes** their changes to the GitHub repository, so that it is always the most up-to-date. Everyone can get the latest changes simply by pulling them from the GitHub repository into their local repo.

Beyond the public hosting service, GitHub's other substantial benefit is that it provides many tools to make it easier to collaborate with other developers. You can easily track bugs and progress, discuss development decisions, raise issues and so on.

A particularly useful addition to the Git workflow is the pull request. A developer commits some code and requests that it is pulled into the main branch. This enables you to review proposed changes and decide whether to accept them.
