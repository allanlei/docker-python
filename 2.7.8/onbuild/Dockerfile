FROM            python:2.7.8-slim

RUN             mkdir -p /usr/src/app
WORKDIR         /usr/src/app

RUN             apt-get update && \
                apt-get install -y gcc python2.7-dev libmemcached-dev libpq-dev libev-dev libxml2-dev libxslt-dev libssl-dev libffi-dev && \
                pip install pip==7.0.0 setuptools==16.0.0 && \
                pip install pyOpenSSL==0.15.1 ndg-httpsclient==0.4.0 pyasn1==0.1.7 pycparser==2.13 cryptography==0.9 cffi==1.0.1 && \
                pip uninstall -y virtualenv && \
                apt-get autoremove -y && \
                apt-get autoclean -y && \
                rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
ONBUILD COPY    requirements.txt /usr/src/app/
ONBUILD RUN     pip install -r requirements.txt

ONBUILD COPY    . /usr/src/app
