**tutorial/index.md**
- Introduces the overall tutorial as a step‐by‐step guide to FastAPI features and concepts.
- Explains that every example is a runnable Python file (often named `main.py`) and can be run with the FastAPI CLI.
- Emphasizes the use of automatic interactive API docs (via Swagger UI and ReDoc) and OpenAPI schema generation.
- Encourages you to copy, run, and edit the examples as you learn.

**tutorial/first-steps.md**
- Presents the simplest FastAPI application:
    - **Example code:**
        
        ```python
        from fastapi import FastAPI
        
        app = FastAPI()
        
        @app.get("/")
        async def read_root():
            return {"message": "Hello World"}
        ```
        
- Instructs to save the code as `main.py` and run with the command:
    
    ```console
    fastapi dev main.py
    ```
    
- Explains that when you access the root URL (e.g. `http://127.0.0.1:8000/`), you get a JSON response.
- Introduces interactive documentation at `/docs` (Swagger UI) and `/redoc` (ReDoc).

**tutorial/path-params.md**
- Demonstrates how to capture parts of the URL as path parameters using Python’s f‐string–like syntax.
- **Key points:**
    - Define a route like `/items/{item_id}`.
    - The function receives `item_id` as an argument.
- **Example code:**
    
    ```python
    @app.get("/items/{item_id}")
    async def read_item(item_id: int):
        return {"item_id": item_id}
    ```
    
- Explains automatic conversion from string (in the URL) to the annotated type (e.g. `int`), plus validation and error responses if conversion fails.

**tutorial/query-params.md**
- Explains that any function parameter not part of the path is interpreted as a query parameter.
- **Key points:**
    - Query parameters come after the `?` in the URL.
    - Default values make parameters optional.
- **Example code:**
    
    ```python
    @app.get("/items/")
    async def read_items(skip: int = 0, limit: int = 10):
        return {"skip": skip, "limit": limit}
    ```
    
- Covers type conversion, default value handling, and the automatic inclusion of these parameters in the OpenAPI schema.

**tutorial/body.md**
- Describes how to receive a request body using Pydantic models.
- **Key points:**
    - Create a Pydantic model to define the expected JSON structure.
    - Use the model as a function parameter in your path operation.
- **Example code:**
    
    ```python
    from pydantic import BaseModel
    
    class Item(BaseModel):
        name: str
        description: str | None = None
        price: float
        tax: float | None = None
    
    @app.post("/items/")
    async def create_item(item: Item):
        return item
    ```
    
- Outlines automatic parsing, validation, error reporting, and documentation.

**tutorial/query-params-str-validations.md**
- Adds extra validation and metadata to query parameters.
- **Key points:**
    - Use the `Query` class (often with `Annotated`) to specify constraints like `max_length`, `min_length`, and even regex `pattern`.
    - Makes optional parameters required to meet specific string conditions.
- **Example code using Annotated (Python 3.10+):**
    
    ```python
    from typing import Annotated
    from fastapi import Query
    
    @app.get("/items/")
    async def read_items(
        q: Annotated[str | None, Query(max_length=50)] = None
    ):
        return {"q": q}
    ```
    
- Explains how this metadata appears in the OpenAPI schema and interactive docs.

**tutorial/path-params-numeric-validations.md**
- Focuses on validating numeric path parameters.
- **Key points:**
    - Use `Path` with parameters such as `ge` (greater than or equal), `gt`, `le`, and `lt` to enforce numeric constraints.
    - Illustrates how ordering of parameters (or using the `*` trick for keyword-only arguments) can matter in non–Annotated usage.
- **Example code:**
    
    ```python
    from fastapi import Path
    
    @app.get("/items/{item_id}")
    async def read_item(item_id: int = Path(..., title="The ID of the item", ge=1)):
        return {"item_id": item_id}
    ```
    
- Explains that even if using defaults, path parameters are always required.

**tutorial/query-param-models.md**
- Shows how to group multiple query parameters into a single Pydantic model.
- **Key points:**
    - Define a model with several fields to represent related query parameters.
    - Reuse the model in multiple endpoints to enforce consistency and reduce duplication.
