# What are Authorisation Scopes?

__ Authorization __
- Authorization is the process of giving someone permission to do or have something.

__ Authorization scopes __
- A scope is a specific string that indicates a list of permissions
- If you are an app, they let your specify what type of access you need
- If you are a user, they determine what data you give the app permission to access
- Scopes determine which objects / resources the access is granted to, and what type of access it is (e.g. read, write)
- Requested scopes will be displayed to the user on the authorize form
- An example list of authorization scopes for a social network:  
`post_to_my_wall  send_notification  post_to_my_friends_wall  read_my_age`

# How do you  use scopes in Hapi?


# How does the Github API use scopes?

To demonstrate how to define scope when authentication with GitHub, we've recycled one of our projects from Monday.

You can see the new forked version here:

(note that to run the application on your machine, you'll need the config.env file)

In the server.js file of our project are the different end points. On the /login path, the user is required to authenticate their GitHub account. We do so like this:

```js
{
  method: 'GET',
  path: '/login',
  handler: (req, reply) => {
    var queryString = querystring.stringify({
      client_id: process.env.CLIENT_ID,
      redirect_uri: process.env.BASE_URL + '/welcome'
    });
    reply.redirect('https://github.com/login/oauth/authorize?' + queryString);
  }
}
```
Now our user is authenticated, but by default GitHub grants only limited access. The default (no-scope) grants read-only access to public information (includes public user profile info, public repository info, and gists). This means that the user won't be able to do much with the app. Yet.

In order to get access to the user's repos, we have to specify what access rights we need as a query parameter in our Get request to GitHub.

That would look like this:

```js
{
  method: 'GET',
  path: '/login',
  handler: (req, reply) => {
    var queryString = querystring.stringify({
      client_id: process.env.CLIENT_ID,
      redirect_uri: process.env.BASE_URL + '/welcome',
      scope: 'user public_repo admin:org	'
    });
    reply.redirect('https://github.com/login/oauth/authorize?' + queryString);
  }
}
```
If we go back to our application's login route, GitHub will recognise that our app is now asking for more permissions than the default. This requires additional authentication from the user.

When the user authenticates again, our app will be able to post to public repos on their behalf.

Read the full docs on scope in GitHub apps here: https://developer.github.com/v3/oauth/#scopes
