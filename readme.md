# kzen hasura engine for local development

-   launch docker compose (db variable - DATABASE_URL)
-   go inside postgress container

    ```
    docker exec -it e203280c3681 bash

    psql -U postgres
    show users: \du
    show tables: \l

    CREATE USER cmfedroyqtfnkp SUPERUSER;
    ALTER ROLE cmfedroyqtfnkp PASSWORD 'grini';
    ALTER ROLE cmfedroyqtfnkp WITH SUPERUSER CREATEDB CREATEROLE REPLICATION BYPASSRLS;
    CREATE DATABASE "public";
    \q
    ```

-   copy dev.db inside docker root. if it is a backup, copy backup
    ```
    docker cp ./dev.sql eb03dd2d5b4e:/
    docker cp ./backup eb03dd2d5b4e:/
    ```

-   for backup, run
    ```
    pg_restore -U postgres -d public -v --clean --no-acl --no-owner backup
    ```

-   run
    ```
    psql -U postgres public < dev.sql
    ```

P.S.

-   To restart my docker compose, removing all info, must be deleted ./pgdata
    ```
    sudo rm -rf ./pgdata
    ```