- **Example code:**
    
    ```python
    from pydantic import BaseModel
    from fastapi import Depends
    
    class CommonQueryParams(BaseModel):
        q: str | None = None
        skip: int = 0
        limit: int = 100
    
    @app.get("/items/")
    async def read_items(commons: CommonQueryParams = Depends()):
        return commons
    ```
    
- Highlights validation, type conversion, and automatic documentation benefits.

**tutorial/body-multiple-params.md**
- Explains handling multiple body parameters in a single request.
- **Key points:**
    - FastAPI distinguishes between JSON bodies, path parameters, and query parameters even if many appear in the same function.
    - You can “embed” a single body model using `Body(embed=True)`.
- **Example code:**
    
    ```python
    from fastapi import Body
    
    @app.post("/items/")
    async def create_item(
        item: Item = Body(...),
        importance: int = Body(..., embed=True)
    ):
        return {"item": item, "importance": importance}
    ```
    
- Describes how the request body should be structured (possibly as a JSON object with nested keys) and how FastAPI converts and validates data.

**tutorial/body-fields.md**
- Demonstrates how to add field-level validations and metadata in Pydantic models.
- **Key points:**
    - Use Pydantic’s `Field()` to set descriptions, examples, and constraints (like title, max_length, etc.).
    - Extra keyword arguments in `Field()` appear in the generated JSON Schema.
- **Example code:**
    
    ```python
    from pydantic import BaseModel, Field
    
    class Item(BaseModel):
        name: str = Field(..., title="The name of the item", max_length=100)
        description: str | None = Field(None, title="A description of the item")
    ```
    
- Explains that these validations help both runtime error messages and the interactive docs.

**tutorial/body-nested-models.md**
- Covers creating nested data structures using Pydantic models.
- **Key points:**
    - Models can be nested arbitrarily, including lists of submodels.
    - Enables complex JSON data structures with full type checking, validation, and editor support.
- **Example code:**
    
    ```python
    class Image(BaseModel):
        url: str
        name: str
    
    class Item(BaseModel):
        name: str
        description: str | None = None
        price: float
        tags: list[str] = []
        image: Image | None = None
    ```
    
- Mentions that nested models’ JSON schema is automatically generated.

**tutorial/schema-extra-example.md**
- Describes how to include example data in your JSON Schema.
- **Key points:**
    - Use Pydantic model configuration (`Config` in v1 or `model_config` in v2) with `schema_extra` or set examples in `Field()`.
    - These examples appear in the OpenAPI schema and interactive docs.
- **Example code (Pydantic v2 style):**
    
    ```python
    class Item(BaseModel):
        name: str
        price: float
    
        model_config = {
            "json_schema_extra": {
                "examples": [
                    {"name": "Foo", "price": 42.0},
                    {"name": "Bar", "price": 24.0}
                ]
            }
        }
    ```
    
- Also covers using the `openapi_examples` parameter with request bodies.

**tutorial/extra-data-types.md**
- Explains support for additional Python data types.
- **Key points:**
    - FastAPI (with Pydantic) supports types such as `UUID`, `datetime`, `date`, `time`, `timedelta`, `frozenset`, `bytes`, and `Decimal`.
    - Incoming values are automatically converted to these types and validated.
- **Example code:**
    
    ```python
    from uuid import UUID
    from datetime import datetime
    from decimal import Decimal
    
    @app.get("/items/")
    async def read_item(
        item_id: UUID,
        created_at: datetime,
        price: Decimal
    ):
        return {"item_id": str(item_id), "created_at": created_at.isoformat(), "price": float(price)}
    ```
    
- Mentions that JSON Schema is generated accordingly for each type.

**tutorial/cookie-params.md**
- Describes how to receive cookie values in your path operations.
- **Key points:**
    - Use the `Cookie` function to declare cookie parameters.
    - They are handled similarly to query parameters but are read from the HTTP cookies.
- **Example code:**
    
    ```python
    from fastapi import Cookie
    
    @app.get("/items/")
    async def read_items(ads_id: str | None = Cookie(default=None)):
        return {"ads_id": ads_id}
    ```
    
- Explains that cookie parameters are added to the OpenAPI schema.

**tutorial/header-params.md**
- Explains declaring header parameters.
- **Key points:**
    - Use `Header` to capture HTTP header values.
    - FastAPI automatically converts Python snake_case names to header names with hyphens.
