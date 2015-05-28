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


Run iruby, tmpnb

```
docker run --net=host -d -e CONFIGPROXY_AUTH_TOKEN=$TOKEN -v /var/run/docker.sock:/docker.sock zischwartz/tmpnb python orchestrate.py --image="zischwartz/others" --allow_origin="*" --command="bash -l -c 'iruby notebook --no-browser --port {port} --ip=* --NotebookApp.allow_origin=* --NotebookApp.base_url={base_path}'" --cull_timeout=240 --cull_period=60
```