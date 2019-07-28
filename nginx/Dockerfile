FROM nginx:alpine

## label and credits
LABEL image="Gitea HTTPS - Nginx Reverse Proxy Docker Image" \
      maintainer="Roozbeh Shafiee, me@roozbeh.cloud" \
      version="1.0.0-production" \
      released="July 28th, 2019" \
      reference="https://roozbeh.cloud, https://github.com/RoozbehShafiee"

## manage packages and repositories
RUN apk add --update --no-cache \
        ca-certificates \
        curl \
        libressl \
        certbot \
        python3 \
        py3-pip \
    && pip3 install --upgrade pip \
    && pip3 install 'certbot-nginx' \
    && pip3 install 'pyopenssl' \
    && rm -f /var/cache/apk/*

## managing files, directories and configuration file
COPY entrypoint.sh /entrypoint.sh
COPY gitea /etc/nginx/conf.d/gitea
COPY nginx.conf /etc/nginx/nginx.conf
RUN chmod +x /entrypoint.sh \
    && mkdir -p /run/nginx \
    && mkdir -p /tmp/nginx

## expose port
EXPOSE 443 80

## running commands to start services
STOPSIGNAL SIGTERM
ENTRYPOINT ["/entrypoint.sh"]
