# Updates

## Schema

![schema](schema.png)

## Aufgaben und Lösungen

1.  Ändern Sie die Adresse des Kunden `Kunnert` auf `Expo Plaza 3, 30539 Hannover`.

```SQL
UPDATE kunde
SET
    PLZ = 30539,
    Straße = 'Expo Plaza',
    Hausnummer = 3,
    Stadt = 'Hannover'
WHERE `Name` = 'Kunnert';
```

2. Ändern Sie den Verkaufspreis des Artikels `Photoshop` auf `489`€

```SQL
UPDATE artikel
SET VK_Preis = 489
WHERE `Name` = 'Photoshop';
```

3. Ändern Sie den Status des Artikel `Nero Burning ROM` auf `Vergriffen`

```SQL
UPDATE artikel a
SET a.`status` =
    (SELECT s.`status` FROM `status` s
    WHERE s.`Name` = 'Vergriffen')
WHERE a.`Name` = 'Nero Burning ROM';
```

4. Erhöhen Sie den VK_Preis aller Drucker um 10%

```SQL
UPDATE artikel
SET VK_Preis = VK_Preis * 1.10
WHERE kategorieNr = 
    (SELECT k.KategorieNr
    FROM kategorie k
    WHERE k.`Name` = 'Drucker');
```

5. Ändern Sie den Status aller Softwareprodukte auf `Vergriffen`

```SQL
UPDATE artikel a
SET a.`status` =
    (SELECT s.status
    FROM `status`
    WHERE s.`Name` = 'Vergriffen')
WHERE a.kategorieNr =
    (SELECT k.kategorieNr
    FROM kategorie k
    WHERE k.`Name` = 'Software')
```