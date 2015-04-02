Dockerized Notebook + SciPy Stack
=================================

Docker container for the [SciPy stack](../scipystack) and configured IPython notebook server.

## Build the Image

```
docker build -t zischwartz/scipyserver  .
```

## To Run 

```
docker run -d -p 8888:8888 zischwartz/scipyserver
```

Assuming you're running boot2docker, now you can visit http://192.168.59.103:8888 in your browser.