- **Example code:**
    
    ```python
    from fastapi import Header
    
    @app.get("/items/")
    async def read_items(user_agent: str = Header(...)):
        return {"User-Agent": user_agent}
    ```
    
- Notes that duplicate headers (if allowed) are returned as lists.

**tutorial/cookie-param-models.md**
- Shows how to group multiple cookie parameters in a Pydantic model.
- **Key points:**
    - Define a model with fields for each expected cookie.
    - Use `Cookie` in the dependency to automatically extract and validate cookies.
- **Example code:**
    
    ```python
    from pydantic import BaseModel
    from fastapi import Cookie, Depends
    
    class Cookies(BaseModel):
        ads_id: str
    
    @app.get("/items/")
    async def read_items(cookies: Cookies = Depends()):
        return cookies
    ```
    
- Emphasizes reusability and validation.

**tutorial/header-param-models.md**
- Similar to cookie models, but for headers.
- **Key points:**
    - Define a Pydantic model for headers.
    - Use `Header` when declaring the dependency so FastAPI extracts each header field.
- **Example code:**
    
    ```python
    class CustomHeaders(BaseModel):
        x_token: str
        user_agent: str
    
    @app.get("/items/")
    async def read_items(headers: CustomHeaders = Depends()):
        return headers
    ```
    
- Explains how extra headers can be forbidden via model configuration.

**tutorial/response-model.md**
- (While not fully detailed in the provided text, the summary covers the core ideas.)
- **Key points:**
    - Use the `response_model` parameter in your path operation decorators to define the shape of the response.
    - FastAPI automatically converts the returned data to the declared response model.
- **Example code:**
    
    ```python
    @app.get("/items/{item_id}", response_model=Item)
    async def read_item(item_id: int):
        # Fetch or create an item dictionary
        return {"name": "Foo", "price": 42.0}
    ```
    
- Helps in validation, documentation, and client generation.

**tutorial/extra-models.md**
- Covers using multiple Pydantic models for different concerns (input, output, database).
- **Key points:**
    - Create separate models for incoming data (with a plaintext password), data to return (without the password), and database models (with hashed passwords).
    - Inheritance and model reuse reduce duplication.
- **Example code:**
    
    ```python
    class UserBase(BaseModel):
        username: str
        email: str | None = None
    
    class UserIn(UserBase):
        password: str
    
    class UserOut(UserBase):
        pass
    
    class UserInDB(UserBase):
        hashed_password: str
    ```
    
- Explains techniques like unpacking a dict (`**user_dict`) to create model instances.

**tutorial/response-status-code.md**
- Describes setting explicit HTTP response status codes.
- **Key points:**
    - Pass `status_code` (or use constants from `fastapi.status`) in the decorator.
    - Status codes affect both the response and OpenAPI documentation.
- **Example code:**
    
    ```python
    from fastapi import status
    
    @app.post("/items/", status_code=status.HTTP_201_CREATED)
    async def create_item(item: Item):
        return item
    ```
    
- Provides an overview of common HTTP status code ranges (200, 400, 500, etc.).

**tutorial/request-forms.md**
- Explains how to receive form data (instead of JSON) with the `Form` function.
- **Key points:**
    - Install `python-multipart` to handle form data.
    - Use `Form` to define parameters that come from HTML forms.
- **Example code:**
    
    ```python
    from fastapi import Form
    
    @app.post("/login/")
    async def login(username: str = Form(...), password: str = Form(...)):
        return {"username": username}
    ```
    
- Mentions that form data is encoded as `application/x-www-form-urlencoded`.

**tutorial/request-form-models.md**
- Shows how to use Pydantic models to validate form data.
- **Key points:**
    - Define a Pydantic model that represents the expected form fields.
    - Use the model with a dependency and `Form` to automatically extract and validate the form data.
- **Example code:**
    
    ```python
    class LoginForm(BaseModel):
        username: str
        password: str
    
    @app.post("/login/")
    async def login(form_data: LoginForm = Depends()):
        return form_data
    ```
    
- Also demonstrates how to forbid extra form fields using model configuration.

**tutorial/request-files.md**
- Covers file upload handling.
- **Key points:**
    - Use the `File` function to declare file parameters.
    - For small files, you can use `bytes`; for larger files, use `UploadFile` which provides an async file-like interface.
