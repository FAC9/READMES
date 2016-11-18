# Authentication

## What is authentication and why do we need it when building web applications?

On the most basic level, authentication is needed when a server is set up to not allow access to its files unless passed the correct username and password. The process compares the credentials provided by the client with a database of authorised users.

There are different processes to identify a user on subsequent requests such as cookies and authentication tokens.

The problem with password-based authentication:
- User names are frequently a combination of the individual’s name, which makes them easy to guess.
- If constraints are not imposed, people often create weak passwords and even strong passwords may be stolen, accidentally revealed or forgotten.

#### The three main types of Authentication:
  1. Knowledge factors (password) - a category of authentication credentials consisting of information that the user possesses, such as a personal identification number (PIN), a user name, a password or the answer to a secret question.

  ![alt text](http://securityxploded.com/images/iepassworddecryptor_screenshot_httpauth.jpg)
  2. Possession factors (smart card) - a category of credentials based on items that the user has with them, typically a hardware device such as a security token or a mobile phone used in conjunction with a software token.

  ![text](http://quendororg.s3-website-us-east-1.amazonaws.com/2009/03/token.jpeg)

  3. Inherence factors (biometrics) - a category of user authentication credentials consisting of elements that are integral to the individual in question, in the form of biometric data.

  ![alt text](https://qph.ec.quoracdn.net/main-qimg-4378e70eaf1a767051f4c654503fc23a-c?convert_to_webp=true)

Resources:
- https://blog.risingstack.com/web-authentication-methods-explained/
- https://codingkilledthecat.wordpress.com/2012/09/04/some-best-practices-for-web-app-authentication/
- https://msdn.microsoft.com/en-us/library/ff648647.aspx#c04618429_007

## What are authentication schemes and strategies?

## SSL/TLS Mutual Authentication
This requires a secure channel to be established through digital certificates, before credentials will be shared.

### What is a digital certificate and how are they used?
A digital certificate is an electronic document that proves ownership of a public key. It contains details about the key, the owner and the Certificate Authority (CA) who vouches for its contents.

Every web client has a default collection of hundreds of certificates from major root authorities, and this collection is then included in browsers.
  - Each certificate in the collection is signed by a single authority
  - The signer's own certificate is in turn signed by another authority, each one becoming more widely accepted
  - Finally the root authority's certificate is self-signed and widely distributed

### SSL
1-way (simple) authentication:
The server provides the client with its certificate. The client then verifies it against its own collection, to decide whether the server is trustworthy
The server's certificate is deemed trustworthy by looking at whether:
- the server's certificate is in the client's collection
- the server's certificate has been signed by a CA whose own certificate is in the client's collection - this is the 'chain of trust'
Authentication is successful after 9 of these "handshakes"

2-way (mutual) authentication:
Both parties supply each other with their certificate collections i.e. 1-way auth + the server also receives the client's collection of certificates.
The same process as above is performed by both parties and authentication is successful after 12 handshake messages.

Problems - the following are not scalable:
- 2-way auth only works if all users have a personal digital certificate that is signed by a root CA
- requires the server to import each client's certificate into its trusted certificate store


## HTTP Basic authentication
Sending an encoded username and password on every HTTP request that needs authentication. This is achieved through a dedicated HTTP header.  
But! This method would mean that the user would have to enter their login credentials every single time an HTTP request is sent. The client (i.e. browser) therefore needs to store, or cache, the credentials for a period of time.

Drawbacks:
- fundamentally insecure
- no standard way to log out
- login is not customisable
- requires broswer to cache credentials securely - must be paired with SSL/TLS (see problems above)


## What are some of the different ways Hapi implements authentication?

## Build a small project which demonstrates authentication using Hapi.
