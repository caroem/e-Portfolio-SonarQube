# e-Portfolio-SonarQube

##Installation SonarQube unter Verwendung des DHBW-Server
- Aktuelle Version von SonarQube unter http://www.sonarqube.org/downloads/ downloaden und entpacken
- SonarQube Server starten 

&nbsp;
  Unter Windows: C:\sonarqube\bin\windows-x86-xx\StartSonar.bat ausführen 
  
  &nbsp;
  Unter UNIX: '/etc/sonarqube/bin/[OS]/sonar.sh console' im Terminal ausführen

- SonarQube Scanner unter http://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner downloaden und entpacken
- In das /conf Verzeichnis des entpackten SonarQube Scanners gehen
- sonar-scanner.properties öffnen und folgende Zeile hinzufügen: `sonar.host.url=http://xxxxxxxxx-karlsruhe.de` 

&nbsp;
  Innerhalb der DH: `sonar.host.url=http://xxx.xxx.xxx.xxx/`

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
