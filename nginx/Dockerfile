FROM nginx:1.9.0

ADD  nginx.conf      /etc/nginx/nginx.conf
ADD  sites-enabled/*    /etc/nginx/conf.d/

RUN usermod -u 1000 www-data

EXPOSE 80 443

