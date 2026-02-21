# Git-Konfiguration

## .gitignore

`.gitignore` legt fest, welche Dateien Git nicht verfolgen soll — zum Beispiel kompilierte Klassen, IDE-Einstellungen oder temporäre Dateien.

```gitignore
##############################
## Java
##############################
.mtj.tmp/
*.class
*.jar
*.war
*.ear
*.nar
hs_err_pid*
replay_pid*

##############################
## Maven
##############################
target/
pom.xml.tag
pom.xml.releaseBackup
pom.xml.versionsBackup
pom.xml.next
pom.xml.bak
release.properties
dependency-reduced-pom.xml
buildNumber.properties
.mvn/timing.properties
.mvn/wrapper/maven-wrapper.jar

##############################
## Gradle
##############################
bin/
build/
.gradle
.gradletasknamecache
gradle-app.setting
!gradle-wrapper.jar

##############################
## IntelliJ
##############################
out/
.idea/
.idea_modules/
*.iml
*.ipr
*.iws

##############################
## Eclipse
##############################
.settings/
bin/
tmp/
.metadata
.classpath
.project
*.tmp
*.bak
*.swp
*~.nib
local.properties
.loadpath
.factorypath

##############################
## NetBeans
##############################
nbproject/private/
build/
nbbuild/
dist/
nbdist/
nbactions.xml
nb-configuration.xml

##############################
## Visual Studio Code
##############################
.vscode/
.code-workspace

##############################
## OS X
##############################
.DS_Store

##############################
## Miscellaneous
##############################
*.log
```

## .gitattributes

`.gitattributes` steuert, wie Git mit Dateien umgeht — vor allem Zeilenenden. Windows verwendet CRLF (`\r\n`), Linux und Git verwenden LF (`\n`). Ohne Konfiguration kann es zu Konflikten kommen, wenn Entwickler auf verschiedenen Betriebssystemen arbeiten.

`* text=auto` weist Git an, Zeilenenden automatisch zu normalisieren: Im Repository werden LF gespeichert, beim Auschecken auf Windows wird auf CRLF umgewandelt.

```gitattributes
# Automatische Normalisierung
* text=auto
.gitignore text eol=lf
.gitattributes text eol=lf
.devcontainer/devcontainer.json text eol=lf

# Java sources
*.java          text diff=java
*.kt            text diff=kotlin
*.groovy        text diff=java
*.scala         text diff=java
*.gradle        text diff=java
*.gradle.kts    text diff=kotlin

# Text-Dateien normalisieren (CRLF => LF)
*.css           text diff=css
*.scss          text diff=css
*.sass          text
*.df            text
*.htm           text diff=html
*.html          text diff=html
*.js            text
*.mjs           text
*.cjs           text
*.jsp           text
*.jspf          text
*.jspx          text
*.properties    text
*.tld           text
*.tag           text
*.tagx          text
*.xml           text

# Binärdateien — nicht anfassen
*.class         binary
*.dll           binary
*.ear           binary
*.jar           binary
*.so            binary
*.war           binary
*.jks           binary

# Build-Tool-Wrapper
mvnw            text eol=lf
gradlew         text eol=lf

# Windows-Dateien bleiben CRLF
*.bat           text eol=crlf
```
