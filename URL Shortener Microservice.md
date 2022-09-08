# URL Shortener Microservice

In this project, we are asked to build a microservice such that:

1. *You can POST a URL to `/api/shorturl` and get a JSON response with `original_url` and `short_url properties`. Here's an example: `{ original_url : 'https://freeCodeCamp.org', short_url : 1}`;*
2. *When you visit `/api/shorturl/<short_url>`, you will be redirected to the original URL;*
3. *If you pass an invalid URL that doesn't follow the valid `http://www.example.com` format, the JSON response will contain `{ error: 'invalid url' }`.*

### Example

[Example](https://request-header-parser-microservice.freecodecamp.rocks/).

### Relevant Documentation:

[URL properties Documentation](https://developer.mozilla.org/en-US/docs/Web/API/URL#properties).

### Solution:

[Solution](https://replit.com/join/gzbbsaqkua-minip). The proposed solution segment is properly identified, after accesssing the *index.js* file.

<p align="center" width="100%"><img width="434" alt="Solution" src="https://user-images.githubusercontent.com/73555298/188330721-33807964-5d08-4ae1-9fcc-372e8b95f131.png">
  </p>

### Solution Breakdown:

This solution is divided into three main sections:

1. URL Validation;
2. A GET route;
3. A POST route.

The first point can be solved using the provided documentation. Basically, it is a function that tries to emulate a middleware: it accepts three arguments, `req`, `res` and `next`. From the `req` variable, which is already properly parsed (point 2.), it can pull the `url` form `req.body`, from which an instance of the `URL` object is created. This is useful, since we can make use of the property `hostname`, which retrieves the hostname corresponding to a given URL. Then, using `dns.lookup(hostname,callback)` we check for the validity of the hostname: in case it is valid, then we pass to the next function, whereas a JSON string `{error: 'invalid url'}` is returned in case it is invalid.

So as to implement the previously mentioned function, we must mount a POST route in the `/api/shortul` endpoint. We do so with the appropriate function, while using a middleware to make the body parameters of the POST request avaible. Thus, we extract said parameter, and check if its short version is already in the longVsShort object. If not, an entry is created and the JSON object is sent. If, however, it belongs to the object, then we return its short version. **NOTE:** this section of the code could have been implemented with MongoDB, but we decided not to do so since it was not the main topic to be explored in this project. A version v2 proposes an implementation of said approach.

Finally, we mount a GET route at the `/api/shorturl/:shortVersion` endpoint, which basically takes care of redirecting the requests to the appropriate original URLs.
