FROM otechlabs/base
# TARGET_IMAGE_NAME zabbix_server:0.9

MAINTAINER Oleksandr Bezpalko <obezpalko@gmail.com>
RUN apt-get update
# Update base images.
RUN $APT_INSTALL libsnmp-dev libsnmp-base libsnmp-perl libnet-snmp-perl \
    librrds-perl mysql-common passwd libjson-perl pwgen mysql-client \
    zabbix-server-mysql snmp-mibs-downloader fping && \
    apt-get -y autoclean autoremove

RUN mkdir -p /var/run/zabbix /etc/zabbix/zabbix_server.conf.d /etc/zabbix/scripts /etc/service/snmptrapd /etc/service/zabbix_server && \
    chown zabbix /var/run/zabbix /etc/zabbix/zabbix_server.conf.d /etc/zabbix/scripts && \
    sed -i '/^#/d; /^$/d; /^DB/d' /etc/zabbix/zabbix_server.conf

RUN apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 10051

COPY zabbix_server.py /etc/service/zabbix_server/run
COPY files/*.mib /usr/share/snmp/mibs/
COPY db_init.sh /sbin/db_init.sh

VOLUME ["/etc/zabbix", "/var/log/snmptt"]
