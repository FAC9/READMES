# Validation

### What is validation and why is it important (absolutely critical)?

- Validation is where you check user inputs match the type or format and length that you expect (and therefore can work with). For example, checking that a telephone number is a specific length and is composed only of digits.

- Front-end vs back-end validation:
  - Resource: https://en.wikipedia.org/wiki/Data_validation
  - Main points:
    * Data validation checks for fitness, accuracy and consistency for various kinds of user inputs into an application.
    * Bad inputs will negatively affect business process execution.
    * Implementation can be part of the user-interface or stored procedures in the database management system.

- Security issues
  - Validation is critical to stop script injections running malicious code in your database management system.
  - Failures in data validation can lead to data being corrupted and security issues. Validation ensures that data is valid, sensible and secure before being processed.

### What is Joi and how would you use it with Hapi?

#### How does validation work in Hapi?

1 - Input validation

Input validation can be set by rules in the `config` object on a route (`server.route`).

|Input parameter    | Parameter passed in the `config` object |
|-------------------|-----------------------------------------|
|path parameters    |`validate.params`                        |
|query parameters   |`validate.query` (*note:* if you specify validation rules for one query parameter you **must** then validate all query parameters)                       |
|headers    |`validate.headers`                        |
|body data    |`validate.payload` (*note:* if you specify validation rules for one query parameter you **must** then validate all query parameters)                      |

2 - Output validation

Input validation can be set by rules in the `response` property of the `config` object on a route (`server.route`). If the response does not pass the specified validation, a 500 (Internal Server Error) response will be sent to the client.

#### What is Joi?

- Joi is a validation library built by the same team as Hapi, and it can be used in conjunction with Hapi or separately. You would use it with Hapi by requiring it (it's a module).

- Joi allows you to create your validations with a simple and clear object syntax.

- Resources:
  * [Egghead tutorial](https://egghead.io/lessons/node-js-hapi-js-request-validation-with-joi)
  * [Hapi-Joi turorial](https://github.com/hapijs/joi)


### Create a small project demonstrating some example situations where you'd use Joi.

Set up some validation schemas for these examples. The hapi.js validation tutorial may be of use to you.

An example validation project can be found [here](https://github.com/FAC9/validation-project/).
