

Dockerized Notebook + SciPy Stack + Nginx
=================================

Docker container for the [SciPy stack](../scipystack) and configured IPython notebook server.

## Build the Image

```
docker build -t zischwartz/thebe-standalone  .
```

## To Run 

```
docker run -d -p 8888:8888 -p 80:80 -v $PWD/public:/var/www/html zischwartz/thebe-standalone
```

Assuming you're running boot2docker, now you can visit http://192.168.59.103:8888 in your browser.


# Run Container Interactively and SSH In (For Debugging)

```
docker run  -p 8888:8888 -p 80:80 -i -t --entrypoint /bin/bash zischwartz/thebe-standalone
```