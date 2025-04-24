FROM python:3.11-slim

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

WORKDIR /code

RUN apt-get update \
    && apt-get install -y build-essential libpq-dev --no-install-recommends \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt /code/
RUN pip install --upgrade pip
RUN pip install -r requirements.txt

COPY . /code/

RUN mkdir -p /vol/web/static /vol/web/media

EXPOSE 8000

CMD ["gunicorn", "blog.wsgi:application", "--bind", "0.0.0.0:8000"]
