FROM ubuntu:12.04

# Update sources list
RUN sed -e 's/\#\ deb/deb/' /etc/apt/sources.list > /tmp/updated.list
RUN mv /tmp/updated.list /etc/apt/sources.list
RUN apt-get -y update

# Install packages
RUN apt-get -y install build-essential g++ git subversion wget vim
RUN apt-get -y build-dep python
RUN apt-get -y install zlib1g-dev libreadline-dev libsqlite3-dev libssl-dev libxslt1-dev libbz2-dev libldap2-dev libsasl2-dev libpcre3-dev libjpeg8-dev libfreetype6-dev liblcms1-dev libwebp-dev libtiff-dev libffi-dev

# Create neede folders
RUN mkdir /var/python
RUN mkdir /var/plone
RUN mkdir /var/pyramid

# Creat users
RUN adduser plone --system
RUN chown -R plone /var/plone
RUN chmod -R 775 /var/plone
RUN adduser pyramid --system
RUN chown -R pyramid /var/pyramid
RUN chmod -R 775 /var/pyramid

# Downloads
RUN mkdir /tmp/downloads
WORKDIR /tmp/downloads
RUN wget https://www.python.org/ftp/python/2.7.6/Python-2.7.6.tgz
RUN wget https://bootstrap.pypa.io/ez_setup.py

# Compile and configure python 2.7
RUN tar zxvf Python-2.7.6.tgz
WORKDIR Python-2.7.6
RUN ./configure --prefix=/var/python/python2.7/ --enable-unicode=ucs4
RUN make
RUN make install

ENV PYTHON27_BIN /var/python/python2.7/bin
RUN $PYTHON27_BIN/python /tmp/downloads/ez_setup.py
RUN $PYTHON27_BIN/easy_install pip
RUN $PYTHON27_BIN//pip install virtualenv

RUN $PYTHON27_BIN//virtualenv --distribute --no-site-packages /var/plone/python2.7
RUN $PYTHON27_BIN//virtualenv --distribute --no-site-packages /var/pyramid/python2.7

ENV PLONE_PY27 /var/plone/python2.7/bin/python
ENV PYRAMID_PY27 /var/pyramid/python2.7/bin/python

CMD /bin/bash
