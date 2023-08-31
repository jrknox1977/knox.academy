---
title: "Building_APIs_with_FastAPI"
date: 2023-08-30T16:31:43-04:00
draft: false
---

IV. Building APIs with FastAPI
# A. Creating routes and endpoints

## 1. Defining route paths

### a. Specifying the URL structure for each route

In FastAPI, we can define route paths using decorators and the `app.route()` method. The route path specifies the URL structure for each route, allowing us to map our API endpoints to specific URLs.

For example, let's define a route path for a simple GET request:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/items")
async def read_items():
    return {"message": "GET request to fetch all items"}
```

In the above code snippet, the `@app.get("/items")` decorator is used to define the route path `/items` for the `read_items()` function. This means that whenever a GET request is made to `/items`, the `read_items()` function will be executed.

### b. Utilizing path parameters and query parameters in route paths

Path parameters and query parameters can be used to make our route paths more dynamic and flexible. Path parameters are parts of the URL that are marked with curly braces `{}` and can be accessed as function parameters. Query parameters, on the other hand, are passed as key-value pairs in the URL query string.

Let's see an example that demonstrates the usage of path and query parameters:

```python
@app.get("/items/{item_id}")
async def get_item(item_id: int, q: str = None):
    return {"item_id": item_id, "q": q}
```

In the above code, the route path `/items/{item_id}` defines a path parameter `item_id`. When a GET request is made to `/items/42`, the `get_item()` function will be executed with `item_id=42`. Additionally, we can also pass a query parameter `q` in the URL query string, like `/items/42?q=search`, which will be accessible as `q="search"` within the function.

## 2. Handling different HTTP methods

### a. Implementing GET, POST, PUT, DELETE, and other HTTP methods

FastAPI allows us to implement various HTTP methods for our API endpoints, such as GET, POST, PUT, DELETE, and more. We can use decorators like `@app.get()`, `@app.post()`, `@app.put()`, and `@app.delete()` to specify the HTTP method for each route.

Let's see an example that demonstrates how to implement different HTTP methods:

```python
@app.get("/items")
async def read_items():
    return {"message": "GET request to fetch all items"}

@app.post("/items")
async def create_item(item: Item):
    return {"message": "POST request to create a new item"}

@app.put("/items/{item_id}")
async def update_item(item_id: int, item: Item):
    return {"message": f"PUT request to update item with ID: {item_id}"}

@app.delete("/items/{item_id}")
async def delete_item(item_id: int):
    return {"message": f"DELETE request to delete item with ID: {item_id}"}
```

In the above code, we have defined route paths for different HTTP methods. For example, the `@app.post("/items")` decorator specifies that the `create_item()` function will handle POST requests made to `/items`. Similarly, the `@app.put("/items/{item_id}")` decorator maps the `update_item()` function to the route path `/items/{item_id}` for PUT requests.

### b. Configuring route handlers for each HTTP method

We can have separate functions to handle different HTTP methods for the same route path. This allows us to have more control and modularity in our code.

Let's see an example that demonstrates this:

```python
@app.route("/items/{item_id}", methods=["GET", "POST"])
async def handle_item(item_id: int):
    if request.method == "GET":
        return {"message": f"GET request for item with ID: {item_id}"}
    elif request.method == "POST":
        return {"message": f"POST request for item with ID: {item_id}"}
