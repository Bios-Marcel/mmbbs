# Zeitschlitz

## Aufgabe

Als neue Funktionalität der Webpräsenz soll der Kunde bereits bei der Eingabe seiner Buchungsabfrage eine Auskunft über die Verfügbarkeit des gewünschten Gerätes erhalten. 

Sie erhalten die Aufgabe, die Methode zur Verfügbarkeitsermittlung zu erstellen. Dabei sind die folgenden Punkte zu berücksichtigen:
* Der Methode sollen folgende Daten übergeben werden: Gerätetyp, Entleihbeginn, Entleihdauer in Tagen
* Als Ergebnis wird bei Verfügbarkeit die GeräteID zurückgegeben, sonst der Wert 0
* Ein Gerät ist verfügbar, wenn es nicht reserviert ist bzw. entliehen ist (Eintragung in Tabelle)

Eine andere Gruppe hat bereits Vorarbeit geleistet und Methoden erstellt, die alle relevanten Daten für die Geräte eines Typs liefert (Entleih- und Reservierungsdaten)

```
vonDat = Reservierungsbeginn
bisDat = Reservierungsende
```

| Funktion | Beschreibung |
| - | - |
| `getGeräteListe(geräteTyp): geräteID[]` | Liefert alle vorhandenen GeräteIDs für ein Gerätetyp |
| `getResDat(GeräteID): buchungsdat[]` | (vonDat, bisDat) liefert Reservierungsdaten für ein Gerät nach „vonDat“ sortiert |

## Lösung

```Pseudocode
function isAvailable(deviceType, startDate, durationInDays) returns integer
    if durationInDays lessOrEqual 0
        return 0

    variable dateToday = getCurrentDate()

    if dateToday greater startDate
        return 0

    foreach device in getGeräteListe(deviceType)
        variable available = true
        variable buchungsDaten = getResDat(device.id)
        for index in 0 to (buchungsDaten - 1) step 2
            varaible startDateIndex = index
            variable endDateIndex = index + 1
            if startDate greaterOrEqual buchungsDate[startDateIndex] and (startDate + durationInDays) lessOrEqual buchungsDaten[endDateIndex] 
                available = false
                skip

        if available equals true
            return device.id

    return 0
```