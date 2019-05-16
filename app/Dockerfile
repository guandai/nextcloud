FROM ubuntu:latest

ENV DEBIAN_FRONTEND="noninteractive" \
	TZ="Europe/Copenhagen"

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
	&& echo $TZ > /etc/timezone \
	&& apt-get update \
	&& apt-get install -y \
		software-properties-common language-pack-en-base \
		mcrypt curl sendmail supervisor net-tools telnet \
		cron ffmpeg git ssh iputils-ping vim imagemagick 

RUN	LC_ALL=en_US.UTF-8 \
	add-apt-repository -y ppa:ondrej/php \
	&& apt-get update \
	&& apt-get install -y \
		php7.2 php7.2-fpm php7.2-mysql php7.2-gd php7.2-soap php7.2-dom \
    	php7.2-curl php7.2-mbstring php-zip php-redis php-memcached php-imagick php7.3-imagick php7.2-imagick

RUN	apt-get clean \
	&& mkdir /run/php \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

#add custom php.ini file
COPY php.ini /etc/php/7.2/fpm/
COPY www.conf /etc/php/7.2/fpm/pool.d/www.conf
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
