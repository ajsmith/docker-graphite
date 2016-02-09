FROM rhel7.1

MAINTAINER Alex Smith <alex.smith@redhat.com>

RUN yum install -y --disablerepo=* --enablerepo=rhel-7-server-rpms https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
    && yum install -y --disablerepo=* --enablerepo=rhel-7-server-rpms --enablerepo=rhel-7-server-optional-rpms --enablerepo=epel python-carbon \
    && yum clean all

ADD rhel/etc/carbon/carbon.conf /etc/carbon/carbon.conf
ADD rhel/etc/carbon/storage-schemas.conf /etc/carbon/storage-schemas.conf

VOLUME ["/var/lib/carbon"]

EXPOSE 2003 2004 7002

# Launch the carbon-cache service.
# The "--debug" option is given to ensure carbon-cache runs in the foreground.
ENTRYPOINT ["/usr/bin/carbon-cache", "--config=/etc/carbon/carbon.conf", "--pidfile=/var/run/carbon-cache.pid", "--debug", "start"]
