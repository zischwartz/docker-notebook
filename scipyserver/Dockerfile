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
# ENV USE_HTTP 0

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


# From https://github.com/tcnksm/dockerfile-rbenv/blob/master/Dockerfile
# Install packages for building ruby
RUN apt-get update
RUN apt-get install -y --force-yes build-essential curl git
RUN apt-get install -y --force-yes zlib1g-dev libssl-dev libreadline-dev libyaml-dev libxml2-dev libxslt-dev
# added by zach, because ruby build was failing https://github.com/sstephenson/ruby-build/issues/690
RUN apt-get install -y --force-yes libffi-dev
RUN apt-get install -y --force-yes bison libreadline6-dev libncurses5-dev libgdbm3 libgdbm-dev 
# added by zach to make ipython work
RUN apt-get install -y --force-yes autoconf libtool automake

RUN apt-get clean

# Install rbenv and ruby-build
RUN git clone https://github.com/sstephenson/rbenv.git /root/.rbenv
RUN git clone https://github.com/sstephenson/ruby-build.git /root/.rbenv/plugins/ruby-build
RUN /root/.rbenv/plugins/ruby-build/install.sh
ENV PATH /root/.rbenv/bin:$PATH

# RUN echo 'eval "$(rbenv init -)"' >> /etc/profile.d/rbenv.sh 
RUN echo 'eval "$(rbenv init -)"' >> /etc/profile
# RUN echo 'eval "$(rbenv init -)"' >> /root/.bashrc
# RUN echo 'eval "$(rbenv init -)"' >> /etc/bash.bashrc

# Just the one version
RUN echo '2.2.0' >> /root/versions.txt

# Install multiple versions of ruby
ENV CONFIGURE_OPTS --disable-install-doc
RUN xargs -L 1 rbenv install 2.2.0

# Install Bundler for each version of ruby
RUN echo 'gem: --no-rdoc --no-ri' >> /.gemrc
RUN bash -l -c 'for v in $(cat /root/versions.txt); do rbenv global $v; gem install bundler; done'

RUN apt-get install libzmq3-dev -y

RUN bash -l -c "gem install iruby"


# RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout key.pem -out key.pem \
    # -subj "/C=XX/ST=XX/L=XX/O=dockergenerated/CN=dockergenerated"

CMD bash -l -c "iruby notebook --no-browser --port 8888 --ip=* --NotebookApp.allow_origin=*"
# CMD ipython3 notebook --no-browser --port 8888 --ip=* --NotebookApp.allow_origin=*
# CMD ipython3 notebook --no-browser --port 8888 --ip=* --NotebookApp.allow_origin=*  --certfile=key.pem