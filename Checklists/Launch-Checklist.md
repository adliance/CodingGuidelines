# Launch Checklist
This should provide a simple checklist of all things that should be checked before a project is completed and launched.


## Web Projects
- Cache Busting berücksichtigt
- Application Insights / Logging (Level) richtig konfiguriert
- Korrekte Appsettings
- Keine kritischen Secrets in den Appsettings
- Mail Konfiguration
- Dummy Daten / Code entfernen
- Im Produktivbetrieb keinerlei detaillierte Fehlermeldungen/Stacktraces anzeigen/liefern
- Keine kritischen Daten Loggen
- Wurde an SQL Injection gedacht?
- Wurde an XSS gedacht? An Stellen wo dynamisch HTML Markup generiert wird darauf achten, dass der HTML Code Sanitized wird.
- Wurde CORS richtig konfiguriert? Keine Wildcards! Wenn API und Frontend unter der gleichen Domain und unter gleichem Port erreichbar sind, kann CORS ganz deaktiviert werden.

## CI & CD
- Anwendungen im Release Modus gebaut
- Deployment/Releases eingerichtet
- Devops Branch Policies richtig konfiguriert

## Azure Hosting
- Produktiv Environment richtig konfiguriert? (Environment Variablen)
- Production API Keys anlegen
- Sinnvolle Credentials vergeben
- Azure Konfiguration korrekt
- Backups eingerichtet
- HTTPS richtig konfiguriert