```

In the above code, the `@app.route("/items/{item_id}", methods=["GET", "POST"])` decorator is used to define a route path that handles both GET and POST requests. Inside the `handle_item()` function, we can check the `request.method` to determine which HTTP method was used and perform the appropriate actions accordingly.

By creating routes and endpoints in FastAPI, we can define the URL structure for each route, utilize path and query parameters, handle different HTTP methods, and configure route handlers accordingly. This allows us to build powerful and flexible APIs.
# IV. Building APIs with FastAPI

## B. Query parameters and pagination

### 1. Handling query parameters
   a. Extracting query parameters from the request URL

   Query parameters are commonly used in APIs to filter and sort data based on specific criteria. In FastAPI, query parameters can be easily extracted from the request URL using the `Query` function from the `fastapi.params` module. 

   Here's an example of how to extract a query parameter named `filter` from the URL:
   ```python
   from fastapi import FastAPI, Query

   app = FastAPI()

   @app.get("/items/")
   async def get_items(filter: str = Query(None)):
       return {"filter": filter}
   ```

   In this example, the `filter` query parameter is of type `str` and has a default value of `None`. If the query parameter is not provided in the URL, the default value is used. 

   b. Applying filters and sorting based on query parameters

   Once the query parameters are extracted, they can be used to filter and sort data in the API endpoint. For instance, if your API returns a list of items, you can apply filters and sorting based on the provided query parameters. 

   Here's an example of how to filter and sort items based on query parameters:
   ```python
   from fastapi import FastAPI, Query

   app = FastAPI()

   @app.get("/items/")
   async def get_items(filter: str = Query(None), sort: str = Query(None)):
       # Apply filters and sorting based on query parameters
       # Retrieve items from the database
       # ...

       return {"items": items}
   ```

   In this example, the `get_items` endpoint accepts two query parameters: `filter` and `sort`. These parameters can be used to filter and sort the items retrieved from the database before returning the response.

### 2. Implementing pagination in APIs
   a. Dividing large result sets into smaller pages

   Pagination is a common technique used in APIs to handle large result sets. It involves dividing the results into smaller pages, allowing users to navigate through the data more efficiently. 

   FastAPI provides built-in support for pagination using query parameters. By specifying the `skip` and `limit` query parameters, you can control the number of items to skip and the maximum number of items to retrieve per page.

   Here's an example of implementing pagination in an API:
   ```python
   from fastapi import FastAPI, Query

   app = FastAPI()

   @app.get("/items/")
   async def get_items(skip: int = Query(0), limit: int = Query(10)):
       # Retrieve items from the database, considering skip and limit
       # ...

       return {"items": items}
   ```

   In this example, the `skip` parameter determines the number of items to skip, and the `limit` parameter specifies the maximum number of items to retrieve per page. By default, the `skip` parameter is set to 0, and the `limit` parameter is set to 10. These values can be adjusted based on your API requirements.

   b. Adding pagination parameters to enable navigation through the pages

   To enable navigation through the pages, additional pagination parameters can be added to the API endpoint. These parameters can include the total number of items, the current page number, and links to previous and next pages.

   Here's an example of adding pagination parameters to an API:
   ```python
   from fastapi import FastAPI, Query

   app = FastAPI()

   @app.get("/items/")
   async def get_items(skip: int = Query(0), limit: int = Query(10)):
       # Retrieve items from the database, considering skip and limit
       # ...

       total_items = 100
       current_page = skip // limit
       total_pages = (total_items // limit) + 1

       previous_link = f"/items/?skip={max(skip - limit, 0)}&limit={limit}" if skip > 0 else None
       next_link = f"/items/?skip={skip + limit}&limit={limit}" if skip + limit < total_items else None

       return {
           "items": items,
           "total_items": total_items,
           "current_page": current_page,
           "total_pages": total_pages,
           "previous_link": previous_link,
           "next_link": next_link
       }
   ```

   In this example, the pagination parameters are calculated based on the `skip` and `limit` values. The `total_items` variable represents the total number of items available. The `current_page` variable is calculated by dividing the `skip` value by the `limit` value. The `total_pages` variable is calculated by dividing the `total_items` value by the `limit` value and adding 1.

   Additionally, the `previous_link` and `next_link` variables are calculated to provide links to the previous and next pages, respectively. These links are included in the API response, allowing users to navigate through the paginated results.

By using query parameters and pagination techniques in FastAPI, you can enhance the functionality of your APIs and provide a more flexible and efficient user experience.
# C. Path parameters and path operations

## 1. Using path parameters in routes

### a. Defining dynamic segments in route paths

FastAPI allows us to define dynamic segments in route paths using path parameters. Path parameters are used to capture values from the URL path and use them in our route handlers. We can define path parameters by enclosing them in curly braces `{}` within the route path.

For example, consider a route that retrieves information about a specific user. We can define a path parameter for the user ID as follows:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/users/{user_id}")
async def get_user(user_id: int):
    return {"user_id": user_id}
```

In the above example, the `user_id` path parameter is defined within the route path `/users/{user_id}`. This allows us to access the value of `user_id` in the `get_user` route handler.

### b. Extracting values from path parameters for further processing

Once we have defined path parameters in our route paths, we can extract their values for further processing within our route handlers. FastAPI automatically converts the path parameter values to the specified type, if any type is provided.

Continuing from the previous example, let's extract the value of the `user_id` path parameter and use it to retrieve the corresponding user information:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/users/{user_id}")
async def get_user(user_id: int):
    # Retrieve user information based on user_id
    user = get_user_by_id(user_id)
    
    return {"user": user}
```

In the above example, the `user_id` path parameter is passed as an argument to the `get_user` route handler. We can then use this value to retrieve the corresponding user information from a hypothetical `get_user_by_id` function.

## 2. Implementing path operations (GET, POST, etc.)

### a. Assigning specific HTTP methods to route handlers

FastAPI allows us to assign specific HTTP methods to our route handlers using decorators. The most common HTTP methods include GET, POST, PUT, DELETE, etc.

For example, let's define a route that handles GET requests for retrieving a list of users:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/users")
async def get_users():
    # Retrieve list of users
    users = get_all_users()
    
    return {"users": users}
```

In the above example, the `@app.get` decorator is used to assign the GET method to the `get_users` route handler.

### b. Executing corresponding actions based on the path operation and HTTP method

Once we have assigned specific HTTP methods to our route handlers, FastAPI executes the corresponding action based on the path operation and HTTP method.

Continuing from the previous example, let's define a route that handles POST requests for creating a new user:

```python
from fastapi import FastAPI

app = FastAPI()

@app.post("/users")
async def create_user(user: User):
    # Create a new user
    created_user = create_new_user(user)
    
    return {"user": created_user}
```

In the above example, the `@app.post` decorator is used to assign the POST method to the `create_user` route handler. When a POST request is made to the `/users` endpoint, FastAPI executes the `create_user` route handler and creates a new user based on the provided user data.

By combining path parameters and path operations, we can build powerful APIs with FastAPI that handle various types of requests and perform different actions based on the provided data.
## D. Request body and payload

### 1. Handling request payload
   a. Receiving and processing data sent in the request body
   
   FastAPI allows you to handle data sent in the request body easily. You can define a request body parameter in your route function with the `Request` type annotation. This will automatically parse and deserialize the request body for you.

   Here's an example of receiving and processing JSON data sent in the request body:

   ```python
   from fastapi import FastAPI, Request

   app = FastAPI()

   @app.post("/items/")
   async def create_item(request: Request):
       item = await request.json()
       # Process the received item
       return {"item": item}
   ```
   
   b. Differentiating between JSON, form data, and other payload formats
   
   By default, FastAPI assumes that the request body contains JSON data. However, you can also handle other payload formats such as form data or plain text. To handle different payload formats, you can use the `content_type` parameter of the `request.body()` method.

   Here's an example of handling form data sent in the request body:

   ```python
   from fastapi import FastAPI, Request

   app = FastAPI()

   @app.post("/items/")
   async def create_item(request: Request):
       form_data = await request.form()
       # Process the received form data
       return {"form_data": form_data}
   ```

### 2. Validating and parsing request body
   a. Implementing data validation on the received request body
   
   FastAPI provides powerful tools for validating the request body data. You can use Pydantic models to define the expected structure and types of the request body. FastAPI will automatically validate the received data against the defined model.

   Here's an example of implementing data validation on the request body:

   ```python
   from fastapi import FastAPI, Request
   from pydantic import BaseModel

   class Item(BaseModel):
       name: str
       price: float

   app = FastAPI()

   @app.post("/items/")
   async def create_item(request: Request, item: Item):
       # The received item is already validated and of type Item
       # Process the received item
       return {"item": item}
   ```

   b. Parsing and converting the request body into Python objects for further processing
   
   Once the request body is validated, you can directly use the parsed and converted request body as Python objects in your route function. FastAPI automatically converts the validated data into the defined model.

   Here's an example of parsing and converting the request body into Python objects:

   ```python
   from fastapi import FastAPI, Request
   from pydantic import BaseModel

   class Item(BaseModel):
       name: str
       price: float

   app = FastAPI()

   @app.post("/items/")
   async def create_item(item: Item):
       # The received item is already validated and of type Item
       # Process the received item
       return {"item": item}
   ```
