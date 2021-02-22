FROM alpine
SHELL ["/bin/sh", "-c"]

RUN set -xe 

RUN apk add --no-cache \
  ca-certificates \
  build-base \
  libffi-dev \
  libxml2 \
  libxml2-dev \
  libxslt \
  libxslt-dev \
  openssl-dev \
  python3 \
  python3-dev \
  py3-pip \
  nano

RUN pip install --upgrade pip \
  && pip install 'cryptography<=3' \
  appdirs \
  cssselect \
  keyring \
  lxml \
  minidb \
  pyyaml \
  requests \
  chump \
  urlwatch

RUN apk del build-base \
  libffi-dev \
  libxml2-dev \
  libxslt-dev \
  openssl-dev \
  python3-dev

RUN echo '*/30 * * * * cd /root/.urlwatch && urlwatch --urls urls.yaml --config urlwatch.yaml --hooks hooks.py --cache cache.db' | crontab -

VOLUME /root/.urlwatch
WORKDIR /root/.urlwatch

CMD ["crond", "-f", "-L", "/dev/stdout"]