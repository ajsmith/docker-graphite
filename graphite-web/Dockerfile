FROM rhel7.1

RUN yum install -y --disablerepo=* --enablerepo=rhel-7-server-rpms https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
RUN yum install -y --disablerepo=* --enablerepo=rhel-7-server-rpms --enablerepo=rhel-7-server-optional-rpms --enablerepo=epel graphite-web graphite-web-selinux MySQL-python

COPY local_settings.py /etc/graphite-web/local_settings.py
COPY graphite-web.conf /etc/httpd/conf.d/graphite-web.conf

VOLUME ["/var/lib/graphite-web"]

EXPOSE 80

ENTRYPOINT ["/usr/sbin/httpd", "-DFOREGROUND"]
