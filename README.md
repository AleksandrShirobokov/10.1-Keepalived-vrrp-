# 10.1 «Keepalived/vrrp»
# Александр Широбоков
## Задание 1. Разверните топологию из лекции и выполните установку и настройку сервиса Keepalived.
### Статус сервиса MASTER:
![Снимок экранГа (67)](https://user-images.githubusercontent.com/69298696/228101851-e94c9948-d4de-4b6c-826a-e7eefd04b4d9.png)
### Статус сервиса BACKUP:
![Снимок экрана (67)](https://user-images.githubusercontent.com/69298696/228101982-5f3fb008-0ed7-4035-bd9b-63cf33296aa6.png)
### Работающая сеть на MASTER:
![Снимок экрана (68)](https://user-images.githubusercontent.com/69298696/228102319-c41ff75c-13b5-41c7-bc44-858a905b4753.png)
### Конфиги MASTER & BACKUP(аутентификацию указываю через PASS, чтобы пропала ошибка "initial state master is incompatible with ah authentication - clearing"):
### MASTER:
![Снимок экрана (69)](https://user-images.githubusercontent.com/69298696/228102462-ad4147de-9588-4d29-9632-3a9e1be1b089.png)

```
vrrp_instance test {  
state MASTER  
interface enp0s3  
virtual_router_id 10  
priority 50   
advert_int 4  
authentication {  
auth_type PASS  
auth_pass 12345  
}   
unicast_peer {  
192.168.0.19  
}   
virtual_ipaddress {   
192.168.0.44 dev enp0s3 label enp0s3:vip  
}   
}
``` 
  
### BACKUP:
![Снимок экрана (70)](https://user-images.githubusercontent.com/69298696/228102591-51645338-4865-4cef-80ae-f69a91313161.png)

```
vrrp_instance failover_test { 
state BACKUP  
interface enp0s3  
virtual_router_id 10  
priority 50 
advert_int 4  
authentication {  
auth_type PASS  
auth_pass 12345  
} 
unicast_peer {  
192.168.0.15  
} 
virtual_ipaddress { 
192.168.0.44 dev enp0s3 label enp0s3:vip  
}   
}   
```

## Задание 2. Проведите тестирование работы ноды, когда один из интерфейсов выключен.
### Устанавливаю Wireshark на третью машину и включаю отслеживание трафика, хост находится на .44 адресе, пингую:
![Снимок экрана (181)](https://user-images.githubusercontent.com/69298696/227948648-b0f83fbc-70f5-40d5-921a-9a53c78ece37.png)
### Затем отключаю порт на мастере, останавливаю Wireshark, и проверяю что мак адрес изменился:
![Снимок экрана (182)](https://user-images.githubusercontent.com/69298696/227948653-b14012f5-6070-4cde-a270-afd250ac09a3.png)

