FROM wordpress:latest

# install Filebeat shipper 
RUN apt-get update && apt-get install -y apt-transport-https
RUN echo "deb https://packages.elastic.co/beats/apt stable main" |  tee -a /etc/apt/sources.list.d/beats.list
RUN curl https://packages.elastic.co/GPG-KEY-elasticsearch | apt-key add -
RUN apt-get update && apt-get install -y filebeat && rm -rf /var/lib/apt/lists/* 

# config Apache logs
RUN sed -i -e 's/ErrorLog.*/ErrorLog \/var\/log\/apache2\/error.log/g' /etc/apache2/apache2.conf
RUN sed -i -e 's/CustomLog.*/CustomLog \/var\/log\/apache2\/access.log combined/g' /etc/apache2/apache2.conf

# add starting filebeat service to docker-entrypoint.sh 
RUN sed -i -e 's/exec.*/service filebeat start\n&/' /entrypoint.sh

