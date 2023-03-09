# Konzept für Sensor Based Activity Recognition Challenge
Von:
- Tobias Buess
- Gabriel Torres Gamez
- Yvo Keller
- Florin Barbisch  

# Ziel
## Bewegungsprofile
Ziel dieser Challenge ist es, Aktivitäten mittels Bewegungsdaten eines mobilen Endgerätes zu erkennen. Es sollen 6 Bewegungsprofile erkannt werden:
 - Gehen (Schweizerdeutsch: Laufen)
 - Laufen (Schweizerdeutsch: Rennen)
 - Treppensteigen
 - Fahrradfahren (Schweizerdeutsch: Velofahren)
 - Stehen
 - Sitzen

## Genauigkeit
Wir haben uns das Ziel gesetzt, eine Genauigkeit (F1-Score Macro) von 95 % zu erreichen.
Dies scheint uns realistisch erreichbar, trotz des Fakts, dass unsere Daten sehr unterschiedlich aufgenommen werden (Smartphone/Smartwatch, Ort am Körper).
Diverse Papers berichten bei Sensor Based Activity Recognition Genauigkeiten zwischen 80 % - 99 %.

Wir haben den F1-Score Macro gewählt, da dieser alle Klassen gleich gewichtet.

Formel für den F1-Score Macro:
$$F1_{macro}=\frac{1}{n}\sum_{i=1}^{n}F1_{i}$$

Formel für den F1-Score der Klasse i:
$$F1_{i} = \frac{2 \cdot Precision_{i} \cdot Recall_{i}}{Precision_{i} + Recall_{i}}$$


# Scope des Projektes
## Was wir erreichen wollen
- mindestens ein ML-Modell und ein DL-Modell
- MLOps (wandb.ai)
- App zum Klassifizieren
- Datengrundlage ist in einer Timeseries-Datenbank
- Tool, um Datenqualität zu überprüfen:
  - Fehlende Daten
  - Daten manuell zuschneiden (Anfang und Ende der Aufzeichnung)
- gemessene Daten beinhalten:
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
 - Iterative Modelling (Klassifikationen aus der App korrigieren und zurück in die Datenbank schreiben)
 - Klassifikation von Smartwatch-Daten. Da diese grundlegend anders aufgenommen werden als die Daten von Smartphones.


# Milestones
| Was                                                    | Wann           |
|--------------------------------------------------------|----------------|
| Daten sammeln, einlesen, zuschneiden + Konzept/Planung | 16. März 2023  |
| Feature Engineering erstes ML-Modell                   | 06. April 2023 |
| ML-Modelle und refining Feature Engineering            | 04. Mai 2023   |
| DL-Modelle                                             | 25. Mai 2023   |
| App mit Modell                                         | 15. Juni 2023  |
| Abgabe Challenge                                       | 15. Juni 2023  |
| Vergleich der Modelle                                  | 15. Juni 2023  |
| Präsentation                                           | KW 25/26       |


# Datensicherung/Datenbeschriftung
Wir haben die Aktivitäten mit der anderen Gruppe abgeglichen, um somit gemeinsam Daten sammeln zu können.
Die Bewegungsdaten sammeln wir alle mit der App [Sensor Logger](https://github.com/tszheichoi/awesome-sensor-logger).
Von da werden die Daten als JSON oder als gezipptes CSV (weil JSON nicht bei allen funktioniert) in einen OneDrive-Ordner von Etienne Roulet exportiert.
In diesem Ordner existiert für jede Aktivität ein Unterordner, in welchem jeweils ein Ordner für jede Person steht. Die Datei selbst muss den Namen des Endgerätes enthalten.
So bleibt es möglich, Smartwatches herauszufiltern.


# Datenverarbeitung & Modellierung
## Data Preprocessing
 - Die Aufzeichnungen werden manuell zugeschnitten, da zu Beginn und am Ende der Aufzeichnung (noch) keine Bewegung stattfindet.
 - Da nicht jedes Gerät und nicht jeder Sensor die Daten mit gleicher Frequenz aufnimmt, müssen die Daten resampled werden.
 - Die Daten müssen in gleich lange Sequenzen/Windows aufgeteilt werden.
 - Fehlende Daten müssen interpoliert werden.

## Feature Engineering
 - Fast Fourier Transformation (FFT), um Frequenzen zu extrahieren
 - (simple) Aggregationen (zeitbasiert und frequenzbasiert) (z.B. Mittelwert, Standardabweichung, Median, ...)
 - Smoothings (z.B. Moving Average)

## Modellierung
 - stratified Train-Test Split (80%/20%)
 - Diverse ML-Modelle trainieren
 - Diverse DL-Modelle trainieren
 - Hyperparameter Tuning mit Cross-Validation
 - Evaluation der Modelle mit verschiedenen Metriken (AUC ROC, F1, Acc, ...)
 - Vergleich der Modelle

# Lieferobjekte
Lieferobjekte dieses Projektes sind:

 - ein gut strukturiertes und dokumentiertes Git-Repository (welches von einer Person ausserhalb des Projektes weiterentwickelt werden könnte),
 - die App zum Klassifizieren,
 - die Daten selbst,
 - eine Präsentation, welche unsere Ergebnisse und unseren Prozess dokumentiert. 
