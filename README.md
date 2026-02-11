# M300 – Modul Dokumentation  
## Toolumgebung & Cloud Grundlagen

**Modul:** M300  
**Thema:** Toolumgebung, Virtualisierung & Cloud Computing  
**Autor:** Dein Name  
**Datum:** TT.MM.JJJJ  

---

# Inhaltsverzeichnis

1. [GitHub Account](#01-github-account)  
2. [Git Client (Git Bash)](#02-git-client-git-bash)  
3. [VirtualBox](#03-virtualbox)  
4. [Vagrant](#04-vagrant)  
5. [Apache Webserver](#05-apache-webserver)  
6. [Visual Studio Code](#06-visual-studio-code)  
7. [Fazit](#07-fazit)  
8. [Fragen & Antworten](#m300--fragen--antworten)  

---

# 01 GitHub Account

## **Ziel**
GitHub wird als zentrales Repository für Code und Dokumentation verwendet.

## **Vorgehen**
- GitHub-Account erstellt  
- Repository **M300** erstellt (public, mit README)  
- SSH-Key lokal erstellt  
  ```bash
  ssh-keygen
  ```
- Public Key (`id_rsa.pub`) im GitHub-Account hinterlegt  

## **Aufgetretene Probleme**
Beim Klonen wurde zuerst der Windows-Benutzername statt des GitHub-Usernames verwendet.  
→ **Lösung:** Repository-URL prüfen  
```
github.com/<username>/<repo>
```

---

# 02 Git Client (Git Bash)

## **Ziel**
Git Bash wird genutzt, um Git- und SSH-Befehle unter Windows auszuführen.

## **Vorgehen**
- Git Bash installiert  
- Git global konfiguriert  
  ```bash
  git config --global user.name "Dein Name"
  git config --global user.email "deine@email.ch"
  ```
- Repository per SSH geklont  
  ```bash
  git clone git@github.com:<username>/<repo>.git
  ```
- Änderungen hochgeladen  
  ```bash
  git add .
  git commit -m "Kommentar"
  git push
  ```

## **Aufgetretene Probleme**
Leere Ordner wurden auf GitHub nicht angezeigt.  
→ **Lösung:** `.gitkeep` Datei im Ordner erstellt.

---

# 03 VirtualBox

## **Ziel**
VirtualBox dient als Virtualisierungsplattform für Vagrant.

## **Vorgehen**
- VirtualBox installiert  
- Keine manuelle VM-Erstellung durchgeführt  
- Nutzung ausschliesslich als Provider für Vagrant  

---

# 04 Vagrant

## **Ziel**
Vagrant ermöglicht das schnelle und reproduzierbare Erstellen einer Ubuntu-VM.

## **Vorgehen**
- Vagrant installiert  
- Projekt initialisiert  
  ```bash
  vagrant init ubuntu/xenial64
  vagrant up
  ```
- Verbindung zur VM  
  ```bash
  vagrant ssh
  ```
- Apache innerhalb der VM installiert  
- Portweiterleitung im `Vagrantfile` konfiguriert  

```ruby
config.vm.network "forwarded_port", guest: 80, host: 8080
```

- VM neu geladen  
  ```bash
  vagrant reload
  ```

## **Wichtige Vagrant-Befehle**
```bash
vagrant up
vagrant halt
vagrant reload
vagrant destroy
vagrant status
vagrant ssh
```

## **Aufgetretene Probleme**

**Problem 1:** Port 80 nicht erreichbar  
→ Ursache: Port-Forwarding fehlte oder VM nicht neu geladen  
→ Lösung: Port-Weiterleitung ergänzen + `vagrant reload`

**Problem 2:** Vagrant-Befehle innerhalb der VM ausgeführt  
→ Lösung:  
- Vagrant-Befehle nur im Host-Terminal  
- Linux-Befehle nur innerhalb der VM (`vagrant ssh`)

---

# 05 Apache Webserver

## **Ziel**
Bereitstellung eines Webservers innerhalb der Vagrant-VM.

## **Vorgehen**

Apache installiert:
```bash
sudo apt update
sudo apt install apache2
```

Status geprüft:
```bash
systemctl status apache2
```

Intern getestet:
```bash
curl http://localhost
```

Extern erreichbar über:
```
http://localhost:8080
```

HTML-Datei bearbeitet:
```
/var/www/html/index.html
```

## **Ergebnis**
- Eigene HTML-Seite wird korrekt angezeigt  
- Apache läuft stabil innerhalb der Vagrant-VM  

---

# 06 Visual Studio Code

## **Ziel**
VS Code wird als Editor für Code und Dokumentation verwendet.

## **Vorgehen**
- Visual Studio Code installiert  
- Repository lokal geöffnet  
- Markdown-Dateien bearbeitet  
- Änderungen mit Git gepusht  

---

# 07 Fazit

Die gesamte Toolumgebung funktioniert vollständig:

- GitHub → Versionierung  
- Git Bash → Git & SSH  
- VirtualBox + Vagrant → Virtualisierung  
- Apache → Webserver  
- VS Code → Entwicklungsumgebung  

Durch Vagrant konnte die VM schnell, reproduzierbar und effizient bereitgestellt werden.

---

# M300 – Fragen & Antworten

## Cloud Computing

### **Was versteht man unter Cloud Computing?**
Cloud Computing bezeichnet die Nutzung von IT-Ressourcen wie Software, Speicherplatz und Rechenleistung über ein Netzwerk (z. B. das Internet), ohne dass diese lokal installiert sein müssen.

---

### **Was versteht man unter Infrastructure as a Service (IaaS)?**
Infrastructure as a Service (IaaS) stellt grundlegende IT-Infrastruktur wie virtuelle Maschinen, Speicher und Netzwerke zur Verfügung. Der Benutzer ist selbst für das Betriebssystem und die installierte Software verantwortlich.

---

## Infrastructure as Code

### **Was ist der Unterschied zur manuellen Installation einer VM?**
Infrastructure as Code ermöglicht eine automatisierte, reproduzierbare und dokumentierte Erstellung von virtuellen Maschinen. Im Gegensatz dazu erfolgt die manuelle Installation meist über eine grafische Benutzeroberfläche.

---

## Vagrant

### **Was wird mit Vagrant erzeugt?**
Mit Vagrant werden virtuelle Maschinen erstellt, konfiguriert und verwaltet.

---

### **Welche Aussagen treffen zu?**
**b)** Vagrant erzeugt virtuelle Maschinen und unterstützt verschiedene Hypervisoren sowie Cloud-Umgebungen.

---

### **In welchen Bereich des Cloud Computings ist Vagrant einzuordnen?**
Vagrant ist dem Bereich **Infrastructure as a Service (IaaS)** zuzuordnen.

---

### **Welche Alternativen zu Vagrant gibt es?**
- Terraform  
- Docker  
- Packer  
- Direkte Konfiguration mit VirtualBox  

---

### **Wo speichert Vagrant seine Konfiguration?**
Die Konfiguration wird im **Vagrantfile** gespeichert.

---

### **Was bedeutet die Fehlermeldung  
„A Vagrant environment or target machine is required to run this command.“?**
Diese Fehlermeldung tritt auf, wenn ein Vagrant-Befehl in einem Verzeichnis ohne `Vagrantfile` ausgeführt wird.

---

### **Bei welcher LPI-Zertifizierung ist Vagrant-Wissen hilfreich?**
Vagrant-Kenntnisse sind besonders hilfreich für die Zertifizierung **LPI DevOps Tools Engineer**.
