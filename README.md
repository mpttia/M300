$$
**M300 Modul Doku**
$$

** 01 GitHub Account**

**Ziel**

GitHub wird als zentrales Repository für Code und Dokumentation verwendet.

**Vorgehen**

GitHub-Account erstellt
Repository M300 erstellt (public, mit README)
SSH-Key lokal erstellt (ssh-keygen)
Public Key (id_rsa.pub) im GitHub-Account hinterlegt

**Aufgetretene Probleme**

Beim Klonen wurde zuerst der Windows-Benutzername statt des GitHub-Usernames verwendet
→ Lösung: Repository-URL prüfen (github.com/<username>/<repo>)



** 02 Git Client (Git Bash)**

**Ziel**

Git Bash wird genutzt, um Git- und SSH-Befehle unter Windows auszuführen.

**Vorgehen**

Git Bash installiert
Git global konfiguriert (user.name, user.email)
Repository per SSH geklont
Änderungen mit git add, git commit, git push hochgeladen

**Aufgetretene Probleme**

Leere Ordner wurden auf GitHub nicht angezeigt
→ Lösung: .gitkeep Datei in Ordnern erstellt


**03 VirtualBox**

**Ziel**

VirtualBox dient als Virtualisierungsplattform für Vagrant.

**Vorgehen**

VirtualBox installiert
Keine manuelle VM-Erstellung durchgeführt
VirtualBox wird ausschliesslich als Provider für Vagrant genutzt



**04 Vagrant**

**Ziel**

Vagrant ermöglicht das schnelle und reproduzierbare Erstellen einer Ubuntu-VM.

**Vorgehen**

Vagrant installiert
VM mit ubuntu/xenial64 erstellt
Apache innerhalb der VM installiert
Portweiterleitung im Vagrantfile konfiguriert (Port 80 → 8080)

**Aufgetretene Probleme**

Port 80 war nicht erreichbar im Browser
→ Ursache: Port-Forwarding fehlte bzw. VM wurde nicht neu geladen
→ Lösung: config.vm.network "forwarded_port", guest: 80, host: 8080
und anschliessend vagrant reload

vagrant Befehle wurden innerhalb der VM ausgeführt
→ Lösung: Vagrant-Befehle nur auf dem Host, Linux-Befehle nur in der VM



**05 Apache Webserver**

**Ziel**

Bereitstellung eines Webservers innerhalb der Vagrant-VM.

**Vorgehen**

Apache mit apt install apache2 installiert
Apache-Status geprüft (systemctl status apache2)
Erreichbarkeit intern mit curl http://localhost getestet
Zugriff extern über http://localhost:8080
index.html unter /var/www/html/ bearbeitet

**Ergebnis**

Eigene HTML-Seite wird korrekt im Browser angezeigt

Apache läuft stabil innerhalb der Vagrant-VM


**06 Visual Studio Code**

**Ziel**

VS Code wird als Editor für Code und Dokumentation verwendet.

**Vorgehen**

Visual Studio Code installiert
Repository lokal geöffnet
Markdown-Dateien bearbeitet
Änderungen über GitHub gepusht

**07 Fazit**

Die Toolumgebung funktioniert vollständig:
GitHub für Versionierung
Git Bash für Git/SSH
VirtualBox + Vagrant für Virtualisierung
Apache als Webserver
VS Code als Entwicklungsumgebung
Durch Vagrant konnte die VM schnell, reproduzierbar und effizient bereitgestellt werden.