---
category: general
date: 2026-06-21
description: Maak een dynamische array met Python en de SEQUENCE-functie in Excel.
  Leer de formule‑resultaten lezen, Excel‑formules opnieuw berekenen en bekijk een
  voorbeeld van de Excel SEQUENCE‑functie.
draft: false
keywords:
- create dynamic array
- sequence function excel
- read formula result
- recalculate excel formulas
- excel sequence example
language: nl
og_description: Maak een dynamische array in Excel met Python. Deze tutorial laat
  zien hoe je de SEQUENCE-functie gebruikt, Excel-formules opnieuw berekent en het
  resultaat van een formule uitleest.
og_title: Dynamische array maken in Excel met Python – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create dynamic array using Python and the SEQUENCE function in Excel.
    Learn to read formula result, recalculate Excel formulas, and see an Excel SEQUENCE
    example.
  headline: Create Dynamic Array in Excel with Python – Step‑by‑Step Guide
  type: TechArticle
tags:
- excel
- python
- xlwings
- dynamic arrays
title: Dynamische array maken in Excel met Python – Stapsgewijze handleiding
url: /nl/python/import-and-export/create-dynamic-array-in-excel-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dynamische Array maken in Excel met Python – Complete Gids

Heb je je ooit afgevraagd hoe je **dynamic array**‑formules in Excel kunt maken zonder je Python‑script te verlaten? Je bent niet de enige. Of je nu een maandelijkse rapport automatiseert of een lichtgewicht data‑engine bouwt, het kunnen invoegen van een `SEQUENCE`‑formule in een werkmap, opnieuw berekenen, en het spill‑bereik terughalen naar Python is een game‑changer.

In deze tutorial lopen we een real‑world **excel sequence example** stap voor stap door, laten we je zien hoe je **read formula result** kunt doen, en leggen we de beste manier uit om **recalculate excel formulas** uit te voeren nadat je nieuwe logica hebt geïnjecteerd. Aan het einde heb je een zelfstandige script die je kunt kopiëren‑plakken, uitvoeren, en aanpassen aan je eigen behoeften.

## Wat je zult leren

- Hoe de `SEQUENCE`‑functie werkt en waarom hij perfect is voor het genereren van matrices.
- Het verschil tussen een gewone celwaarde en een spill‑bereik‑adres.
- Gebruik van `wb.calculate_formula()` (of het equivalent) om Excel te dwingen nieuwe formules te evalueren.
- Het extraheren van het adres van een dynamische array met `ANCHORARRAY`.
- Een volledige, uitvoerbare Python‑voorbeeld die je in elk project kunt gebruiken.

Ervaring met Excel’s nieuwe dynamic‑array engine is niet vereist—alleen een basiskennis van Python en een bibliotheek zoals **xlwings** die met Excel kan communiceren.

---

## Hoe een dynamische array te maken met SEQUENCE in Excel met Python

De eerste stap is om een **dynamic array**‑formule direct in een werkbladcel te schrijven. In moderne Excel kan de `SEQUENCE`‑functie een matrix van getallen on-the-fly genereren. Hier is de syntaxis die we gaan gebruiken:

```python
# Step 1: Write a dynamic array formula that generates a 3×2 matrix starting at 10 with step 5
ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"   # Returns a 3×2 array
```

**Why `SEQUENCE`?**  
Beschouw het als Excel’s ingebouwde `range()` voor spreadsheets. Het laat je rijen, kolommen, een startwaarde en een stapgrootte opgeven — allemaal in één nette regel. In ons geval vragen we om 3 rijen en 2 kolommen, beginnend bij 10 en stapend met 5, wat oplevert:

|   | A | B |
|---|---|---|
|1|10|15|
|2|20|25|
|3|30|35|

Omdat de formule in `A1` staat, spilt Excel automatisch het resultaat uit naar de aangrenzende cellen `A1:B3`. Die spill is wat we later zullen ophalen.

---

## De SEQUENCE‑functie gebruiken in Excel – Een snel Excel‑sequence‑voorbeeld

Als je Excel handmatig opent en `=SEQUENCE(3,2,10,5)` in een cel typt, zie je dezelfde matrix onmiddellijk verschijnen. De functie maakt deel uit van Excel’s **dynamic array**‑engine geïntroduceerd in Office 365, wat betekent:

- Geen Ctrl+Shift+Enter nodig.
- Het resultaat kan automatisch uitbreiden of krimpen.
- Je kunt het volledige spill‑bereik refereren met functies zoals `@` of `#`.

In Python is het enige verschil dat we de formule als een string toewijzen aan de `.formula`‑eigenschap van de cel. De bibliotheek regelt de rest.

---

## Het spill‑bereik‑adres ophalen met ANCHORARRAY

Zodra de dynamische array op zijn plaats staat, moet je vaak weten waar Excel de waarden daadwerkelijk heeft geplaatst. Daar komt `ANCHORARRAY` van pas. Het retourneert het adres van de boven‑linker cel van het spill‑bereik — precies wat we nodig hebben om terug in ons script te lezen.

```python
# Step 2: Retrieve the address of the spill range produced by the formula in A1
ws.cells["C1"].formula = "=ANCHORARRAY(A1)"      # Returns the address of the spill range
```

Deze formule in `C1` plaatsen geeft ons een tekststring zoals "A1:B3". Merk op dat we **reading the formula result** als een gewone waarde lezen, niet als een andere formule. Deze kleine truc vermijdt de noodzaak om het werkblad handmatig te parseren.

---

## Excel‑formules opnieuw berekenen en het resultaat lezen

Excel rekent niet altijd meteen opnieuw wanneer een nieuwe formule vanuit een extern script wordt geïnjecteerd. Om te garanderen dat de werkmap de laatste wijzigingen weergeeft, activeren we expliciet een berekeningsstap.

