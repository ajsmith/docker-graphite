FROM rhel7.1

RUN yum install -y --disablerepo=* --enablerepo=rhel-7-server-rpms https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
RUN yum install -y --disablerepo=* --enablerepo=rhel-7-server-rpms --enablerepo=rhel-7-server-optional-rpms --enablerepo=epel python-carbon

VOLUME ["/var/lib/carbon"]

EXPOSE 2003

ENTRYPOINT ["/usr/bin/carbon-cache", "--config=/etc/carbon/carbon.conf", "--pidfile=/var/run/carbon-cache.pid", "--logdir=/var/log/carbon/", "start"]
