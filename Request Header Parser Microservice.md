# Request Header Parser Microservice

In this project, we are asked to build a microservice such that:

1. *You should provide your own project, not the example URL;*
2. *A request to `/api/whoami` should return a JSON object with your IP address in the `ipaddress` key;*
3. *A request to `/api/whoami` should return a JSON object with your preferred language in the `language` key;*
4. *A request to `/api/whoami` should return a JSON object with your `software` in the software key.*

### Example

### Relevant Documentation:

[Documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date).

### Solution:

[Solution](https://replit.com/join/leuyabzstx-minip). The proposed solution segment is properly identified, after accesssing the *index.js* file.

<p align="center" width="100%"><img width="434" alt="Solution" src="https://user-images.githubusercontent.com/73555298/188279004-5905db6a-1037-4432-95b6-f859ea21cb79.png">
  </p>

### Solution Breakdown:

We start by creating a route for a GET method to path `.../api/:date?`, where `:date` is the *route parameter*. It is necessary to take into account four separate cases:

- `:date` is an empty string, in which case request.params.date is *undefined*;
- `:date` is an invalid date string;
- `:date` is a valid date string in the unix format. In that case, it is the string form of a number;
- `:date` is a valid date string in any other format;

In any of the last three cases, the request.params object has a key with a well *defined* value. Let us start by the first case of the `if` chain.

If `:date` is an empty string (6. and 7.), then the server must return a JSON object with the keys *unix* and *utc*, whose values are the current time in the unix and utc format, respectively. Thus, we check fr the empty condition by using the sentence `typeof req.params.date === "undefined"`. In that case, we initiate a new instance of the `Date()` object, `result`, and return the desired JSON object: for the first entry, we use `Date.now()` which "Returns the numeric value corresponding to the current time (...)" (unix format); regarding the second entry, one applies the `.toUTCString()` method so as to return the proper utc format.

Secondly, there is the possibility that :date is not a valid input string (5.). By invalid we mean a string composed of only numbers or a string of a non-standard combination of characters. However, the first case should return a date, as per requested in 3. Thus, if the string is parsed into a number then it is not a proper Invalid Date. So as to captue the second case, therefore, we can check the value of an instance of the `Date()` object, denoted by `test`. If `test` is an *Invalid Date* (first condition in the second if statement), we should check whe ther it can be parsed into a number. In case it does not, then it is an Invalid Date in the true sense, in which case the server sends the object `{error: "Invalid Date"}`.

In order to capture the "improper" Invalid Date, step 3., we must check if the request.params.date is a non-empty string (which can be discarded, since the empty string should trigger the first `if` statement) and if is is a number. If that is the case, then `request.params.date` is the millisecond representaiton of a date - unix format- and we retrieve a JSON object in the desired format (1. and 2.).

Lastly, we present the piece of code that takes care of the valid date formats. An instance of `Date()` is initiated and its utc and unix format is obtained by using the appropriate methods, `.toUTCString()` and `Date.parse((...))`. Finally, a JSON object is sent.
