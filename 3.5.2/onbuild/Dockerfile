FROM            python:3.5.2-alpine
MAINTAINER      Allan Lei<allanlei@helveticode.com>

ENV             PYTHON_SETUPTOOLS_VERSION 25.1.6
ENV             PYTHON_WHEEL_VERSION 0.29.0
ENV             PYTHONUNBUFFERED True
ENV             PIP_NO_CACHE_DIR off
ENV             PIP_DISABLE_PIP_VERSION_CHECK on
ENV             LIBRARY_PATH /lib:/usr/lib

RUN             pip install setuptools==$PYTHON_SETUPTOOLS_VERSION wheel==$PYTHON_WHEEL_VERSION && \
                mkdir -p /usr/src/app/
WORKDIR         /usr/src/app/

ONBUILD COPY    requirements.txt /usr/src/app/
ONBUILD COPY    requirements.*.txt /usr/src/app/
ONBUILD RUN     apk --no-cache add --virtual .build-deps \
                    build-base \
                    openssl-dev \
                    libffi-dev \
                    zlib-dev && \
                if [ -s "requirements.build.txt" ]; then cat requirements.build.txt | xargs apk --no-cache add --virtual .build-deps; fi && \
                pip install \
                    cython==0.24.1 \
                    pyOpenSSL==16.0.0 \
                    ndg-httpsclient==0.4.2 \
                    pyasn1==0.1.9 \
                    pyasn1-modules==0.0.8 \
                    pycparser==2.14 \
                    cryptography==1.4 \
                    cffi==1.7.0 \
                    certifi==2016.8.8 && \
                pip install -r requirements.txt && \
                if [ -s "requirements.run.txt" ]; then cat requirements.run.txt | xargs apk --no-cache add --virtual .run-deps; fi && \
                pip uninstall -y cython && \
                apk del .build-deps && \
                find /usr/ \
                    \( -type d -a -name test -o -name tests \) \
                    -o \( -type f -a -name '*.pyc' -o -name '*.pyo' \) \
                    -exec rm -rf '{}' + && \
                find . -type d -name "__pycache__" -exec rm -rf '{}' +
ONBUILD COPY    . /usr/src/app
