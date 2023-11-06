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

### Main API and endpoints

The API facilitates greenhouse environment monitoring and management, handling sensor data for temperature and humidity, and allows for configuration changes and retrieval of current settings. It supports the creation of new facility, building, and sensor records, and offers a dashboard view for real-time data and alerts

#### Welcome Page

```http
GET /
```

Serves the HTML welcome page for the Greenhouse Temperature and Humidity API.

#### Setup

```http
POST /change_target_building/
Content-Type: application/json
  {
    "facility": {
      "id": 0,
      "beskrivelse": "string"
    },
    "building": {
      "id": 0,
      "name": "string",
      "facility_id": 0
    }
  }
```

#### Change Target Building

```http
POST /change_target_building/
Content-Type: application/json

{
  "building_id": [building_id]
}
```

Endpoint to change the target building to the specified ID.

#### Change Target Facility

```http
POST /change_target_facility/
Content-Type: application/json

{
  "facility_id": [facility_id]
}
```

Endpoint to change the target facility to the specified ID.

#### Change Target Sensor Name

```http
POST /change_target_name/
Content-Type: application/json

{
  "sensor_name": "[sensor_name]"
}
```

Endpoint to change the target sensor to the specified name.

#### Get Target Building

```http
GET /get_target_building/
```

Retrieves the currently targeted building.

#### Get Target Facility

```http
GET /get_target_facility/
```

Retrieves the currently targeted facility.

#### Get Target Sensor Name

```http
GET /get_target_name/
```

Retrieves the currently targeted sensor name.

#### Create Facility

```http
POST /facility/
Content-Type: application/json

{
  "facility": "[facility_object]"
}
```

Creates a new facility entry with the given details.

#### Create Building

```http
POST /building/
Content-Type: application/json

{
  "building": "[building_object]"
}
```

Creates a new building entry with the given details.

#### Create Sensor

```http
POST /create_sensor/
Content-Type: application/json

{
  "sensor": "[sensor_object]"
}
```

Creates a new sensor or returns an existing one based on the serial number.

#### Post Sensor Value

```http
POST /sensor_value/
Content-Type: application/json

{
  "sensor_value": "[sensor_value_object]"
}
```

Creates a new sensor value record.

#### Create Alarm

```http
POST /alarm/
Content-Type: application/json

{
  "alarm": "[alarm_object]"
}
```

Creates a new alarm based on the sensor data.

#### Get Sensor by Serial Number

```http
GET /get_sensor_by_serial/{serial_number}
```

Retrieves sensor details by its serial number.

#### Dashboard Data

```http
GET /dashboard/
```

Retrieves dashboard data, including sensor values and alarms.

#### Get Temperature Data by Sensor ID

```http
GET /get_temp_data/{sensor_id}
```

Fetches the latest temperature data for a given sensor ID.

#### Get Humidity Data by Sensor ID

```http
GET /get_humid_data/{sensor_id}
```

Fetches the latest humidity data for a given sensor ID.

#### Update Threshold Settings

```http
PUT /threshold-settings/
Content-Type: application/json

{
  "sensor_type": "[sensor_type]",
  "max_value": [max_value],
  "low_value": [low_value]
}
```

Updates the threshold settings for a given sensor type.

#### Get Threshold Settings

```http
GET /threshold-settings/
```

Retrieves the list of all threshold settings for sensors.

#### Get All Sensor Serial Numbers

```http
GET /get_all_sensor_serial_numbers
```

Retrieves all sensor serial numbers in the system.

<a name="tools-and-frameworks"></a>

#### Tools and Frameworks

