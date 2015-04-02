FROM ipython/scipystack

MAINTAINER IPython Project <ipython-dev@scipy.org>

# VOLUME /notebooks
WORKDIR /notebooks

EXPOSE 8888

# You can mount your own SSL certs as necessary here
# ENV PEM_FILE /key.pem
# $PASSWORD will get `unset` within notebook.sh, turned into an IPython style hash
# ENV PASSWORD Dont make this your default
ENV USE_HTTP 1

# RUN apt-get install libfreeimage3

# Need this for add-apt below
RUN apt-get install python-software-properties software-properties-common -y
# Moviepy needs this
RUN add-apt-repository ppa:jon-severinsson/ffmpeg
RUN apt-get update && apt-get install ffmpeg -y

# COPY blank.ipynb /notebooks/blank.ipynb
COPY requirements.txt requirements.txt
RUN pip2.7 install -r requirements.txt

RUN unset PASSWORD

# ADD notebook.sh /
# RUN chmod u+x /notebook.sh
# CMD ["/notebook.sh"]

CMD ipython3 notebook --no-browser --port 8888 --ip=* --NotebookApp.allow_origin=* 


# docker run --net=host -d -e CONFIGPROXY_AUTH_TOKEN=$TOKEN -v /var/run/docker.sock:/docker.sock jupyter/tmpnb python orchestrate.py --command="ipython3 notebook --no-browser --port {port} --ip=* --NotebookApp.allow_origin=* --NotebookApp.base_url={base_path}"
# jupyter/tmpnb python orchestrate.py --image='jupyter/demo' --command="ipython3 notebook --no-browser --port {port} --ip=* --NotebookApp.allow_origin=*"

# ipython/scipyserver/