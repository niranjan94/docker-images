FROM alpine:3.7
MAINTAINER Niranjan Rajendran <me@niranjan.io>

ENV NGINX_VERSION=1.12.2-r3 NODE_VERSION=v6.11.3 NPM_VERSION=5

# Install nginx, nodejs, npm, yarn
RUN echo "http://dl-4.alpinelinux.org/alpine/v3.7/main" >> /etc/apk/repositories && \
    apk add --update git curl make gcc g++ python linux-headers libgcc libstdc++ ca-certificates binutils-gold nginx=${NGINX_VERSION} && \
    curl -sSL https://nodejs.org/dist/${NODE_VERSION}/node-${NODE_VERSION}.tar.gz | tar -xz && \
    cd /node-${NODE_VERSION} && \
    ./configure --prefix=/usr --without-snapshot && \
    make -j$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) | grep 'error\|fail\|fatal' && \
    make install && \
    apk add yarn && \
    cd / && \
    npm install -g npm@${NPM_VERSION} && \
    apk del curl make gcc g++ python linux-headers binutils-gold gnupg libstdc++ && \
    rm -rf /node-${NODE_VERSION} /usr/include \
    /usr/share/man /tmp/* /var/cache/apk/* /root/.npm /root/.node-gyp \
    /usr/lib/node_modules/npm/man /usr/lib/node_modules/npm/doc /usr/lib/node_modules/npm/html && \
    chown -R nginx:www-data /var/lib/nginx && \
    node --version && npm --version && yarn --version

COPY root /

# Expose the ports for nginx
EXPOSE 80 443

ENTRYPOINT ["entrypoint.sh"]
