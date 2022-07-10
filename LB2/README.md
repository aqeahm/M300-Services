# Einleitung <!-- omit in toc -->
Einleitung zum LB2 Projekt (Erklärungen)


# Inhaltsverszeichnis <!-- omit in toc -->
- [Service-Aufbau](#service-aufbau)
- [Umsetzung](#umsetzung)
  - [Erstellung der Container](#erstellung-der-container)
    - [MySql Server Container erstellen](#mysql-server-container-erstellen)
    - [Wordpress Container erstellen](#wordpress-container-erstellen)
    - [Beenden der Installation in einem Browser](#beenden-der-installation-in-einem-browser)
  - [Images](#images)
    - [Docker HUB](#docker-hub)
      - [Account erstellen](#account-erstellen)
      - [`Docker login`](#docker-login)
    - [Repositories erstellen](#repositories-erstellen)
    - [Images erstellen](#images-erstellen)
    - [Images auf Repo pushen](#images-auf-repo-pushen)
- [Testing](#testing)
- [Troubleshooting](#troubleshooting)
- [Fazit](#fazit)
  - [Aqeb Ahmed:](#aqeb-ahmed)
  - [Abi Kani:](#abi-kani)
- [Quellen](#quellen)

## Service-Aufbau 
Eine schnelle Wordpress VM 
Für schnelle kurze Seiten


## Umsetzung


### Erstellung der Container
Eine erfolgreiche WordPress-Installation besteht aus drei Elementen:

- WordPress-Software
- MySQL- oder MariaDB-Datenbank (Wir werden in diesem Beispiel MySQL verwenden)
- Abschließende Installationsschritte im Browser    durchgeführt

Für die folgenden Beispiele werden die WordPress- und MySQL-Komponenten in separaten verknüpften Containern ausgeführt. Der Container, auf dem die WordPress-Software ausgeführt wird, wird einem Port auf dem Host zugeordnet, sodass Sie in Ihrem Browser darauf zugreifen können.

#### MySql Server Container erstellen
Führen Sie zunächst einen Container namens my-db mit dem Root-Passwort mysql-password aus. 

Starten Sie einen Container mit dem Befehl:

 `$ sudo docker run --name my-db -e MYSQL_ROOT_PASSWORD=db-password -d mysql`

#### Wordpress Container erstellen
Führen Sie als Nächstes einen Container aus dem offiziellen WordPress-Image aus, der dem Host-Port 8080 zugeordnet und mit dem Datenbankcontainer verknüpft ist.

Zwei Vorbehalte:

- Wenn Sie eine Firewall haben, müssen Sie möglicherweise den Zugriff auf Port 8080 hinzufügen.
- Wenn Sie bereits einen anderen Dienst auf Port 8080 ausführen, können Sie einen anderen Port auf dem Host auswählen.

Der Befehl unterscheidet sich geringfügig, je nachdem, ob Sie MySQL:

Starten Sie den WordPress-Container mit dem folgenden Befehl:

`sudo docker run --name my-wordpress -p 8080:80 --link my-db:mysql -d wordpress`

#### Beenden der Installation in einem Browser
bild


### Images
erklärung
#### Docker HUB
beschreibung
##### Account erstellen
bild
##### `Docker login`
bild 
#### Repositories erstellen
bild


#### Images erstellen
sudo docker commit -m "Added MySQL Login data and Website installation skip" -a "Abi and Aqeb" my-wordpress aqeahm/wordpress:1.0
#### Images auf Repo pushen
sieht man in repo


## Testing
| Beschreibung  | SOLL | IST | Beweis |
|---|---|---|---|
| --- | --- | --- | <img src="./images/testing1.png"/> |

## Troubleshooting
https://stackoverflow.com/questions/50151833/cannot-login-to-docker-account



## Fazit 
### Aqeb Ahmed:
gbswdgoh

### Abi Kani:
ouagudgio


## Quellen
1. https://www.ionos.de/digitalguide/server/knowhow/wordpress-in-docker-containern/
2. https://itler.net/mysql-befehle-uebersicht-die-wichtigsten-datenbank-kommandos-ueber-die-konsole/
3. https://www.ionos.de/digitalguide/server/knowhow/einrichten-eines-docker-repository/
4. https://docs.docker.com/engine/reference/commandline/login/
5. https://www.ionos.de/digitalguide/server/knowhow/docker-images-erstellen/


