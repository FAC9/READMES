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

### Tutorial on hosting a node.js app

(**Tutorial by scotch.io**)[https://scotch.io/tutorials/how-to-deploy-a-node-js-app-to-heroku]

(**tutorial by heroku**)[https://devcenter.heroku.com/articles/getting-started-with-nodejs#introduction]

Step 1:
Create a node.js application

NOTE: must use 'process.env.PORT' as the port variable

Step 2:
Deploy the add

- 'heroku create' whilst in the git repository.

 Creates a remote repository (called heroku as opposed to our main origin remote repository) so our application knows where to push our deployable code

- Rename the app from its random hyku name.

$ heroku apps:rename heroku-node --app calm-reaches-6216

- can bypass this by setting the name after the heroku create command.

By default, Heroku configures HTTP as the Git transport..you can check using:

$ git remote -v

- If this hasn't happened.. You can also take an existing Git repository and add a remote using the git URL provided when you created your app

To add a Heroku app as a Git remote, you need to execute:

heroku git:remote -a yourapp




- Now that we have everything in order, go ahead and push to Heroku!

$ git push heroku master

This informs git that we would like to push to the newly create heroku repository and the master branch.

- ensure one instance is running

We want to be sure that our app is running. Type the following to get confirmation:

$ heroku ps:scale web=1

- DEFINING A SPECIFIC RUN COMMAND

By default, Heroku will look into our package.json file under the scripts section and grab start. Sometimes we won’t have that defined or it will be different than what we want the server to execute. We can specify the exact command we want by creating a Procfile.

Just create a **Procfile** in the root of your project and define the following:

web: node server.js

This tells Heroku that when deploying to the web, this command should be used to start our application.

### Using a Current Heroku App

If you switch to a different computer and want to access an already existing project. The steps are simple.

Download the Heroku Toolbelt
Login: heroku login
Add your public key: heroku keys:add
Pull down your current application heroku git:clone -a app-name
Make your improvements
Git add and commit your changes
Push back to heroku: git push heroku master

5) Where else could you host your site, what are the pros and cons of other hosting options?
