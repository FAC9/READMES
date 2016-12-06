# What is two-factor authentication?
# What are the benefits of oAuth?
# How do you write tests for an Authenticated endpoint?

### Why?
You want to ensure certain routes that require authentication are only accessible by users browsers that carry valid cookies in their browsers.
### Method
Set up your server, then use server.inject to inject the authenticated route with a request containing a header that includes valid credentials (that includes known details about the user).  
For test example, see [here](https://github.com/njsfield/authentication-test/blob/master/README.md)
# How and why should you hash user passwords and sensitive information? (Bcrypt example)
