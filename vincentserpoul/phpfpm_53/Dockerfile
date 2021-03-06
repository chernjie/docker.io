# VERSION: phpfpm ubuntu precise, php 5.3

FROM ubuntu:12.04

MAINTAINER Vincent Serpoul <vincent@serpoul.com>

# Set the env variable DEBIAN_FRONTEND to noninteractive
ENV DEBIAN_FRONTEND noninteractive

# Fix locales
RUN locale-gen en_US.UTF-8 && dpkg-reconfigure locales

# Set correct environment variables.
ENV HOME /root

# Run upgrades
RUN echo udev hold | dpkg --set-selections && \
echo initscripts hold | dpkg --set-selections &&\
echo upstart hold | dpkg --set-selections &&\
apt-get update -q &&\
apt-get -y upgrade

# phpfpm Fastcgi
RUN apt-get install -y -q iputils-ping wget curl tree vim
RUN apt-get install -y -q php5-fpm php5-cli php5-mcrypt php5-mysqlnd php5-xdebug php5-curl php5-gd php-apc
ADD etc/php5/fpm/php-fpm.conf /etc/php5/fpm/php-fpm.conf
ADD etc/php5/fpm/pool.d/www.conf /etc/php5/fpm/pool.d/www.conf

# Expose the default port
EXPOSE 9000

# Add volume so that it is accessible from outside the container to the fastcgi container
ADD var/www /var/www
VOLUME ["/var/www"]

# Set default container command
ENTRYPOINT  ["service", "php5-fpm", "start"]

# docker build -t vincentserpoul/phpfpm_53 .
# docker stop myphpfpm_53;docker rm myphpfpm_53;docker run --name myphpfpm_53 -i -t -p 9000:9000 -v ~/docker.io/vincentserpoul/phpfpm_53/shared/php-fpm_log:/var/log/php-fpm -d vincentserpoul/phpfpm_53
