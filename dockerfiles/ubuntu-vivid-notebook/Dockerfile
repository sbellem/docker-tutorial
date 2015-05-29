FROM ubuntu:15.04

MAINTAINER Sylvain Bellemare <sbellem@gmail.com>

RUN apt-get update
RUN apt-get install -y build-essential python python-dev python-pip 

RUN pip install ipython jinja2 jsonschema pyzmq tornado

VOLUME /notebooks
WORKDIR /notebooks

EXPOSE 8888

CMD ipython notebook --ip=0.0.0.0 --no-browser
