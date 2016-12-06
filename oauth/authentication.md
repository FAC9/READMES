# What is two-factor authentication?
# What are the benefits of oAuth?
# How do you write tests for an Authenticated endpoint?

### Why?
You want to ensure certain routes that require authentication are only accessible by users browsers that carry valid cookies in their browsers.
### Method
Set up your server, then use server.inject to inject the authenticated route with a request containing a header that includes a valid cookie (that includes known details about the user).  
- Write a test that expects 200 Status code when the header contains the correct token.
- Write a test that expects a 401 status code when the header contains no cookie/unauthorised cookie.
# How and why should you hash user passwords and sensitive information? (Bcrypt example)
