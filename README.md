# 🟢 Clean Django React Nginx project

## Starting up

- Rename `.env.example` to `.env` and fill all fields with your values
- Then start command `docker compose up -d --build` or
`docker-compose up -d --build` if you have a docker compose V1
- Go to http://localhost and check result

### Endpoints

- http://localhost (react build folder)
- http://localhost/admin/ (django admin)

## 📚 Structure
```bash
├── README.md
├── .env.example
├── backend
│   ├── Dockerfile
│   ├── __init__.py
│   ├── core
│   │   ├── __init__.py
│   │   ├── asgi.py
│   │   ├── settings
│   │   │   ├── __init__.py
│   │   │   ├── base.py
│   │   │   ├── local.py
│   │   │   └── production.py
│   │   ├── urls.py
│   │   └── wsgi.py
│   ├── gunicorn_config.py
│   ├── manage.py
│   ├── requirements.txt
│   ├── scripts
│   │   ├── collectstatic.sh
│   │   ├── entrypoint.sh
│   │   └── migrate.sh
├── docker-compose.yml
├── frontend
│   ├── Dockerfile
│   ├── package-lock.json
│   ├── package.json
│   ├── public
│   │   ├── favicon.ico
│   │   ├── index.html
│   │   ├── logo192.png
│   │   ├── logo512.png
│   │   ├── manifest.json
│   │   └── robots.txt
│   ├── src
│   │   ├── App.css
│   │   ├── App.js
│   │   ├── App.test.js
│   │   ├── index.css
│   │   ├── index.js
│   │   ├── logo.svg
│   │   ├── reportWebVitals.js
│   │   └── setupTests.js
│   └── yarn.lock
└── nginx 
    nginx.conf
```

- The `backend` directory is root directory for the Django project 
- The `frontend` directory is root directory for the React project
- The `nginx` directory contains the `nginx.conf` file which configures the proxying of backend and frontend requests

### `backend/gunicorn_config.py`

Config file to set up gunicorn in project

1. `command`: Setting the path to the `gunicorn` in the container
2. `pythonpath`: Setting the path to the `python` in the container
3. `bind`: Sets up the host on which `django` will run
4. `workers`: Set the maximum number of threads
5. `raw_env`: Set the path to `settings` file

### `backend/scripts/`

The directory for the scripts you need to run your django project

1. `collectstatic.sh`: A script to collect statics in a django project
2. `migrate.sh`: Script for creating migrations, applying migrations and creating a superuser
3. `entrypoint.sh`: A script to run the entire project inside the container, running `collectstatic.sh`, `migrate.sh` and raising `gunicorn`
