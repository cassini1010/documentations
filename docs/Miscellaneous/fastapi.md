# FastAPI

A simple working code to get started

```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/")
def root():
    return {"Hello": "JK"}

@app.get("/items/{item_id}")
def get_item(item_id: int, skip: int = 0, limit: int = 30):
    return {
            "item_id": item_id,
            "limit": limit,
            "skip": skip
            }
```

## Path Parameter

Path parameter is provided in python `f-string` style. 

## Query Parameter

Query parameters are the extra parameter that are not part of the path. In a URL they are provided after a `?` and separated by `&`

Example : `http://localhost:8000/items/4?skip=0&limit=10`

> If a parameter is also present in the path its a `path parameter`. If a parameter is of singular type like `int` , `float` , `str` ,`bool` etc... then it is a `query parameter`. If a parameter is a `Pydantic Model` then its a `Request Body` used in post or put calls.

## Important Status Codes

### Success Codes

| Status Code | Description                                            |
| ----------- | ------------------------------------------------------ |
| 200         | Request was successful and a response body is returned |
| 204         | Request was successful but the response body is empty  |

### Client-Side Status Codes

| Status Code | Description                                                                      |
| ----------- | -------------------------------------------------------------------------------- |
| 400         | Bad Request                                                                      |
| 401         | Unauthorized                                                                     |
| 403         | Forbidden. The client (browser) is not allowed to access the requested resource. |
| 404         | Page not found                                                                   |

### Server-Side Status Codes

| Status Code | Description                                                             |
| ----------- | ----------------------------------------------------------------------- |
| 500         | Internal Server Error                                                   |
| 502         | Bad Gateway                                                             |
| 503         | Service Unavailable. The server is currently unavailable or turned off. |

## Testing

Testing of APIs are done by `TestClient` in Fastapi.

- Import `TestClient` 

- Create a `TestClient` by passing your **FastAPI** application to it.

- Create functions with a name that starts with `test_` (this is standard `pytest` conventions).

```python
from fastapi import FastAPI
from fastapi.testclient import TestClient

app = FastAPI()


@app.get("/")
async def read_main():
    return {"msg": "Hello World"}
```

Keep the testing logic in other file. Ex: `test_main.py`

```python
from fastapi.testclient import TestClient


client = TestClient(app)


def test_read_main():
    response = client.get("/")
    assert response.status_code == 200
    assert response.json() == {"msg": "Hello World"}
```

## Debugging

You can debug your FastAPI application using the following code snippet. Run the code with the VS Code Python debugger enabled.

```python
if __name__ == "__main__":
    uvicorn.run(app, host="0.0.0.0", port=8000)
```

## FastAPI deployment

To **deploy** an application means to perform the necessary steps to make it **available to users**.

Ensure that you use the appropriate version of FastAPI that is best suited for your production application. Using a dependency management tool like `uv` will handle this automatically.

```toml
fastapi[standard]>=0.112.0,<0.113.0
```

> **WARNING**: Do not specify a version for the starlette library.



> IMPORTANT : It is a common practice to have **one program/HTTP server** (TLS Termination Proxy) running on the server (the machine, host, etc.) and **managing all the HTTPS parts** like receiving the **encrypted HTTPS requests**, sending the **decrypted HTTP requests** to the actual HTTP application running in the same server (the **FastAPI** application, in this case), take the **HTTP response** from the application, **encrypt it** using the appropriate **HTTPS certificate** and sending it back to the client using **HTTPS**.



### TLS Termination Proxy

- Traefik (has certificate renewal feature)

- Caddy (has certificate renewal feature)

- Nginx (`certbot` can be used for cert renewal)

- Kubernetes with an Ingress Controller like Nginx ✅
