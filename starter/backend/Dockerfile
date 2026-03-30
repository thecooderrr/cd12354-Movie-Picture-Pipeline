FROM public.ecr.aws/docker/library/python:3.10-slim-bullseye

RUN useradd -u 1000 -m app

WORKDIR /app

RUN apt-get update && apt-get install -y --no-install-recommends \
  build-essential \
  gcc \
  libpcre3 \
  libpcre3-dev \
  libssl-dev \
  libffi-dev \
  curl \
  && pip install --no-cache-dir pipenv \
  && rm -rf /var/lib/apt/lists/*

COPY Pipfile* /app/

RUN pipenv install --system --deploy

COPY . /app

EXPOSE 5000

USER app

CMD ["uwsgi", "--http", "0.0.0.0:5000", "--wsgi-file", "__init__.py", "--callable", "app"]
