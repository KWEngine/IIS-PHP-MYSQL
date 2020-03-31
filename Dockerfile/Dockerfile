# Dockerfile for Nano Server with IIS Role, PHP and MySQL.

FROM nanoserver/iis

MAINTAINER nanoserver.es@gmail.com

ADD https://windows.php.net/downloads/releases/php-7.4.4-Win32-vc15-x64.zip php.zip
ADD https://www.lutzkarau.de/downloads/vcruntime140.dll C:\\Windows\\System32\\vcruntime140.dll
ADD https://www.lutzkarau.de/downloads/iisfcgi.dll C:\\Windows\\System32\\inetsrv\\iisfcgi.dll

ENV PHP C:\\php

RUN powershell -command Expand-Archive -Path c:\php.zip -DestinationPath C:\php

RUN setx PATH /M %PATH%;C:\php 

# ADD https://jbit.es/files/php.ini C:\\php\\php.ini

RUN powershell -command \

    rm C:\Windows\System32\inetsrv\config\Applicationhost.config ; \
    Invoke-WebRequest -uri https://jbit.es/files/ApplicationHost.dll -outfile C:\\Windows\\System32\\inetsrv\\config\\Applicationhost.config ; \
    Remove-Item c:\php.zip -Force

ADD https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.22-winx64.zip mysql.zip
RUN powershell -command \
    Expand-Archive -Path c:\mysql.zip -DestinationPath C:\ ; \
    ren C:\mysql-5.7.22-winx64 C:\MySQL ; \
    New-Item -Path C:\MySQL\data -ItemType directory ; \
    C:\MySQL\bin\mysqld.exe --initialize --console --explicit_defaults_for_timestamp ; \
    C:\MySQL\bin\mysqld.exe --install ; \
    Start-Service mysql ; \
    Remove-Item c:\mysql.zip -Force
    
ENV MYSQL C:\\MySQL
RUN setx PATH /M %PATH%;C:\MySQL\bin
