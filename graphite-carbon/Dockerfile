FROM rhel7.1

RUN yum install -y --disablerepo=* --enablerepo=rhel-7-server-rpms https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
RUN yum install -y --disablerepo=* --enablerepo=rhel-7-server-rpms --enablerepo=rhel-7-server-optional-rpms --enablerepo=epel python-carbon

VOLUME ["/var/lib/carbon"]

EXPOSE 2003 2004 7002

# Launch the carbon-cache service.
# The "--debug" option is given to ensure carbon-cache runs in the foreground.
ENTRYPOINT ["/usr/bin/carbon-cache", "--config=/etc/carbon/carbon.conf", "--pidfile=/var/run/carbon-cache.pid", "--logdir=/var/log/carbon/", "--debug", "start"]