- **Example code:**
    
    ```python
    from fastapi import File, UploadFile
    
    @app.post("/upload/")
    async def upload_file(file: UploadFile = File(...)):
        contents = await file.read()
        return {"filename": file.filename, "size": len(contents)}
    ```
    
- Explains the advantages of using `UploadFile` (memory efficiency, access to metadata, async methods).

**tutorial/request-forms-and-files.md**
- Explains combining form fields and file uploads in one request.
- **Key points:**
    - Use both `Form` and `File` in the same path operation.
    - The entire request must be sent as `multipart/form-data`.
- **Example code:**
    
    ```python
    @app.post("/upload-form/")
    async def upload_form(
        description: str = Form(...),
        file: UploadFile = File(...)
    ):
        contents = await file.read()
        return {"description": description, "filename": file.filename}
    ```
    
- Notes that you cannot also expect JSON body parameters when using form data.

**tutorial/handling-errors.md**
- Describes error handling and returning HTTP error responses.
- **Key points:**
    - Use `HTTPException` to raise errors that return specific status codes and details.
    - When validation fails or a resource is not found, FastAPI returns a structured error response.
- **Example code:**
    
    ```python
    from fastapi import HTTPException
    
    @app.get("/items/{item_id}")
    async def read_item(item_id: int):
        if item_id != 42:
            raise HTTPException(status_code=404, detail="Item not found")
        return {"item_id": item_id}
    ```
    
- Explains how to add custom headers to error responses and override default exception handlers.

**tutorial/path-operation-configuration.md**
- Covers configuring path operations through decorator parameters.
- **Key points:**
    - Set response status codes (using `status_code`).
    - Add metadata such as tags, summary, description, and even mark endpoints as deprecated.
- **Example code:**
    
    ```python
    @app.get(
        "/items/{item_id}",
        status_code=200,
        tags=["items"],
        summary="Get an item by ID",
        response_description="The found item"
    )
    async def read_item(item_id: int):
        return {"item_id": item_id}
    ```
    
- Demonstrates how these settings affect the generated OpenAPI documentation.

**tutorial/encoder.md**
- Explains the `jsonable_encoder()` utility function.
- **Key points:**
    - Converts complex objects (like Pydantic models or datetime objects) into JSON‐compatible data (dicts, lists, strings).
- **Example code:**
    
    ```python
    from fastapi.encoders import jsonable_encoder
    from datetime import datetime
    
    item = Item(name="Foo", price=42.0, created_at=datetime.now())
    json_compatible_item_data = jsonable_encoder(item)
    ```
    
- Useful for saving data in NoSQL databases or for custom responses.

**tutorial/body-updates.md**
- (Although not fully detailed in the provided excerpt, the core ideas are:)
- **Key points:**
    - Describes techniques for updating a model’s data using PUT/PATCH operations.
    - Shows how to merge the incoming update with existing data.
    - Explains using Pydantic’s `.model_dump()` (or `.dict()` in v1) to handle partial updates.
- Emphasizes that the update mechanism is similar to creating a new model instance with updated fields.

**Dependencies: tutorial/dependencies/index.md**
- Introduces FastAPI’s dependency injection system.
- **Key points:**
    - Dependency injection means declaring “dependencies” (shared logic, database sessions, security, etc.) that FastAPI automatically resolves and injects.
    - Simplifies code reuse and testing.
- **Example code:**
    
    ```python
    from fastapi import Depends
    
    def common_parameters(q: str | None = None, skip: int = 0, limit: int = 100):
        return {"q": q, "skip": skip, "limit": limit}
    
    @app.get("/items/")
    async def read_items(commons: dict = Depends(common_parameters)):
        return commons
    ```
    
- Emphasizes that dependencies work just like regular functions and can have parameters, sub‐dependencies, and caching.

**Dependencies: tutorial/dependencies/classes-as-dependencies.md**
- Shows that you can use classes as dependencies.
- **Key points:**
    - A class is “callable” (its constructor is called) so you can use it with `Depends`.
    - Better editor support via type hints and instance attributes.
- **Example code:**
    
    ```python
    class CommonQueryParams:
        def __init__(self, q: str | None = None, skip: int = 0, limit: int = 100):
            self.q = q
            self.skip = skip
            self.limit = limit
    
    @app.get("/items/")
    async def read_items(commons: CommonQueryParams = Depends()):
        return commons.__dict__
    ```
    
