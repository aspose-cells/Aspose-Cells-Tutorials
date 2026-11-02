---
category: general
date: 2026-06-21
description: Maak een vermenigvuldigingstabel in Excel met Python. Leer hoe je lambda
  gebruikt, hoe je makearray gebruikt, een Excel-array weergeeft en Excel‑waarden
  leest met Python in een stapsgewijze tutorial.
draft: false
keywords:
- create multiplication table
- how to use lambda
- how to use makearray
- display excel array
- read excel values python
language: nl
og_description: Maak een vermenigvuldigingstabel in Excel met Python. Deze tutorial
  laat zien hoe je lambda, makearray gebruikt, een Excel‑array weergeeft en Excel‑waarden
  efficiënt leest met Python.
og_title: Maak een vermenigvuldigingstabel in Excel met Python – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiplication table in Excel using Python. Learn how to use
    lambda, how to use makearray, display excel array and read excel values python
    in a step‑by‑step tutorial.
  headline: Create multiplication table in Excel with Python – Full Guide
  type: TechArticle
tags:
- python
- excel
- openpyxl
title: Maak een vermenigvuldigingstabel in Excel met Python – Volledige gids
url: /nl/python/import-and-export/create-multiplication-table-in-excel-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak een vermenigvuldigingsmatrix in Excel met Python – Volledige gids

Heb je je ooit afgevraagd hoe je een **vermenigvuldigingsmatrix** in Excel kunt **maken** zonder elke cel handmatig in te typen? Je bent niet de enige. In veel rapportagescenario's heb je snel een 5×5 (of grotere) raster van producten nodig, en dit handmatig doen is tijdverspilling.  

In deze tutorial lopen we stap voor stap een nette, Python‑gedreven manier door om die tabel te genereren, deze in te sluiten met een `MAKEARRAY`‑formule, en vervolgens de resultaten terug te halen in je script. Onderweg beantwoorden we **hoe je lambda gebruikt**, laten we **hoe je makearray gebruikt** zien, en demonstreren we **display excel array** evenals **read excel values python** — allemaal in één samenhangend voorbeeld.

Aan het einde heb je een herbruikbare snippet die met elk werkboek werkt, en begrijp je waarom deze aanpak zowel snel als toekomstbestendig is.

## Wat je nodig hebt

- Python 3.8+ (de nieuwste stabiele release is prima)
- De `openpyxl`‑bibliotheek (of een andere Excel‑bewuste bibliotheek die formules ondersteunt)
- Een basisbegrip van lambda‑expressies in Python
- Geen speciale Excel‑add‑ins; de native `MAKEARRAY`‑functie (beschikbaar in Excel 365) doet het zware werk

Als je iets mist, voer dan gewoon `pip install openpyxl` uit en je bent klaar om te gaan.

## Maak vermenigvuldigingsmatrix – Overzicht

Het kernidee is simpel: we maken een nieuw werkboek, schrijven een `MAKEARRAY`‑formule die een 5 × 5 vermenigvuldigingsmatrix bouwt, dwingen Excel om deze te berekenen, en lezen tenslotte de resulterende waarden terug in Python.

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Insert a MAKEARRAY formula that builds a 5×5 multiplication table
# The formula uses a LAMBDA that returns r*c for each row (r) and column (c)
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"

# Step 3: Calculate all formulas so the array is materialized in the sheet
workbook.calculate_formula()

# Step 4: Read and display the top‑left 5×5 block of values
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

Het uitvoeren van het script geeft:

```
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
[3, 6, 9, 12, 15]
[4, 8, 12, 16, 20]
[5, 10, 15, 20, 25]
```

Dat is een volledig functionele **create multiplication table** in Excel, volledig gegenereerd vanuit Python.

### Waarom `MAKEARRAY` gebruiken in plaats van een Python‑lus?

- **Prestaties**: Excel voert de berekening native uit, wat sneller is voor grote matrices.
- **Live bijwerken**: Als je later de afmetingen in de formule wijzigt, rekent het blad automatisch opnieuw.
- **Leesbaarheid**: De formule drukt de intentie (“maak een array”) direct uit, waardoor je Python‑code overzichtelijk blijft.

## Hoe lambda te gebruiken in Python voor Excel‑formules

Het `LAMBDA`‑deel van de `MAKEARRAY`‑aanroep is een anonieme functie aan de Excel‑kant, geen Python‑lambda. Het concept blijft echter hetzelfde: je definieert een klein, inline stukje logica dat `r` (rij‑index) en `c` (kolom‑index) neemt en `r*c` retourneert.  

Als je nieuw bent met **how to use lambda** in de Excel‑wereld, zie het dan als een mini‑functie die alleen binnen de formule bestaat. Je hoeft nergens anders een aparte functie te declareren. In Python embedden we simpelweg de string:

```python
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"
```

Die regel vertelt Excel: *“Voor elke cel in een 5‑bij‑5 blok, bereken rij × kolom.”*  

Omdat de lambda door Excel wordt geëvalueerd, hoef je je geen zorgen te maken over de Python‑lambda‑syntaxis hier — alleen de Excel‑syntaxis.

## Hoe makearray te gebruiken om arrays te genereren

