FROM mysql:latest

# install Filebeat shipper 
RUN apt-get update && apt-get install -y apt-transport-https curl
RUN echo "deb https://packages.elastic.co/beats/apt stable main" |  tee -a /etc/apt/sources.list.d/beats.list
RUN curl https://packages.elastic.co/GPG-KEY-elasticsearch | apt-key add -
RUN apt-get update && apt-get install -y filebeat && rm -rf /var/lib/apt/lists/* 


# config slow queries log of mysql server
RUN sed -i -e 's/\[mysqld\]/&\nlog_queries_not_using_indexes/' /etc/mysql/my.cnf
RUN sed -i -e 's/\[mysqld\]/&\nlong_query_time = 5/' /etc/mysql/my.cnf
RUN sed -i -e 's/\[mysqld\]/&\nslow_query_log_file = \/var\/log\/mysql\/slow.log/' /etc/mysql/my.cnf
RUN sed -i -e 's/\[mysqld\]/&\nslow_query_log = 1/' /etc/mysql/my.cnf

# config error log of mysql server
RUN sed -i -e 's/\[mysqld\]/&\nlog_error_verbosity = 3/' /etc/mysql/my.cnf
RUN sed -i -e 's/\[mysqld\]/&\nlog_error = \/var\/log\/mysql\/error.log/' /etc/mysql/my.cnf

# config error log of mysqld_safe
RUN sed -i -e 's/\[mysqld_safe\]/&\nlog_error_verbosity = 3/' /etc/mysql/my.cnf
RUN sed -i -e 's/\[mysqld_safe\]/&\nlog_error = \/var\/log\/mysql\/error.log/' /etc/mysql/my.cnf

# cdd starting filebeat service to docker-entrypoint.sh 
RUN sed -i -e 's/exec.*/service filebeat start\n&/' /usr/local/bin/docker-entrypoint.sh

