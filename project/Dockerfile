# pull official base image
FROM python:3.9.2-slim-buster

# set working directory
WORKDIR /usr/src/app

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# install system dependencies
RUN apt-get update && apt-get -y install netcat gcc && apt-get clean

# install python dependencies
RUN pip install --upgrade pip
RUN pip install "poetry==1.1.6"
COPY poetry.lock pyproject.toml /usr/src/app/
RUN poetry config virtualenvs.create false && poetry install --no-interaction --no-ansi

# add app
COPY . /usr/src/app/

# add entrypoint.sh
COPY ./entrypoint.sh /usr/src/app/
RUN chmod +x /usr/src/app/entrypoint.sh

# run entrypoint.sh
ENTRYPOINT ["/usr/src/app/entrypoint.sh"]