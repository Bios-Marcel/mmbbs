# Inserts

## Schema

![schema](schema.png)

## Aufgaben und Lösungen

1. Fügen Sie einen neuen Kunden ein mit folgenden Daten (Franz Schmidt, Nebenstraße 1, 30167 Hannover, f.schmidt@mmbbs.de, Kennwort=“emembebees“)
    ```SQL
    INSERT INTO kunde (`Name`, Straße, Hausnummer, PLZ, Stadt, EMail, Kennwort)
    VALUES ('Franz Schmidt', 'Nebenstraße', 1, 30167, 'Hannover', 'f.schmidt@mmbbs.de', 'emembebees');
    ```
2. Fügen Sie eine neue Kategorie („Grafikkarte“) ein
    ```SQL
    INSERT INTO kategorie (`Name`)
    VALUES ('Grafikkarte');
    ```
3. Fügen Sie einen neuen Artikel (eine Grafikkarte) mit folgenden Daten (Name=“Nvida Power Grafikkarte“, Status =“Verfügbar“, EK_Preis=“216“, VK_Preis=“333“)
    ```SQL
    INSERT INTO artikel (`Name`, `Status`, EK_Preis, VK_Preis, KategorieNR)
    VALUES ('Nvidia Power Grafikkarte',
        (SELECT s.`Status` FROM status s where s.`Name` = 'Verfügbar')),
        216,
        333,
        (SELECT k.KategorieNr FROM kategorie k WHERE k.`Name` = 'Grafikkarte')
    );
    ```
4. Erzeugen Sie eine neue Bestellung, so kauft der neue Kunde Franz Schmidt eine Nvida Power Grafikkarte und Micosoft Office!
    ```SQL
    INSERT INTO bestellung (KundenNr, Datum)
    VALUES (
        (SELECT k.KundenNr FROM kunde k WHERE k.`Name` = 'Franz Schmidt'),
        NOW()
    );

    INSERT INTO position (BestellNr, ArtikelNr, Menge)
    VALUES (
        (SELECT b.BestellNr
            FROM bestellung b
            WHERE KundenNr = (
                SELECT k.KundenNr
                FROM kunde k
                WHERE k.`Name` = 'Franz Schmidt' LIMIT 1)
            ORDER BY Datum DESC LIMIT 1),
        (SELECT a.ArtikelNr FROM artikel a WHERE a.`Name` = 'Nvidia Power Grafikkarte'),
        1
    );

    INSERT INTO position (BestellNr, ArtikelNr, Menge)
    VALUES (
        (SELECT b.BestellNr
            FROM bestellung b
            WHERE KundenNr = (
                SELECT k.KundenNr
                FROM kunde k
                WHERE `Name` = 'Franz Schmidt' LIMIT 1)
            ORDER BY Datum DESC LIMIT 1),
        (SELECT a.ArtikelNr FROM artikel a WHERE a.`Name` = 'Microsoft Office'),
        1
    );
    ```
5. Erzeugen Sie einen neuen Artikel (einen Drucker) mit folgenden Daten (Name=“Epson Power Jet“,Status=“verfügbar“, EK_Preis=“317.12“,VK_Preis=“412“)
    ```SQL
    INSERT INTO artikel (`Name`, `Status`, EK_Preis, VK_Preis, KategorieNr)
    VALUES (
        'Epson Power Jet',
        (SELECT s.`Status` FROM status s WHERE s.`Name` = 'Verfügbar'),
        317.12,
        412,
        (SELECT k.KategorieNr FROM kategorie k WHERE k.`Name` = 'Drucker')
    );
    ```