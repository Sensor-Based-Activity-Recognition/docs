# Sensor Data Challenge | Besprechung 23.2.2023

Wir haben ein Klassifikationsproblem.

Wir klassifizieren folgende Aktivitäten:
- Laufen 
- Rennen
- Treppenlaufen
- Velofahren
- Stehen
- Sitzen

Wir messen unsere Daten mit der App “Sensor Logger”
- Einstellungen:
    - Sample as Frequently as possible bei allen Einstellungen
    - Log all inertial and non inertial Sensors
    - Include Uncalibrated Data
- Wie wird gemessen:
    - Geräte
        - Handy in der oberen, vorderen Hosentasche
        - Smartwatch
    - Durchführung einer Messung
        - Aufzeichnung starten
        - Handy in Hosentasche
        - 5s stillstehen
        - Aktivität durchführen
        - 5s stillstehen
        - Handy hervornehmen
        - Aufzeichnung beenden
    - Kriterien für eine einzelne Messung: 
        - min: 1 Minute
        - max: open end
    - Zu jeder Aktivität nimmt jede Person mindestens 10 Minuten auf

Unsere Datenstruktur sieht so aus:
- Aktivitätstyp
    - Personenname
        - XX_DeviceType.json
Beispiel:
- Laufen
    - Gabriel
        - 01_iPhone13ProMax.json

Wie wir die Daten speichern:
- OneDrive (Etienne gibt Informationen bekannt)

Notiz: 
Bis 1. März nehmen alle zu jeder Aktivität eine Observation auf, um zu testen, ob dieses System verhebt. :)