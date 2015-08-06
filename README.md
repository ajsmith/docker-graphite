# docker-graphite

This project provides resources for deploying Graphite in Docker.

## Image Platform

RHEL 7.1

## Image Dependencies

RHEL7 Subscription

EPEL for RHEL7

## Building

 1. Build the MySQL image:

    ```
    $ (cd mysql && docker build -t graphite-mysql .)
    ```

 2. Build the Graphite image:

    ```
    $ (cd graphite && docker build -t graphite .)
    ```

## Launching Graphite

 1. Launch the MySQL image:

    ```
    $ docker run -d --name graphite-mysql graphite-mysql
    ```

 2. Launch the Graphite image:

    ```
    $ docker run -d --link graphite-mysql:mysql --name graphite graphite
    ```

## Networking

The MySQL image exposes ports ...

The Graphite image exposes ports ...
