## Отчет по лабораторной работе №4

---

--- 

### План работы:
#### 1) Создать docker image (образ)
#### 2) Запустить в контейнере приложение “aafire”
#### 3) Настроить сеть между двумя контейнерами
#### 4) Проверить связь между контейнерами
#### 5) Написать отчет в каталоге report/Readme.md

---

## Реализация:

### Установка Docker:

```sudo apt install docker.io```

### Настройка прав доступа:

#### ```sudo group add docker``` - создание  docker группы 
#### ```sudo usermod -aG docker $USER``` - добавление пользователя в созданную группу
#### ```newgrp docker``` - новая docker группа

###  Dockerfile:

#### Dockerfile — это текстовый файл, содержащий инструкции для автоматизированного создания образа Docker.

```
FROM ubuntu:latest

RUN apt-get update -y 
RUN apt-get install libaa-bin -y
RUN apt-get install iputils-ping -y
RUN apt-get install net-tools -y

```

###  Docker image:

#### ```docker build -t aafire .``` - сборка образа с тегом "aafire"


###  Установка и запуск контейнеров:

#### На основе образа создаются два контейнера - "mycontainer1" и "mycontainer2":

```docker run -t -it --name mycontainer2 aafire```

```docker run -t -it --name mycontainer1 aafire```

###  Настройка сети:

#### Создается сеть, к которй подключаются имющиеся контейнеры:

```docker network create myNetwork```

```docker network connect myNetwork mycontainer1```
```docker network connect myNetwork mycontainer2```

### Проверка сети и связи между контейнерами:

```docker network inspect myNetwork```

![image](https://github.com/cs-itmo-2023/lab-4-MrL013/blob/main/report/src/net.png)

#### Проверка связи между контейнерами "mycontainer1" и "mycontainer2":

```docker exec -it mycontainer1 ping mycontainer2```

![image](https://github.com/cs-itmo-2023/lab-4-MrL013/blob/main/report/src/ping2.png)

```docker exec -it mycontainer2 ping mycontainer1```

![image](https://github.com/cs-itmo-2023/lab-4-MrL013/blob/main/report/src/ping1.png)

### Заруск aafire из контейнера:

![image](https://github.com/cs-itmo-2023/lab-4-MrL013/blob/main/report/src/fire.png)

#### пламя показывается - значит все процедуры были выполнены корректно.
