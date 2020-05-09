FROM biopython/biopython:latest
MAINTAINER Tiago Antao <tra@popgen.net>

ENV DEBIAN_FRONTEND noninteractive

#For BioSQL
RUN apt-get install -y postgresql python3-psycopg2
RUN apt-get install -y mysql-server python-mysqldb
RUN apt-get install -y python3-mysql.connector
RUN apt-get install -y postgresql-server-dev-all
RUN apt-get clean

#RUN pip3 install psycopg2 --upgrade

#Database servers
RUN echo "host    all             all             ::1/128                 trust" > /etc/postgresql/10/main/pg_hba.conf
RUN echo "service postgresql start" > .bashrc
RUN echo "service mysql start" >> .bashrc
RUN echo "export LANG=en_GB.UTF-8" >> .bashrc
RUN echo "service postgresql start" > entrypoint.sh
RUN echo "service mysql start" >> entrypoint.sh
