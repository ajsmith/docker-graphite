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
    $ (cd mariadb && docker build -t graphite-mariadb .)
    ```

 2. Build the Graphite image:

    ```
    $ (cd graphite && docker build -t graphite .)
    ```

## Launching Graphite

 1. Launch the MariaDB image:

    ```
    $ docker run -d --name graphite-mariadb graphite-mariadb
    ```

 2. Launch the Graphite image:

    ```
    $ docker run -d --link graphite-mariadb:mariadb --name graphite graphite
    ```

## Networking

The MariaDB image exposes ports ...

The Graphite image exposes ports ...
