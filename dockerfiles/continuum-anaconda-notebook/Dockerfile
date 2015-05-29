FROM continuumio/anaconda

MAINTAINER Sylvain Bellemare <sbellem@gmail.com>

RUN conda update -y --all
RUN conda install -y seaborn

RUN apt-get update
RUN apt-get install -y python-dev libpq-dev
RUN pip install --upgrade pip
RUN pip install psycopg2
RUN pip install elasticsearch

EXPOSE 8888

VOLUME /notebooks
WORKDIR /notebooks

CMD ipython notebook --no-browser --ip=0.0.0.0
