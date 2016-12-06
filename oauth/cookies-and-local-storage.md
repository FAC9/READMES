# What are cookies, how do you create, transport, access and expire them?
# What do you need to do in Hapi to set a cookie?
# How do you get a cookie from a request in Hapi?

# Briefly describe Local Storage and Session Storage (browser api)?
"The Web Storage API provides mechanisms by which browsers can store key/value pairs, in a much more intuitive fashion than using cookies."

Session storage:
- separate storage per window (or tab in browsers like Chrome and Firefox) that is available for as long as the browser is open, including page reloads and restores
Local storage:
- storage that persists until explicitly deleted, even when the browser is closed and reopened

# If using Local Storage to store your users access_token, how do you transport the token to and from your server?
