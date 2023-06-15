# Datenbank
Als Datenbank haben wir [QuestDB](https://questdb.io/) verwendet. Das ist eine Open-Source Timeseries-Datenbank.

## Installation
Wir haben die Datenbank auf Docker aufgesetzt. Dazu haben wir folgenden Befehl ausgeführt:
```bash
QUESTDBPATH="<ERSETZEN_MIT_PFAD>"

docker run -p 9000:9000  \
      -p 8812:8812 \
      -p 9009:9009 \
      -v $QUESTDBPATH:/var/lib/questdb \
      questdb/questdb
```

## Exportieren der Daten
1. Webinterface öffnen: http://localhost:9000/
2. Query ausführen: `SELECT * FROM prod`
3. CSV-Donwload-Button klicken


## Importieren/Wiederherstellen der Daten
1. Webinterface öffnen: http://localhost:9000/
2. Auf "Import" klicken
3. CSV-Datei auswählen, mit "click here to browse"
4. Tabelle umbenennen: `RENAME TABLE "<CSV-FILE-NAME>" TO "prod";`

Ein exportiertes CSV mit den aktuellen Daten kann auf [Onedrive](https://fhnw365-my.sharepoint.com/:u:/g/personal/florin_barbisch_students_fhnw_ch/EVDBHvT9XutLqBT3ds7oPSEB1TXj7PthArsjR60wl9rQfg?e=wLhOkH) gefunden werden.
