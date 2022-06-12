# Einleitung allgemein<!-- omit in toc -->
Einleitung allgemein (Erklärungen zum ganzen M300-Projekt)

# Inhaltsverszeichnis<!-- omit in toc -->
- [Vagrant](#vagrant)
  - [Vagrant cheat sheet](#vagrant-cheat-sheet)
    - [Erstellen einer VM](#erstellen-einer-vm)
    - [Starten einer VM](#starten-einer-vm)
    - [Einsteigen in eine VM](#einsteigen-in-eine-vm)
    - [Anhalten einer VM](#anhalten-einer-vm)
    - [Aufräumen einer VM](#aufräumen-einer-vm)
    - [Boxen](#boxen)
    - [Speichern von Fortschritt](#speichern-von-fortschritt)
    - [Tipps](#tipps)
  - [Vagrant Apache2](#vagrant-apache2)
  - [Vagrant Ngnix](#vagrant-ngnix)
- [Docker](#docker)
  - [Docker cheat sheet](#docker-cheat-sheet)
- [Docker Container MariaDB](#docker-container-mariadb)
  - [Image herunterladen](#image-herunterladen)
  - [Container erstellen](#container-erstellen)
  - [Ausführen und Anhalten des Containers](#ausführen-und-anhalten-des-containers)
- [30-Container](#30-container)
- [35-Sicherheit 2](#35-sicherheit-2)
- [40-Container-Orchestrierung](#40-container-orchestrierung)
- [50-Add-ons](#50-add-ons)
- [60-Reflexion](#60-reflexion)

## Vagrant

Kurz gesagt ist Vagrant ein Werkzeug für die Arbeit mit virtuellen Umgebungen, und in den meisten Fällen bedeutet dies die Arbeit mit virtuellen Maschinen. Vagrant bietet einen einfachen und leicht zu bedienenden Kommandozeilen-Client für die Verwaltung dieser Umgebungen und einen Interpreter für die textbasierten Definitionen, wie jede Umgebung aussieht, genannt Vagrantfiles. Vagrant ist quelloffen, d.h. jeder kann es herunterladen, modifizieren und frei weitergeben.

### Vagrant cheat sheet
Die Eingabe von "vagrant" in der Befehlszeile zeigt eine Liste aller verfügbaren Befehle an.

Stellen Sie sicher, dass Sie sich im gleichen Verzeichnis wie die Vagrant-Datei befinden, wenn Sie diese Befehle ausführen!

#### Erstellen einer VM
- `vagrant init` -- Initialisiert Vagrant mit einer Vagrantdatei und dem Verzeichnis ./.vagrant, wobei kein Basis-Image angegeben wird. Bevor Sie vagrant up ausführen können, müssen Sie ein Basis-Image in der Vagrant-Datei angeben.
- vagrant init <boxpath>` -- Initialisiert Vagrant mit einer bestimmten Box. Um eine Box zu finden, gehen Sie zum [public Vagrant box catalog] (https://app.vagrantup.com/boxes/search). Wenn Sie eine finden, die Ihnen gefällt, ersetzen Sie einfach den Namen durch boxpath. Zum Beispiel: "Vagrant init ubuntu/trusty64".

#### Starten einer VM
- `$ vagrant up` -- startet die Vagrant-Umgebung (wird auch nur beim ERSTEN Vagrant up bereitgestellt)
- `$ vagrant resume` -- nimmt eine angehaltene Maschine wieder auf (vagrant up funktioniert auch hier problemlos)
- `$ vagrant provision` -- erzwingt die erneute Bereitstellung der Vagrant-Maschine
- `$ vagrant reload` -- startet die Vagrant-Maschine neu und lädt eine neue Vagrantfile-Konfiguration
- `$ vagrant reload --provision` -- startet die virtuelle Maschine neu und erzwingt die Provisionierung

#### Einsteigen in eine VM
- `$ vagrant ssh` -- verbindet sich mit der Maschine über SSH
- `$ vagrant ssh <boxname>` -- Wenn Sie Ihrer Box einen Namen in Ihrem Vagrantfile geben, können Sie sich per SSH mit boxname einloggen. Funktioniert von jedem Verzeichnis aus.

#### Anhalten einer VM
- `$ vagrant halt` -- hält die Vagrant-Maschine an
- `$ vagrant suspend` -- setzt eine virtuelle Maschine aus (merkt sich den Zustand)

#### Aufräumen einer VM
- `$ vagrant destroy` -- stoppt und löscht alle Spuren der Vagrant-Maschine
- `$ vagrant destroy -f` -- wie oben, ohne Bestätigung

#### Boxen
- `$ vagrant box list` -- zeigt eine Liste aller installierten Boxen auf Ihrem Computer an
- `$ vagrant box add <Name> <url>` -- lädt ein Box-Image auf Ihren Computer herunter
- `$ vagrant box outdated` -- prüft auf Aktualisierungen vagrant box update
- `$ vagrant box remove <Name>` -- löscht eine Box vom Rechner
- `$ vagrant package` -- verpackt eine laufende virtualbox env in eine wiederverwendbare Box

#### Speichern von Fortschritt
-`$ vagrant snapshot save [options] [vm-name] <name>` -- vm-name ist oft `default`. Erlaubt uns zu speichern, so dass wir zu einem späteren Zeitpunkt ein Rollback durchführen können.

#### Tipps
- `$ vagrant -v` -- liefert die Vagrant-Version
- `$ vagrant status` -- gibt den Status der Vagrant-Maschine aus
- `$ vagrant global-status` -- gibt den Status aller Vagrant-Maschinen aus
- `$ vagrant global-status --prune` -- wie oben, aber ungültige Einträge werden entfernt
- `$ vagrant provision --debug` -- verwendet das Debug-Flag, um die Ausführlichkeit der Ausgabe zu erhöhen
- vagrant push` -- ja, vagrant kann so konfiguriert werden, dass es [Code verteilt](http://docs.vagrantup.com/v2/push/index.html)!
- `$ vagrant up --provision | tee provision.log` -- Führt `$ vagrant up` aus, erzwingt die Bereitstellung und protokolliert alle Ausgaben in einer Datei


### Vagrant Apache2
(Noch nicht fertig)

### Vagrant Ngnix
![Netzwerkplan](img/ngnix.jpg)
Wir mussten auf der TBZ-VM, welcher uns zu geteilt wurde, ein Vagrant Container mit einem Webservice bzw. ngnix installieren. Dabei mussten wir die Daten für die Webseite ausserhalb vom Container speichern, damit man die Daten nicht verliert, wenn man den Container löschen `$ vagrant destroy`  und wieder aufsetzen `$ vagrant up`. Dabei hat mein zwei wichtige Dateien. Das erste wäre das Vagrant-File welches für die Installation veranwortlich ist. In diesem File ist beschrieben, welches Image es installieren soll und ein Pfad zum Provisioning-File. Das Provisioning-File ist die andere Datei. Das File ist für die Konfiguration des Container verantwortlich bzw. es ist ein Shellskript.

## Docker
Docker ist eine Freie Software zur Isolierung von Anwendungen mit Hilfe von Containervirtualisierung. Docker vereinfacht die Bereitstellung von Anwendungen, weil sich Container, die alle nötigen Pakete enthalten, leicht als Dateien transportieren und installieren lassen. 
### Docker cheat sheet
![Docker cheat sheet](img/dockercheatsheet.png)

## Docker Container MariaDB
### Image herunterladen
Sie können ein MariaDB-Image für Docker aus dem offiziellen Docker MariaDB herunterladen oder ein anderes Image auswählen, das Ihren Anforderungen besser entspricht. Sie können Docker Hub (den offiziellen Satz von Repositorys) mit diesem Befehl nach einem Image durchsuchen: <br />
`$ docker search mariadb`
<br />
Wenn Sie ein Image gefunden haben, das Sie verwenden möchten, können Sie es über Docker herunterladen. Einige Schichten einschließlich der erforderlichen Abhängigkeiten werden ebenfalls heruntergeladen. Beachten Sie, dass Docker eine einmal heruntergeladene Schicht für ein bestimmtes Image nicht erneut für ein anderes Image herunterladen muss.<br />
Wenn Sie zum Beispiel das Standard-MariaDB-Image installieren möchten, können Sie Folgendes eingeben:<br />
`$ docker pull mariadb:10.4`

Damit wird die Version 10.4 installiert. Die Versionen 10.2, 10.3 und 10.5 sind ebenfalls eine gute Wahl.

Es wird eine Liste der erforderlichen Schichten angezeigt. Für jede Schicht gibt Docker an, ob sie bereits vorhanden ist oder wie weit der Download fortgeschritten ist.

Um eine Liste der installierten Images zu erhalten:<br />
`$ docker images`

### Container erstellen

Ein Image ist kein laufender Prozess, sondern nur die Software, die gestartet werden soll. Um es auszuführen, müssen wir zuerst einen Container erstellen. Der für die Erstellung eines Containers erforderliche Befehl ist in der Regel in der Dokumentation des Images zu finden. Zum Beispiel, um einen Container für das offizielle MariaDB-Image zu erstellen:

`$ docker run --name mariadbtest -e MYSQL_ROOT_PASSWORD=mypass -p 3306:3306 -d docker.io/library/mariadb:10.3`

"mariadbtest" ist der Name, den wir dem Container geben wollen. Wenn wir keinen Namen angeben, wird automatisch eine ID generiert.

### Ausführen und Anhalten des Containers
Mit Docker können wir einen Container mit einem einzigen Befehl neu starten:<br />
`$ docker restart mariadbtest`

Der Container kann auch auf diese Weise angehalten werden:
`$ docker stop mariadbtest`

Der Container wird durch diesen Befehl nicht zerstört. Die Daten befinden sich weiterhin im Container, auch wenn MariaDB nicht läuft. Um den Container neu zu starten und unsere Daten zu sehen, können wir den Befehl:
`$ docker start mariadbtest`

Mit docker stop wird der Container ordnungsgemäß beendet: ein SIGTERM-Signal wird an den mysqld-Prozess gesendet, und Docker wartet, bis der Prozess heruntergefahren ist, bevor es die Kontrolle an die Shell zurückgibt. Es ist jedoch auch möglich, einen Timeout zu setzen, nach dem der Prozess sofort mit einem SIGKILL beendet wird. Es ist auch möglich, den Prozess sofort und ohne Zeitüberschreitung zu beenden.

`$ docker stop --time=30 mariadbtest` <br/>
`$ docker kill mariadbtest`

Wenn wir einen Container zerstören wollen, etwa weil das Bild nicht unseren Anforderungen entspricht, können wir ihn anhalten und dann ausführen:

`$ docker rm mariadbtest`

Beachten Sie, dass der obige Befehl das Datenvolumen, das Docker für /var/lib/mysql erstellt hat, nicht zerstört. Wenn Sie das Datenträger ebenfalls zerstören möchten, verwenden Sie:

`docker rm -v mariadbtest`

## 30-Container
Einträge (eigene Erkenntnisse während dem Bearbeiten dieses Kapitels)

## 35-Sicherheit 2
Einträge (eigene Erkenntnisse während dem Bearbeiten dieses Kapitels)

## 40-Container-Orchestrierung
Einträge (eigene Erkenntnisse während dem Bearbeiten dieses Kapitels)

## 50-Add-ons 
Einträge (eigene Erkenntnisse während dem Bearbeiten dieses Kapitels)

## 60-Reflexion
Lernprozess festgehalten (Form frei wählbar)


- - -
<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/ch/"><img alt="Creative Commons Lizenzvertrag" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/3.0/ch/88x31.png" /></a><br />Dieses Werk ist lizenziert unter einer <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/ch/">Creative Commons Namensnennung - Nicht-kommerziell - Weitergabe unter gleichen Bedingungen 3.0 Schweiz Lizenz</a>

- - -
