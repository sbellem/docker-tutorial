FROM python:3.4.3

RUN apt-get update && apt-get install -y pandoc texlive

RUN mkdir -p /usr/src/slides
WORKDIR /usr/src/slides

COPY requirements.txt /usr/src/slides/
RUN pip install -r requirements.txt

COPY . /usr/src/slides

VOLUME build

CMD make slides
