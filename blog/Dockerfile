# Use official Python image as a parent image
FROM python:3.11-slim

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Set working directory
WORKDIR /code

# Install system dependencies
RUN apt-get update \
    && apt-get install -y build-essential libpq-dev --no-install-recommends \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install dependencies
COPY requirements.txt /code/
RUN pip install --upgrade pip
RUN pip install -r requirements.txt

# Copy project files
COPY . /code/

# Collect static files
RUN mkdir -p /vol/web/static /vol/web/media
# RUN python manage.py collectstatic --noinput

# Port to expose
EXPOSE 8000

# Run the application
CMD ["gunicorn", "blog.wsgi:application", "--bind", "0.0.0.0:8000"]
