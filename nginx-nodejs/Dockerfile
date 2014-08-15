From ubuntu:trusty
MAINTAINER Elliott Ye

# Set noninteractive mode for apt-get
ENV DEBIAN_FRONTEND noninteractive

# Update
RUN apt-get update

### Start editing ###
# Install package here for cache
RUN apt-get -y install supervisor software-properties-common logrotate curl
RUN curl -sL https://deb.nodesource.com/setup | bash - \
 && apt-get -y install nodejs python build-essential
RUN add-apt-repository ppa:nginx/stable && apt-get update \
 && apt-get -y install nginx-full \
 && echo "daemon off;" >> /etc/nginx/nginx.conf \
 && rm /etc/nginx/sites-enabled/default

# Add files
#supervisor
ADD nginx-nodejs.conf /etc/supervisor/conf.d/nginx-nodejs.conf
#nodejs
ONBUILD ADD src/package.json /src/package.json
ONBUILD RUN cd /src && npm install
ONBUILD ADD src /src
#nginx
ONBUILD ADD nginx/sites-enabled /etc/nginx/sites-enabled

# Run
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]
