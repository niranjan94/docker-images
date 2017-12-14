FROM alpine:3.7
MAINTAINER Niranjan Rajendran <me@niranjan.io>

# Install nginx, nodejs, npm, yarn
RUN echo "http://dl-4.alpinelinux.org/alpine/v3.7/main" >> /etc/apk/repositories && \
    apk add --update ca-certificates nginx && \
    update-ca-certificates && \
    apk add yarn && \
    rm -rf /usr/include \
    /usr/share/man /tmp/* /var/cache/apk/* /root/.npm /root/.node-gyp \
    /usr/lib/node_modules/npm/man /usr/lib/node_modules/npm/doc /usr/lib/node_modules/npm/html && \
    chown -R nginx:www-data /var/lib/nginx && \
    node --version && npm --version && yarn --version

COPY root /

# Expose the ports for nginx
EXPOSE 80 443

ENTRYPOINT ["entrypoint.sh"]
