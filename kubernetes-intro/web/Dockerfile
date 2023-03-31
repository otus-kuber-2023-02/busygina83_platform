FROM nginx:latest

MAINTAINER Busygina Inna

ENV TZ=Europe/Moscow

RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN mkdir /app
RUN echo "Hello OTUS!" > /app/homework.html
RUN sed -i -e 's/80;/8000;/g' /etc/nginx/conf.d/default.conf
RUN sed -i -e 's/\/usr\/share\/nginx\/html/\/app/g' /etc/nginx/conf.d/default.conf
RUN sed -i -e 's/index.html index.htm/\*/g' /etc/nginx/conf.d/default.conf

WORKDIR /app
RUN chown -R nginx:nginx /app && chmod -R 755 /app && \
        chown -R nginx:nginx /var/cache/nginx && \
        chown -R nginx:nginx /var/log/nginx && \
        chown -R nginx:nginx /etc/nginx/conf.d
RUN touch /var/run/nginx.pid && \
        chown -R nginx:nginx /var/run/nginx.pid

USER nginx
CMD nginx
