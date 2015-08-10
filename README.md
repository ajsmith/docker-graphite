# docker-graphite

This project provides resources for deploying Graphite in Docker.

## Image Platform

RHEL 7.1

## Image Dependencies

RHEL7 Subscription

EPEL for RHEL7

## Building

 1. Build the MariaDB image:

    ```
    $ cd mariadb
    $ docker build -t graphite-mariadb .
    ```

 2. Build the Graphite images:

    ```
    $ cd graphite
    $ docker build -t graphite-carbon -f Dockerfile.carbon .
    $ docker build -t graphite-web -f Dockerfile.web .
    ```

## Launching Graphite

 1. Create a data volume container for MariaDB:

    ```
    $ docker create --name graphite-db-data graphite-mariadb
    ```

 2. Launch the MariaDB image:

    ```
    $ docker run -d --volumes-from graphite-db-data --name graphite-mariadb \
        graphite-mariadb
    ```

 3. Create a data volume container for Carbon:

    ```
    $ docker create --name carbon-data graphite-carbon
    ```

 4. Launch Carbon:

    ```
    $ docker run -d -P --volumes-from carbon-data --name graphite-carbon \
        graphite-carbon
    ```

 5. Initialize the Graphite database:

    ```
    $ docker run --rm --link graphite-mariadb:db \
        --entrypoint /usr/lib/python2.7/site-packages/graphite/manage.py \
        graphite-web syncdb --noinput
    ```

 6. Launch Graphite:

    ```
    $ docker run -d -P --volumes-from carbon-data --link graphite-mariadb:db \
        --name graphite-web graphite-web
    ```

## Networking

The MariaDB image exposes port 3306

The Graphite Carbon image exposes port 2003.

The Graphite Web image exposes port 80.
