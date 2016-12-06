# What are Authorisation Scopes?

__Authorization__
- Authorization is the process of giving someone permission to do or have something.

__Authorization scopes__
- A scope is a specific string that indicates a list of permissions
- If you are an app, they let your specify what type of access you need
- If you are a user, they determine what data you give the app permission to access
- Scopes determine which objects / resources the access is granted to, and what type of access it is (e.g. read, write)
- Requested scopes will be displayed to the user on the authorize form
- An example list of authorization scopes for a social network:  
`post_to_my_wall  send_notification  post_to_my_friends_wall  read_my_age`

# How do you  use scopes in Hapi?


# How does the Github API use scopes?

To demonstrate how to define scope when authorising with GitHub, we've recycled one of our projects from Monday.

You can see the new forked version here: https://github.com/shireenzoaby/oauth-workshop

(note that to run the application on your machine, you'll need a registered GitHub app and a config.env file)

The end points for our project are set up in the server.js file in the root. On the /login route, the user is required to authenticate their GitHub account. The code for that looks like this:

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
Now our user is authenticated. The default (no-scope) grants read-only access to public information. This means that the user won't be able to do much with our app. Yet.

What we actually want to do is allow the user to create issues for a GitHub issue via our app. This would require additional permissions from GitHub.

In the query parameters of our 'GET' request, we can specify the permissions we would need.

This is where scope comes in, and it would look like this:

```js
{
  method: 'GET',
  path: '/login',
  handler: (req, reply) => {
    var queryString = querystring.stringify({
      client_id: process.env.CLIENT_ID,
      redirect_uri: process.env.BASE_URL + '/welcome',
      scope: 'user public_repo admin:org	' // <-- this is it!
    });
    reply.redirect('https://github.com/login/oauth/authorize?' + queryString);
  }
}
```
If we go back to our application's login route, GitHub will recognise that our app is now asking for more permissions than the default. The user will be informed of the changes, and will need to authorise access to more information.

When the user confirms again, our app will be able to post to public repos on their behalf.

Read the full docs on scope in GitHub apps here: https://developer.github.com/v3/oauth/#scopes
