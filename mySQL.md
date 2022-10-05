# Informationen wie man eine MySQL Datenbank in Docker erstellt und mit phpmyadmin visualisiert. 

**Um ein mySQL Container zuerstellen benötigt man:**

`1. docker pull mysql/mysql-server:latest`
- `:latest` sagt aus das man die letzte Version pullen möchte.

`2. docker run --name=[container_name] -d [image_tag_name]`
- `-d` steht für das image auf dem Container, der im hintergrund agiert.

`3. docker logs mysql-container 2>&1 | grep GENERATED`  
- `logs` sagt die Information aus die der Container hat.
- Um das generierte Passwort herauszufinden kann man mit dem befehl ´grep´ das Passwort entnehmen.

4. mysql> (`ALTER USER 'root'@'localhost' IDENTIFIED BY '[newpassword]';`) Muss in mysql verzeichnis rein geschrieben werden.
- `ALTER USER` lässt veränderungen an mySQL accounts zu 
_________________________________________________________________________________________________________________________________
**Um phpmyadmin einzurichten benutzt man:**

`1. docker pull phpmyadmin`

`2. docker run --name  -d -e PMA_ARBITRARY=1 -p 8085:80 phpmyadmin` // Hierbei muss der Port ein nicht verwendeter Port sein.
- `-d` steht für das image auf dem Container, der im hintergrund agiert.
- `-e` ist sowie execute (Ausführen)?????????
- `-p` sagt den Port aus.
_________________________________________________________________________________________________________________________________
**Um ins bash von mySQL zu kommen benötigt man folgende befehle:**

`1. docker exec -it [container_name] bash`
- `-it` steht für interactive terminal, damit kann man Commands einsetzen, auch wenn der **Container läuft**.
- `bash` ist das System um mysql befehle auszuführen.

`2. mysql -u root -p`
- `-u` steht für user.
- `-p` steht für password.
_________________________________________________________________________________________________________________________________
**Um mySQL mit phpmyadmin zuverbinden benutzt man:**

`1. docker run -d --name phpmyadmin-container --link Mysql-container:db -p 8085:80 phpmyadmin`
- TIPP: (Vor)___:db kommt immer der Container wo mysql drauf ist.
- `-d` steht für das image auf dem Container, der im hintergrund agiert.
- `--name` ist die bennung eines etwas
- `--link` benutzt man um den phpmyadmin Container mit den mySQL Container zusammen zuverbinden

_________________________________________________________________________________________________________________________________
**Um Access bei mysql/phpmyadmin zu haben benutzt man:**

`1. docker exec -it mysql1 mysql -u root -p`

`2. update mysql.user set host='%' where user='root' and host = 'localhost';`
- `host='%'` sagt aus das jeder beliebige sich anmelden kann.

`3. flush privileges;`
- Aktualisiert(Spült) die Privilegien des Users.
