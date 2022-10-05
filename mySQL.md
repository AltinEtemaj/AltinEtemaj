# Informationen wie man eine MySQL Datenbank in Docker erstellt und mit phpmyadmin visualisiert. 

**Um ein mySQL Container zuerstellen benötigt man:**

`1. docker pull mysql/mysql-server:latest`
- `:latest` sagt aus das man die letzte Version pullen möchte.

`2. docker run --name=[mysql container_name] -d [image_tag_name]`
- `-d` steht dafür das der Container im hintergrund agiert.

`3. docker logs mysql-container 2>&1 | grep GENERATED`  
- `logs` sagt die Information aus die der Container hat.
- Um das generierte Passwort herauszufinden kann man mit dem befehl ´grep´ das Passwort entnehmen.

`4. docker exec -it [mysql container_name] bash`
- `-it` steht für interactive terminal, damit kann man Commands einsetzen, auch wenn der **Container läuft**.
- `bash` ist das System um mysql befehle auszuführen.

`5. mysql -u root -p`
- `-u` steht für user.
- `-p` steht für password.

6. mysql> (`ALTER USER 'root'@'localhost' IDENTIFIED BY '[newpassword]';`) **Muss in mysql verzeichnis rein geschrieben werden.
- `ALTER USER` lässt veränderungen an mySQL accounts zu 
_________________________________________________________________________________________________________________________________

**Um phpmyadmin einzurichten benutzt man:**

`1. docker pull phpmyadmin`

`2. docker run -d --name phpmyadmin-container --link Mysql-container:db -p 8085:80 phpmyadmin`
- TIPP: (Vor)___:db kommt immer der Container wo mysql drauf ist.
- `-d` steht dafür das der Container im hintergrund agiert.
- `--name` ist die bennung eines etwas
- `--link` benutzt man um den phpmyadmin Container mit den mySQL Container zusammen zuverbinden
_________________________________________________________________________________________________________________________________
**Um Access bei mysql/phpmyadmin zu haben benutzt man:**

`1. docker exec -it [mysql container_name] mysql -u root -p`

`2. update mysql.user set host='%' where user='root' and host = 'localhost';`
- `host='%'` sagt aus das jeder beliebige Host sich anmelden kann.

`3. flush privileges;`
- Aktualisiert(Spült) die Privilegien des Users.
