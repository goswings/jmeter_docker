# jmeter_docker

# Master docker_compose
version: '2'  
services:  
  master:  
    image: goswing/jmeter-master:v1  
    stdin_open: true  
    network_mode: host  
    tty: true  
    ports:  
    - 60000:60000/tcp  
    labels:  
      io.rancher.scheduler.affinity:host_label: io.rancher.host.name=master  
      io.rancher.container.pull_image: always  

# Racher_compose
version: '2'  
services:  
  master:  
    scale: 1  
    start_on_create: true  

# Slave docker_compose
version: '2'  
services:  
  slave01:  
    image: goswings/jmeter-slave:v1  
    environment:  
      HOST_IP: xxx.xxx.xx.xx  
    stdin_open: true  
    tty: true  
    ports:  
    - 1099:1099/tcp  
    - 50000:50000/tcp  
    labels:  
      io.rancher.container.pull_image: always  
      io.rancher.scheduler.affinity:host_label: host.ip=xxx.xx.xx.xx  

# Rancher_compose
version: '2'  
services:  
  slave01:  
    scale: 1  
    start_on_create: true  
