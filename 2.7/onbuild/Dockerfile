FROM python:2.7.9

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

RUN apt-get update && \
    apt-get install -y libmemcached-dev && \
    apt-get autoremove -y && \
    apt-get autoclean -y
ONBUILD COPY requirements.txt /usr/src/app/
ONBUILD RUN pip install -r requirements.txt
# Fix: debian broken gevent.ssl by removing PROTOCOL_SSLv3
ONBUILD RUN sed -i 's/PROTOCOL_SSLv3/PROTOCOL_SSLv23/g' /usr/local/lib/python2.7/site-packages/gevent/ssl.py 2> /dev/null

ONBUILD COPY . /usr/src/app
