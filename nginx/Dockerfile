FROM gliderlabs/alpine:3.3

MAINTAINER Okello Ambrose Felix <ambokello@gmail.com>

RUN apk add --no-cache nginx sed supervisor ca-certificates bash && \
    update-ca-certificates && \
    apk del build-dependencies

RUN mkdir -p /var/log/nginx/app


#RUN rm /etc/nginx/sites-enabled/default
COPY nginx.conf /etc/nginx/nginx.conf
RUN mkdir -p /etc/ssl/certs/
RUN mkdir -p /etc/ssl/private/
COPY *.crt /etc/ssl/certs/
COPY *.key /etc/ssl/private/
RUN echo "daemon off;" >> /etc/nginx/nginx.conf


RUN mkdir -p /var/log/supervisor
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY supervisord.conf /etc/supervisord.conf

CMD ["supervisord"]
