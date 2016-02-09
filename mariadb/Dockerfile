FROM rhel:7.2

MAINTAINER Alex Smith <alex.smith@redhat.com>

COPY graphite.sql /tmp/graphite.sql

RUN yum install -y --disablerepo=* --enablerepo=rhel-7-server-rpms mariadb-server \
    && yum clean all

RUN /usr/bin/mysql_install_db --datadir=/var/lib/mysql --user=mysql --skip-name-resolve

RUN /usr/bin/mysqld_safe --basedir=/usr --nowatch &&\
    until mysql -e ";" ; do sleep 1; done &&\
    mysql < /tmp/graphite.sql &&\
    rm /tmp/graphite.sql

ENTRYPOINT ["/usr/bin/mysqld_safe", "--basedir=/usr"]

VOLUME ["/var/lib/mysql"]

EXPOSE 3306
