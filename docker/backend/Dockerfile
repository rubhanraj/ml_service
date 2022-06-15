FROM ubuntu:latest
ENV TZ=Europe/London \
    DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:deadsnakes/ppa && \
    apt-get update && \
    apt-get install -y python3.9 python3.9-dev python3-pip python3.9-distutils

WORKDIR /app
COPY requirements.txt .
RUN rm -f /usr/bin/python && ln -s /usr/bin/python3.9 /usr/bin/python
RUN rm -f /usr/bin/python3 && ln -s /usr/bin/python3.9 /usr/bin/python3

RUN pip3 install -r requirements.txt
RUN pip3 install gunicorn==19.9.0

ADD ./backend /app/backend
ADD ./docker /app/docker
ADD ./research /app/research

#RUN mkdir -p /app/backend/server/staticfiles
RUN mkdir -p /app/backend/server/static
RUN chmod +x /app/docker/backend/wsgi-entrypoint.sh
