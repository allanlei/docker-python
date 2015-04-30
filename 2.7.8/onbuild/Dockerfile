FROM            python:2.7.8-slim

RUN             mkdir -p /usr/src/app
WORKDIR         /usr/src/app

RUN             apt-get update && \
                apt-get install -y gcc python2.7-dev libmemcached-dev libpq-dev libev-dev libxml2-dev libxslt-dev libssl-dev libffi-dev && \
                apt-get autoremove -y && \
                apt-get autoclean -y && \
                rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
                pip install pip==6.1.1 setuptools==15.2 pyOpenSSL ndg-httpsclient pyasn1 && \
                pip uninstall -y virtualenv
ONBUILD COPY    requirements.txt /usr/src/app/
ONBUILD RUN     pip install -r requirements.txt

ONBUILD COPY    . /usr/src/app
