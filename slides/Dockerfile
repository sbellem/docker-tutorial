FROM python:3.4.3

RUN apt-get update && apt-get install -y pandoc texlive

RUN mkdir -p /usr/src/slides/build
WORKDIR /usr/src/slides

COPY requirements.txt ./
RUN pip install -r requirements.txt

COPY Makefile ./
COPY source ./source

VOLUME build

CMD make slides
