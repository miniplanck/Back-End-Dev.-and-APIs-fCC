# Request Header Parser Microservice

In this project, we are asked to build a microservice such that:

1. *You should provide your own project, not the example URL;*
2. *A request to `/api/whoami` should return a JSON object with your IP address in the `ipaddress` key;*
3. *A request to `/api/whoami` should return a JSON object with your preferred language in the `language` key;*
4. *A request to `/api/whoami` should return a JSON object with your `software` in the software key.*

### Example

[Example](https://request-header-parser-microservice.freecodecamp.rocks/).

<p align="center" width="100%"><img width="434" alt="Solution" src="https://user-images.githubusercontent.com/73555298/188320816-f3c78702-e4b1-4096-acb2-9f5474cad94f.png">
  </p>

### Relevant Documentation:

[Documentation](https://expressjs.com/en/api.html) and [documentation](https://sailsjs.com/documentation/reference/request-req).

### Solution:

[Solution](https://replit.com/join/oavdjwqaee-minip). The proposed solution segment is properly identified, after accesssing the *index.js* file.

<p align="center" width="100%"><img width="434" alt="Solution" src="https://user-images.githubusercontent.com/73555298/188313263-5e411199-64f1-4905-91f4-1f4dbd2bc6bf.png">
  </p>

### Solution Breakdown:

This project focuses on the `req` parameter. We start by defining a route for the path `/api/whoami`, triggered by the `GET` method. When the `GET` request is sent by the user, the middleware does the following:

- Initiates a variable `ip`, whose value is the ip address of the user. Its value is captured by `req.ip`;
- Initiates a variable `software`, whose value contains the information regarding the software used to access the website. This value can be retrieved by using `req.headers['user-agent']` (cf. the second link for the documentation);
- Initiates a variable `lang`, whose value contains the information regarding preferred language. This value can be retrieved by using `req.headers['accept-language']` (cf. the second link for the documentation);

Lastly, a JSON object is returned in the appropriate configuration.
