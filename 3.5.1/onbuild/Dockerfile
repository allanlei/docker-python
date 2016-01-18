FROM            alpine:3.3
MAINTAINER      Orbweb Inc. <devs@orbweb.com>

ENV             LANG C.UTF-8
ENV             PYTHONUNBUFFERED True
ENV             PYTHON_VERSION 3.5.1-r0

RUN             mkdir -p /usr/src/app
WORKDIR         /usr/src/app

RUN             apk --no-cache add \
                    python3=$PYTHON_VERSION && \
                ln -s $(which python3) /usr/bin/python && \
                python -m ensurepip --default-pip && \
                apk --no-cache add --virtual build-dependencies \
                    build-base python3-dev=$PYTHON_VERSION openssl-dev libffi-dev zlib-dev \
                    libmemcached-dev postgresql-dev libev-dev libxml2-dev libxslt-dev \
                    jpeg-dev tiff-dev libwebp-dev freetype-dev openjpeg-dev && \
                ln -s /lib/libz.so /usr/lib/. && \
                pip install --disable-pip-version-check --no-cache-dir \
                    wheel==0.26.0 cython==0.23.4 \
                    readline==6.2.4.1 \
                    pyOpenSSL==0.15.1 ndg-httpsclient==0.4.0 \
                    pyasn1==0.1.9 pyasn1-modules==0.0.8 pycparser==2.14 \
                    cryptography==1.0.2 cffi==1.2.1 certifi==2015.11.20.1

ONBUILD COPY    requirements.txt /usr/src/app/
ONBUILD RUN     pip install -vvv --disable-pip-version-check --no-cache-dir -r requirements.txt && \
                pip uninstall -y cython && \
                apk del build-dependencies
ONBUILD COPY    . /usr/src/app
