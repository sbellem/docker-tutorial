FROM continuumio/anaconda

MAINTAINER Sylvain Bellemare <sbellem@gmail.com>

# 5
RUN apt-get update
RUN apt-get install -y python-dev libpq-dev
RUN pip install --upgrade pip
RUN pip install psycopg2

# 1
EXPOSE 8888

# 2
VOLUME /notebooks

# 3
WORKDIR /notebooks

# 0
CMD ipython notebook --no-browser --ip=0.0.0.0
