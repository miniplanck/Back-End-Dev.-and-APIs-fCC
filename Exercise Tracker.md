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
15. *You can add `from`, `to` and `limit` parameters to a `GET /api/users/:_id/logs` request to retrieve part of the log of any user. `from` and `to` are dates in `yyyy-mm-dd` format. `limit` is an integer of how many logs to send back.*

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

The solution to this problem is divided into three main parts, which correspond to each of the four images in the solution section.

1. Database integration;
2. User creation;
3. Exercise creation;
4. Log retrieval.

Since we are mainly dealing with a system of registration, a database can be used. In this project, we have decided to use MongoDB Atlas, which was presented in the course. 

MongoDB is a NoSQL database, which means data is stored in **collections**, composed of several **documents** - entries - which are highly flexible, in that data can be stored in several types. So as to create documents, **schemas** and **models** are needed. To the the requirements of the challenge, we concluded that this database was an adequate one.

The solution starts by integrating the database, handled by `mongoose.connect()`.

Now that the database is successfully connected to the rest of the program, we focus on steps 1.-5. First, we must create the schemas for the `User` and `Log` models: the reason we have chosen not to create one for `Exercise` was that the corresponding information can be retrieved from POST requests and stored in the `logs` collection. Thus, we do not overload the database with unnecessary data, which hopefully, at a larger scale, can make a difference.

Having created said Models, we create a POST route mounted at `/api/users`, which handles the user creation. If the user already exists, it throws an error (later caught and sent to the user), since ideally we do not want several users with the same username. If it does not already exist, a document is added to the database. So as to retrieve all users, a GET route is mounted at the same endpoint: it uses the `.find()` method of `Model`, with no filter, so as to retrieve all the users in the database. The `_id` property is automatically created by MongoDB, and, since it is unique, no further tinkering is needed.

Onwards to the Exercise creation. This section of the code is the most contrieved one, which is the downfall of not overloading the database. The main goal is to show a record of the Exercise a certain user, with a given `_id`, executes, which must be accompanied by a description - in string form - of the exercise and its duration - in number form - both required. Optionally, we can opt for submiting a date in the `yyyy-mm-ddd` format, but if none (or an invalid one) is passed, we assume that it corresponds to the date of submition.

So as to achieve the desired results, we create a POST route at `/api/users/:_id/exercises`, and start by checking whether the requested user exists. If it does not, the user gets a warning message, as was expected. In case there is such user, we start by creating the Exercise object, composed of the `username` and `_id` properties, which can be easily retrieved from the `data` object (which results from a query). If the `req.body.date` is invalid, we attribute the present date to it. Finally, `duration` and `description` are added to the object by accessing the body of the POST request. 

Since we do not wish to save the exercise, we propose the following: let us search for the logs corresponding to the user; if the user has no exercises logged, we create a record and log the previous exercise as their first one; if a log already exists, then we update the exercises. In order to do so, we first check if there is any record (using `LogModel.countDocuments()`): in case there are 0 documents, we create a log and save it, with `count:1`; otherwise, we update the `log` property of the document so as to include the new exercise, as well as increment the `count` property value. If any error occurs during the submission, whether by invalid fields on missing ones, a proper warning is thrown.

Last but not least, we must account for `GET /api/users/:_id/logs` requests. This section of the code creates the Log object using the information for the database query, and applies the proper filters from the URL query.
