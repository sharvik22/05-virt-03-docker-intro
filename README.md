
# Домашнее задание к занятию 4 «Оркестрация группой Docker контейнеров на примере Docker Compose» Шарапат Виктор

### Инструкция к выполению

1. Для выполнения заданий обязательно ознакомьтесь с [инструкцией](https://github.com/netology-code/devops-materials/blob/master/cloudwork.MD) по экономии облачных ресурсов. Это нужно, чтобы не расходовать средства, полученные в результате использования промокода.
2. Практические задачи выполняйте на личной рабочей станции или созданной вами ранее ВМ в облаке.
3. Своё решение к задачам оформите в вашем GitHub репозитории в формате markdown!!!
4. В личном кабинете отправьте на проверку ссылку на .md-файл в вашем репозитории.

## Задача 1

Сценарий выполнения задачи:
- Установите docker и docker compose plugin на свою linux рабочую станцию или ВМ.
- Если dockerhub недоступен создайте файл /etc/docker/daemon.json с содержимым: ```{"registry-mirrors": ["https://mirror.gcr.io", "https://daocloud.io", "https://c.163.com/", "https://registry.docker-cn.com"]}```
- Зарегистрируйтесь и создайте публичный репозиторий  с именем "custom-nginx" на https://hub.docker.com (ТОЛЬКО ЕСЛИ У ВАС ЕСТЬ ДОСТУП);
- скачайте образ nginx:1.21.1;
- Создайте Dockerfile и реализуйте в нем замену дефолтной индекс-страницы(/usr/share/nginx/html/index.html), на файл index.html с содержимым:
```
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I will be DevOps Engineer!</h1>
</body>
</html>
```
- Соберите и отправьте созданный образ в свой dockerhub-репозитории c tag 1.0.0 (ТОЛЬКО ЕСЛИ ЕСТЬ ДОСТУП). 
- Предоставьте ответ в виде ссылки на https://hub.docker.com/<username_repo>/custom-nginx/general .

## Решение 1

- Установите docker и docker compose plugin на свою linux рабочую станцию или ВМ.
 
![Screenshot_10](https://github.com/user-attachments/assets/5f86e807-3b75-4f5e-a9ba-d5dde609e057)

- скачайте образ nginx:1.21.1;

![Screenshot_3](https://github.com/user-attachments/assets/60fcb613-fdcc-469b-a3fe-10e3a16c5ccb)

- Создайте Dockerfile и реализуйте в нем замену дефолтной индекс-страницы(/usr/share/nginx/html/index.html), на файл index.html с содержимым:

создал файл Dockerfile c содержимым

![Screenshot_4](https://github.com/user-attachments/assets/c7e530c8-6406-4139-8559-d27841448c84)

и файл index.html

![image](https://github.com/user-attachments/assets/9ddf0410-99bd-4872-ba6f-b23e0b35a6e2)

- Соберите и отправьте созданный образ в свой dockerhub-репозитории c tag 1.0.0 (ТОЛЬКО ЕСЛИ ЕСТЬ ДОСТУП).

собрал образ

![Screenshot_8](https://github.com/user-attachments/assets/08037bc8-fccf-4e61-9d2d-ba87821ae14a)

залогинился на dockerhub и отправил образ

![Screenshot_9](https://github.com/user-attachments/assets/15df38dd-227c-46a3-aa6c-06084a0bd373)

![Screenshot_11](https://github.com/user-attachments/assets/85b038f9-d0b5-42d1-94d0-b3025aec3551)

- Предоставьте ответ в виде ссылки на https://hub.docker.com/<username_repo>/custom-nginx/general .
https://hub.docker.com/repository/docker/sharvik22/my-nginx-image/general

---


## Задача 2
1. Запустите ваш образ custom-nginx:1.0.0 командой docker run в соответвии с требованиями:
- имя контейнера "ФИО-custom-nginx-t2"
- контейнер работает в фоне
- контейнер опубликован на порту хост системы 127.0.0.1:8080
2. Переименуйте контейнер в "custom-nginx-t2"
3. Выполните команду ```date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080  ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html```
4. Убедитесь с помощью curl или веб браузера, что индекс-страница доступна.

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

## Решение 2

1. Запустите ваш образ custom-nginx:1.0.0 командой docker run в соответвии с требованиями:
- имя контейнера "ФИО-custom-nginx-t2"
- контейнер работает в фоне
- контейнер опубликован на порту хост системы 127.0.0.1:8080
  
Я сделал образ с именем sharvik22/my-nginx-image:1.0.0. Удалил все образы и контейнеры и заново загрузил свой образ с dockerhub

остановить все контейнеры
docker stop $(docker ps -a -q)

удалить все контейнеры
docker rm $(docker ps -a -q)

удалить все образы
docker rmi $(docker images -q)

загрузить  образ
docker push sharvik22/my-nginx-image:tagname

![Screenshot_2](https://github.com/user-attachments/assets/cc95b456-09f5-46e7-8ae0-4cae1e5fcaa1)

![Screenshot_3](https://github.com/user-attachments/assets/cb3bdd08-7cb3-4577-96d3-dbdf44d1bde6)

2. Переименуйте контейнер в "custom-nginx-t2"

остановил и удалил контейнер и заново создал с именем custom-nginx-t2 и своим образом 

![Screenshot_6](https://github.com/user-attachments/assets/71902d1d-757f-4d06-b299-027c628dba22)


3. Выполните команду ```date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080  ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html```

 ![Screenshot_7](https://github.com/user-attachments/assets/2936acc1-d86a-4ecc-8d10-7f0e3293538c)


 4. Убедитесь с помощью curl или веб браузера, что индекс-страница доступна.

 ![image](https://github.com/user-attachments/assets/299de4d9-d977-4e72-9a0b-7614be16ec28)

---

## Задача 3
1. Воспользуйтесь docker help или google, чтобы узнать как подключиться к стандартному потоку ввода/вывода/ошибок контейнера "custom-nginx-t2".
2. Подключитесь к контейнеру и нажмите комбинацию Ctrl-C.
3. Выполните ```docker ps -a``` и объясните своими словами почему контейнер остановился.
4. Перезапустите контейнер
5. Зайдите в интерактивный терминал контейнера "custom-nginx-t2" с оболочкой bash.
6. Установите любимый текстовый редактор(vim, nano итд) с помощью apt-get.
7. Отредактируйте файл "/etc/nginx/conf.d/default.conf", заменив порт "listen 80" на "listen 81".
8. Запомните(!) и выполните команду ```nginx -s reload```, а затем внутри контейнера ```curl http://127.0.0.1:80 ; curl http://127.0.0.1:81```.
9. Выйдите из контейнера, набрав в консоли  ```exit``` или Ctrl-D.
10. Проверьте вывод команд: ```ss -tlpn | grep 127.0.0.1:8080``` , ```docker port custom-nginx-t2```, ```curl http://127.0.0.1:8080```. Кратко объясните суть возникшей проблемы.
11. * Это дополнительное, необязательное задание. Попробуйте самостоятельно исправить конфигурацию контейнера, используя доступные источники в интернете. Не изменяйте конфигурацию nginx и не удаляйте контейнер. Останавливать контейнер можно. [пример источника](https://www.baeldung.com/linux/assign-port-docker-container)
12. Удалите запущенный контейнер "custom-nginx-t2", не останавливая его.(воспользуйтесь --help или google)

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

## Решение 3

1. Воспользуйтесь docker help или google, чтобы узнать как подключиться к стандартному потоку ввода/вывода/ошибок контейнера "custom-nginx-t2".
docker attach custom-nginx-t2
docker logs custom-nginx-t2

![Screenshot_1](https://github.com/user-attachments/assets/8a8b40a4-e734-40ed-8d38-c161a6eddb52)

![Screenshot_2](https://github.com/user-attachments/assets/0e8d55c4-8774-46c0-b5dc-b4fcf74b303f)

2. Подключитесь к контейнеру и нажмите комбинацию Ctrl-C.

![image](https://github.com/user-attachments/assets/00780bfe-6fe5-4aea-9773-2b481e7469ae)

3. Выполните ```docker ps -a``` и объясните своими словами почему контейнер остановился.

Контейнер не остановился, комбинацию Ctrl-C - команда прерывания процесса (SIGINT). docker stop custom-nginx-t2 - остановит контейнер.

![image](https://github.com/user-attachments/assets/abc966df-6019-4776-94d8-6268b0a6cd58)

4. Перезапустите контейнер

![image](https://github.com/user-attachments/assets/84996b71-fd11-4847-8b98-f8a4571c6b18)

5. Зайдите в интерактивный терминал контейнера "custom-nginx-t2" с оболочкой bash.

![image](https://github.com/user-attachments/assets/7ada7ae1-c0ed-4dbe-9d6c-d9f44c4991ac)

6. Установите любимый текстовый редактор(vim, nano итд) с помощью apt-get.

![image](https://github.com/user-attachments/assets/34d09a41-23c6-4de8-95ee-e25dcdfc8c7c)

![image](https://github.com/user-attachments/assets/4e1daf30-0f92-4603-bf0f-4be722953eef)

7. Отредактируйте файл "/etc/nginx/conf.d/default.conf", заменив порт "listen 80" на "listen 81".

![image](https://github.com/user-attachments/assets/c9308ce6-fd7d-4ef8-9649-a8ce4d5c2a9a)

![image](https://github.com/user-attachments/assets/3061322d-a795-4ce5-9f89-e327ff7a622c)


8. Запомните(!) и выполните команду ```nginx -s reload```, а затем внутри контейнера ```curl http://127.0.0.1:80 ; curl http://127.0.0.1:81```.

![image](https://github.com/user-attachments/assets/ffdc39da-ce27-4ce8-bd64-a07792fa20e1)


9. Выйдите из контейнера, набрав в консоли  ```exit``` или Ctrl-D.

![image](https://github.com/user-attachments/assets/3b42cf0a-e7f8-4099-93f4-446d20b3c957)

10. Проверьте вывод команд: ```ss -tlpn | grep 127.0.0.1:8080``` , ```docker port custom-nginx-t2```, ```curl http://127.0.0.1:8080```. Кратко объясните суть возникшей проблемы.

![image](https://github.com/user-attachments/assets/b1ed8c5e-a023-45c2-b01e-687e2f47f5bb)

ss -tlpn | grep 127.0.0.1:8080 - 
ss - команда, которая выводит информацию о сокетах, -tlpn - это её флаги. grep 127.0.0.1:8080 - фильтрует вывод (вывод, только тех строк, где есть 127.0.0.1:8080)
вывод будет пустой, т.к. у нас нет сокетов, процессов, прослушивающих порт 8080

docker port custom-nginx-t2
выводит список портов с которыми запускался контейнер custom-nginx-t2 (сопоставление портов в внутри и снаружи контейнера)

0.0.0.0:8080->80/tcp, :::8080->80/tcp

curl http://127.0.0.1:8080
команда проверки доступности по HTTP протоколу.Отправка запроса по IP и порту. Результат - ответа нет, по данному IP и порту/

Суть проблемы нет доступа или недоступен ресурс по 127.0.0.1:8080
docker port custom-nginx-t2 - результат дал, так как при запуске был проброс портов у контейнера.


13. Удалите запущенный контейнер "custom-nginx-t2", не останавливая его.(воспользуйтесь --help или google)

![image](https://github.com/user-attachments/assets/73e5221f-ecd7-40fb-8a34-f2d93e99ad9e)

---

## Задача 4


- Запустите первый контейнер из образа ***centos*** c любым тегом в фоновом режиме, подключив папку  текущий рабочий каталог ```$(pwd)``` на хостовой машине в ```/data``` контейнера, используя ключ -v.
- Запустите второй контейнер из образа ***debian*** в фоновом режиме, подключив текущий рабочий каталог ```$(pwd)``` в ```/data``` контейнера. 
- Подключитесь к первому контейнеру с помощью ```docker exec``` и создайте текстовый файл любого содержания в ```/data```.
- Добавьте ещё один файл в текущий каталог ```$(pwd)``` на хостовой машине.
- Подключитесь во второй контейнер и отобразите листинг и содержание файлов в ```/data``` контейнера.


В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

## Решение 4

- Запустите первый контейнер из образа ***centos*** c любым тегом в фоновом режиме, подключив папку  текущий рабочий каталог ```$(pwd)``` на хостовой машине в ```/data``` контейнера, используя ключ -v.

![image](https://github.com/user-attachments/assets/c6527419-977c-42b5-9540-3488d6d33b02)

- Запустите второй контейнер из образа ***debian*** в фоновом режиме, подключив текущий рабочий каталог ```$(pwd)``` в ```/data``` контейнера.

![image](https://github.com/user-attachments/assets/040a1f27-b02e-46fd-88a6-939aaa3e5722)

- Подключитесь к первому контейнеру с помощью ```docker exec``` и создайте текстовый файл любого содержания в ```/data```.

![image](https://github.com/user-attachments/assets/dea45ca1-18c8-4cc9-a7ae-343c6e82c74e)

- Добавьте ещё один файл в текущий каталог ```$(pwd)``` на хостовой машине.

![image](https://github.com/user-attachments/assets/8f77715e-55ef-414c-b011-713ee15950bd)

- Подключитесь во второй контейнер и отобразите листинг и содержание файлов в ```/data``` контейнера.

![image](https://github.com/user-attachments/assets/5d4dcfe0-991f-40c5-b089-00eb195dda83)

---


## Задача 5

1. Создайте отдельную директорию(например /tmp/netology/docker/task5) и 2 файла внутри него.
"compose.yaml" с содержимым:
```
version: "3"
services:
  portainer:
    image: portainer/portainer-ce:latest
    network_mode: host
    ports:
      - "9000:9000"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
```
"docker-compose.yaml" с содержимым:
```
version: "3"
services:
  registry:
    image: registry:2
    network_mode: host
    ports:
    - "5000:5000"
```

И выполните команду "docker compose up -d". Какой из файлов был запущен и почему? (подсказка: https://docs.docker.com/compose/compose-application-model/#the-compose-file )

2. Отредактируйте файл compose.yaml так, чтобы были запущенны оба файла. (подсказка: https://docs.docker.com/compose/compose-file/14-include/)

3. Выполните в консоли вашей хостовой ОС необходимые команды чтобы залить образ custom-nginx как custom-nginx:latest в запущенное вами, локальное registry. Дополнительная документация: https://distribution.github.io/distribution/about/deploying/
4. Откройте страницу "https://127.0.0.1:9000" и произведите начальную настройку portainer.(логин и пароль адмнистратора)
5. Откройте страницу "http://127.0.0.1:9000/#!/home", выберите ваше local  окружение. Перейдите на вкладку "stacks" и в "web editor" задеплойте следующий компоуз:

```
version: '3'

services:
  nginx:
    image: 127.0.0.1:5000/custom-nginx
    ports:
      - "9090:80"
```
6. Перейдите на страницу "http://127.0.0.1:9000/#!/2/docker/containers", выберите контейнер с nginx и нажмите на кнопку "inspect". В представлении <> Tree разверните поле "Config" и сделайте скриншот от поля "AppArmorProfile" до "Driver".

7. Удалите любой из манифестов компоуза(например compose.yaml).  Выполните команду "docker compose up -d". Прочитайте warning, объясните суть предупреждения и выполните предложенное действие. Погасите compose-проект ОДНОЙ(обязательно!!) командой.

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод, файл compose.yaml , скриншот portainer c задеплоенным компоузом.

## Решение 5

1.

![image](https://github.com/user-attachments/assets/3f23e9ac-cf39-4280-97a2-f9326faebfb6)

![image](https://github.com/user-attachments/assets/5f631beb-1c13-4941-af71-21a358ab4d03)

Какой из файлов был запущен и почему?




---

### Правила приема

Домашнее задание выполните в файле readme.md в GitHub-репозитории. В личном кабинете отправьте на проверку ссылку на .md-файл в вашем репозитории.


