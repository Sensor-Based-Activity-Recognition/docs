# Einleitung

Im Rahmen der Sensor Based Activity Recognition Challenge wurde ein Projekt entwickelt, das darauf abzielte, ein System zur Erkennung von Aktivitäten mithilfe von Sensordaten zu realisieren. Die Hauptfragestellung dieses Projekts ist, ob die Verwendung von ausschliesslich Deep Learning Modellen für die Klassifikation von Sensordaten empfehlenswert ist oder ob ähnliche oder bessere Ergebnisse mit einfacheren Machine Learning Modellen erzielt werden können.

Die Motivation für dieses Projekt ergibt sich aus der steigenden Popularität von Sensordaten in verschiedenen Bereichen sowie der Notwendigkeit, effiziente Methoden zur Analyse und Klassifikation dieser Daten zu entwickeln. Eine umfassende Übersicht über den aktuellen Stand der Technik und die durchgeführte Recherche im Rahmen dieses Projekts finden Sie unter [docs/recherche](https://github.com/Sensor-Based-Activity-Recognition/docs/blob/main/recherche/README.md).

# Methodik und Metriken

Im Rahmen der Aktivitätserkennung wurden verschiedene Modelle verwendet, darunter das Convolutional Neural Network (CNN) und der Histogram Gradient Boosting Classifier (HGBC).

Zur Bewertung der Modellleistung wurde der Macro F1-Score verwendet, jedoch haben wir diesen noch mit der Accuracy ergänzt. 
- Wir haben Accuracy als Metrik genommen, um einen Gesamtüberblick über die Anzahl richtiger Klassifikationen zu erhalten. 
- Wir haben den Macro F1-Score genommen, um festzustellen, ob ein Modell alle Klassen gleich gut klassifizieren kann. Falls der F1-Score der Accuracy nicht nahe liegen soll, deutet das darauf hin, dass das Modell nicht alle Klassen gleich gut klassifizieren kann. Das können wir danach mit einer automatisch generierten Confusion Matrix prüfen.

Uns standen verschiedene Optionen für Train-Val-Test-Splits zur Verfügung, darunter ein segmentbasierter Split oder ein personenbasierter Split.
- Bei einem segmentbasierten Split erhält das Modell Daten von jedem Nutzer. Somit lohnt sich ein segmentbasierter Split, wenn man die Performance auf bereits vorhandene Nutzerdaten testen will. 
- Ein personenbasierter Split hingegen teilt die Daten nach Personen auf und bewertet die Performance von neuen Nutzern, welche nicht bei der Datensammlung beteiligt waren. 

In diesem Projekt haben wir uns für einen segmentbasierten Split entschieden, da wir aufgrund der begrenzten Datenmenge von nur 10 Personen nicht genügend Daten hatten, um ein Modell zu entwickeln, das auf neue Nutzer abgestimmt ist. Daher lag unser Fokus auf der Entwicklung von Modellen, die auf uns abgestimmt sind und bei der App gute Ergebnisse auf uns erziehlt. Bei einer grösseren Datenmenge hätten wir uns wahrscheinlich für einen personenbasierten Split entschieden, um auch gute Ergebnisse bei neuen Nutzern zu erziehlen.

# Modelle

Ein ausführliche Übersicht aller Modelle ist unter [Modelle](https://github.com/Sensor-Based-Activity-Recognition/docs/blob/main/Modelle.md) zu finden.

## CNN-Modell

Das CNN-Modell wurde auf Grundlage des Papers von [Chen (2021)](https://github.com/Sensor-Based-Activity-Recognition/docs/blob/adaboost-docs/recherche/Chen_2021.md) entwickelt. Wie im Paper beschrieben, wurden Spectrogramme aus den Sensordaten mithilfe der Short-Time Fourier Transform erstellt. Die Implementierung des CNN erfolgte mit PyTorch und das Modell wurde geringfügig angepasst.

Die Daten wurden aus der Datenbank extrahiert und auf 50Hz resampelt. Anschliessend wurden sie in 5-Sekunden-Fenster aufgeteilt und der Train-Test-Split durchgeführt. Während der STFT-Phase wurden die Spectrogramme erstellt. Die Phase dvclive trainierte das Modell und die evaluate-Phase erstellte eine Konfusionsmatrix, um die Art der Fehler zu analysieren, die das CNN macht.

Die Architektur des Modells besteht aus vier Convolutional Layers, jeweils gefolgt von einem Pooling Layer. Nach dem Convolution-Teil folgt eine Global Average Pooling Layer und zwei Fully Connected Layers. Das Modell erzielte eine Test-Accuracy von über 90%.

## HGBC-Modell

Das HGBC-Modell verwendet den [HistGradientBoostingClassifier](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.HistGradientBoostingClassifier.html) von sklearn. Als Eingabe für unsere Verarbeitungspipeline verwenden wir folgende Features: Accelerometer (X-, Y-, Z-Achse), Gyroskop (X-, Y-, Z-Achse), Magnetometer (X-, Y-, Z-Achse). Die Daten wurden resampelt, in 5-Sekunden-Segmente aufgeteilt und jedes Segment wurde in den Frequenzspektrumraum projiziert. Anschliessend wurde ein Train-Test-Split durchgeführt und das Modell wurde trainiert. Das HGBC-Modell erzielte eine beeindruckende Test-Accuracy von 98%.

## Vergleich der beiden Modelle

Der Vergleich der beiden Modelle ergab, dass sowohl das CNN-Modell als auch das HGBC-Modell beeindruckende Ergebnisse erzielten.

### CNN
![CNN Confusion Matrix](https://camo.githubusercontent.com/950d1d27d04bb036fe6c75a19a0ba25f7d33c515742af690c83350300f13cf2a/68747470733a2f2f61737365742e636d6c2e6465762f333130666232643939393662656562393439653034633438343962646461656466653361376662333f636d6c3d706e672663616368652d6279706173733d31663538623465622d383135662d343132352d613032622d303364643266666536306131)

Das CNN-Modell kann fast alle Klassen gut klassifizieren. Jedoch hat dieses Modell ein wenig Probleme bei der Unterscheidung von der Klasse "Sitzen" und "Stehen". Gleichzeitig klassifiert es einige "Treppenlaufen" Segmente als "Laufen". Dies könnte daran liegen, dass während der Aufnahme vom Treppenlaufen zwischen den Treppen auch flache Ebenen gab, bei welcher die User zur nächsten Treppe liefen.

![CNN Metrics CV](https://camo.githubusercontent.com/07f48e25532dea024c6c2981f1cfb44dde1b95cd24f927b5d73d3b085382d01e/68747470733a2f2f61737365742e636d6c2e6465762f313833383833626537306131373639666163363238373836336536646334386337383031353534303f636d6c3d706e672663616368652d6279706173733d35366265313166622d616537622d346435612d626263332d353232626532303433316562)

Der F1 Macro Score liegt bei einer 10-fold Cross Validation bei etwa 0.9062 mit einer Standardabweichung von 0.0288. Die Accuracy liegt bei etwa 0.8972 mit einer Standardabweichung von 0.0326

### HGBC
![HGBC Confusion Matrix](https://camo.githubusercontent.com/5d23ce9145ef32a020e2a129834f2d8530ca06d4f96f491ccd97215ae817e3bf/68747470733a2f2f61737365742e636d6c2e6465762f393066306538363239353166663366616330666630373136653330376339376261616262353339373f636d6c3d706e672663616368652d6279706173733d30663738363036642d396431352d343465352d393537332d393538376661623936313438)

Das HGBC-Modell hat bei der Klassifizierung die gleichen Probleme wie das CNN, insbesondere bei der Unterscheidung von "Sitzen" & "Stehen" sowie "Treppenlaufen" & "Laufen". Dennoch kann dieses Modell diese Probleme deutlich besser bewältigen als das CNN.

![HGBC Metrics CV](https://camo.githubusercontent.com/71ddbcafd2baa820395cb364da0ab2bb17d83dbcee6cedcabfeab0310ebf47b9/68747470733a2f2f61737365742e636d6c2e6465762f346138303764643765323061633336353636333132353133323464666263643963373562323438333f636d6c3d706e672663616368652d6279706173733d65666531616563372d376634372d346163392d616435392d393632383335383230323561)

Der F1 Macro Score liegt bei einer 10-fold Cross Validation bei etwa 0.9820 mit einer Standardabweichung von 0.0039. Die Accuracy liegt bei etwa 0.9841 mit einer Standardabweichung von 0.0034

### Sicherheit bei der Klassifikation
Das CNN-Modell ist bei den Klassifikationen weniger sicher und gibt eine niedrigere Wahrscheinlichkeit zurück. Im Gegensatz dazu ist sich das HGBC-Modell bei fast allen Klassifikationen sehr sicher. Man könnte meinen, dass es zu sicher ist und daher eher unrealistisch erscheint: Die Wahrscheinlichkeiten liegen oft sehr nahe oder genau bei 100%.

### App
Da beide Modelle sehr leistungsfähig sind und unterschiedliche Stärken und Schwächen aufweisen, haben wir uns dazu entschieden, beide Modelle in unserem Prototypen zu implementieren.

# Lessons Learned

Eine wichtige Erkenntnis aus diesem Projekt ist, dass man sich nicht ausschliesslich auf Deep-Learning-Modelle verlassen sollte. Es ist auch wichtig, herkömmliche Machine-Learning-Modelle zu analysieren und in Betracht zu ziehen. Im Rahmen dieses Projekts konnten wir feststellen, dass einfache Modelle wie der HGBC in einigen Fällen sogar bessere Ergebnisse erzielen können als Deep-Learning-Modelle. Dies unterstreicht die Bedeutung der Auswahl des geeigneten Modells für das jeweilige Problem und die vorhandenen Daten.

Zudem haben wir DVC für unsere Challenge genutzt und von Anfang an unsere Pipeline auf Basis von MLOps entwickelt. Dies ermöglichte uns, unsere Pipeline sehr modular aufzubauen und unsere Modelle bei jeder Änderung automatisiert mit einem Runner zu testen. Obwohl dieser Prozess für unseren Anwendungsfall wahrscheinlich etwas Overkill war, konnten wir erste Erfahrungen für mögliche Anwendungen in zukünftigen Projekten und in der Arbeitswelt sammeln.

Bei der Entwicklung haben wir darauf geachtet, dass bei der Arbeit mehrerer Nutzer an einem Repository mit Branches gearbeitet wird und alle Änderungen, die im Main landen sollten, auch durch Peer-Review überprüft werden. Auf diese Weise konnten wir sicherstellen, dass unser Code von mehreren Personen akzeptiert wurde und unseren Qualitätsstandards entspricht.
