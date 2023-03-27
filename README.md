# 10.1 «Keepalived/vrrp»
# Александр Широбоков
## Задание 1. Разверните топологию из лекции и выполните установку и настройку сервиса Keepalived.
### Статус сервиса MASTER:
![Снимок экрана (175)](https://user-images.githubusercontent.com/69298696/227924066-0d37fc50-9c99-4b06-8c66-2c0be8ba753f.png)
### Статус сервиса BACKUP:
![Снимок экрана (176)](https://user-images.githubusercontent.com/69298696/227924278-735af708-55d1-485f-aa4b-0a91b0afb8fe.png)
### Работающая сеть на MASTER:
![Снимок экрана (177)](https://user-images.githubusercontent.com/69298696/227924791-ced5fc61-a235-4322-8f51-2ceaccb8c7bc.png)
### Конфиги MASTER & BACKUP:
### MASTER:
![Снимок экрана (178)](https://user-images.githubusercontent.com/69298696/227925521-eeaf4c7d-2192-4156-87cf-f9f8dfd430e3.png)

vrrp_instance test {  
state MASTER  
interface enp0s3  
virtual_router_id 10  
priority 50   
advert_int 4  
authentication {  
auth_type AH  
auth_pass 0000  
}   
unicast_peer {  
192.168.0.18  
}   
virtual_ipaddress {   
192.168.0.44 dev enp0s3 label enp0s3:vip  
}   
}   
  

### BACKUP:
![Снимок экрана (179)](https://user-images.githubusercontent.com/69298696/227925617-09ba47a3-5857-47be-b9fa-0574974f510d.png)

vrrp_instance failover_test { 
state BACKUP  
interface enp0s3  
virtual_router_id 10  
priority 50 
advert_int 4  
authentication {  
auth_type AH  
auth_pass 0000  
} 
unicast_peer {  
192.168.0.11  
} 
virtual_ipaddress { 
192.168.0.44 dev enp0s3 label enp0s3:vip  
}   
}   
![Снимок экрана (181)](https://user-images.githubusercontent.com/69298696/227948648-b0f83fbc-70f5-40d5-921a-9a53c78ece37.png)
![Снимок экрана (182)](https://user-images.githubusercontent.com/69298696/227948653-b14012f5-6070-4cde-a270-afd250ac09a3.png)

