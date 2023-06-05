# Einleitung

Im Rahmen der Sensor Based Activity Recognition Challenge wurde ein Projekt entwickelt, das darauf abzielte, ein System zur Erkennung von Aktivitäten mithilfe von Sensordaten zu realisieren. Die Hauptfragestellung dieses Projekts ist, ob die Verwendung von ausschliesslich Deep Learning Modellen für die Klassifikation von Sensordaten empfehlenswert ist oder ob ähnliche oder bessere Ergebnisse mit einfacheren Machine Learning Modellen erzielt werden können.

Die Motivation für dieses Projekt ergibt sich aus der steigenden Popularität von Sensordaten in verschiedenen Bereichen sowie der Notwendigkeit, effiziente Methoden zur Analyse und Klassifikation dieser Daten zu entwickeln. Eine umfassende Übersicht über den aktuellen Stand der Technik und die durchgeführte Recherche im Rahmen dieses Projekts finden Sie unter [docs/recherche](https://github.com/Sensor-Based-Activity-Recognition/docs/blob/main/recherche/README.md).

# Methodik und Metriken

Im Rahmen der Aktivitätserkennung wurden verschiedene Modelle verwendet, darunter das Convolutional Neural Network (CNN) und der Histogram Gradient Boosting Classifier (HGBC).

Zur Bewertung der Modellleistung wurden die Accuracy und der Macro F1-Score verwendet. Die Accuracy gibt an, wie gut das Modell insgesamt die Aktivitäten klassifiziert, während der Macro F1-Score ein gewichtetes Mittelmass für die Präzision und den Recall aller Aktivitäten darstellt. Die Entscheidung, die Accuracy als Metrik zu verwenden, ermöglichte uns eine umfassende Bewertung und Vergleich der Gesamtleistung der Modelle. Eine hohe Accuracy deutet darauf hin, dass das Modell die Aktivitäten korrekt erkennt und klassifiziert. Der Macro F1-Score wurde ausgewählt, um sicherzustellen, dass die Leistung des Modells gleichmässig für alle Aktivitäten berücksichtigt wird. Er gewichtet die Präzision und den Recall für jede Aktivität gleich, unabhängig von der Datenverteilung. Diese Metrik ermöglichte uns eine Bewertung und Vergleich der Leistung der Modelle bei der Erkennung verschiedener Aktivitäten.

Der Train-Val-Test-Split wurde entweder auf segmentebasierter Ebene oder durch einen personenbasierten Split durchgeführt, um die Leistung des Systems zu bewerten. Bei einem segmentbasierten Split wurden die Daten auf Segmentebene aufgeteilt, um eine detaillierte Bewertung der Aktivitätserkennung zu ermöglichen. Diese Methode ermöglicht die Präzisierung der Aktivitäten auf einzelne Segmente und die Erkennung spezifischer Aktivitätsmuster. Allerdings könnte sie den Einfluss individueller Unterschiede zwischen den Benutzern verringern. Ein personenbasierter Split hingegen teilt die Daten nach Personen auf und bewertet die Leistung des Systems anhand der Accuracy und des Micro F1-Scores. Diese Methode berücksichtigt individuelle Unterschiede zwischen den Benutzern und ermöglicht eine genauere Bewertung der Systemleistung für jede einzelne Person. Allerdings könnte sie die Präzision bei der Erkennung spezifischer Aktivitätsmuster verringern.

In diesem Projekt haben wir uns für einen segmentbasierten Split entschieden, da wir aufgrund der begrenzten Datenmenge von nur 10 Personen nicht genügend Daten hatten, um ein Modell zu entwickeln, das auf die breitere Masse abgestimmt ist. Daher lag unser Fokus auf der Entwicklung von Modellen, die auf unsere spezifische Leistung abgestimmt sind.

# Modelle

Ein ausführliche Übersicht aller Modelle kann man unter [Modelle](https://github.com/Sensor-Based-Activity-Recognition/docs/blob/main/Modelle.md) finden.

## CNN-Modell

Das CNN-Modell wurde auf Grundlage des Papers von [Chen (2021)](https://github.com/Sensor-Based-Activity-Recognition/docs/blob/adaboost-docs/recherche/Chen_2021.md) entwickelt. Wie im Paper beschrieben, wurden Spectrogramme aus den Sensordaten mithilfe der Short-Time Fourier Transform erstellt. Die Implementierung des CNN erfolgte mit PyTorch und das Modell wurde geringfügig angepasst.

Die Daten wurden aus der Datenbank extrahiert und auf 50Hz resampelt. Anschliessend wurden sie in 5-Sekunden-Fenster aufgeteilt. Während der STFT-Phase wurden die Spectrogram,e erstellt. Die Phase dvclive trainierte das Modell und die evaluate-Phase erstellte eine Konfusionsmatrix, um die Art der Fehler zu analysieren, die das CNN macht.

Die Architektur des Modells besteht aus vier Convolutional Layers, gefolgt von Pooling Layers. Nach dem Convolution-Teil folgt eine Global Average Pooling Layer und zwei Fully Connected Layers. Das Modell erzielte eine Test-Accuracy von über 90%.

## HGBC-Modell

Das HGBC-Modell verwendet den [HistGradientBoostingClassifier](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.HistGradientBoostingClassifier.html) von sklearn. Als Eingabe für unsere Verarbeitungspipeline verwenden wir folgende Features: Accelerometer (X-, Y-, Z-Achse), Gyroskop (X-, Y-, Z-Achse), Magnetometer (X-, Y-, Z-Achse). Die Daten wurden resampelt, in 5-Sekunden-Segmente aufgeteilt und jedes Segment wurde in den Frequenzspektrumraum projiziert. Anschliessend wurde ein Train-Test-Split durchgeführt und das Modell wurde trainiert. Das HGBC-Modell erzielte eine beeindruckende Test-Accuracy von 98%.

## Vergleich der beiden Modelle

Der Vergleich der beiden Modelle ergab, dass sowohl das CNN-Modell als auch das HGBC-Modell beeindruckende Ergebnisse erzielten. Das CNN-Modell zeigte seine Stärken bei der Erkennung von Aktivitäten aufgrund seiner Fähigkeit, spezifische Merkmale aus den Spectrograms zu extrahieren. Das HGBC-Modell hingegen erreichte eine hohe Genauigkeit, insbesondere bei der Erkennung von Aktivitäten mit einfachen Bewegungsmustern. 

# Lessons Learned

Eine wichtige Lesson Learned ist, dass man nicht ausschliesslich auf Deep Learning Modelle setzen sollte. Es ist auch wichtig, herkömmliche Machine Learning Modelle zu analysieren und in Betracht zu ziehen. Im Rahmen dieses Projekts konnten wir feststellen, dass einfache Modelle wie der HGBC in einigen Fällen sogar bessere Ergebnisse erzielen können als Deep Learning Modelle. Dies unterstreicht die Bedeutung der Auswahl des geeigneten Modells für das jeweilige Problem und die vorhandenen Daten.
