Отчет по лабораторной работе №3
=====
1. создала и настроила три виртуальные машины с дистрибутивом Ubuntu
2. Узнаю IP адресса каждой виртуальной машины, с помощью команды 
 ```bash
   ip a
   ```

![Screenshot from 2024-11-17 19-11-35](https://github.com/user-attachments/assets/78d72dc3-821e-4248-aec4-c3f5c6d9ac09)
![Screenshot from 2024-11-17 19-12-16](https://github.com/user-attachments/assets/d17c3e25-a91e-4c4f-b01c-0d63d79bc49a)
![Screenshot from 2024-11-17 19-11-54](https://github.com/user-attachments/assets/24327b0a-b5a0-4d47-9bc8-54b489763252)


3. Проверяю доступ к сети интернет на машине А, с помощью команды
 ```bash
   ping -c 4 8.8.8.8
   ```
(-c 4 обозначает четыре запроса к указанному IP-адрессу 8.8.8.8.(DNS-сервер Google))


![Screenshot from 2024-11-17 19-11-19](https://github.com/user-attachments/assets/fa26a4b0-3c7b-4890-a7cf-d2a6940248a8)


4. Обеспечиваю сетевой доступ от машины А к машине B. Использую команду:
    ```bash
   ping -c 4 192.168.83.132
   ```
![Screenshot from 2024-11-17 19-13-00](https://github.com/user-attachments/assets/a32fdb46-cc35-455e-ab3e-53cd27f2ce6c)

  на скриншоте видно, что соединение активно

    
5. Также обеспечиваю и проверяю сетевой доступ от машины А к машине C

![Screenshot from 2024-11-17 19-13-24](https://github.com/user-attachments/assets/f6ba2c19-c53a-4b8c-8e60-769254f96c9c)


6. Запрещаю доступ из машины В к машине С. В терминале машины С ввожу данную команду:
  ```bash
   sudo iptables -A INPUT -s 192.168.83.132 -j DROP
   ```
![unnamed (1)](https://github.com/user-attachments/assets/de95f8df-b740-4c3f-9560-35dd8e9f0d63)


7. Проверяю соединение из машины В к машине С. В терминале машины В ввожу команду
  ```bash
   ping -c 4 192.168.83.133
   ```
![unnamed (2)](https://github.com/user-attachments/assets/6e08135a-100c-40cf-bd17-6d87dd6243ef)



видим, что как и требовалось, доступ заблокирован
