FROM            python:3.5.2-alpine
MAINTAINER      Allan Lei<allanlei@helveticode.com>

ENV             PYTHONUNBUFFERED True
ENV             PIP_DISABLE_PIP_VERSION_CHECK on
ENV             WORKDIR /usr/src/app/

WORKDIR         $WORKDIR
RUN             echo "@edge-main http://dl-cdn.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories && \
                echo "@edge-community http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories && \
                echo "@edge-testing http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories

# ISSUE: https://github.com/docker/docker/issues/13045
ONBUILD COPY    requirements*.txt $WORKDIR
ONBUILD RUN     apk --no-cache add --virtual .build-deps \
                    build-base \
                    openssl-dev \
                    libffi-dev \
                    zlib-dev && \
                cat requirements.build.txt 2> /dev/null | xargs -r apk --no-cache add --virtual .build-deps && \
                pip install --no-cache-dir --use-wheel \
                    pyOpenSSL==16.0.0 \
                    ndg-httpsclient==0.4.2 \
                    pyasn1==0.1.9 \
                    pyasn1-modules==0.0.8 \
                    pycparser==2.14 \
                    cryptography==1.4 \
                    cffi==1.7.0 \
                    certifi==2016.8.8 && \
                pip install --no-cache-dir --use-wheel -r requirements.txt && \
                cat requirements.run.txt 2> /dev/null | xargs -r apk --no-cache add --virtual .run-deps && \
                scanelf --needed --nobanner --recursive /usr/local \
                    | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
                    | sort -u \
                    | xargs -r apk info --installed \
                    | sort -u \
                    | xargs -r apk --no-cache add --virtual .run-deps && \
                apk del .build-deps && \
                find /usr/local -depth \
            		\( \
            			\( -type d -a -name test -o -name tests \) \
            			-o \
            			\( -type f -a -name '*.pyc' -o -name '*.pyo' \) \
            		\) -exec rm -rf '{}' + && \
                find . -type d -name "__pycache__" -exec rm -rf '{}' +
ONBUILD COPY    . $WORKDIR
