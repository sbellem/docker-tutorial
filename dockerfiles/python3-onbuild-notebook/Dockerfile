FROM python:3.4.3-onbuild

MAINTAINER Sylvain Bellemare <sbellem@gmail.com>

RUN apt-get update
RUN apt-get install -y libfreetype6-dev pkg-config

RUN pip install --upgrade pip

VOLUME /notebooks
WORKDIR /notebooks

EXPOSE 8888

CMD ipython notebook --ip=0.0.0.0 --no-browser
