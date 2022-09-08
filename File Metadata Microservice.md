# File Metadata Microservice

In this project, we are asked to build a microservice such that:

1. *You can submit a form that includes a file upload;*
2. *The form file input field has the `name` attribute set to `upfile`;*
3. *When you submit a file, you receive the file `name`, `type`, and `size` in bytes within the JSON response.*

### Example

[Example](https://file-metadata-microservice.freecodecamp.rocks/).


### Relevant Documentation:

[Mutler Documentation](https://expressjs.com/en/api.html).

### Solution:

[Solution](https://replit.com/join/wahsedhghl-minip). The proposed solution segment is properly identified, after accesssing the *index.js* file.

<p align="center" width="100%"><img width="434" alt="Solution" src="https://user-images.githubusercontent.com/73555298/189097856-350e4650-28d0-4b52-a974-9eb2fb612b63.png">
  </p>

### Solution Breakdown:

So as to access the file metadata, we make use of the `multer` npm package.

Thus, only a `POST` route mounted at `/api/fileanalyse` is necessary. The middleware uploads the image, as is described in the documentation, and the callback function sends a JSON file with the required information, which can be accessed from the `req.file` object.
