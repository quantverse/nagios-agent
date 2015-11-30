FROM debian:stable

MAINTAINER info@quantverse.com
RUN apt-get update && apt-get install -y nagios-nrpe-server
ADD startup.sh /opt/startup.sh
RUN sed -e 's/^server_address=127.0.0.1/#server_address=127.0.0.1/' \
        -e 's/^allowed_hosts=127.0.0.1/#allowed_hosts=127.0.0.1/' \
        -i /etc/nagios/nrpe.cfg

RUN echo "command[check_load]=/usr/lib/nagios/plugins/check_load -w 15,10,5 -c 30,25,20" >> /etc/nagios/nrpe.d/load.cfg && \
    echo "command[check_users]=/usr/lib/nagios/plugins/check_users -w 5 -c 10" >> /etc/nagios/nrpe.d/load.cfg && \
    echo "command[check_rootfs]=/usr/lib/nagios/plugins/check_disk -w 10% -c 5% -p /dev/vda1" >> /etc/nagios/nrpe.d/load.cfg && \
    echo "command[check_zombie_procs]=/usr/lib/nagios/plugins/check_procs -w 5 -c 10 -s Z" >> /etc/nagios/nrpe.d/load.cfg && \
    echo "command[check_total_procs]=/usr/lib/nagios/plugins/check_procs -w 150 -c 200" >> /etc/nagios/nrpe.d/load.cfg

EXPOSE 5666

CMD ["/opt/startup.sh"]
