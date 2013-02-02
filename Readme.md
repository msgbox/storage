MsgBox Storage
=====================

Provides an API for permanent storage of incoming messages. This currently uses a Postgres database but should eventually provide an agreeded upon API that can be used with other data storage soultions.

## Requirements

A postgres database and the following environment variable:

* DB_NAME
* DB_USER
* DB_PASS
* DB_HOST
* DB_PORT
* DB_SSL (boolean)