- Introduces a shortcut using `Depends()` without repeating the class name in the parameter.

**Dependencies: tutorial/dependencies/sub-dependencies.md**
- Explains how dependencies can have their own dependencies (sub-dependencies).
- **Key points:**
    - Functions can call other dependency functions.
    - FastAPI caches dependency results so the same dependency is not re‐executed within a request unless specified.
- **Example code:**
    
    ```python
    def query_extractor(q: str | None = None):
        return q
    
    def query_or_cookie_extractor(
        q: str = Depends(query_extractor), last_query: str | None = Cookie(None)
    ):
        return q or last_query
    
    @app.get("/items/")
    async def read_query(query: str = Depends(query_or_cookie_extractor)):
        return {"q": query}
    ```
    
- Notes the possibility of disabling caching with `use_cache=False` if necessary.

**Dependencies: tutorial/dependencies/dependencies-in-path-operation-decorators.md**
- Demonstrates including dependencies in the decorator rather than as function parameters.
- **Key points:**
    - Use the `dependencies` parameter in the decorator to force dependency execution without needing their return values in the function.
- **Example code:**
    
    ```python
    @app.get("/items/", dependencies=[Depends(some_dependency)])
    async def read_items():
        return [{"item": "Foo"}]
    ```
    
- Useful to avoid “unused parameter” warnings and to enforce side effects (like security checks).

**Dependencies: tutorial/dependencies/global-dependencies.md**
- Shows how to add dependencies that apply to every path operation in the app.
- **Key points:**
    - Pass a list of dependencies when creating the FastAPI app instance.
    - All routes will then inherit those dependencies.
- **Example code:**
    
    ```python
    app = FastAPI(dependencies=[Depends(common_parameters)])
    ```
    
- Also mentions grouping dependencies for multiple routers.

**Dependencies: tutorial/dependencies/dependencies-with-yield.md**
- Covers dependencies that use a `yield` statement to provide cleanup (like closing a database session).
- **Key points:**
    - A dependency can yield a resource and then execute “teardown” code after the response is sent.
    - FastAPI creates a context manager from such functions.
- **Example code:**
    
    ```python
    async def get_db():
        db = create_db_session()
        try:
            yield db
        finally:
            db.close()
    ```
    
- Emphasizes that you should yield only once per dependency.

**Security: tutorial/security/index.md**
- Provides an overview of FastAPI’s security tools.
- **Key points:**
    - Explains that security is handled via dependency injection.
    - Outlines common security schemes (API keys, HTTP basic, OAuth2, OpenID Connect).
    - Emphasizes standards (OpenAPI) integration for interactive docs.
- Serves as a preface to the detailed security chapters.

**Security: tutorial/security/first-steps.md**
- Introduces the OAuth2 “password flow” for authentication.
- **Key points:**
    - Uses `OAuth2PasswordBearer` to declare a dependency that extracts a token from the Authorization header.
    - Provides an “Authorize” button in the docs.
- **Example code snippet:**
    
    ```python
    from fastapi.security import OAuth2PasswordBearer
    
    oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")
    ```
    
- Explains that at this stage the token isn’t verified yet—it just extracts the token string.

**Security: tutorial/security/get-current-user.md**
- Extends the security flow by retrieving the current user from the provided token.
- **Key points:**
    - Defines a Pydantic `User` model.
    - Implements a dependency (`get_current_user`) that uses `oauth2_scheme` to get the token and then “decodes” it (or looks up the user in a (fake) database).
- **Example code snippet:**
    
    ```python
    async def get_current_user(token: str = Depends(oauth2_scheme)):
        user = fake_decode_token(token)
        if not user:
            raise HTTPException(status_code=401, detail="Invalid authentication credentials")
        return user
    ```
    
- Demonstrates injecting the current user into path operations.

**Security: tutorial/security/simple-oauth2.md**
- Builds a complete (though simplified) OAuth2 password flow.
- **Key points:**
    - Uses `OAuth2PasswordRequestForm` to extract `username`, `password`, and optional `scope` from form data.
    - Checks the user’s credentials against a fake database.
    - Returns a JSON response with an access token and token type.
