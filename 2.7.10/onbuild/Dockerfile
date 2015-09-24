FROM            python:2.7.10-slim

RUN             mkdir -p /usr/src/app
WORKDIR         /usr/src/app

RUN             apt-get update && \
                apt-get install -y gcc make python2.7-dev libmemcached-dev libpq-dev libev-dev libxml2-dev libxslt-dev libssl-dev libffi-dev libreadline-dev libncurses-dev patch && \
                pip install --no-cache-dir pip==7.1.2 setuptools==18.3.2 wheel==0.26.0 && \
                pip install --no-cache-dir pyOpenSSL==0.15.1 ndg-httpsclient==0.4.0 pyasn1==0.1.8 pyasn1-modules==0.0.6 pycparser==2.14 cryptography==1.0.1 cffi==1.1.2 readline==6.2.4.1 && \
                pip uninstall -y virtualenv && \
                apt-get autoremove -y && \
                apt-get autoclean -y && \
                rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
ONBUILD COPY    requirements.txt /usr/src/app/
ONBUILD RUN     pip install --no-cache-dir -r requirements.txt

ONBUILD COPY    . /usr/src/app
