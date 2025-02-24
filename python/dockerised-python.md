The following `Dockerfile` configuration:
1. Figures out what shell you’re running.
2. Adds a `deactivate` function to your shell, and messes around with `pydoc`.
3. Changes the shell prompt to include the virtualenv name.
4. Unset the `PYTHONHOME` environment variable, if someone happened to set it.
5. Sets two environment variables: `VIRTUAL_ENV` and `PATH`.
```
FROM python:3.12-slim

ENV VIRTUAL_ENV=/opt/venv
RUN python3 -m venv $VIRTUAL_ENV
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

# Install dependencies:
COPY requirements.txt .
RUN pip install -r requirements.txt

# Run the application:
COPY myapp.py .
CMD ["python", "myapp.py"]
```

Build the image:
```
docker build -t getting-started .
```

Start the container:
```
docker run -d -p 80:80 getting-started
```

_Sources:_
- _[https://pythonspeed.com/articles/activate-virtualenv-dockerfile/](https://pythonspeed.com/articles/activate-virtualenv-dockerfile/)_
- _[https://docs.docker.com/get-started/workshop/02_our_app/](https://docs.docker.com/get-started/workshop/02_our_app/)_
