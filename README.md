# docker
Environment 

# hub
https://hub.docker.com/r/codexteam/ifmo.su/

# Временная инструкция

1. git clone https://github.com/codex-team/docker

2. cd docker

3. git clone https://github.com/codex-team/codex www

4. docker-compose build

5. docker-compose up

6. (в отдельной консоли, не закрывая предыдущую):
  > docker_db_1 - это имя контейнера с php. Он может называться по-другому. Узнать командой docker ps
  > docker exec -i docker_db_1 mysql -uroot -proot < configs/codex-db.sql
  
7. echo "127.0.0.1   codex.dev" » /etc/hosts

8. cp configs/database.php www/application/config/database.php

9. mkdir www/application/cache

10. mkdir www/application/logs

11. chmod 777 www/application/logs/ www/application/cache/

12. cp configs/oauth.php  www/application/config/oauth.php

> Сайт: http://codex.dev:8081/

> Админка БД: http://codex.dev:8082/ (server - db, username - root, password - root)
