# Explorative Datenanalyse
In diesem Dokument halten wir die wichtigsten Erkenntnisse zur Explorativen Datenanalyse fest.

## Sensorbasierte Erkenntnisse
Hier liegt eine Beschreibung zur Analyse der einzelnen Sensoren:

### Accelerometer
#### Was macht der Sensor?
#### Was wie sehen die Daten aus?
#### Wie nützlich sind die Daten für die Klassifikation der Aktivitäten?
#### Nehmen wir diesen Sensor für unsere Modelle?
Ja, weil...

### Gravity
#### Was macht der Sensor?
Software Sensor berechnet die auf die verschiedenen Achsen wirkende Schwerkraft.
#### Was wie sehen die Daten aus?
L2 norm ergibt fast immer 9.81 m/s^2 und schwankt um ca +- 2E-5 m/s^2. Periodische Muster zu erkennen.
Bei einzelnen Personen sind verglichen zu anderen Personen viele Nan's vorhanden (bis 0.35% pro Aktivität).
#### Wie nützlich sind die Daten für die Klassifikation der Aktivitäten?
Könnte theoretisch nützlich sein, da die FFT's der einzelnen Aktivitäten qualitativ unterschiedlich sind.
#### Nehmen wir diesen Sensor für unsere Modelle?
Nein, weil dieser Sensor nicht physisch vorhanden ist. Möglicherweise kann das Resultat dieses Sensors aus dem Accelerometer rekonstruiert werden.

### Gyroskop
#### Was macht der Sensor?
Der Sensor misst die Rotation um die einzelnen Achsen.
#### Was wie sehen die Daten aus?
Periodische Muster zu erkennen.
Bei einzelnen Personen sind verglichen zu anderen Personen viele Nan's vorhanden (bis 0.35% pro Aktivität).
#### Wie nützlich sind die Daten für die Klassifikation der Aktivitäten?
Periodische Muster sind via FFT qualitativ gut zu unterscheiden. 
Auch ein erster Test mittels (Rohdaten x Achse -> resampling -> Segmentierung -> FFT transformation -> PCA -> HistGradientBoostingClassifier)
zeigt, dass eine Klassifikation durchgeführt werden kann.
#### Nehmen wir diesen Sensor für unsere Modelle?
Ja, weil dieser Sensor mit grosser Wahrscheindlichkeit physisch vorhanden ist und dieser in der Lage ist, periodische Signale messen zu können.

### Magnetometer
#### Was macht der Sensor?
#### Was wie sehen die Daten aus?
#### Wie nützlich sind die Daten für die Klassifikation der Aktivitäten?
#### Nehmen wir diesen Sensor für unsere Modelle?
Ja, weil...

### Barometer
#### Was macht der Sensor?
#### Was wie sehen die Daten aus?
#### Wie nützlich sind die Daten für die Klassifikation der Aktivitäten?
#### Nehmen wir diesen Sensor für unsere Modelle?
Nein, weil...

### LocationGPS
#### Was macht der Sensor?
#### Was wie sehen die Daten aus?
#### Wie nützlich sind die Daten für die Klassifikation der Aktivitäten?
#### Nehmen wir diesen Sensor für unsere Modelle?
Nein, weil...