```python
# Step 3: Recalculate all formulas in the workbook and read the result
wb.calculate_formula()               # Forces Excel to evaluate pending formulas
print(ws.cells["C1"].value)          # → "A1:B3"
```

**Why call `calculate_formula()`?**  
Als je deze stap overslaat, kan `ws.cells["C1"].value` nog steeds `None` of een oud adres retourneren omdat Excel nog bezig is met het bijwerken van de afhankelijkheidsboom. Door een herberekening af te dwingen, zorgen we ervoor dat de **read formula result** up‑to‑date is.

---

## Volledig script – Van begin tot eind

Hieronder staat een volledig, kant‑klaar voorbeeld dat alles samenbrengt. Het gaat ervan uit dat je **xlwings** geïnstalleerd hebt (`pip install xlwings`) en dat Excel beschikbaar is op je machine.

```python
import xlwings as xw

def create_dynamic_array_example():
    # Open a new workbook (or attach to an existing one)
    wb = xw.Book()               # Creates a fresh Excel workbook
    ws = wb.sheets[0]            # Grab the first worksheet

    # 1️⃣ Write the SEQUENCE formula – this creates a 3×2 matrix starting at 10, step 5
    ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"

    # 2️⃣ Use ANCHORARRAY to capture the spill range address in C1
    ws.cells["C1"].formula = "=ANCHORARRAY(A1)"

    # 3️⃣ Force Excel to recalculate so that the ANCHORARRAY result is current
    wb.calculate_formula()

    # 4️⃣ Read back the address – this is our **read formula result** step
    spill_address = ws.cells["C1"].value
    print(f"The dynamic array spills into: {spill_address}")

    # 5️⃣ Optionally, fetch the actual values from the spill range
    # xlwings can read a range by address, so we demonstrate that too
    data = ws.range(spill_address).value
    print("Matrix values:")
    for row in data:
        print(row)

    # Clean up – close without saving to keep the demo tidy
    wb.close(save=False)

if __name__ == "__main__":
    create_dynamic_array_example()
```

### Verwachte output

```
The dynamic array spills into: A1:B3
Matrix values:
[10, 15]
[20, 25]
[30, 35]
```

Het uitvoeren van het script opent Excel, injecteert de `SEQUENCE`‑formule, rekent opnieuw, en print vervolgens zowel het spill‑adres als de matrix zelf. Geen handmatige klikken nodig.

---

## Veelvoorkomende valkuilen en pro‑tips

- **Valkuil:** Het vergeten van `wb.calculate_formula()`.  
  *Resultaat:* `C1` blijft leeg of toont een verouderd adres.  
  *Oplossing:* Altijd een berekening activeren na het schrijven van nieuwe formules.

- **Valkuil:** Een oudere versie van Excel gebruiken die de `SEQUENCE`‑functie niet heeft.  
  *Resultaat:* `#NAME?`‑fout.  
  *Oplossing:* Zorg dat je Office 365 of Excel 2021+ hebt.

- **Pro‑tip:** Als je het spill‑bereik nodig hebt voor verdere verwerking (bijv. grafieken), kun je het adres direct invoeren in `ws.range(spill_address)` zoals hierboven getoond.

- **Pro‑tip:** `ANCHORARRAY` werkt met elke dynamische array, niet alleen met `SEQUENCE`. Vervang door `=SORT(A2:A10)` of `=FILTER(...)` en je krijgt nog steeds het juiste spill‑adres.

- **Randgeval:** Wanneer het doelgebied al bezet is, geeft Excel een `#SPILL!`‑fout. In dat geval, maak eerst het bestemmingsbereik leeg of verplaats de formule naar een andere cel.

---

## Voorbeeld uitbreiden – Wat nu?

Nu je weet hoe je **create dynamic array**‑formules, **read formula result**, en **recalculate excel formulas** maakt, kun je meer geavanceerde scenario's verkennen:

- **Dynamische chart‑data** – voer een spill‑bereik in als chart‑bron en laat de chart automatisch groeien.
- **Voorwaardelijke opmaak** – pas regels toe op het spill‑bereik met behulp van het adres.
- **Cross‑workbook referenties** – schrijf een dynamische array in één werkmap en haal de gegevens op in een andere via `xlwings`‑links.

Elk van deze bouwt voort op de kernconcepten die hier behandeld zijn, dus voel je vrij om te experimenteren. De enige beperking is je verbeelding (en misschien de maximale rijen/kolommen van Excel).

---

## Conclusie

We hebben zojuist een volledige workflow doorlopen om **create dynamic array**‑formules in Excel vanuit Python te maken, de **SEQUENCE function excel** te gebruiken, het spill‑bereik op te halen met **ANCHORARRAY**, **recalculate excel formulas** uit te voeren, en uiteindelijk **read formula result** terug te lezen in je script. Het korte voorbeeld toont hoe krachtig Excel’s nieuwe dynamic‑array engine kan zijn in combinatie met automatiseringstools zoals **xlwings**.

Probeer het in je eigen projecten, pas de matrixdimensies aan, of vervang `SEQUENCE` door een andere dynamische functie. Naarmate je meer vertrouwd raakt, zul je merken dat het automatiseren van Excel niet alleen mogelijk, maar ook aangenaam eenvoudig wordt.

Heb je vragen of wil je delen hoe je dit patroon hebt uitgebreid? Laat een reactie achter hieronder, en happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Gegevens verwerken met Array‑functie in Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)
- [Dynamische lijndiagrammen maken in Excel met Aspose.Cells voor .NET: Een stap‑voor‑stap gids](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [Dynamische Excel‑grafieken maken met Aspose.Cells Java: Een uitgebreide gids voor ontwikkelaars](/cells/english/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}