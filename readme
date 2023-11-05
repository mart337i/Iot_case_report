# Embedded Programming Report
![fontpage](img/frontpage.png "fontpage")

## Table of Contents
1. [Introduction](#introduction)
2. [Server Side](#server-side)
   - [Main API](#main-api)
     - [About the API](#about-the-api)
     - [How to Use It](#how-to-use-it)
     - [Tools and Frameworks](#tools-and-frameworks)
   - [Dashboard API and Website](#dashboard-api-and-website)
     - [Tools and Frameworks](#tools-and-frameworks-1)
   - [Server Configuration](#server-configuration)
     - [Tools and Frameworks](#tools-and-frameworks-2)
3. [Client Side](#client-side)
   - [Linux Based Client](#linux-based-client)
     - [Tools and Frameworks](#tools-and-frameworks-3)
   - [Embedded Device](#embedded-device)
     - [Tools and Frameworks](#tools-and-frameworks-4)
4. [Server Configuration](#server-configuration-1)

<a name="introduction"></a>
## Introduction
//Write about the case and how the program client and server you developed accomplished the goal

<a name="server-side"></a>
## Server Side

<a name="main-api"></a>
### Main API

<a name="about-the-api"></a>
#### About the API
//Details about the main API

<a name="how-to-use-it"></a>
#### How to Use It
//Instructions on how to use the main API

<a name="tools-and-frameworks"></a>
#### Tools and Frameworks
//List and description of tools and frameworks used

<a name="dashboard-api-and-website"></a>
### Dashboard API and Website

<a name="about-the-dashboard"></a>
#### About the Dashboard
//Details about the dashboard API and website

<a name="how-to-use-it-1"></a>
#### How to Use It
//Instructions on how to use the dashboard

<a name="tools-and-frameworks-1"></a>
#### Tools and Frameworks
//List and description of tools and frameworks used for dashboard

<a name="server-configuration"></a>
### Server Configuration

<a name="about-the-server"></a>
#### About the Server
//Details about the server configuration

<a name="how-to-use-it-2"></a>
#### How to Use It
//Instructions on how to configure the server

<a name="tools-and-frameworks-2"></a>
#### Tools and Frameworks
//List and description of tools and frameworks used for server configuration

<a name="client-side"></a>
## Client Side

<a name="linux-based-client"></a>
### Linux Based Client

<a name="about-the-client"></a>
#### About the Client
//Details about the Linux-based client

<a name="how-to-use-it-3"></a>
#### How to Use It
//Instructions on how to use the Linux-based client

<a name="tools-and-frameworks-3"></a>
#### Tools and Frameworks
//List and description of tools and frameworks used for the Linux-based client

<a name="embedded-device"></a>
### Embedded Device

<a name="about-the-device"></a>
#### About the Device
//Details about the embedded device

<a name="how-to-use-it-4"></a>
#### How to Use It
//Instructions on how to use the embedded device

<a name="tools-and-frameworks-4"></a>
#### Tools and Frameworks
//List and description of tools and frameworks used for the embedded device

<a name="server-configuration-1"></a>
## Server Configuration

### Nginx Configuration
```bash
# Creates a server cluster that redirects to a unix socket
upstream app_server {
    server unix:/home/pi/code/fastapi-nginx-gunicorn/run/gunicorn.sock fail_timeout=0;
}

server {
    listen 80;
    server_name meo.local;
    keepalive_timeout 5;
    client_max_body_size 4G;

    access_log /home/pi/code/fastapi-nginx-gunicorn/logs/nginx-access.log;
    error_log /home/pi/code/fastapi-nginx-gunicorn/logs/nginx-error.log;

    location / {
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_redirect off;

        if (!-f $request_filename) {
            proxy_pass http://app_server;
            break;
        }
    }
}
```

### Gunicorn Configuration
```bash
NAME=fastapi-app
DIR=/home/pi/code/fastapi-nginx-gunicorn
USER=pi
GROUP=pi
WORKERS=3
WORKER_CLASS=uvicorn.workers.UvicornWorker
VENV=$DIR/.venv/bin/activate
BIND=unix:$DIR/run/gunicorn.sock
LOG_LEVEL=info

cd $DIR
source $VENV

exec gunicorn main:app
 
```

### Supervisor
```bash
[program:fastapi-app]
command=/home/pi/code/fastapi-nginx-gunicorn/gunicorn_start
user=pi
autostart=true
autorestart=true
redirect_stderr=true
stdout_logfile=/home/pi/code/fastapi-nginx-gunicorn/logs/gunicorn-error.log

```

