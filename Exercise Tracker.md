# Exercise Tracker

In this project, we are asked to build a microservice such that:

1. *You can `POST` to `/api/users` with form data `username` to create a new user;*
2. *The returned response from `POST /api/users` with form data `username` will be an object with `username` and `_id` properties;*
3. *You can make a `GET` request to `/api/users` to get a list of all users;*
4. *The `GET` request to `/api/users` returns an array;*
5. *Each element in the array returned from `GET /api/users` is an object literal containing a user's `username` and `_id`;*
6. *You can `POST` to `/api/users/:_id/exercises` with form data `description`, `duration`, and optionally `date`. If no date is supplied, the current date will be used;*
7. *The response returned from `POST /api/users/:_id/exercises` will be the user object with the exercise fields added;*
8. *You can make a `GET` request to `/api/users/:_id/logs` to retrieve a full exercise log of any user;*
9. *A request to a user's log `GET /api/users/:_id/logs` returns a user object with a `count` property representing the number of exercises that belong to that user;*
10. *A `GET` request to `/api/users/:_id/logs` will return the user object with a log array of all the exercises added;*
11. *Each item in the log array that is returned from `GET /api/users/:_id/logs` is an object that should have a `description`, `duration`, and `date` properties;*
12. *The `description` property of any object in the log array that is returned from `GET /api/users/:_id/logs` should be a string;*
13. *The `duration` property of any object in the log array that is returned from `GET /api/users/:_id/logs` should be a number;*
14. *The `date` property of any object in the log array that is returned from `GET /api/users/:_id/logs` should be a string. Use the `dateString` format of the `Date` API;*
15. *You can add `from`, `to` and `limit` parameters to a `GET /api/users/:_id/logs` request to retrieve part of the log of any user. `from` and `to` are dates in `yyyy-mm-dd` format. `limit` is an integer of how many logs to send back;*

Each response should have the following structures:

Exercise:

```
{
  username: "fcc_test",
  description: "test",
  duration: 60,
  date: "Mon Jan 01 1990",
  _id: "5fb5853f734231456ccb3b05"
} 
  
```
  
User: 

```
{
  username: "fcc_test",
  _id: "5fb5853f734231456ccb3b05"
} 
  
```

Log:

```
{
  username: "fcc_test",
  count: 1,
  _id: "5fb5853f734231456ccb3b05",
  log: [{
  description: "test",
  duration: 60,
  date: "Mon Jan 01 1990",
  }] 
} 
  
```
  
**Hint:** For the `date` property, the `toDateString` method of the `Date`API can be used ot achieve the expected output.
  
### Example

[Example](https://exercise-tracker.freecodecamp.rocks/).

### Relevant Documentation:

[Date Documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) and [Mongoose Documentation](https://mongoosejs.com/).


### Solution:

[Solution](https://replit.com/join/jhrwyjhsag-minip). The proposed solution segment is properly identified, after accesssing the *index.js* file.

**Database integration:**

<p align="center" width="100%"><img width="434" alt="Solution" src="https://user-images.githubusercontent.com/73555298/189091385-8a069272-05f2-429e-b54d-003378d55860.png">
  </p>
  
**Solution:**

<p align="center" width="100%"><img width="434" alt="Solution" src="https://user-images.githubusercontent.com/73555298/189091515-6055e9dd-44e9-4223-b394-9b35394efb87.png">
  </p>
  
<p align="center" width="100%"><img width="434" alt="Solution" src="https://user-images.githubusercontent.com/73555298/189091519-01224f3f-eef8-4114-982e-53496fdde5a0.png">
  </p>
 
<p align="center" width="100%"><img width="434" alt="Solution" src="https://user-images.githubusercontent.com/73555298/189091520-8dcf5ff5-b50d-48af-972c-a932173be67e.png">
  </p>

### Solution Breakdown:

