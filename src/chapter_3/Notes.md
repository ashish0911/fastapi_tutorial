# Building a CRUD REST API 

## What is CRUD?

CRUD represents the four basic data operations:

- **Create (C):**

  - _Objective:_ Add new data.
  - _Action:_ Insert a new record or entity.

- **Read (R):**

  - _Objective:_ Retrieve existing data.
  - _Action:_ Fetch data without modification.

- **Update (U):**

  - _Objective:_ Modify existing data.
  - _Action:_ Update attributes or values.

- **Delete (D):**
  - _Objective:_ Remove data.
  - _Action:_ Delete a record or entity.

CRUD operations are fundamental in data management, commonly used in applications dealing with data persistence.

### A simple CRUD API implementation
Our simple CRUD API will have a few endpoints to perform CRUD operations on a simple in-memory database of books. Here's a list of endpoints that we shall have in our CRUD API.

| Endpoint        | Method | Description         |
| --------------- | ------ | ------------------- |
| /books          | Get    | Read all books      |
| /books          | POST   | Create a book       |
| /book/{book_id} | GET    | Get a book by id    |
| /book/{book_id} | PATCH  | Update a book by id |
| /book/{book_id} | DELETE | Delete a book by id |

The provided table describes various API endpoints, their associated HTTP methods, and their functionalities:

1. **`/books` - GET: Read all books**

   - _Description:_ This endpoint is designed to retrieve information about all available books. When a client makes an HTTP GET request to `/books`, the server responds by providing details on all books in the system.
   - `@app.get("/books", response_model=List[Book])`: Use `response_model` to validate and fix the structure of the response.
   - Also we can pass the json object in the `Book` object inherited from `BaseModel`.
   - Finally output was a list of json, so we have to pass `List[Book]` in `response_model`.

2. **`/books` - POST: Create a book**

   - _Description:_ To add a new book to the system, clients can make an HTTP POST request to `/books`. This operation involves creating and storing a new book based on the data provided in the request body.
   - `@app.post("/books", status_code=status.HTTP_201_CREATED)`: We will pass `status_code` to show that the object is created.
   - `book_data.model_dump()`: This will dump the content of `book_data` as a json.

3. **`/book/{book_id}` - GET: Get a book by id**

   - _Description:_ By making an HTTP GET request to `/book/{book_id}`, clients can retrieve detailed information about a specific book. The `book_id` parameter in the path specifies which book to fetch.
   - `HTTPException(status_code=status.HTTP_404_NOT_FOUND, detail="Book not found")`: This is used to raise a error.

4. **`/book/{book_id}` - PATCH: Update a book by id**

   - _Description:_ To modify the information of a specific book, clients can send an HTTP PATCH request to `/book/{book_id}`. The `book_id` parameter identifies the target book, and the request body contains the updated data.

5. **`/book/{book_id}` - DELETE: Delete a book by id**
   - _Description:_ This endpoint allows clients to delete a specific book from the system. By sending an HTTP DELETE request to `/book/{book_id}`, the book identified by `book_id` will be removed from the records.