# Explorative Datenanalyse
In diesem Dokument halten wir die wichtigsten Erkenntnisse zur Explorativen Datenanalyse fest.

## Sensorbasierte Erkenntnisse
Hier liegt eine Beschreibung zur Analyse der einzelnen Sensoren:

### Accelerometer
#### Was macht der Sensor?
Der Beschleunigungssensor misst die Beschleunigung des Geräts auf allen Achsen (x,y,z). Im Smartphone hat er die Aufgabe, die derzeitige Lage des Geräts und ihre Veränderungen zu erkennen. Beim Drehen des Smartphones verändert sich die Richtung, aus der die Schwerkraft auf das Gerät wirkt.
#### Wie sehen die Daten aus?
Die Beschleunigung ist bei den Unterschiedlichen Aktivitäten erkennbar anders. Zusätzlich zeigt der y-Sensor (Entlang des Beins) interessante Muster, die sehr wahrscheinlich auf die Position des Handys in der vorderen Linken Hosentasche bei den Messungen zurückzuführen sind.
<img width="1120" alt="image" src="https://user-images.githubusercontent.com/22744751/228468538-b89959c2-017e-4d4d-8d93-b353cb2d8d6e.png">

#### Wie nützlich sind die Daten für die Klassifikation der Aktivitäten?
Bei den verschiedenen Aktivitäten sind deutliche Unterschiede in der Verteilung und Intensität der Messungen zu erkennen. 
#### Nehmen wir diesen Sensor für unsere Modelle?
Ja, weil in der EDA klare Unterschiede der Sensormessungen bei den Aktivitäten zu erkennen waren. Wir gehen davon aus, dass dieser Sensor eine wichtige Grundlage für die Klassifizierung der Aktiviäten bilden wird. Auch in anderen Studien ist dieser Sensor oft sehr zentral.

### Gravity
#### Was macht der Sensor?
Software Sensor berechnet die auf die verschiedenen Achsen wirkende Schwerkraft.
#### Wie sehen die Daten aus?
L2 norm ergibt fast immer 9.81 m/s^2 und schwankt um ca +- 2E-5 m/s^2. Periodische Muster zu erkennen.
Bei einzelnen Personen sind verglichen zu anderen Personen viele Nan's vorhanden (bis 0.35% pro Aktivität).
#### Wie nützlich sind die Daten für die Klassifikation der Aktivitäten?
Könnte theoretisch nützlich sein, da die FFT's der einzelnen Aktivitäten qualitativ unterschiedlich sind.
#### Nehmen wir diesen Sensor für unsere Modelle?
Nein, weil dieser Sensor nicht physisch vorhanden ist. Möglicherweise kann das Resultat dieses Sensors aus dem Accelerometer rekonstruiert werden.

### Gyroskop
#### Was macht der Sensor?
Der Sensor misst die Rotation um die einzelnen Achsen.
#### Wie sehen die Daten aus?
Periodische Muster sind zu erkennen.
Bei einzelnen Personen sind verglichen zu anderen Personen viele Nan's vorhanden (bis 0.35% pro Aktivität).
#### Wie nützlich sind die Daten für die Klassifikation der Aktivitäten?
Periodische Muster sind via FFT qualitativ gut zu unterscheiden. 
Auch ein erster Test mittels (Rohdaten x Achse -> resampling -> Segmentierung -> FFT transformation -> PCA -> HistGradientBoostingClassifier)
zeigt, dass eine Klassifikation durchgeführt werden kann.
#### Nehmen wir diesen Sensor für unsere Modelle?
Ja, weil dieser Sensor mit grosser Wahrscheindlichkeit physisch vorhanden ist und dieser in der Lage ist, periodische Signale messen zu können.

### Magnetometer
#### Was macht der Sensor?
Er misst die Richtung des magnetischen Nordens aus sicht des Smartphones im Microteslas.
#### Wie sehen die Daten aus?
Es sind periodische Muster zu erkennen. Es wird die x-, y- und z-Ausrichtung angegeben.
#### Wie nützlich sind die Daten für die Klassifikation der Aktivitäten?
So semi, weil zwar periodische Muster zu erkennen sind. Aber darüber ist auch noch die Ausrichtung des Gerätes versteckt, was man zuerst richtig bereinigen muss.
#### Nehmen wir diesen Sensor für unsere Modelle?
Ja, weil wir periodische Muster erkennen können.

### Barometer
#### Was macht der Sensor?
Er misst den athmosphärischen Druck in Hekto-Pascal und berechnet dadurch die relative Höhe. 
#### Wie sehen die Daten aus?
Sehr starke Schwankungen. Der Moving Average muss eine Minute betragen, um das Rauschen loszuwerden.
#### Wie nützlich sind die Daten für die Klassifikation der Aktivitäten?
Nicht sehr nützlich, weil es ein sehr grosses Rauschen hat und die Windows gross sein müssen um etwas zu erkennen.
#### Nehmen wir diesen Sensor für unsere Modelle?
Nein, weil es viel Rauschen in den Daten hat und die Höhenveränderung unserer Meinung nach keine guten Rückschlüsse auf die Aktivität zulassen.

### LocationGPS
#### Was macht der Sensor?
Dieser Sensor misst die Koordinaten des Endgeräts.
#### Wie sehen die Daten aus?
Die Spalten LocationGps_latitude und LocationGps_longitute enthalten Koordinaten in der Decimal Degrees Notation.
Jedoch sind nur wenige Daten vorhanden (Ingesamt nur 2018 Datensätze).
#### Wie nützlich sind die Daten für die Klassifikation der Aktivitäten?
Da wir nur Daten für Tobias erhalten haben, nützen uns diese Daten nicht.
#### Nehmen wir diesen Sensor für unsere Modelle?
Nein, da fast alle OBservationen keinen Wert beinhalten.

### Orientation
#### Was macht der Sensor?
Er misst die Orientation in die x, y und z Achse.
#### Wie sehen die Daten aus?
Leider haben wir nur NA Werte.
#### Wie nützlich sind die Daten für die Klassifikation der Aktivitäten?
Garnicht, da wir keine Daten haben.
#### Nehmen wir diesen Sensor für unsere Modelle?
Nein, da wir keine Daten haben.
