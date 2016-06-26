# docker_wordpress_elk

The docker compose file will build modified MySQL and WordPress images with Filebeat shippers installed on them. Then it will start MySQL and WordPress containers. Their logs will be sent to logstash container. Finally, the logstash container ships the logs to elasticsearch container which will be linked to Kibana container.

The modified images ```mysql_filebeat``` and ```wordpress_filebeat``` images from the latest tags of the official mysql and wordpress images. The ```Filebeat``` Shipper is installed on them. Also, the Apache logs (```wordpress_filebeat image```) are configured as ```access.log``` and  ```errorr.log```, whereas MySQL logs are configured as ```slow.log``` (slow queries that is more than 5 seconds) and ```error.log```.

* The access of the kibana server will be at ```http://localhost:5601```. The index pattern will ```blog-beat-*```.
* The access of the WordPress will be at ```http://localhost:8080```.
* The Elasticsearch types of the ```blog-beat-*``` index will be:
 * ```blog-beat-apache-access``` type for ```/var/log/apache2/access.log``` file
 * ```blog-beat-apache-error``` type for ```/var/log/apache2/error.log``` file
 * ```blog-beat-mysql-slow``` type for ```/var/log/mysql/error.log``` file
 * ```blog-beat-mysql-error``` type for ```/var/log/mysql/slow.log``` file
 
To launch the WordPress blog and ELK run:
```bash
# docker-compose up
```

