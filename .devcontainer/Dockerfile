FROM ubuntu:latest

ARG LOCAL_WORKSPACE_FOLDER_BASENAME

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    apache2 \
    mysql-server \
    php \
    libapache2-mod-php \
    php-mysql \
    php-zip \
    php-gd \
    php-json \
    php-mbstring \
    php-curl \
    php-xml \
    phpmyadmin \
    curl \
    git \
    vim \
    unzip \
    nano

RUN curl -OL https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && \
    chmod +x wp-cli.phar && \
    mv wp-cli.phar /usr/local/bin/wp

RUN sed -i 's/bind-address.*/bind-address = 0.0.0.0/' /etc/mysql/mysql.conf.d/mysqld.cnf && \
    sed -i 's/mysqlx-bind-address.*/mysqlx-bind-address = 0.0.0.0/' /etc/mysql/mysql.conf.d/mysqld.cnf

RUN a2enmod rewrite && \
    a2enmod headers && \
    a2enmod ssl && \
    echo "ServerName localhost" >> /etc/apache2/apache2.conf

RUN mkdir -p /workspaces/$LOCAL_WORKSPACE_FOLDER_BASENAME/wordpress && \
    chown -R www-data:www-data /workspaces/$LOCAL_WORKSPACE_FOLDER_BASENAME/wordpress && \
    chmod -R 755 /workspaces/$LOCAL_WORKSPACE_FOLDER_BASENAME/wordpress

RUN sed -i "s#DocumentRoot /var/www/html#DocumentRoot /workspaces/$LOCAL_WORKSPACE_FOLDER_BASENAME/wordpress#g" /etc/apache2/sites-available/000-default.conf && \
    echo '<Directory /workspaces/'$LOCAL_WORKSPACE_FOLDER_BASENAME'/wordpress>' >> /etc/apache2/sites-available/000-default.conf && \
    echo '    Options FollowSymLinks' >> /etc/apache2/sites-available/000-default.conf && \
    echo '    AllowOverride All' >> /etc/apache2/sites-available/000-default.conf && \
    echo '    Require all granted' >> /etc/apache2/sites-available/000-default.conf && \
    echo '</Directory>' >> /etc/apache2/sites-available/000-default.conf

RUN echo "<?php" > /etc/phpmyadmin/config.inc.php && \
    echo "\$cfg['blowfish_secret'] = 'a8b7c6d5e4f3g2h1i0j9k8l7m6n5o4p3';" >> /etc/phpmyadmin/config.inc.php && \
    echo "\$cfg['TempDir'] = '/var/lib/phpmyadmin/tmp';" >> /etc/phpmyadmin/config.inc.php && \
    echo "\$cfg['Servers'][1]['auth_type'] = 'cookie';" >> /etc/phpmyadmin/config.inc.php && \
    echo "\$cfg['Servers'][1]['host'] = '127.0.0.1';" >> /etc/phpmyadmin/config.inc.php

RUN echo "Listen 8080" >> /etc/apache2/ports.conf && \
    echo '<VirtualHost *:8080>' > /etc/apache2/sites-available/phpmyadmin.conf && \
    echo '    DocumentRoot /usr/share/phpmyadmin' >> /etc/apache2/sites-available/phpmyadmin.conf && \
    echo '    <Directory /usr/share/phpmyadmin>' >> /etc/apache2/sites-available/phpmyadmin.conf && \
    echo '        Options FollowSymLinks' >> /etc/apache2/sites-available/phpmyadmin.conf && \
    echo '        DirectoryIndex index.php' >> /etc/apache2/sites-available/phpmyadmin.conf && \
    echo '        AllowOverride All' >> /etc/apache2/sites-available/phpmyadmin.conf && \
    echo '        Require all granted' >> /etc/apache2/sites-available/phpmyadmin.conf && \
    echo '    </Directory>' >> /etc/apache2/sites-available/phpmyadmin.conf && \
    echo '</VirtualHost>' >> /etc/apache2/sites-available/phpmyadmin.conf

RUN chown -R www-data:www-data /usr/share/phpmyadmin && \
    chmod -R 755 /usr/share/phpmyadmin && \
    ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin && \
    a2ensite phpmyadmin.conf

EXPOSE 80 8080

CMD ["/bin/bash", "-c", "service mysql start && service apache2 start && tail -f /dev/null"]
