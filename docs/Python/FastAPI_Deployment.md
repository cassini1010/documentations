# FastAPI Deployment

To **deploy** an application means to perform the necessary steps to make it **available to users**.

Ensure that you use the appropriate version of FastAPI that is best suited for your production application. Using a dependency management tool like `uv` will handle this automatically.

```toml
fastapi[standard]>=0.112.0,<0.113.0
```

> **WARNING**: Do not specify a version for the starlette library.
