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








