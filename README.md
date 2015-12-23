# hit_counter

A basic Python web app to demonstrate linking docker containers

## How to use

Clone this repository for use with:

    $ git clone https://github.com/coopermaa/hit_counter

Build a docker image for python web application:

    $ docker build -t coopermaa/web .

Run a redis container, the container will export port 6379:

    $ docker run --name redis -d redis

Run python web application and link it with redis container:

    $ docker run --name web --link redis:redis \
      -p 5000:5000 -d coopermaa/web python app.py

The web app should now be listening on port 5000 on your docker daemon, we can visit it:

    # Inside Docker Host
    $ curl localhost:5000
    Hello World! I have been seen 1 times.
    $ curl localhost:5000
    Hello World! I have been seen 2 times.

    # Outside Docker host
    $ curl <docker host>:5000
    Hello World! I have been seen 3 times.