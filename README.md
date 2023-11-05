# Embedded Programming Report
![fontpage](img/frontpage.png "fontpage")

## Table of Contents
1. [Introduction](#introduction)
2. [Server Side](#server-side)
   - [Main API](#main-api)
     - [About the API](#about-the-api)
     - [Endpoints](#main-api-endpoints)
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

<a name="main-api-endpoints"></a>

### Endpoints

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

