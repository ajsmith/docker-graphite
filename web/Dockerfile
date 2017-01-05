FROM rhel:7.2

MAINTAINER Alex Smith <alex.smith@redhat.com>

RUN yum install -y --disablerepo=* --enablerepo=rhel-7-server-rpms https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
    && yum install -y --disablerepo=* --enablerepo=rhel-7-server-rpms --enablerepo=epel graphite-web graphite-web-selinux MySQL-python \
    && yum clean all

ADD rhel/etc/graphite-web/dashboard.conf /etc/graphite-web/dashboard.conf
ADD rhel/etc/graphite-web/local_settings.py /etc/graphite-web/local_settings.py
ADD rhel/etc/httpd/conf.d/graphite-web.conf /etc/httpd/conf.d/graphite-web.conf

VOLUME ["/var/lib/graphite-web", "/var/log/graphite-web", "/var/log/httpd"]

EXPOSE 80

ENTRYPOINT ["/usr/sbin/httpd", "-DFOREGROUND"]
