From ubuntu:trusty
MAINTAINER Elliott Ye

# Set noninteractive mode for apt-get
ENV DEBIAN_FRONTEND noninteractive

# Update
RUN apt-get update

### Start editing ###
# Install package here for cache
RUN apt-get -y install supervisor software-properties-common \
	&& add-apt-repository ppa:nginx/stable \
	&& add-apt-repository ppa:chris-lea/php5.5 \
	&& apt-get update \
	&& apt-get -y install nginx php5-common php5-fpm php5-cli php5-dev php-apc php-pear
RUN echo "daemon off;" >> /etc/nginx/nginx.conf \
	&& sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php5/fpm/php-fpm.conf \
	&& sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/" /etc/php5/fpm/php.ini

# Add files
#supervisor
ADD nginx-php5.conf /etc/supervisor/conf.d/nginx-php5.conf
#nginx
ADD default /etc/nginx/sites-available/default

# Run
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]
