FROM gliderlabs/alpine:3.3

MAINTAINER Okello Ambrose Felix <ambokello@gmail.com>

RUN apk add --no-cache python bash && \
    apk add --no-cache --virtual=build-dependencies wget ca-certificates && \
    apk add --no-cache uwsgi-python sed supervisor && \
    wget "https://bootstrap.pypa.io/get-pip.py" -O /dev/stdout | python && \
    apk del build-dependencies

RUN mkdir -p /var/log/uwsgi/app/

COPY uwsgi.ini /var/www/app/
RUN mkdir -p /var/log/uwsgi/app/app/static-files

RUN mkdir -p /var/log/supervisor
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY supervisord.conf /etc/supervisord.conf

copy app /var/www/app
RUN pip install -r /var/www/app/requirements.txt

VOLUME ["var/www/app"]

CMD ["supervisord"]
