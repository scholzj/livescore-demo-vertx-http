[![Build Status](https://travis-ci.org/scholzj/livescore-demo-vertx-http.svg?branch=master)](https://travis-ci.org/scholzj/livescore-demo-vertx-http)

# LiveScore service demo with Vert.x and HTTP/REST API

This is a simple service for keeping live scores. It has HTTP based API, which allows to:
* add games
* update scores
* request score results

The service is using Vert.x 3.

## API

The API can be accessed using HTTP. The different requests are described below.

### Add new game

#### Request

* URL: `api/v1.0/scores`
* Method:`POST`
* Request body:
```json
{
  "homeTeam": "Aston Villa",
  "awayTeam": "Preston North End",
  "startTime": "14th January 2017, 17:30"
}
```

#### Response

In case of success:

* HTTP `200`
* Response body:
```json
{
  "awayTeam": "Preston North End",
  "awayTeamGoals": 0,
  "gameTime": "0",
  "homeTeam": "Aston Villa",
  "homeTeamGoals": 0,
  "startTime": "Saturday 14th January 2017, 17:30"
}
```

In case of problems:
* HTTP `400`
* Response body:
```json
{
  "error": "<Error message>"
}
```

### Update game score

#### Request

* URL: `api/v1.0/scores`
* Method:`PUT`
* Request body:
```json
{
  "homeTeam": "Aston Villa",
  "awayTeam": "Preston North End",
  "homeTeamGoals": 1,
  "awayTeamGoals": 0,
  "gameTime": "HT"
}
```

#### Response

In case of success:

* HTTP `200`
* Response body:
```json
{
  "awayTeam": "Preston North End",
  "awayTeamGoals": 1,
  "gameTime": "HT",
  "homeTeam": "Aston Villa",
  "homeTeamGoals": 0,
  "startTime": "Saturday 14th January 2017, 17:30"
}
```

In case of problems:
* HTTP `400`
* Response body:
```json
{
  "error": "<Error message>"
}
```

### Get game scores

#### Request

* URL: `api/v1.0/scores`
* Method:`GET`
* Request body: Empty

#### Response

In case of success:

* HTTP `200`
* Response body:
```json
[
  {
    "awayTeam": "Preston North End",
    "awayTeamGoals": 1,
    "gameTime": "HT",
    "homeTeam": "Aston Villa",
    "homeTeamGoals": 0,
    "startTime": "Saturday 14th January 2017, 17:30"
  }
]
```

### API Examples

You can use the qpid-send and qpid-receive utilities from Apache Qpid project to communicate with the service from the command line:

* Create a new game
```bash
curl -X POST --data '{ "homeTeam": "Aston Villa", "awayTeam": "Preston North End", "startTime": "14th January 2017, 17:30" }' http://localhost:8080/api/v1.0/scores
```

* Update the score
```bash
curl -X PUT --data '{ "homeTeam": "Aston Villa", "awayTeam": "Preston North End", "homeTeamGoals": 1, "awayTeamGoals": 0, "gameTime": "HT"}' http://localhost:8080/api/v1.0/scores
```

* Get scores
```bash
curl -X GET --data '' http://localhost:8080/api/v1.0/scores
```


## Kubernetes deployment

The `Kubernetes` directory contains YAML files which can be used for deployment into Kubernetes cluster. Use the `kubectl` utility to deploy it.

```bash
kubectl create -f config.yaml
kubectl create -f deployment.yaml
```
