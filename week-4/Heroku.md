# Heroku

## What is it

  Heroku lets you deploy, run and manage **applications.** written a number of languages, including Node.js

  An **application** is a collection of source code along with a description of it dependencies.

  GitHub pages are good for static webpages and **Heroku** is better for **dynamic webpages** (front AND back-end)

## Git and Heroku

  Heroku also uses git as a version control. WWhen you create an application on Heroku, it associates a new git remote, typically named heroku, with the local git repository for your application. You can use
  ```
  git push heroku master
  ```

  In addition Heroku allows for [Github Integration](https://devcenter.heroku.com/articles/github-integration). Once your Heroku project is connected to a github project you can selectively deploy, or configure heroku to get and deploy your code updates automatically. In addition you can configure to Heroku to only deploy code that passes continuous integration testing run by a service such as Travis


## How you get into a Herokrew
In a git folder type
```
heroku create
```
This will create a Heroku page with a bizarre haiku esque name. (limitless savannah, profound eagle, whipsering clooney, etc)

Use the command
```
git push heroku master
```
This will push your work onto heroku, which will attempt to build your application. It will install your NPM dependencies, then if all goes well your site should be live!


## What's a procfile

A procfile is a file that tells Heroku how to run your application.

A basic procfile might contain the following code.
```
web: node server.js
```
This tells heroku which server file should handle web traffic.

## Heroku comes with its own command-line interface. What are the most useful commands to know?
```
heroku create //makes a new heroku app
heroku open //opens your current app in the browser
heroku help //helps?!
```
## How to host an application

You shouldn't need to make many major changes to your application in order to run it on Heroku.

You do however need to ensure that you are listening on the correct server.
```
var port = (process.env.PORT || 3000)
```
