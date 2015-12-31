FROM            alpine:3.3
MAINTAINER      Orbweb Inc. <devs@orbweb.com>

ENV             PYTHONUNBUFFERED=True

RUN             mkdir -p /usr/src/app
WORKDIR         /usr/src/app

RUN             apk --no-cache add \
                    python=2.7.11-r2 py-pip && \
                apk --no-cache add --virtual build-dependencies \
                    build-base python-dev=2.7.11-r2 openssl-dev libffi-dev zlib-dev \
                    libmemcached-dev postgresql-dev libev-dev libxml2-dev libxslt-dev \
                    jpeg-dev tiff-dev libwebp-dev freetype-dev openjpeg-dev && \
                ln -s /lib/libz.so /usr/lib/. && \
                pip install --no-cache-dir \
                    pip==7.1.2 setuptools==19.2 wheel==0.26.0 \
                    pyOpenSSL==0.15.1 ndg-httpsclient==0.4.0 \
                    pyasn1==0.1.9 pyasn1-modules==0.0.8 pycparser==2.14 \
                    cryptography==1.0.2 cffi==1.2.1 certifi==2015.11.20.1

ONBUILD COPY    requirements.txt /usr/src/app/
ONBUILD RUN     pip install --no-cache-dir -r requirements.txt && \
                apk del build-dependencies
ONBUILD COPY    . /usr/src/app
