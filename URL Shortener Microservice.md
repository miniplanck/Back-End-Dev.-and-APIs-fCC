# URL Shortener Microservice

In this project, we are asked to build a microservice such that:

1. *You should provide your own project, not the example URL;*
2. *You can `POST` a URL to `/api/shorturl` and get a JSON response with `original_url` and `short_url properties`. Here's an example: `{ original_url : 'https://freeCodeCamp.org', short_url : 1}`;*
3. *When you visit `/api/shorturl/<short_url>`, you will be redirected to the original URL;*
4. *If you pass an invalid URL that doesn't follow the valid `http://www.example.com` format, the JSON response will contain `{ error: 'invalid url' }`.*

### Example

[Example](https://request-header-parser-microservice.freecodecamp.rocks/).

### Relevant Documentation:

[Documentation](https://expressjs.com/en/api.html) and [documentation](https://sailsjs.com/documentation/reference/request-req).

### Solution:

[Solution](https://replit.com/join/oavdjwqaee-minip). The proposed solution segment is properly identified, after accesssing the *index.js* file.

<p align="center" width="100%"><img width="434" alt="Solution" src="https://user-images.githubusercontent.com/73555298/188313263-5e411199-64f1-4905-91f4-1f4dbd2bc6bf.png">
  </p>

### Solution Breakdown:
