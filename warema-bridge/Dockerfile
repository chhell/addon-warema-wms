ARG BUILD_FROM
FROM ${BUILD_FROM}

RUN apk add --no-cache nodejs

WORKDIR /srv

COPY srv/package.json srv/package-lock.json ./

# rebuild from sources to avoid issues with prebuilt binaries (https://github.com/serialport/node-serialport/issues/2438)
RUN apk add --no-cache --virtual .build-deps npm python3 make g++ linux-headers \
    && npm ci --omit=dev \
    && npm rebuild --build-from-source \
    && apk del .build-deps

COPY etc /etc
COPY srv /srv
RUN chmod a+x /etc/services.d/warema-bridge/*
