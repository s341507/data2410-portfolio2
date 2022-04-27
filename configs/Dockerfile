FROM ubuntu:20.04
ENV TZ=Europe/Oslo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime  && echo $TZ > /etc/timezone
RUN apt-get -y update
RUN apt install iputils-ping -y
RUN apt install net-tools -y
RUN apt install nano -y
#RUN apt-get -y install apache2
#CMD ["apachectl", "-D", "FOREGROUND"]
CMD ["tail", "-f", "/dev/null"]
