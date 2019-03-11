下载rpm包：
---
    curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-6.6.1-x86_64.rpm

安装：
---
    sudo rpm -vi filebeat-6.6.1-x86_64.rpm

启动：
---
    systemctl start filebeat.service
    systemctl enable filebeat.service

修改配置文件：
---
    cp /etc/filebeat/filebeat.yml /etc/filebeat/filebeat.yml.bak
    其他地方不动，主要修改下面的地方：
      paths:
        - /var/log/*.log
       - /var/lib/docker/contrainers/*/*.log
        - /var/log/syslog
        #- c:\programdata\elasticsearch\logs\*	
    #-------------------------- Elasticsearch output ------------------------------
    output.elasticsearch:
      # Array of hosts to connect to.
      hosts: ["elasticsearch的IP地址:9200"]
      template.name: "filebeat"  
      template.path: "filebeat.template.json"  
      template.overwrite: false 
      # Optional protocol and basic auth credentials.
    #protocol: "https"
    #username: "elastic"
    #password: "changeme"
  
检测配置文件是否正确
---
    filebeat.sh -configtest -e

重启filebeat服务
---
    systemctl restart filebeat.service
