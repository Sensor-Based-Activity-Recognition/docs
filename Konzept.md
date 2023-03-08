# Konzept für Sensor Based Activity Recognition Challenge
Von:
- Tobias Buess
- Gabriel Torres Gamez
- Yvo Keller
- Florin Barbisch  

# Ziel
## Bewegungsprofile
Ziel dieser Challenge ist es Aktivitäten anhanden von Bewegungsdaten eines mobilen Endgerätes zu erkennen. Es sollen 6 Bewegungsprofile erkannt werden:
 - Gehen (Schweizerdeutsch: Laufen)
 - Laufen (Schweizerdeutsch: Rennen)
 - Treppensteigen
 - Velofahren
 - Stehen
 - Sitzen

## Genauigkeit
Wir haben uns das Ziel gesetzt, eine Genauigkeit von 95% zu erreichen (welche Metrik (AUC ROC, F1, Acc?)).
Dies scheint uns realistisch erreichbar, trotz dem Fakt, dass unsere Daten sehr unterschiedlich aufgenommen werden (Smartphone/Smartwatch, Ort am Körper).
Diverse Papers berichten bei Sensor Based Activity Recognition Genauigkeiten zwischen 80%-99%.

# Scope des Projektes
## Was wir erreichen wollen
- mindestens ein ML-Modell und ein DL-Modell
- MLOps (wandb.ai)
- App zum Klassifizieren/Aufzeichnen der Aktivitäten
- Datengrundlage ist in einer Timeseries-Datenbank
- Tool um Datenqualität zu überprüfen:
  - Missing Data
  - Daten manuell zuschneiden (Anfang und Ende der Aufzeichnung)
- gemessene Daten beinhalten (npch nicht klar ob wir alle verwenden werden):
  - Inertial Sensors:
    - Accelerometer
    - Beschleunigungssensor
    - Gyroskop
    - Orientierungssensor
  - Non-inertial Sensors:
    - Magnetometer
    - Barometer
    - Standort


# Was wir nicht erreichen wollen
 - Reinforcment Learning (Klassifikationen der App korrigieren)
 - Klassifikation von Smartwatch-Daten

# Milestones
|Was|Wann                         |
|---|-----------------------------|
|Daten sammeln, einlesen, zuschneiden + Konzept/Planung|16. März 2023                |
|Feature Engineering erstes ML Modell|6. April 2023                |
|ML-Modelle und refining Feature Engineering|4. Mai 2023                  |
|DL-Modelle|25. Mai 2023                 |
|App mit Modell|15. Juni 2023                |
|Abgabe Challenge|15. Juni 2023                |
|Vergleich der Modelle|15. Juni 2023                |
|Präsentation|KW 25/26                     |

# Datensicherung/Datenbeschriftung
Wir die Aktivitäten mit der anderen Gruppe abgestummen habe um somit gemeinsam Daten sammeln zu können.
Die Bewegungsdaten sammeln wir alle mit der App [Sensor Logger](https://github.com/tszheichoi/awesome-sensor-logger).
Von da werden die Daten als JSON oder als gezipptes CSV (weil JSON nicht bei allen funktioniert) in einen OneDrive Ordner von Etienne Roulet exportiert.
In diesem Ordner existiert für jede Aktivität ein Unterordner in welchem jeweils ein Ordner für jede Person steht. Die Datei selbst muss den Namen des Endgerätes enthalten.
So bleibt es möglich Smartwatches herauszufiltern.

TODO: vllt automatischi Backups nach Github oder so?

# Datenverarbeitung & Modellierung
CHume nid ganz drus. Wie gnau müesemer das scho ahgäh, bevor mir experimentiert hei? Ig denke, d Idee isch, das mir Papers läse und üs es Bild vo mögliche Methode mache und denne die gwählte hie niederschriebe.
#AntiAgile

# Output
(in welcher Form die Erkenntnisse präsentiert werden sollen (Output))
Präsi + docs repo
