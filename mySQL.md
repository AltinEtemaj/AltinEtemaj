# Informationen wie man eine MySQL Datenbank in Docker erstellt und mit phpmyadmin visualisiert. 

**Um ein mySQL Container zuerstellen benötigt man:**

`1. docker pull mysql/mysql-server:latest`

`2. docker run --name=[container_name] -d [image_tag_name]`

`3. docker logs mysql-container 2>&1 | grep GENERATED` // Um das generierte Passwort herauszufinden.

4. mysql> (`ALTER USER 'root'@'localhost' IDENTIFIED BY '[newpassword]';`) // Muss in mysql verzeichnis rein geschrieben werden.
_________________________________________________________________________________________________________________________________
**Um phpmyadmin einzurichten benutzt man:**

`1. docker pull phpmyadmin`

`2. docker run --name  -d -e PMA_ARBITRARY=1 -p 8085:80 phpmyadmin` // Hierbei muss der Port ein nicht verwendeter Port sein.
_________________________________________________________________________________________________________________________________
**Um ins bash von mySQL zu kommen benötigt man folgende befehle:**

`1. docker exec -it [container_name] bash`

`2. mysql -u root -p`
_________________________________________________________________________________________________________________________________
**Um mySQL mit phpmyadmin zuverbinden benutzt man:**

`1. docker run -d --name phpmyadmin-container --link Mysql-container:db -p 8085:80 phpmyadmin` // hinter :db kommt immer der Container wo mysql drauf ist.
_________________________________________________________________________________________________________________________________
**Um Access bei mysql/phpmyadmin zu haben benutzt man:**

`1. docker exec -it mysql1 mysql -u root -p`

`2. update mysql.user set host='%' where user='root' and host = 'localhost';`

`3. flush privileges;`
