# Creating a Simple Web Server

## Introduction

The `@app` decorator associates the function with the HTTP GET method via the `get` method. We then provide the path (route) of the root path (`/`). This means that whenever the `/` route is accessed, the defined message will be returned.

All HTTP methods such as `post`,`put`,`head`,`patch`, `delete`, `trace` and `options` are all available on the `@app` decorator.

### **Running the FastAPI Application:**

To run our FastAPI application, we shall use the `fastapi`command we introduced in the previous chapter. Open a terminal and execute the following command within the virtual environment:

```console title="Running the server with the FastAPI CLI"
(env)$ fastapi dev main.py
```

The `fastapi dev` command enables us to execute our FastAPI application in development mode. This feature facilitates running our application with auto-reload functionality, ensuring that any modifications we make are automatically applied, restarting the server accordingly. It operates by identifying the FastAPI instance within the specified module or Python package, which in our scenario is `main.py`, where we have defined the app object. When we initiate our application, it will display the following output.

Running the server will make your application available at this web address: `http://localhost:8000`.

## Managing Requests and Responses

There are very many ways that clients can pass request data to a FastAPI API route. These include:

- Path Parameters
- Query Parameters
- Headers e.t.c.

Through such ways, we can obtain data from incoming requests to our APIs.

### Parameter type declarations

All parameters in a FastAPI request are required to have a type declaration via _type hints_. Primitive Python types such (`None`,`int`,`str`,`bool`,`float`), container types such as (`dict`,`tuples`,`dict`,`set`) and some other complex types are all supported.

Additionally FastAPI also allows all types present within Python's `typing` module.
These data types represent common conventions in Python and are utilized for variable type annotations. They facilitate type checking and model validation during compilation. Examples include `Optional`, `List`, `Dict`, `Set`, `Union`, `Tuple`, `FrozenSet`, `Iterable`, and `Deque`.

### Path Parameters

All request data supplied in the endpoint URL of a FastAPI API is acquired through a path parameter, thus rendering URLs dynamic. FastAPI adopts curly braces (`{}`) to denote path parameters when defining a URL. Once enclosed within the braces, FastAPI requires that they be provided as parameters to the route handler functions we establish for those paths.

### Query Parameters

These are key-value pairs provided at the end of a URL, indicated by a question mark (`?`). Just like path parameters, they also take in request data. Whenever we want to provide multiple query parameters, we use the ampersand (`&`) sign.

### Optional Parameters

There may also be cases when the API route can operate as needed even in the presence of a path or query param. In this case, we can make the parameters optional when annotating their types in the route handler functions.

## Request Body

Frequently, clients need to send data to the server for tasks like creating or updating resources through methods like POST, PATCH, PUT, DELETE, or for various other operations. FastAPI simplifies this process by enabling you to define a Pydantic model to establish the structure of the data being sent. Furthermore, it aids in validating data types using type hints. Let's delve into a straightforward example to illustrate this concept.

#### Note

There can indeed be scenarios that necessitate the use of all the features we've discussed. You can have an API route that accepts path, query, and optional parameters, and FastAPI is capable of handling such complexity seamlessly.

### Request Headers

During a request-response transaction, the client not only sends parameters to the server but also provides information about the context of the request's origin. This contextual information is crucial as it enables the server to customize the type of response it returns to the client.

Common request headers include:

- `User-Agent`: This string allows network protocol peers to identify the application responsible for the request, the operating system it's running on, or the version of the software being used.

- `Host`: This specifies the domain name of the server, and (optionally) the TCP port number on which the server is listening.

- `Accept`: Informs the server about the types of data that can be sent back.

- `Accept-Language`: This header informs the server about the preferred human language for the response.

- `Accept-Encoding`: The encoding algorithm, usually a compression algorithm, that can be used on the resource sent back.

- `Referer`: This specifies the address of the previous web page from which a link to the currently requested page was followed.

- `Connection`: This header controls whether the network connection stays open after the current transaction finishes.

To access such headers, FastAPI provides us with the `Header` function giving us the ability to get the values of these headers using the exact names but in a snake-case syntax forexample, `User-Agent` is `user_agent`, `Accept-Encoding` is `accept_encoding` and so on.

### Status Codes

We can set the status codes like this `@app.get('/get_headers',status_code=201)`