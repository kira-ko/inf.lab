Отчет по лабораторной работе №4.
===

Задание:
---
Запустить в контейнере приложение “aafire”. Обратите внимание, что оно бесконечное и контейнер не будет автоматически отключаться.
Приложить скриншот в процессе работы контейнера.

Далее в рамках лабораторной работы необходимо самостоятельно настроить сеть между двумя контейнерами, также как в предыдущей работе вы настраивали связь между двумя виртуальными машинами.

Для проверки сети между контейнерами вам потребуется утилита ping. Поскольку контейнеры очень маленькие и в них нет ничего лишнего (по сравнению с виртуальными машинами) - ping там не установлен. В вашем образе нужно будет установить пакет с этой утилитой, помимо aafire.

Далее запустите два контейнера с aafire и оставьте их в работающем состоянии.
Откройте ещё одно окно терминала и создайте сеть при помощи команды

docker network create myNetwork
После этого нужно будет подключить контейнеры к вашей сети. Названия контейнеров можно увидеть при выводе списка действующих контейнеров у вас на машине.

docker network connect myNetwork mycontainer1
docker network connect myNetwork mycontainer2
Теперь при помощи следующей команды вы можете увидеть настройки созданной вами сети.

docker network inspect myNetwork
Далее вам нужно самостоятельно протестировать соединение между контейнерами утилитой ping и приложить скриншот.

Решение:
----
1. Устанавливаю Docker и проверяю, что он установлен с помощью команды:
 ```bash
   sudo apt-get update && sudo apt-get install -y docker.io
   ```

 ```bash
   docker -- version
   ```

2. Создаю рабочую папку для проекта:
```bash
   mkdir lab4 && cd lab4
   ```
3. Создаем и открываем для редактирования файл Dockerfile внутри папки lab4:
   ```bash
   nano Dockerfile
   ```
![unnamed](https://github.com/user-attachments/assets/3c36f6e9-35d4-46d0-8da6-58d8d0e72070)

4. Прописываю в файле следующие команды:
  ```bash
  FROM ubuntu:latest  
  RUN apt-get update && apt-get install -y libaa-bin fortune && apt-get install iputils-ping -y
  ```
  Здесь: 
  
  * первая строка FROM ubuntu:latest - обозначает, что мы используем базовый образ Ubuntu
  
  * вторая строка - устанавливаем нужные пакеты. 
  
    - iputils-ping — утилита для проверки соединения между устройствами через ICMP (используется для команды ping).
    - Флаг -y автоматически подтверждает установку, чтобы процесс не требовал ввода "да/нет".
    - Объединение через &&: Гарантирует, что вторая команда выполнится только после успешного выполнения первой.

Сохраняю файл (Ctrl + O)
Выйти (Ctrl + X)

5. Собираю Docker-образ командой:
  ```bash
  sudo docker build -t libaa-bin .
  ```
![unnamed](https://github.com/user-attachments/assets/139924f2-1046-4190-b5ce-91966ee47705)

  Проверяю, что образ создан:
  ```bash
  sudo docker images
  ```
![unnamed](https://github.com/user-attachments/assets/e6f72163-ba27-4925-a3d0-7a0e44b8ccb8)


6. Запуская первый и второй контейнер:
```bash
  sudo docker run -dit --name mycontainer1 libaa-bin
  sudo docker run -dit --name mycontainer2 libaa-bin
  ```
Проверка, что оба контейнера работают:
 ```bash
  sudo docker ps
  ```
![unnamed](https://github.com/user-attachments/assets/30696c67-946b-4e14-995a-0d273d4f3d01)


7. Создаю пользовательскую сеть:
 ```bash
  docker network create myNetwork
  ```
8.  Подключаю оба контейнера к созданной сети:
 ```bash
  sudo docker network connect myNetwork mycontainer1
  sudo docker network connect myNetwork mycontainer2
  ```
![unnamed](https://github.com/user-attachments/assets/6c239c95-fd72-4b81-86aa-54daeea90db0)


 Проверяю параметры сети с поомщью команды:
 ```bash
  sudo docker network inspect myNetwork
  ```
![unnamed](https://github.com/user-attachments/assets/ac2ad424-9c14-401a-b34e-f46b3691616e)


9. Проверяю связь между контейнерами.
Подключаюсь к первому контейнеру:
```bash
  sudo docker exec -it mycontainer1 bash
  ```

Проверяю связь с контейнером 2:
```bash
  ping 172.18.0.3
  ```
где 172.18.0.3 - IP-фдресс второго контейнера

10. Чтобы увидить работу aafire
внутри контейнера ввожу команду:
```bash
  aafire
  ```




