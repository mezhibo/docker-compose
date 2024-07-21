**Задача 1**

Сценарий выполнения задачи:

- Установите docker и docker compose plugin на свою linux рабочую станцию или ВМ.

- Если dockerhub недоступен создайте файл /etc/docker/daemon.json с содержимым: {"registry-mirrors": ["https://mirror.gcr.io", "https://daocloud.io", "https://c.163.com/", "https://registry.docker-cn.com"]}

- Зарегистрируйтесь и создайте публичный репозиторий с именем "custom-nginx" на https://hub.docker.com (ТОЛЬКО ЕСЛИ У ВАС ЕСТЬ ДОСТУП);
скачайте образ nginx:1.21.1;

- Создайте Dockerfile и реализуйте в нем замену дефолтной индекс-страницы(/usr/share/nginx/html/index.html), на файл index.html с содержимым:

'''

<html>
<head>
Hey, Netology
</head>
<body>
<h1>I will be DevOps Engineer!</h1>
</body>
</html>

'''

- Соберите и отправьте созданный образ в свой dockerhub-репозитории c tag 1.0.0 (ТОЛЬКО ЕСЛИ ЕСТЬ ДОСТУП).

- Предоставьте ответ в виде ссылки на https://hub.docker.com/<username_repo>/custom-nginx/general .


**Решение 1**


Проверяем наши версии docker и docker compose

Скачиваем к себе docker image nginx 1.21.1

![alt text](https://github.com/mezhibo/docker-compose/blob/01d7e387556b270ba6c00a9fc823b4e908750d3f/IMG/1.jpg)


Создаем репу на докер-хаб


![alt text](https://github.com/mezhibo/docker-compose/blob/01d7e387556b270ba6c00a9fc823b4e908750d3f/IMG/2.jpg)


Собираем свой Dockerfile

![alt text](https://github.com/mezhibo/docker-compose/blob/01d7e387556b270ba6c00a9fc823b4e908750d3f/IMG/3.jpg)


Создаем привественную веб страницу, котору будем подменять внутри контейнера nginx


![alt text](https://github.com/mezhibo/docker-compose/blob/01d7e387556b270ba6c00a9fc823b4e908750d3f/IMG/4.jpg)


Собираем нужный нам образ с нужной веб страницей



![alt text](https://github.com/mezhibo/docker-compose/blob/01d7e387556b270ba6c00a9fc823b4e908750d3f/IMG/5.jpg)


Проверямем что браз наш есть в спике docker image


![alt text](https://github.com/mezhibo/docker-compose/blob/01d7e387556b270ba6c00a9fc823b4e908750d3f/IMG/6.jpg)



Авторизуемся в докер-хаб и пушим наш собранный контейнер nginx с тегом

![alt text](https://github.com/mezhibo/docker-compose/blob/01d7e387556b270ba6c00a9fc823b4e908750d3f/IMG/7.jpg)


Возвращаемся в докер-хаб, и видим что наш образ докера с нашим тегом успешно загружен на докер-хаб

![alt text](https://github.com/mezhibo/docker-compose/blob/01d7e387556b270ba6c00a9fc823b4e908750d3f/IMG/8.jpg)


Вот [ССЫЛКА](https://hub.docker.com/r/mezhibo/custom-nginx) на образ в docker-hub



**Задача 2**

1) Запустите ваш образ custom-nginx:1.0.0 командой docker run в соответвии с требованиями:

- имя контейнера "ФИО-custom-nginx-t2"

- контейнер работает в фоне

- контейнер опубликован на порту хост системы 127.0.0.1:8080

2) Не удаляя, переименуйте контейнер в "custom-nginx-t2"

3)Выполните команду date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080  ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html

4) Убедитесь с помощью curl или веб браузера, что индекс-страница доступна.

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.



**Решение 2**

Запускаем собранный в предыдущем задании контейнер с фоне с моей фамилией в названии, и вешаем на порт 8080

![alt text](https://github.com/mezhibo/docker-compose/blob/636f733bc309866c688ca15457c16d4b3b26cd8d/IMG/9.jpg)

Потом перименовывем контейнер, и далее выолняем команды, которые нас просят в задании

![alt text](https://github.com/mezhibo/docker-compose/blob/636f733bc309866c688ca15457c16d4b3b26cd8d/IMG/10.jpg)

И теперь попробуем через curl дернуть нашу локальную веб-страницу из запущенного на порту 8080 контенйера nginx

![alt text](https://github.com/mezhibo/docker-compose/blob/636f733bc309866c688ca15457c16d4b3b26cd8d/IMG/11.jpg)



**Задача 3**

1) Воспользуйтесь docker help или google, чтобы узнать как подключиться к стандартному потоку ввода/вывода/ошибок контейнера "custom-nginx-t2".

2) Подключитесь к контейнеру и нажмите комбинацию Ctrl-C.

3) Выполните docker ps -a и объясните своими словами почему контейнер остановился.

4) Перезапустите контейнер

5) Зайдите в интерактивный терминал контейнера "custom-nginx-t2" с оболочкой bash.

6) Установите любимый текстовый редактор(vim, nano итд) с помощью apt-get.

7) Отредактируйте файл "/etc/nginx/conf.d/default.conf", заменив порт "listen 80" на "listen 81".

8) Запомните(!) и выполните команду nginx -s reload, а затем внутри контейнера curl http://127.0.0.1:80 && curl http://127.0.0.1:81.

