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

## What are authentication schemes and strategies?

### SSL/TLS Mutual Authentication
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

SCHEMES

A scheme is a general type of authentication like ```basic``` and ```digest```. You can think of a scheme as a template for authentication. A scheme isn’t used directly to authenticate users, instead you create a specific strategy from the scheme.

STRATEGIES

A strategy is a configured instance of a scheme with an assigned name. Strategies exist so you can use the same scheme several times, in a slightly different way. For instance, might decide to you want use basic authentication in your app. For some routes you might wish to validate a user’s passwords against a value in a database and for some other routes, you might wish to check the password against a value stored in a text file. In this case you can create 2 different strategies from the scheme. The scheme to strategy relationship is described visually below:

![scheme_strategies](./images/scheme_strategies.png)

### One-way encryption of user passwords with Bcrypt


 We have to make sure that the password is always encrypted before being saved.

>In cryptography, a salt is random data that is used as an additional input to a one-way function that "hashes" a password or passphrase.  The primary function of salts is to defend against dictionary attacks or against its hashed equivalent, a pre-computed rainbow table attack.
>
>A new salt is randomly generated for each password.
>
> In a typical setting, the salt and the password (or its version after Key stretching) are concatenated and processed with a cryptographic hash function, and the resulting output (but not the original password) is stored with the salt in a database. Hashing allows for later authentication without keeping and therefore risking the plaintext password in the event that the authentication data store is compromised.

>Since salts do not have to be memorized by humans they can make the size of the rainbow table required for a successful attack prohibitively large without placing a burden on the users. Since salts are different in each case, they also protect commonly used passwords, or those who use the same password on several sites, by making all salted hash instances for the same password different from each other.

> From Wikipedia

genSalt(rounds, callback)
- rounds - [OPTIONAL] - the number of rounds to process the data for. (default - 10)
- callback - [REQUIRED] - a callback to be fired once the salt has been generated.
  - error - First parameter to the callback detailing any errors.
  - result - Second parameter to the callback providing the generated salt.

hash(data, salt, progress, cb)
- data - [REQUIRED] - the data to be encrypted.
- salt - [REQUIRED] - the salt to be used to hash the password.
- progress - a callback to be called during the hash calculation to signify progress
- callback - [REQUIRED] - a callback to be fired once the data has been encrypted.
  * error - First parameter to the callback detailing any errors.
  * result - Second parameter to the callback providing the encrypted form.

compare(data, encrypted, cb)
- data - [REQUIRED] - data to compare.
- encrypted - [REQUIRED] - data to be compared to.
-  callback - [REQUIRED] - a callback to be fired once the data has been compared.
  - error - First parameter to the callback detailing any errors.
  - result - Second parameter to the callback providing whether the data and encrypted forms match [true | false].

  > Bcrypt.compare(candidate_plain_text_password, hash, callback) compares the candidate password provided in
  > plain text with a given hash. You don’t need to hash your candidate before checking if they match.

```
var Bcrypt = require('bcrypt');
var SALT_WORK_FACTOR = 10;
var pass = '123456789';

Bcrypt.genSalt(SALT_WORK_FACTOR, function(err, salt) {
        if(err) {
                return console.error(err);
        }

        Bcrypt.hash(pass, salt, function(err, hash) {
                if(err) {
                        return console.error(err);
                }

                console.log(hash);

                Bcrypt.compare(pass, hash, function(err, isMatch) {
                        if(err) {
                                return console.error(err);
                        }

                        console.log('do they match?', isMatch);
                });

        });
});
```
## Authentication example

- hapi-auth-basic is plugin (you have to register plugins)

To create an authentication strategy for your hapi server, leverage the server.auth.strategy(name, scheme, options) function that expects three (optionally four) parameters:

- name: your strategy name that will be used throughout your app
- scheme: the scheme name on which the strategy is based upon (e.g. basic)
- options: additional options

validateFunc. That’s a function with the signature function(request, username, password, callback), where

- request: is the hapi request object which requires authentication
- username: username send by the client
- password: password send by the client
- callback: with the signature function(err, isValid, credentials)
  *  err: internal error object that replaces the default Boom.unauthorized if defined
  *  isValid: boolean that indicates if the username was found and passwords match
  * credentials: user’s credentials, only included if isValid is true

```
const hapi = require('hapi');
const server = new hapi.Server();
const BasicAuth = require('hapi-auth-basic');
const Bcrypt = require('bcrypt');

var users = {
  future: {
    id: '1',
    username: 'future',
    password: '$2a$04$YPy8WdAtWswed8b9MfKixebJkVUhEZxQCrExQaxzhcdR2xMmpSJiG'  // 'studio'
  }
}

server.connection({
  host: 'localhost',
  port: 5000
});

server.register(BasicAuth, function(err){
   if (err) throw err;
  var basicValidation = function(request,username,password,callback){
    var user = users[username];
    if (!user) return callback(null,false);
    console.log(user.username,user.password);
    Bcrypt.compare(password,user.password, function(err,isValid){
      callback(err, isValid, { id: user.id, username: user.username });
    });
  };
  server.auth.strategy('simple','basic', {validateFunc:basicValidation})


  server.route({
    method: 'GET',
    path: '/private-route',
    config: {
      auth: 'simple',
      handler: function (request, reply) {
        reply('Yeah! This message is only available for authenticated users!')
      }
    }
  });

  server.start(function(err){
    if (err) throw err;
    console.log(`Server is running at port ${server.info.uri}`);
  });

});

```

## References
- [devsmash](http://devsmash.com/blog/password-authentication-with-mongoose-and-bcrypt)
- [soledadpenades](https://soledadpenades.com/2015/01/03/hashing-passwords-with-bcrypt-and-node-js/)
- [npm-bcrypt](https://www.npmjs.com/package/bcrypt-nodejs)
- [futurestud](https://futurestud.io/tutorials/hapi-basic-authentication-with-username-and-password)
- [dwyl/learn-json-webtokens](https://github.com/dwyl/learn-json-web-tokens)
- [hapi-auth-basic](https://github.com/hapijs/hapi-auth-basic)
- [risingstack](https://blog.risingstack.com/web-authentication-methods-explained/)
- [codingkilledthecat](https://codingkilledthecat.wordpress.com/2012/09/04/some-best-practices-for-web-app-authentication/)
- [msdn microsoft](https://msdn.microsoft.com/en-us/library/ff648647.aspx#c04618429_007)
