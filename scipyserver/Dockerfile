FROM ipython/scipystack

MAINTAINER IPython Project <ipython-dev@scipy.org>

# VOLUME /notebooks
WORKDIR /notebooks

EXPOSE 8888

# You can mount your own SSL certs as necessary here
# ENV PEM_FILE /key.pem
# $PASSWORD will get `unset` within notebook.sh, turned into an IPython style hash
# ENV PASSWORD Dont make this your default
ENV USE_HTTP 0

# RUN apt-get install libfreeimage3

# Need this for add-apt below
RUN apt-get install python-software-properties software-properties-common -y

# Moviepy needs this, but sometimes the ppa isn't found
# RUN add-apt-repository ppa:jon-severinsson/ffmpeg
# RUN apt-get update && apt-get install ffmpeg -y

RUN pip install --upgrade pip
COPY requirements.txt requirements.txt
RUN pip2.7 install -r requirements.txt

RUN unset PASSWORD
RUN mkdir images

RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout key.pem -out key.pem \
    -subj "/C=XX/ST=XX/L=XX/O=dockergenerated/CN=dockergenerated"

CMD ipython3 notebook --no-browser --port 8888 --ip=* --NotebookApp.allow_origin=*  --certfile=key.pem