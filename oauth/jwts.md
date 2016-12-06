# What is a JWT?

## Abstract definition
> A JSON Web Token (JWT) is a JSON object that is defined in RFC 7519 as a safe way to represent and transmit a set of
> information between two parties. The token is composed of a header, a payload, and a signature.

## JWT format
```
header.payload.signature
```
## How and why JWTs are used
![jwt explained](./jwts-images/jwt.png)

## JWTs - common characteristics

- JWTs are used across several programming languages .NET, Python, Node.js, Java, PHP, Ruby, Go, JavaScript, and Haskell.

- JWTs are self-contained: self-contained means that the payload contains all the necessary infomation about the user, avoiding to query the database more than once.

- JWTs are versatile and can be passed around easily. They are small, they can be sent through URL, POST parameters, or inside an HTTP header.  

## When should you use JSON Web Tokens?

- Authentication: the most common use of JWTs. After logging in, each subsequent request will include the JWT, allowing the user to access the routes and services that are allowed with that token.

- Information Exchange: JWTs can be used to securely transmit information between parties, since they can be signed e.g.: using public/private key pairs. The signature is determined based on both the header and the payload using a hashing algorithm, so you can check that the content hasn't been tampered with.

# How do you create a JWT?
### Breaking down a JSON Web Token
The format of a JSON Web Token consists of three strings separated by `.` :
![JWT basic signature](./jwts-images/jwt-signature.png)
Each of the three sections of a JWT can be created separately as described below.

#### Big word alert: Encoding vs Encryption
- **Encoding** is data transformation and the goal is not to keep the data secret but to ensure the data has the right format for proper consumption.

*Example:*
```javascript
querystring.stringify({"url": "http://domain.com"});
// outputs 'url=http%3A%2F%2Fdomain.com'

```
-  **Encryption** is data transformation where the goal is to ensure that data cannot be consumed by any other user except for the intended recipients.

*Example:*  
A hashing algorithm or in practice, the `bcrypt` Node module to encrypt user passwords.

#### Create a JWT in three steps:

##### 1) Create header (algorithm and token type) using encoding

Example (JSON object - remove comments before using)
```javascript
{
  // declare type of header
  "typ": "JWT",
  // define the hashing algorithm
  // in this case HMAC - SHA256
  "alg": "HS256"
}
```
*Note*: In order for the transmitted information to be verified, it has to be digitally signed. JWTs can be signed using a secret (with HMAC algorithm) or a public/private key pair using RSA.

If you then `base64UrlEncode` (this is not a built-in JavaScript function) the header json object, you get the string `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9` for the first part of the JWT.

##### 2) Create payload (bulk of information) using encoding
It can contain reserved, public and private claims (i.e. statements about different entities such as the user and additional metadata).  

*Example (JSON object - remove comments before using)*
```javascript
{
  // reserved claim for the issuer of the token
  "iss": "scotch.io",
  // Registered claim - expiration in NumericDate value.
  // The expiration MUST be after the current date/time.
  "exp": 1300819380,
  // public claim
  "name": "Chris Sevilleja",
  // public claim
  "admin": true
}
```
*Note*: private claims have to be agreed between a producer and a consumer. Use with caution as these are subject to collision.

If you then `base64UrlEncode` (this is not a built-in JavaScript function) the payload json object, you get the string `eyJpc3MiOiJzY290Y2guaW8iLCJleHAiOjEzMDA4MTkzODAsIm5hbWUiOiJDaHJpcyBTZXZpbGxlamEiLCJhZG1pbiI6dHJ1ZX0` for the second part of the JWT.

##### 3) Create signature using encryption and encoding  
You take the encoded header, the encoded payload and using the algorithm specified in the header, you generate a secret, encode all components and sign the JWT.

*Example (JSON object - remove comments before using)*   
```javascript
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  'secret')
```
The snippet above generates the third part of the JWT, which is the signature held by the server to verify existing tokens and sign new ones: `03f329983b86f7d9a9f5fef85305880101d5e302afafa20154d094b229f75773`

Combining all three parts above, the JWT looks like this:
`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzY290Y2guaW8iLCJleHAiOjEzMDA4MTkzODAsIm5hbWUiOiJDaHJpcyBTZXZpbGxlamEiLCJhZG1pbiI6dHJ1ZX0.03f329983b86f7d9a9f5fef85305880101d5e302afafa20154d094b229f75773
`
# How do you decode a JWT?    
```javascript
const jwt = require('json-web-token');
var secret = process.env.JWT_SECRET;

    jwt.decode(secret, token, function (err, decodedJWT) {
      if (err) {
        return console.log(err, 'There was an error decoding');
      } else {
        console.log(decodedJWT);
      }
    });

    <!-- token is the JWT you are trying to decode -->
```

[Check out this cool resource](http://calebb.net/)  to see what a decoded JWT looks like before and after.

To see the full example this code snippet came from, [look here.](https://www.npmjs.com/package/json-web-token)

# How do you use the module `hapi-auth-jwt2`?   
`hapi-auth-jwt2` is the authentication scheme for Hapi.js apps using JWTs.

For a full walk-through [see DWYL's excellent README](https://github.com/dwyl/hapi-auth-jwt2).

```javascript
var people = { // our "users database"
    1: {
      id: 1,
      name: 'Jen Spencer'
    }
};

// Our own validation function
var validate = function (decoded, request, callback) {

    // do your checks to see if the person is valid
    if (!people[decoded.id]) {
      return callback(null, false);
    }
    else {
      return callback(null, true);
    }
};

var server = new Hapi.Server();
server.connection({ port: 8000 });
  // ** INCLUDE MODULE HERE ↓↓ **
server.register(require('hapi-auth-jwt2'), (err) => {
  if(err){ console.log(err);
  }

  server.auth.strategy('jwt', 'jwt',
    { key: process.env.JWT_SECRET,         
      validateFunc: validate,            // validate function defined above
      verifyOptions: { algorithms: [ 'HS256' ] } // pick a strong algorithm
    });

    server.auth.default('jwt');

    server.route([
      {
        method: "GET",
        path: "/",
        config: { auth: false },
        handler: function(request, reply) {
          reply({text: 'Token not required'});
        }
      },
      {
        method: 'GET',
        path: '/restricted',
        config:{ auth: 'jwt' },
        handler: function(request, reply){
          reply({text: 'You used a Token!'})
          .header("Authorization", request.headers.authorization);
        }
      }
    ]);
});

server.start(function () {
  console.log('Server running at:', server.info.uri);
});
```

### Resources
- [Medium article on jwt](https://medium.com/vandium-software/5-easy-steps-to-understanding-json-web-tokens-jwt-1164c0adfcec#.fl1xahvou)
- [The anatomy of a JSON web token](https://scotch.io/tutorials/the-anatomy-of-a-json-web-token)
- [Learn about JSON web tokens](https://auth0.com/learn/json-web-tokens/)
- [jwtt.io](https://jwt.io/)
- [encoding vs encryption](https://danielmiessler.com/study/encoding-encryption-hashing-obfuscation/#encoding)
