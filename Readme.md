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

## Schema

This is the minimum postgres schema currently for using this:

```sql
CREATE TABLE accounts(
    id              uuid PRIMARY KEY DEFAULT uuid_generate_v4(),
    username        varchar(40) NOT NULL,
    email           text NOT NULL,
    password        text NOT NULL,
    name            text,
    avatar_url      text,
    created_at      timestamp NOT NULL,
    modified_at     timestamp,
    CONSTRAINT "User already exists" UNIQUE(username),
    CONSTRAINT "Email already in user" UNIQUE(email)
    );


CREATE TABLE boxes(
    id              uuid PRIMARY KEY DEFAULT uuid_generate_v4(),
    account_id      uuid NOT NULL REFERENCES accounts (id),
    name            varchar(40) NOT NULL,
    created_at      timestamp NOT NULL,
    modified_at     timestamp
    );


CREATE TABLE messages(
    id              uuid PRIMARY KEY,
    user_id         uuid NOT NULL REFERENCES accounts (id),
    box_id          uuid NOT NULL REFERENCES boxes (id),
    creator         text NOT NULL,
    created_at      bigint NOT NULL,
    status          bool DEFAULT false,
    payload         text
    );
```