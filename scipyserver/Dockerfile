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

COPY requirements.txt requirements.txt
RUN pip2.7 install -r requirements.txt

RUN unset PASSWORD
RUN mkdir images

CMD ipython3 notebook --no-browser --port 8888 --ip=* --NotebookApp.allow_origin=* 