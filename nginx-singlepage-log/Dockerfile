FROM alpine
LABEL cvc.com.br.version="1.0" \
      vendor="CVC Brasil S.A." \
      cvc.com.br.release-date="2017-11-10"

RUN apk add --no-cache nginx \
    && rm -f var/log/nginx/access.log && ln -sf /dev/stdout /var/log/nginx/access.log \
    && rm -f /var/log/nginx/error.log && ln -sf /dev/stderr /var/log/nginx/error.log

COPY nginx/nginx.conf /etc/nginx/nginx.conf

RUN rm -f /etc/nginx/conf.d/default.conf \
    && mkdir -p /var/www/html 

COPY nginx/conf.d/* /etc/nginx/conf.d/

CMD ["nginx", "-g", "daemon off;"]

EXPOSE 80
