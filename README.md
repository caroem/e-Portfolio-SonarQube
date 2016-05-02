# e-Portfolio-SonarQube

##Installation SonarQube unter Verwendung des DHBW-Servers

- Erstellung eines neuen Accounts auf http://193.196.7.25/users/new
- 
- Aktuelle Version von SonarQube unter http://www.sonarqube.org/downloads/ downloaden und entpacken
- SonarQube Server starten 

&nbsp;
  Unter Windows: C:\sonarqube\bin\windows-x86-xx\StartSonar.bat ausführen 
  
  &nbsp;
  Unter UNIX: '/etc/sonarqube/bin/[OS]/sonar.sh console' im Terminal ausführen

- SonarQube Scanner unter http://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner downloaden und entpacken
- In das /conf Verzeichnis des entpackten SonarQube Scanners gehen
- sonar-scanner.properties öffnen und folgende Zeile hinzufügen: `sonar.host.url=http://193.196.7.25/` 

&nbsp;
  Innerhalb der DH: `sonar.host.url=http://193.196.7.25/users/new`

- sonar-scanner/bin zum PATH hinzufügen 

&nbsp;
  Unter UNIX: `gedit ~/.bashrc` ausführen und `export PfadZumSonarScanner/bin` einfügen
  
## Konfiguration eines Java-Projekts
Wird kein build-Tool (Maven, Gradle...) verwendet, muss im root Verzeichnis des Projekts eine Datei namens `sonar-project.properties`
angelegt werden und folgender Inhalt reinkopiert werden:


``` 
sonar.projectKey=my:project
# this is the name displayed in the SonarQube UI
sonar.projectName=myProjectName
sonar.projectVersion=myProjectVersion

# Path is relative to the sonar-project.properties file. Replace "\" by "/" on Windows.
# Since SonarQube 4.2, this property is optional if sonar.modules is set.
# If not set, SonarQube starts looking for source code from the directory containing
# the sonar-project.properties file.
sonar.sources=.

#sonar.sourceEncoding=UTF-8
``` 
Hier müssen noch die Variablen sonar.projectKey, sonar.projectName, sonar.projectVersion angepasst werden.

Um die Code-Analyse zu starten muss `sonar-runner` innerhalb des Projekts im Terminal ausgeführt werden. Danach kann das Projekt unter der Adresse http://193.196.7.25/ eingesehen werden.

## Konfiguration eines Java Projekts mit Gradle
- In `build.gradle` folgendes einfügen
```
apply plugin: 'sonar-runner'

sonarRunner {
    sonarProperties {
        property "sonar.host.url", "http://193.196.7.25/"
        property "sonar.projectName", "xxxxx"
        property "sonar.projectVersions", "1.0.0"
        property "sonar.sources", "xxxx"
        property "sourceEncoding", "UTF-8"
    }
}
```
- sonar.host.url (URL/IP zum SonarQube Server), sonar.projectName, sonar.projectVersions, sonar.sources (Pfad zum main-Verzeichnis) anpassen

Danach muss im Projekt im Terminal `gradle sonarRunner` ausgeführt werden. Die Ergebnisse können unter der URL des SonarQube Servers eingesehen werden.