- Tools

  - Nginx (TLDR: I used it mostly has a reverse proxy )

    - NGINX is a high‑performance, highly scalable web server and reverse proxy

      - Base Nginx config -> [Base Nginx config](#nginx_base_configuration)
      - Custom Nginx config -> [Custom Nginx config](#nginx_custom_configuration)


  - Gunicorn

    - Python Web Server Gateway Interface (WSGI)

      - My Config

  - Uvicorn (TLDR: Webserver)
    - This is part of FASTapi python framework
  - Mariadb (TLDR : Database)
  - Superviser (TLDR: SystemD but more encapsulated )

    - Supervisor is a client/server system that allows its users to monitor and control a number of processes on UNIX-like operating systems.
    - My Config

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

The client is a raspberry 3 using grovepi sensors

<a name="how-to-use-it-3"></a>

#### How to Use It

//Instructions on how to use the Linux-based client

<a name="tools-and-frameworks-3"></a>

#### Tools and Frameworks

- SystemD

  - systemd is system and service manager for most Unix like operating systems
    As the system boots up, the first process created, i.e. init process with
    PID = 1, is systemd system that initiates the userspace services.

    For this project it is used to start the client service, to collect information from the sensors.
    The main benefit is the automatic start on boot and the auto restart on failiure.
    <br/><br/>

  - SystemD config

    ```bash
    [Unit]
    Description=embeded service
    After=multi-user.target

    [Service]
    StartLimitBurst=0
    Type=simple
    Restart=on-failure
    StartLimitIntervalSec=10
    ExecStart=/usr/bin/python3 /home/pi/code/embeded_device/main.py

    [Install]
    WantedBy=multi-user.target
    ```

- Python libs
  - grovepi
    - open-source platform for connecting Grove Sensors to the Rasberry Pi.
  - datetime
    - Used for constructing datetime objects.
  - requests
    - allows you to send HTTP/1.1 requests extremely easily.
  - python-dotenv
    - Python-dotenv reads key-value pairs from a .env file
  - json
    - built-in package which can be used to work with JSON data.
  - logging
    - provides a flexible framework for writing log messages
  - time
    - provides functions for handling time-related tasks (Only used the sleep method)

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
Server configurations

### Nginx Base Configuration

<a name="nginx_base_configuration"></a>

```nginx
# Base config with changes

user pi;
worker_processes auto;
pid /run/nginx.pid;
error_log /var/log/nginx/error.log;
include /etc/nginx/modules-enabled/*.conf;

events {
    worker_connections 768;
    # multi_accept on;
}

http {
    
    ##
    # Basic Settings
    ##
    
    sendfile on;
    tcp_nopush on;
    types_hash_max_size 2048;
    large_client_header_buffers 8 16k;
    client_header_timeout 32;
    # server_tokens off;

    # server_names_hash_bucket_size 64;
    # server_name_in_redirect off;

    include /etc/nginx/mime.types;
    default_type application/octet-stream;

    ##
    # SSL Settings
    ##
    
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2 TLSv1.3; # Dropping SSLv3, ref: POODLE
    ssl_prefer_server_ciphers on;

    ##
    # Logging Settings
    ##
    
    access_log /var/log/nginx/access.log;

    ##
    # Gzip Settings
    ##
    
    gzip on;

    # gzip_vary on;
    # gzip_proxied any;
    # gzip_comp_level 6;
    # gzip_buffers 16 8k;
    # gzip_http_version 1.1;
    # gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;

    ##
    # Virtual Host Configs
    ##
    
    include /etc/nginx/conf.d/*.conf;
    include /etc/nginx/sites-enabled/*;
}
```

### Custom Nginx Configuration

<a name="nginx_custom_configuration"></a>

```nginx
upstream fastapi_app_server {
    server unix:/home/pi/code/fastapi-nginx-gunicorn/run/gunicorn.sock fail_timeout=0;
}

upstream dashboard {
    server 127.0.0.1:8000 fail_timeout=0;
}

server {
    listen 80;
    server_name meo.local;

    keepalive_timeout 5;
    client_max_body_size 8k;

    access_log /home/pi/code/fastapi-nginx-gunicorn/logs/nginx-access.log;
    error_log /home/pi/code/fastapi-nginx-gunicorn/logs/nginx-error.log;

    # Route traffic to FastAPI for /api URLs
    location /api/ {
        proxy_pass http://fastapi_app_server/;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_redirect off;
    }

    # Route all other traffic to Dashboard
    location / {
        proxy_pass http://dashboard/;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_redirect off;
    }
}
```

### Gunicorn Configuration

```bash
#!/bin/bash
# fastapi-app is used by the main api to startup
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

-----------New File ----------------

#!/bin/bash
# This is used to start the dashboard app
NAME=dashboard
DIR=/home/pi/code/dashboard_fastapi-nginx-gunicorn
USER=pi
GROUP=pi
WORKERS=3
WORKER_CLASS=uvicorn.workers.UvicornWorker
VENV=$DIR/.venv/bin/activate
BIND=127.0.0.1:8000
LOG_LEVEL=info

cd $DIR
source $VENV

exec gunicorn main:app \
  --name $NAME \
  --workers $WORKERS \
  --worker-class $WORKER_CLASS \
  --user=$USER \
  --group=$GROUP \
  --bind=$BIND \
  --log-level=$LOG_LEVEL \
  --log-file=-


```

### Supervisor

```bash

#Fastapi app / main API : this calles the gunicorn_start bash script
[program:fastapi-app]
command=/home/pi/code/fastapi-nginx-gunicorn/gunicorn_start
user=pi
autostart=true
autorestart=true
redirect_stderr=true
stdout_logfile=/home/pi/code/fastapi-nginx-gunicorn/logs/gunicorn-error.log

-----------New File ----------------

#Dashboard : this calles the gunicorn_start bash script
[program:dashboard]
command=/home/pi/code/dashboard_fastapi-nginx-gunicorn/gunicorn_start
user=pi
autostart=true
autorestart=true
redirect_stderr=true
stdout_logfile=/home/pi/code/dashboard_fastapi-nginx-gunicorn/logs/gunicorn-error.log

```

### Firewall settings

```bash
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere
22                         ALLOW       Anywhere
80                         ALLOW       Anywhere
443                        ALLOW       Anywhere
OpenSSH (v6)               ALLOW       Anywhere (v6)
22 (v6)                    ALLOW       Anywhere (v6)
80 (v6)                    ALLOW       Anywhere (v6)
443 (v6)                   ALLOW       Anywhere (v6)
```

### Code of conduct

#### File structure

```bash

/home/pi/code
|   dashboard
|   fastapi (Main api)
|   Nginx_log (Error and access log for both)
|
/etc/nginx
|   nginx.conf (Base config)
|   sites-enabled
|       fastapi-app.conf (Custom config)
|
/etc/supervisor/conf.d
    dashboard.conf (Dashboard config)
    fastapi-app.conf (Fastapi config)

```

#### Git guidelines

Not all of the following has been used but is still consideres part of the Code conduct.

```Text
    [FIX] for bug fixes: mostly used in stable version but also valid if you are fixing a recent bug in development version;

    [REF] for refactoring: when a feature is heavily rewritten;

    [ADD] for adding new modules;

    [REM] for removing resources: removing dead code, removing views, removing modules, …;

    [REV] for reverting commits: if a commit causes issues or is not wanted reverting it is done using this tag;

    [MOV] for moving files: use git move and do not change content of moved file otherwise Git may loose track and history of the file; also used when moving code from one file to another;

    [IMP] for improvements: most of the changes done in development version are incremental improvements not related to another tag;

    [MERGE] for merge commits: used in forward port of bug fixes but also as main commit for feature involving several separated commits;

    [I18N] for changes in translation files;

```

### Still missing overall

- Fail2ban (SSH Brutefore attack protecion)
- JTW or another token based api security
- SSL Cert
- auth0 for dashboard (Maybe over engineering)