9) Выйдите из контейнера, набрав в консоли exit или Ctrl-D.

10) Проверьте вывод команд: ss -tlpn | grep 127.0.0.1:8080 , docker port custom-nginx-t2, curl http://127.0.0.1:8080. Кратко объясните суть возникшей проблемы.

11) Это дополнительное, необязательное задание. Попробуйте самостоятельно исправить конфигурацию контейнера, используя доступные источники в интернете. Не изменяйте конфигурацию nginx и не удаляйте контейнер. Останавливать контейнер можно. пример источника

12) Удалите запущенный контейнер "custom-nginx-t2", не останавливая его.(воспользуйтесь --help или google)


В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.




**Решение 3**

Подключаемся к контейнеру через docker attach

![alt text](https://github.com/mezhibo/docker-compose/blob/446cc59cc88a6cbd0fcc7089b66e9db99cee9d24/IMG/12.jpg)

Ввидим вывод потока. нажимаем ctrl+c и у нас завершается работа контейнера, т.к ctrl+c это стандарный сигнал заврешения процесса, чтобы контейнер работал в фоне, нужно установить ключи -d, -itБ и тогда мы просто отклбчимся от него а не заврешим.

![alt text](https://github.com/mezhibo/docker-compose/blob/446cc59cc88a6cbd0fcc7089b66e9db99cee9d24/IMG/13.jpg)


Перезапускаем контейнгер уже с ключом -it, через exec проваливаемся в него и выполняем сначал обновление компоеннтов из репозиториев, а далее ставим редактор nano для комофртного редактирования конфига nginx

![alt text](https://github.com/mezhibo/docker-compose/blob/8733e3440851a56556977b16485a8b39a97e2d72/IMG/14.jpg)


Изменяем внутри конфига прослушиваемый порт с 80 на 81 

![alt text](https://github.com/mezhibo/docker-compose/blob/8733e3440851a56556977b16485a8b39a97e2d72/IMG/15.jpg)


Теперь перезапускаем nginx для применения конфигурации и дергаем curlom старый порт и новый порт 

![alt text](https://github.com/mezhibo/docker-compose/blob/8733e3440851a56556977b16485a8b39a97e2d72/IMG/16.jpg)

Видим что с 81 порта мы можем получить ответ на запрос

Теперь выйдем из контейнера и попробуем дернуть по 8080 наш nginx, то получаем ошибку.

![alt text](https://github.com/mezhibo/docker-compose/blob/8733e3440851a56556977b16485a8b39a97e2d72/IMG/17.jpg)

ПОЧЕМУ?

та потому что при запуске мы указывали что 80 порт нашего контейнера прокидывается на 8080 порт машины, а сейчас мы просто поменяли 80 на 81 не перепроросив 81 порт на порт 8080, вот и вся проблема.

Так как контейнерм "мы сломали" ))) он на мбольше не нужен, то мы его удаляем, и не просто так, а без остановки, т.е. на горячуюю, для этого нам нужен будет ключ -f (force)


![alt text](https://github.com/mezhibo/docker-compose/blob/8733e3440851a56556977b16485a8b39a97e2d72/IMG/18.jpg)

и через docker ps -a убеждаемся что контейнер грохнули окончательно


**Задача 4**

- Запустите первый контейнер из образа centos c любым тегом в фоновом режиме, подключив папку текущий рабочий каталог $(pwd) на хостовой машине в /data контейнера, используя ключ -v.

- Запустите второй контейнер из образа debian в фоновом режиме, подключив текущий рабочий каталог $(pwd) в /data контейнера.

- Подключитесь к первому контейнеру с помощью docker exec и создайте текстовый файл любого содержания в /data.

- Добавьте ещё один файл в текущий каталог $(pwd) на хостовой машине.

- Подключитесь во второй контейнер и отобразите листинг и содержание файлов в /data контейнера.

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.



**Решение 4**


Запускаем 2 конетейнера с разными операционаками, и прбрасываем нашу текущуб директорию нашей рабочей ОС внктрь обоих контейнеров в каталог data

![alt text](https://github.com/mezhibo/docker-compose/blob/a89b9a420db5180f96a620a3733aa81caae820d8/IMG/19.jpg)


Теперь через exec провалимся внутрь каждого контейнера и создадим там file1 через контейнер centos, и file2 через debian

В итоге мы можем заметить, что в какой бы контейнер бы не заходили в папку дата, эти оба файла создаются в докальной директории на нашей хостовой машине


![alt text](https://github.com/mezhibo/docker-compose/blob/a89b9a420db5180f96a620a3733aa81caae820d8/IMG/20.jpg)


![alt text](https://github.com/mezhibo/docker-compose/blob/63e6357cf0323cca6dbebdc7b433d3cd34f40b4a/IMG/21.jpg)



**Задача 5**

1) Создайте отдельную директорию(например /tmp/netology/docker/task5) и 2 файла внутри него. "compose.yaml" с содержимым:

'''
version: "3"
services:
  portainer:
    image: portainer/portainer-ce:latest
    network_mode: host
    ports:
      - "9000:9000"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      '''
"docker-compose.yaml" с содержимым:

'''
version: "3"
services:
  registry:
    image: registry:2
    network_mode: host
    ports:
    - "5000:5000"

  '''

И выполните команду "docker compose up -d". Какой из файлов был запущен и почему? (подсказка: https://docs.docker.com/compose/compose-application-model/#the-compose-file )

2) Отредактируйте файл compose.yaml так, чтобы были запущенны оба файла. (подсказка: https://docs.docker.com/compose/compose-file/14-include/)

3) Выполните в консоли вашей хостовой ОС необходимые команды чтобы залить образ custom-nginx как custom-nginx:latest в запущенное вами, локальное registry. Дополнительная документация: https://distribution.github.io/distribution/about/deploying/

4) Откройте страницу "https://127.0.0.1:9000" и произведите начальную настройку portainer.(логин и пароль адмнистратора)

5) Откройте страницу "http://127.0.0.1:9000/#!/home", выберите ваше local окружение. Перейдите на вкладку "stacks" и в "web editor" задеплойте следующий компоуз:

'''

version: '3'

services:
  nginx:
    image: 127.0.0.1:5000/custom-nginx
    ports:
      - "9090:80"
      '''
      
6) Перейдите на страницу "http://127.0.0.1:9000/#!/2/docker/containers", выберите контейнер с nginx и нажмите на кнопку "inspect". В представлении <> Tree разверните поле "Config" и сделайте скриншот от поля "AppArmorProfile" до "Driver".

7) Удалите любой из манифестов компоуза(например compose.yaml). Выполните команду "docker compose up -d". Прочитайте warning, объясните суть предупреждения и выполните предложенное действие. Погасите compose-проект ОДНОЙ(обязательно!!) командой.

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод, файл compose.yaml , скриншот portainer c задеплоенным компоузом.




**Решение 5**


Если запущен контейнер portainer, это означает, что был использован файл compose.yaml. Если запущен контейнер registry, это означает, что был использован файл docker-compose.yaml.

На практике, поведение Docker Compose может зависеть от версии и конфигурации.


![alt text](https://github.com/mezhibo/docker-compose/blob/129c6dd5e02cdcec1ada44340d0cac3b8dbc3e5e/IMG/22.jpg)


Теперь отредактирую файлик compose.yaml

![alt text](https://github.com/mezhibo/docker-compose/blob/8e601deb1d5947a53fbc624eea082ebfe9c12274/IMG/23.jpg)


И проверим что завелись оба контейнера 

![alt text](https://github.com/mezhibo/docker-compose/blob/8e601deb1d5947a53fbc624eea082ebfe9c12274/IMG/24.jpg)


Плмечаем на ранее созданный кастамный образ и пушим его 

![alt text](https://github.com/mezhibo/docker-compose/blob/facebded0b02effc6e4b99a74beef216f013508c/IMG/25.jpg)


сейчас проверим что у на сработает локальный репозиторий

Дропнем localhost:5000/custom-nginx

Подтянем его с локлаьной репы

Проверим есть ли localhost:5000/custom-nginx в нашем списке


![alt text](https://github.com/mezhibo/docker-compose/blob/dae958a68aa78a00dcf0f9adbf48cfe4f511aab5/IMG/26.jpg)



Теперь зайдем на веб-интерфер Portnainer


![alt text](https://github.com/mezhibo/docker-compose/blob/8678bb4c53ada68eceeb39518d22e41f38f318d1/IMG/27.jpg)


Запустим compose-nginx через веб интерфейс

![alt text](https://github.com/mezhibo/docker-compose/blob/8678bb4c53ada68eceeb39518d22e41f38f318d1/IMG/28.jpg)


Зайдем в консоль машины и увидем что контейнер запустился 

![alt text](https://github.com/mezhibo/docker-compose/blob/8678bb4c53ada68eceeb39518d22e41f38f318d1/IMG/29.jpg)


Далее по заданию делаем снимок контейнера в portainer от от поля AppArmorProfile до Driver


![alt text](https://github.com/mezhibo/docker-compose/blob/8678bb4c53ada68eceeb39518d22e41f38f318d1/IMG/30.jpg)


Теперь удалим compose.yaml и попробуем прогнать docker compose up -d. И сразу видим предупреждение что найдены потерянные контейнеры для этого проекта.
Описание контейнера Portainer было в удалённом файле compose.yaml, можно запустить команду с флагом --remove- orphans, чтобы очистить ее.

![alt text](https://github.com/mezhibo/docker-compose/blob/8678bb4c53ada68eceeb39518d22e41f38f318d1/IMG/31.jpg)


И теперь останавливаем все контейнеры одной командой

![alt text](https://github.com/mezhibo/docker-compose/blob/8109ef210570ab9e86d23feb637b33bf8da4b32d/IMG/32.jpg)


