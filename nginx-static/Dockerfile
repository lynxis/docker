# nginx + PHP5-FPM + owncloud +  supervisord on Docker
#
# VERSION               0.0.1
FROM        ubuntu:14.04
MAINTAINER  Alexander Couzens "lynxis@fe80.eu"

RUN apt-get update && apt-get -qy upgrade
RUN locale-gen de_DE.UTF-8 && dpkg-reconfigure locales

RUN echo "Europe/Berlin" > /etc/timezone
RUN dpkg-reconfigure --frontend noninteractive tzdata

# install curl
RUN apt-get install -y curl

# Install nginx
RUN apt-get -y install nginx

# Install Supervisord
RUN apt-get -y install python-setuptools
RUN easy_install supervisor
ADD supervisord.conf /etc/supervisord.conf

VOLUME ["/var/www", "/var/log/nginx"]

# Configure nginx for PHP websites
ADD nginx_default.conf /etc/nginx/sites-available/default
# dont log acces - upstream loadbalancer does this
#RUN sed -i 's/access_log/#access_log/g' /etc/nginx/nginx.conf
CMD supervisord -n -c /etc/supervisord.conf 

# use this for debugging from within container
# CMD supervisord -c /etc/supervisord.conf && /bin/bash