- **Example code snippet:**
    
    ```python
    @app.post("/token")
    async def login_for_access_token(form_data: OAuth2PasswordRequestForm = Depends()):
        user = authenticate_user(fake_users_db, form_data.username, form_data.password)
        if not user:
            raise HTTPException(status_code=400, detail="Incorrect username or password")
        return {"access_token": user.username, "token_type": "bearer"}
    ```
    
- Explains that this lays the groundwork for real-world security.

**Security: tutorial/security/oauth2-jwt.md**
- Upgrades the simple OAuth2 example to use secure password hashing and JWT tokens.
- **Key points:**
    - Introduces JWT (JSON Web Tokens) as a standard for creating signed tokens.
    - Explains installation and use of PyJWT and PassLib for token creation and password hashing.
    - Provides utility functions for hashing passwords and verifying them.
    - Updates the `get_current_user` dependency to decode and verify JWT tokens.
- **Example code snippets:**
    - **Hashing and verifying passwords:**
        
        ```python
        from passlib.context import CryptContext
        pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto")
        
        def verify_password(plain_password, hashed_password):
            return pwd_context.verify(plain_password, hashed_password)
        
        def get_password_hash(password):
            return pwd_context.hash(password)
        ```
        
    - **Creating a JWT token:**
        
        ```python
        import jwt
        from datetime import timedelta, datetime
        
        SECRET_KEY = "your-secret-key"
        ALGORITHM = "HS256"
        
        def create_access_token(data: dict, expires_delta: timedelta | None = None):
            to_encode = data.copy()
            expire = datetime.utcnow() + (expires_delta or timedelta(minutes=15))
            to_encode.update({"exp": expire})
            encoded_jwt = jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)
            return encoded_jwt
        ```
        
- Summarizes the full security flow from authentication to protected endpoints.

**tutorial/middleware.md**
- Explains how to add middleware to a FastAPI app.
- **Key points:**
    - Middleware intercepts every request and response.
    - Use the `@app.middleware("http")` decorator.
- **Example code:**
    
    ```python
    import time
    from fastapi import Request
    
    @app.middleware("http")
    async def add_process_time_header(request: Request, call_next):
        start_time = time.perf_counter()
        response = await call_next(request)
        process_time = time.perf_counter() - start_time
        response.headers["X-Process-Time"] = str(process_time)
        return response
    ```
    
- Mentions ordering: middleware runs before dependency cleanup and before background tasks.

**tutorial/cors.md**
- Describes setting up Cross-Origin Resource Sharing (CORS) to allow frontend clients from other origins.
- **Key points:**
    - Use `CORSMiddleware` to configure allowed origins, methods, headers, and credentials.
    - Explains the difference between using a wildcard (`*`) and specific origins.
- **Example code:**
    
    ```python
    from fastapi.middleware.cors import CORSMiddleware
    
    app.add_middleware(
        CORSMiddleware,
        allow_origins=["https://example.com", "http://localhost:3000"],
        allow_credentials=True,
        allow_methods=["*"],
        allow_headers=["*"],
    )
    ```
    
- Highlights that CORS settings affect both security and documentation.

**tutorial/sql-databases.md**
- Explains integration with SQL databases (e.g. via SQLAlchemy).
- **Key points:**
    - Shows how to create database sessions as dependencies.
    - Demonstrates executing queries and managing transactions.
- (Exact code examples are in the tutorial file but typically include creating a session dependency and using it in path operations.)

**tutorial/bigger-applications.md**
- Covers structuring larger applications.
- **Key points:**
    - Organize code into multiple modules and use APIRouters to group endpoints.
    - Shows how to “mount” routers into the main app.
- **Example structure:**
    
    ```python
    from fastapi import APIRouter
    
    router = APIRouter()
    
    @router.get("/users/")
    async def read_users():
        return [{"username": "johndoe"}]
    
    app.include_router(router, prefix="/api/v1")
    ```
    
- Emphasizes code reuse, scalability, and maintainability.

**tutorial/background-tasks.md**
- Explains how to schedule background tasks to run after a response is sent.
- **Key points:**
    - Use the `BackgroundTasks` dependency in your path operations.
    - Background tasks are useful for sending emails, logging, or other operations that don’t need to block the response.
