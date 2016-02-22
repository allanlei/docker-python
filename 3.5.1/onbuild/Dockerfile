FROM            alpine:3.3
MAINTAINER      Orbweb Inc. <devs@orbweb.com>

ENV             LANG C.UTF-8
ENV             PYTHON_VERSION 3.5.1
ENV             PYTHON_PIP_VERSION 7.1.2
ENV             PYTHONUNBUFFERED True
ENV             PIP_NO_CACHE_DIR off
ENV             PIP_DISABLE_PIP_VERSION_CHECK on

COPY            gnureadline-6.3.3-cp35-cp35m-linux_x86_64.whl /tmp/
RUN             apk --no-cache add \
                    python3=$PYTHON_VERSION-r0 && \
                ln -s $(which idle3) /usr/local/bin/idle && \
                ln -s $(which pydoc3) /usr/local/bin/pydoc && \
                ln -s $(which python3) /usr/local/bin/python && \
                ln -s $(which python-config3) /usr/local/bin/python-config && \
                python -m ensurepip --default-pip && \
                pip install pip==$PYTHON_PIP_VERSION && \
                pip install /tmp/gnureadline-6.3.3-cp35-cp35m-linux_x86_64.whl && \
                rm /tmp/gnureadline-6.3.3-cp35-cp35m-linux_x86_64.whl

RUN             apk --no-cache add --virtual .build-deps \
                    build-base \
                    python3-dev=$PYTHON_VERSION-r0 \
                    openssl-dev \
                    libffi-dev \
                    zlib-dev && \
                ln -s /lib/libz.so /usr/lib/. && \
                pip install wheel==0.26.0 && \
                pip install \
                    cython==0.23.4 \
                    pyOpenSSL==0.15.1 \
                    ndg-httpsclient==0.4.0 \
                    pyasn1==0.1.9 \
                    pyasn1-modules==0.0.8 \
                    pycparser==2.14 \
                    cryptography==1.2.1 \
                    cffi==1.5.0 \
                    certifi==2015.11.20.1 && \
                apk --no-cache add --virtual .rundeps \
                    zlib && \
                mkdir -p /usr/src/app/
WORKDIR         /usr/src/app/
CMD             ["python"]

ONBUILD COPY    requirements.txt /usr/src/app/
ONBUILD RUN     cat requirements.txt | grep -oh -E "builddeps:(\w|,|-)*" | awk '{split($0,a,":"); print a[2]}' | awk '{gsub(/,/, "\n", $0); print $0}' | sort -u | xargs apk --no-cache add --virtual .builddeps && \
                cat requirements.txt | grep -oh -E "rundeps:(\w|,|-)*" | awk '{split($0,a,":"); print a[2]}' | awk '{gsub(/,/, "\n", $0); print $0}' | sort -u | xargs apk --no-cache add --virtual .rundeps && \
                pip install -r requirements.txt && \
                pip uninstall -y cython && \
                apk del .builddeps && \
                find /usr/ \
                    \( -type d -a -name test -o -name tests \) \
                    -o \( -type f -a -name '*.pyc' -o -name '*.pyo' \) \
                    -exec rm -rf '{}' + && \
                find . -type f -name "__pycache__" -exec rm -rf '{}' +
ONBUILD COPY    . /usr/src/app
