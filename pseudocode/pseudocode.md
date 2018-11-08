# Pseudocode

## Aufgabe

Die PixelPic AG benötigt eine Methode, die nach einem Algorithmus eine Prüfziffernbe- rechnung für Kreditkartennummern durchführt.
  1. Multiplikation aller Ziffern an gerader Stelle mit 3
  2. Bildung der Quersummen aller Ergebnisse aus Schritt 1 und Addition dieser Quersummen
  3. Addition aller Ziffern an ungerader Stelle
  4. Addition der Ergebnisse aus Schritt 2 und 3
  5. Berechnung der Differenz zwischen dem Ergebnis aus Schritt 4 und der nächstgrößeren durch 10 teilbaren Zahl, ergibt sich als Differenz 10, wird diese auf 0 gesetzt. Hinweis: Der Methode wird die Kreditkartennummer als String übergeben. Ist die Kartennummer gültig, wird true, sonst false zurückgegeben.

## Lösung

```Pseudocode
function validateKreditkartennummer(string number) returns boolean
    variable evenMultiliedByThree = 0
    variable quersummenAddedUp = 0
    variable oddNumbersAddedUp = 0

    for zeichenIndex in 1 to length(number)
        zeichenAlsZahl = convertCharacterToInteger(number[zeichenIndex])

        if zeichenIndex % 2 equals 0
            variable multipliedTemp = zeichenAlsZahl * 3
            evenMultiliedByThree = evenMultiliedByThree + multipliedTemp
            quersummenAddedUp = quersummenAddedUp + calculateQuersumme(evenMultiliedByThree)
        else 
            oddNumbersAddedUp = oddNumbersAddedUp + zeichenAlsZahl

    


function calculateQuersumme(integer number) returns integer
    variable numberAsString = number.asString()
    variable result = 0
    
    foreach zeichen in numberAsString
        result = result + convertCharacterToInteger(zeichen)
    
    return zeichen

function convertCharacterToInteger(zeichen) returns integer
    ...
```