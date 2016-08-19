# docker-graphite

This project provides resources for deploying Graphite in Docker.

## Image Platform

RHEL7

## Image Dependencies

RHEL7 Subscription

EPEL for RHEL7

## Building

 1. Build the Graphite Carbon image:

    ```
    $ cd carbon
    $ docker build -t graphite-carbon .
    ```

 2. Build the Graphite Web image:

    ```
    $ cd web
    $ docker build -t graphite-web .
    ```

### Customizing the Carbon Image

The Carbon image copies in configuration files found in the
*carbon/rhel* directory. To produce a Carbon image with custom
configuration, the following files may be modified:

  - *carbon/rhel/etc/carbon/carbon.conf*
  - *carbon/rhel/etc/carbon/storage-schemas.conf*

## Launching Graphite

*Note: Before launching Graphite, you will have needed to configured and
started a database for use with Graphite. The following steps assume this has
already been done in a container named "graphite-db".*

 1. Launch Carbon:

    ```
    $ docker run -d -P --name graphite-carbon graphite-carbon
    ```

 2. Initialize the Graphite database:

    ```
    $ docker run --rm --link graphite-db:db \
        --entrypoint /usr/lib/python2.7/site-packages/graphite/manage.py \
        graphite-web syncdb --noinput
    ```

 4. Launch Graphite:

    ```
    $ docker run -d -P --volumes-from graphite-carbon --link graphite-db:db \
        --name graphite-web graphite-web
    ```

## Networking

The Graphite Carbon image exposes ports 2003, 2004, and 7002.

The Graphite Web image exposes port 80.

## Release Notes

### v1.2.0 unreleased

- Remove MariaDB image resources.

### v1.1.0 2016-07-14

- Allow Graphite Carbon image customization.
- Allow Graphite Web image customization of dashboard configuration.
- Modernize images to latest RHEL7 and Graphite releases.
- Enable Carbon UDP listener by default.

### v1.0.0 2015-12-04

- Initial release.