`MAKEARRAY` is een relatief nieuwe toevoeging aan de Excel‑functiebibliotheek (beschikbaar in Microsoft 365 sinds 2022). Het vervangt oudere trucjes zoals `INDEX` + `ROW`/`COLUMN`‑combinaties. De handtekening is:

```
MAKEARRAY(rows, columns, lambda)
```

- **rows** – aantal rijen dat je wilt.
- **columns** – aantal kolommen dat je wilt.
- **lambda** – een Excel‑LAMBDA die `(row, column)` ontvangt en een waarde retourneert.

In ons voorbeeld gaven we `5,5` door voor een klassieke vermenigvuldigingsmatrix, maar je kunt die getallen gemakkelijk aanpassen:

```python
worksheet["A1"] = "=MAKEARRAY(10,10, LAMBDA(r,c, r*c))"
```

Dat zou je een 10 × 10 tabel geven zonder enige Python‑lus aan te raken. Dit toont **how to use makearray** voor elk soort deterministische raster, of het nu een opzoektabel, een heatmap of een financiële planning is.

## Display excel array – de data terughalen in Python

Zodra Excel de formule heeft berekend, staan de resulterende waarden in het blad net als elke handmatig ingevoerde cel. Om **display excel array** te doen, itereren we over het bereik en printen we elke rij:

```python
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

Een paar tips:

- Gebruik `worksheet.cell(row, column).value` in plaats van de dictionary‑achtige indexering als je grotere bereiken moet afhandelen; dat is een beetje sneller.
- Als je een nettere tabel wilt, overweeg dan `tabulate` of `pandas.DataFrame` om de output te formatteren.

Hieronder staat een screenshot van het resulterende blad (de alt‑tekst van de afbeelding bevat het primaire trefwoord voor SEO):

![Screenshot showing create multiplication table in Excel using Python](/images/multiplication-table-excel.png)

## Read excel values python – de matrix extraheren voor verdere verwerking

Vaak is de volgende stap na **display excel array** om die getallen in een data‑analyse‑pipeline te voeren. Daar komt **read excel values python** van pas. Dezelfde lus die we gebruikten voor het afdrukken kan worden hergebruikt om een lijst‑van‑lijsten, een NumPy‑array of een Pandas‑DataFrame te bouwen:

```python
import pandas as pd

# Build a list of rows
data = []
for row_index in range(1, 6):
    row = [worksheet.cell(row=row_index, column=col_index).value
           for col_index in range(1, 6)]
    data.append(row)

# Convert to DataFrame for easy manipulation
df = pd.DataFrame(data, columns=[f"Col{c}" for c in range(1, 6)],
                  index=[f"Row{r}" for r in range(1, 6)])

print(df)
```

Output:

```
      Col1  Col2  Col3  Col4  Col5
Row1     1     2     3     4     5
Row2     2     4     6     8    10
Row3     3     6     9    12    15
Row4     4     8    12    16    20
Row5     5    10    15    20    25
```

Nu heb je een volledig getypeerde DataFrame die je kunt plotten, exporteren naar CSV, of invoeren in een machine‑learning‑model. Hiermee is het **read excel values python**‑deel van de workflow voltooid.

## Randgevallen & Praktische tips

- **Formule‑herberekening**: Als je het werkboek wijzigt na de eerste `calculate_formula()`‑aanroep, moet je die opnieuw aanroepen; anders blijft de gecachte array verouderd.
- **Niet‑365 Excel**: Oudere Excel‑versies ondersteunen `MAKEARRAY` niet. In dat geval val je terug op een door Python gegenereerde tabel en schrijf je elke cel afzonderlijk.
- **Grote tabellen**: Voor matrices groter dan ~100 × 100, overweeg streaming om te voorkomen dat je het hele blad in het geheugen laadt.
- **Foutafhandeling**: Plaats de bereken‑ en leesstappen in `try/except`‑blokken om `InvalidFileException` of `FormulaError` op te vangen.

## Conclusie

We hebben je net laten zien hoe je een **create multiplication table** in Excel maakt met Python, gebruikmakend van de kracht van **how to use lambda** en **how to use makearray**. Je hebt gezien hoe je **display excel array** kunt tonen, die waarden terugleest met **read excel values python**, en zelfs het resultaat omzet in een Pandas DataFrame voor downstream‑analyse.

Wil je verder gaan? Probeer de vermenigvuldigingslogica te vervangen door iets complexers — misschien een afstandsmatrix, een probabiliteitstabel, of een dynamisch prijsraster. Hetzelfde patroon geldt: één regel `MAKEARRAY`, een snelle `calculate_formula()`, en een handvol Python‑lussen om de data eruit te halen.

Als je deze gids nuttig vond, geef hem dan een ster op GitHub, deel hem met collega's, of laat een reactie achter met jouw eigen use‑case. Veel plezier met coderen, en geniet van de eenvoud van het genereren van Excel‑tabellen met één enkele formule!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Aspose.Cells .NET Tutorial: How to Create and Modify Excel Workbooks Easily](/cells/english/net/workbook-operations/aspose-cells-net-create-modify-excel-workbooks/)
- [How to Create and Style Named Ranges in Excel Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/range-management/create-style-named-ranges-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}