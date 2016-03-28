FROM nginx:1.9.0

ADD  nginx.conf      /etc/nginx/nginx.conf
ADD  sites-enabled/*    /etc/nginx/conf.d/

EXPOSE 80
VOLUME ["/var/www"]

