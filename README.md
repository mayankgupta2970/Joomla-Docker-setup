# Joomla-Docker-setup

This project sets up a Joomla service with custom dockerfile . There are three dockerfiles one for Joomls, one for PHP-FPM and one for database .The dockerfile for joomla 
conntaines base image ubuntu and a nginx server installed to handle requests.


a. Create a Dockerfile for Joomla with following components:
   1. Use Ubuntu latest as base image.
   2. install all updates and install nginx server on the dockerfile
	RUN apt-get update && apt-get install -y nginx wget

   3. Install the required dependencies for Joomla CMS software
	
	RUN apt-get install -y \
    	apache2-utils \
    	libapache2-mod-php \
    	libgd-dev \
    	libjpeg-dev \
    	libpng-dev \
    	libxml2-dev \
    	libxslt-dev \
    	php \
    	php-cli \
    	php-curl \
    	php-gd \
    	php-intl \
    	php-mbstring \
    	php-mysql \
    	php-xml \
    	php-zip \
    	unzip
    
    4. Download the files from joomla.org and install them on the dockerfile in the following directory
	unzip /tmp/joomla.zip -d /var/www/html 


    5. now copy the changed nginx.conf file to the container
        COPY nginx.conf /etc/nginx/nginx.conf
    
    6. Expose port 80 for nginx server.
    
    7. Start the Nginx service in CMD.


b. Create a Dockerfile for php-fpm service-Expose port 9000:

c. Create another Dockerfile for Mariadb to be used as database- Expose port 3306 .
   make sure to keep the env variables correct for joomla
	
	ENV MYSQL_ROOT_PASSWORD=password
	ENV MYSQL_DATABASE=joomla
	ENV MYSQL_USER=joomla
	ENV MYSQL_PASSWORD=joomla

d. Create a docker-compose file to build and make these services up and running.Mention the rrot directory  as volumes
   for php service and nginx service.
   
