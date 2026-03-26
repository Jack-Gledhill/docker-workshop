# Docker Workshop

Hello and welcome! Here, you'll find resources for the practical part of the 2026 Docker Workshop. Please let one of the presenters know if you need any help throughout the workshop :)

## Prerequisities

Before you can begin the practical, you'll need to make sure you have Docker Desktop installed and running on your machine. If you don't already have it, you can download it [here](https://www.docker.com/products/docker-desktop/).

You can also find the slides for the workshop [here](https://docs.google.com/presentation/d/1cGJq96nYjEv6e9qEKliwDzeD01LFHF_7/edit?usp=sharing&ouid=117861215468504628058&rtpof=true&sd=true) (university login required)!

## Task 1: Basic Flask App

First, we're going to setup a basic Python Flask application using Docker. Flask is a web framework for Python, allowing you to run a simple web server on your local machine with very little code.

To get started, you'll want to create a new directory **and take note of its path**. Then, within that directory you'll want to create three files:

1. `app.py`: this is the Python file that will contain your Flask code
2. `requirements.txt`: this is a file used by PIP to store your application's dependencies (similar to `package.lock` in Node.js)
3. `dockerfile`: this tells Docker how to construct an image for your application

You'll then need to populate each of these files. Starting with `requirements.txt`, you'll want to add the following lines:

```
requirements.txt
```

Now onto your `app.py`:
```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
  return '<h1>Hello from Flask + Docker</h1>'

if __name__ == "__main__":
  app.run(host="0.0.0.0", port=8067)
```

And lastly, your `dockerfile`:

```
FROM python:3.8-slim-buster

WORKDIR /python-docker

COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt

COPY . .

EXPOSE 8067:8067

CMD ["python3", "app.py"]
```

## Task 2: Build your Docker Image

Now that you've setup your application, you'll want to open up your command-line and `cd` into the directory you created earlier. Now, you'll want to tell Docker to package your application into an image, which you can do by running:

```bash
docker build --tag python-docker .
```

With that done, it's time to run your application. This is done with another Docker command:

```bash
docker run -d -p 8067:8067 python-docker
```

You should now be able to test your application by visiting [localhost:8067](http://localhost:8067).

## Task 3: Over to you

If you've got this far, you might want to consider having a go at running Docker on your own. You could run more interesting containers like wordpress or minecraft. You could even try creating your own dockerfile for one of your other projects. Have a go, see what you can do! 
