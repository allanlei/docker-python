FROM            python:2.7.10-slim

RUN             mkdir -p /usr/src/app
WORKDIR         /usr/src/app
ENV             PYTHON_PIP_VERSION 7.1.2

RUN             apt-get update && \
                apt-get install -y gcc make python2.7-dev libmemcached-dev libpq-dev libev-dev libxml2-dev libxslt-dev libssl-dev libffi-dev libreadline-dev libncurses-dev patch && \
                pip install --no-cache-dir -U pip==$PYTHON_PIP_VERSION setuptools==18.3.2 wheel==0.26.0 && \
                pip install --no-cache-dir pyOpenSSL==0.15.1 ndg-httpsclient==0.4.0 pyasn1==0.1.9 pyasn1-modules==0.0.8 pycparser==2.14 cryptography==1.0.2 cffi==1.2.1 readline==6.2.4.1 && \
                apt-get autoremove -y && \
                apt-get autoclean -y && \
                rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