- **Example code:**
    
    ```python
    from fastapi import BackgroundTasks
    
    def write_log(message: str):
        with open("log.txt", "a") as f:
            f.write(message)
    
    @app.post("/send-notification/")
    async def send_notification(background_tasks: BackgroundTasks):
        background_tasks.add_task(write_log, "Notification sent")
        return {"message": "Notification sent in background"}
    ```
    
- Mentions that background tasks run after the response is sent.

**tutorial/metadata.md**
- Details how to set global metadata for the API and for tags.
- **Key points:**
    - Configure API title, summary, description, version, terms, contact, and license info via FastAPI’s constructor.
    - Define `openapi_tags` to add metadata (description, external docs) to groups of endpoints.
- **Example code:**
    
    ```python
    app = FastAPI(
        title="My API",
        description="This is a very fancy project, with **FastAPI**!",
        version="2.0.0",
        openapi_tags=[
            {
                "name": "users",
                "description": "Operations with users. **Read**, **create**, etc.",
            },
            {
                "name": "items",
                "description": "Manage items. _List_, _update_, etc.",
            },
        ]
    )
    ```
    
- Explains that metadata appears in the automatically generated OpenAPI docs and interactive UIs.

**tutorial/static-files.md**
- Explains how to serve static files (CSS, JS, images) with FastAPI.
- **Key points:**
    - Use `StaticFiles` from Starlette (available via FastAPI) to “mount” a directory.
    - Mounting creates an independent sub-application that handles all paths under a prefix.
- **Example code:**
    
    ```python
    from fastapi.staticfiles import StaticFiles
    
    app.mount("/static", StaticFiles(directory="static"), name="static")
    ```
    
- Notes that the mounted app’s OpenAPI schema is separate from the main app.

**tutorial/testing.md**
- Covers testing FastAPI applications.
- **Key points:**
    - Use the `TestClient` from Starlette (or httpx) to simulate requests.
    - Write tests as normal functions using pytest.
- **Example code:**
    
    ```python
    from fastapi.testclient import TestClient
    from main import app
    
    client = TestClient(app)
    
    def test_read_root():
        response = client.get("/")
        assert response.status_code == 200
        assert response.json() == {"message": "Hello World"}
    ```
    
- Mentions that async path operations are called synchronously by the TestClient.

**tutorial/debugging.md**
- Provides guidance on debugging FastAPI applications.
- **Key points:**
    - Run Uvicorn directly from your code so you can attach a debugger (e.g. with VS Code or PyCharm).
    - Use the `if __name__ == "__main__":` block to run your app locally.
- **Example code:**
    
    ```python
    if __name__ == "__main__":
        import uvicorn
        uvicorn.run(app, host="0.0.0.0", port=8000)
    ```
    
- Explains how to set breakpoints and use integrated debugging tools.

### Dependencies
**tutorial/dependencies/index.md**
- Introduces dependency injection: a way to declare and “inject” shared code or resources.
- **Key points:**
    - Dependencies can handle shared logic like authentication, database sessions, etc.
    - FastAPI automatically resolves dependencies declared with `Depends()`.
- **Example:** See the earlier `common_parameters` example in query parameters.

**tutorial/dependencies/classes-as-dependencies.md**
- Shows that classes (with an `__init__`) can be used as dependencies.
- **Key points:**
    - Using classes can improve type hinting and reuse.
    - A shortcut exists: when the dependency is a class, you can write `Depends()` without repeating the class name.
- **Example code:** (see earlier section)

**tutorial/dependencies/sub-dependencies.md**
- Demonstrates that dependencies may have their own dependencies.
- **Key points:**
    - Sub-dependencies are resolved first and can be cached per request.
    - You can disable caching if needed.
- **Example code:** (see earlier query/cookie extractor example)

**tutorial/dependencies/dependencies-in-path-operation-decorators.md**
- Explains adding dependencies directly in the route decorator.
- **Key points:**
    - Use the `dependencies` parameter to execute dependencies whose return values are not needed.
    - Helps avoid “unused” parameters in your function signature.
- **Example code:** (see earlier example)

**tutorial/dependencies/global-dependencies.md**
- Describes setting global dependencies on the FastAPI application.
- **Key points:**
    - Global dependencies apply to every route in the application.
    - Useful for things like common authentication or logging.
