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

 2. Build the Graphite Carbon image:

    ```
    $ cd graphite-carbon
    $ docker build -t graphite-carbon .
    ```

 3. Build the Graphite Web image:

    ```
    $ cd graphite-web
    $ docker build -t graphite-web .
    ```

### Customizing the Carbon Image

The Carbon image copies in configuration files found in the
*graphite-carbon/rhel* directory. To produce a Carbon image with custom
configuration, the following files may be modified:

  - *graphite-carbon/rhel/etc/carbon/carbon.conf*
  - *graphite-carbon/rhel/etc/carbon/storage-schemas.conf*

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

The Graphite Carbon image exposes ports 2003, 2004, and 7002.

The Graphite Web image exposes port 80.

## Release Notes

### v1.1.0 unreleased

- Allow Carbon image customization.

### v1.0.0 2015-12-04

- Initial release.
