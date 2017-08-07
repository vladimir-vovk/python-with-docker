FROM python:2.7
ENV PYTHONUNBUFFERED 1
RUN apt-get update && apt-get install -y mercurial git
RUN pip install --upgrade pip
RUN pip install ipython ipdb

RUN mkdir /app
ADD requirements.txt /app/requirements.txt
RUN pip install -r /app/requirements.txt

WORKDIR /app
