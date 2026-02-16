FROM ubuntu:16.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y apache2 gcc libc6-dev gdb wget curl \
    libapache2-mod-fcgid apache2-suexec-pristine apache2-bin \
    libwww-perl perl gcc make && \
    apt-get clean

RUN a2enmod cgid
RUN sed -i 's|ScriptAlias /cgi-bin/|ScriptAlias /cgi-bin/ /usr/lib/cgi-bin/|g' /etc/apache2/sites-enabled/000-default.conf

RUN mkdir -p /var/log/apache2 && \
    chown -R www-data:www-data /var/log/apache2 && \
    chmod -R 755 /var/log/apache2

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

RUN mkdir -p /usr/lib/cgi-bin && chmod 755 /usr/lib/cgi-bin

COPY house.cgi /usr/lib/cgi-bin/house.cgi
RUN chmod 755 /usr/lib/cgi-bin/house.cgi

COPY flag  /usr/lib/cgi-bin/flag
RUN chmod 755 /usr/lib/cgi-bin/flag
EXPOSE 80
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

