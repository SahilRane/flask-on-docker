# Flask on Docker with Postgres, Gunicorn, and Nginx

## Overview

This repository contains a Flask web application containerized with Docker and backed by a PostgreSQL database. The application serves dynamic content, static files, and user-uploaded media files. In a production environment, it runs with Gunicorn as the WSGI server and Nginx as a reverse proxy.

This setup allows for a scalable and maintainable deployment of Flask applications, utilizing best practices for containerization and database management. By leveraging Docker Compose, we streamline the development, testing, and deployment process, ensuring that the application behaves consistently across different environments. The use of Gunicorn improves application performance in production, while Nginx provides efficient request handling and secure static/media file delivery.

A demonstration of the upload capabilities is below:
![Uploading Image](screen_recording.gif)

## Build Instructions

### Prerequisites

Ensure you have the following installed on your machine:

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

### Development Setup

To bring up the development environment, run:

```sh
# Clone the repository
$ git clone https://github.com/yourusername/flask-on-docker.git
$ cd flask-on-docker

# Build and start the containers
$ docker-compose up -d --build

# Create the database tables
$ docker-compose exec web python manage.py create_db
```

After running the above commands, navigate to:

- **Flask API**: [http://localhost:1043/](http://localhost:1043/)
- **Upload page**: [http://localhost:1043/upload](http://localhost:1043/upload)

To check the database contents, run:

```sh
$ docker-compose exec db psql --username=hello_flask --dbname=hello_flask_dev
```

### Production Setup

For a production-ready deployment with Gunicorn and Nginx, use:

```sh
# Bring down any existing containers
$ docker-compose -f docker-compose.prod.yml down -v

# Build and start the production containers
$ docker-compose -f docker-compose.prod.yml up -d --build

# Initialize the production database
$ docker-compose -f docker-compose.prod.yml exec web python manage.py create_db
```

Access the application at:

- **App URL**: [http://localhost:1339/](http://localhost:1339/)
- **Upload page**: [http://localhost:1339/upload](http://localhost:1339/upload)
- **Media files**: [http://localhost:1339/media/](http://localhost:1339/media/)

### Stopping Containers

To shut down the services and remove volumes:

```sh
$ docker-compose down -v
```

For production:

```sh
$ docker-compose -f docker-compose.prod.yml down -v
```

## Features

- Flask API containerized with Docker
- PostgreSQL database for persistent storage
- Gunicorn for serving the Flask app in production
- Nginx as a reverse proxy for improved performance
- Static and media file handling via Nginx
- Environment-specific configurations for development and production

