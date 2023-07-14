# Docker image manuell starten 

```
1. docker auf tomcat server installieren (schnellste Weg) - Ubuntu 

sudo su -
snap install docker  


2. registry - image runterziehen testen (gitlab) 



# image wird runtergezogen 
# 1. Es wird eine interaktive Shell gestartet -it 
# 2. und es wird das Programm bash (Shell) gestartet 
docker run -it registry.gitlab.com/training.tn11/jochentest1 bash 

-> Mhm, geht nicht, keine Berechtigung 

3. Einloggen in Docker (Versuch 1) 

docker login registry.gitlab.com/training.tn11 -utraining.tn11 -p<Dein Passwort>

-> Mhm, geht nicht, brauchen wir vielleicht ein Token 

4. Access Token anlegen

-> unter Profil -> bearbeiten -> Linkes Menü -> Access Token 
nur registry lesen 


5. Einloggen mit Token an der registry (Token dient als Password) 

docker login registry.gitlab.com/training.tn11 -utraining.tn11 -p<Dein Access Token>

6. Image starten 

docker run -it registry.gitlab.com/training.tn11/jochentest1 bash 

7. ist ssh drin ?
# hinter dem Prompt eingeben
```

```
ssh
cat /etc/os-release 
```
