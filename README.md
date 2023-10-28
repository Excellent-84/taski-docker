## Проект контейнеры и CI/CD для Taski.

### Описание проекта: 

Taski - Приложение для планирования задач.
Задачи можно добавлять, изменять, удалять и переводить из группы "незавершённые" в "завершённые".
Настройка запуска проекта Taski в контейнерах.     
Настройка автоматического тестирования и деплоя этого проекта на удалённый сервер.

### Стек технологий:
<img src="https://img.shields.io/badge/Python-FFFFFF?style=for-the-badge&logo=python&logoColor=3776AB"/><img src="https://img.shields.io/badge/django-FFFFFF?style=for-the-badge&logo=django&logoColor=082E08"/><img src="https://img.shields.io/badge/Django REST Framework-FFFFFF?style=for-the-badge&logo=&logoColor=361508"/><img src="https://img.shields.io/badge/PostgreSQL-FFFFFF?style=for-the-badge&logo=PostgreSQL&logoColor=4169E1"/><img src="https://img.shields.io/badge/Nginx-FFFFFF?style=for-the-badge&logo=Nginx&logoColor=009639"/><img src="https://img.shields.io/badge/gunicorn-FFFFFF?style=for-the-badge&logo=gunicorn&logoColor=499848"/><img src="https://img.shields.io/badge/GitHub Actions-FFFFFF?style=for-the-badge&logo=GitHub Actions&logoColor=2088FF"/><img src="https://img.shields.io/badge/Docker-FFFFFF?style=for-the-badge&logo=Docker&logoColor=2496ED"/>

### Как запустить проект: 

##### Клонировать репозиторий: 
``` 
git clone https://github.com/Excellent-84/taski-docker.git
```
##### Настроить Docker:
``` 
sudo apt update
sudo apt install curl
curl -fSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh
sudo apt-get install docker-compose-plugin
```
##### Создать файл .env и указать переменные по примеру .env.example:
``` 
cd taski-docker
sudo nano .env
```
##### Установить и запустить Nginx:
```
sudo apt install nginx -y
sudo systemctl start nginx
```
##### Настроить и включить firewall:
```
sudo ufw allow 'Nginx Full'
sudo ufw allow OpenSSH
sudo ufw enable
```
##### Открыть файл Nginx и поменять настройки, сохранить и закрыть:
```
sudo nano /etc/nginx/sites-enabled/default
```
```
server {
    listen 80;
    server_name your_domain_name.com;
    
    location / {
        proxy_set_header HOST $host;
        proxy_pass http://127.0.0.1:8000;

    }
}
```
##### Проверить корректность настроек и перезапустить Nginx: 
```
sudo nginx -t
sudo systemctl start nginx
```
##### Загрузить образы из DockerHub:
```
sudo docker compose -f docker-compose.production.yml pull
```
##### Остановить и удалить все контейнеры:
```
sudo docker compose -f docker-compose.production.yml down
```
##### Запустить контейнеры из образов в фоновом режиме: 
```
sudo docker compose -f docker-compose.production.yml up -d
```
##### Выполнить миграции: 
``` 
sudo docker compose -f docker-compose.production.yml exec backend python manage.py migrate 
```
##### Собрать статику:
``` 
sudo docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic
```
##### Создать суперпользователя (указать логин, e-mail, пароль):
``` 
sudo docker compose -f docker-compose.production.yml exec backend python manage.py createsuperuser 
```

#### Автор [Горин Евгений](https://github.com/Excellent-84)