- **Example code:**
    
    ```python
    app = FastAPI(dependencies=[Depends(common_parameters)])
    ```
    
**tutorial/dependencies/dependencies-with-yield.md**
- Covers dependencies that use `yield` to provide a resource and run cleanup code afterward.
- **Key points:**
    - Useful for managing resources (like database sessions).
    - FastAPI turns such functions into context managers.
- **Example code:** (see earlier `get_db()` example)
### Security
**tutorial/security/index.md**
- Provides an overview of FastAPI’s security system.
- **Key points:**
    - Security is built on top of dependency injection.
    - Supports multiple schemes: API keys, OAuth2, HTTP Basic, etc.
    - Integrates with OpenAPI for automatic docs.

**tutorial/security/first-steps.md**
- Introduces a basic OAuth2 password flow.
- **Key points:**
    - Uses `OAuth2PasswordBearer` to extract a token from the `Authorization` header.
    - Enables the “Authorize” button in the docs.
- **Example code:** (see earlier snippet)

**tutorial/security/get-current-user.md**
- Implements a dependency to retrieve the current user based on a token.
- **Key points:**
    - Defines a Pydantic `User` model.
    - Uses a fake utility (or real database lookup) to decode the token.
- **Example code:** (see earlier snippet)

**tutorial/security/simple-oauth2.md**
- Completes a simple OAuth2 flow using form data.
- **Key points:**
    - Uses `OAuth2PasswordRequestForm` to get `username`, `password`, and optional `scope`.
    - Authenticates the user and returns a token.
- **Example code:** (see earlier snippet)

**tutorial/security/oauth2-jwt.md**
- Upgrades the simple flow with JWT tokens and secure password hashing.
- **Key points:**
    - Introduces JWT for signing tokens.
    - Uses PyJWT and PassLib to hash passwords and create/verify tokens.
    - Updates dependencies to decode JWT and protect endpoints.
- **Example code:** (see earlier hashing and JWT examples)

**tutorial/middleware.md**
- Explains how to add middleware to intercept requests/responses.
- **Key points:**
    - Use `@app.middleware("http")` to wrap requests.
    - Can measure process time, add headers, or log data.
- **Example code:** (see earlier)

**tutorial/cors.md**
- Shows how to configure CORS settings.
- **Key points:**
    - Use `CORSMiddleware` to allow cross-origin requests.
    - Configure allowed origins, methods, headers, and credentials.
- **Example code:** (see earlier)

**tutorial/sql-databases.md**
- (Not fully excerpted here, but covers:)
- Connecting to SQL databases (using SQLAlchemy, for example).
- Managing sessions with dependencies.
- Executing queries and handling transactions.

**tutorial/bigger-applications.md**
- Describes structuring large FastAPI applications.
- **Key points:**
    - Organize code with multiple modules and routers.
    - Use `APIRouter` and mount routers on prefixes.
- **Example code:** (see earlier router example)

**tutorial/background-tasks.md**
- Explains running tasks in the background after sending a response.
- **Key points:**
    - Use the `BackgroundTasks` parameter to schedule tasks.
    - Ideal for sending emails, logging, etc.
- **Example code:** (see earlier)

**tutorial/metadata.md**
- Details how to configure API metadata and docs URLs.
- **Key points:**
    - Set title, description, version, terms, contact, and license when creating the FastAPI app.
    - Define tag metadata via `openapi_tags`.
- **Example code:** (see earlier)

**tutorial/static-files.md**
- Covers serving static files from a directory.
- **Key points:**
    - Use `StaticFiles` and mount it to a specific URL prefix.
- **Example code:** (see earlier)

**tutorial/testing.md**
- Explains how to test FastAPI applications.
- **Key points:**
    - Use `TestClient` from Starlette (or httpx) along with pytest.
    - Write tests as normal functions and assert responses.
- **Example code:** (see earlier)

**tutorial/debugging.md**
- Provides tips on debugging your FastAPI app.
- **Key points:**
    - Run Uvicorn directly (with a `__main__` block) to enable IDE debugging.
    - Set breakpoints and use integrated debugger features in VS Code/PyCharm.
- **Example code:** (see earlier)

_Source: [https://fastapi.tiangolo.com/tutorial/](https://fastapi.tiangolo.com/tutorial/) (summarised by o3-mini-high)_