---
category: general
date: 2026-06-21
description: Schakel spellingscontrole in terwijl je Excel JSON exporteert met GridJs.
  Leer hoe je xlsx naar JSON converteert, lazy loading configureert en een Excel-werkmap
  efficiënt laadt.
draft: false
keywords:
- enable spell check
- export excel json
- convert xlsx to json
- configure lazy loading
- load excel workbook
language: nl
og_description: Schakel spellingscontrole in tijdens het exporteren van Excel JSON
  met GridJs. Deze gids laat zien hoe je xlsx naar JSON converteert, lazy loading
  configureert en een Excel-werkmap laadt.
og_title: Spellingscontrole inschakelen & Excel JSON exporteren met GridJs
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Enable spell check while you export Excel JSON using GridJs. Learn
    to convert xlsx to JSON, configure lazy loading, and load Excel workbook efficiently.
  headline: Enable Spell Check & Export Excel JSON with GridJs
  type: TechArticle
tags:
- GridJs
- Excel
- JSON
- Python
title: Spellingcontrole inschakelen & Export Excel JSON met GridJs
url: /nl/python/import-and-export/enable-spell-check-export-excel-json-with-gridjs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Spellingscontrole inschakelen & Excel JSON exporteren met GridJs

Heb je ooit **spellingscontrole** moeten inschakelen in een web‑gebaseerde spreadsheet‑UI en je afgevraagd hoe je de gegevens tegelijk als JSON kunt krijgen? Je bent niet de enige. Veel ontwikkelaars lopen tegen dezelfde muur wanneer ze proberen **Excel JSON te exporteren** vanuit een werkmap terwijl ze geavanceerde functies zoals formule‑validatie behouden.

In deze tutorial lopen we stap voor stap door een compleet, uitvoerbaar voorbeeld dat laat zien hoe je een **Excel‑werkmap laadt**, deze omzet naar een JSON‑payload met GridJs, **lazy loading configureert**, en natuurlijk **spellingscontrole inschakelt**. Aan het einde kun je **xlsx naar JSON converteren** in slechts een handvol regels—geen mysterie, geen ontbrekende stukjes.

> **Wat je zult meenemen**  
> * Een Python‑script dat een `.xlsx`‑bestand leest, een GridJs‑serverobject opzet, en `grid_data.json` schrijft.  
> * Inzicht in waarom elke optie belangrijk is (spellingscontrole, formule‑controle, lazy loading).  
> * Tips om de oplossing te schalen naar grotere werkmappen.

---

## Voorwaarden

Voordat we beginnen, zorg ervoor dat je het volgende op je machine hebt staan:

| Voorwaarde | Waarom het belangrijk is |
|------------|--------------------------|
| Python 3.9+ | Vereist voor de `cells`‑package die hieronder wordt gebruikt. |
| `cells`‑bibliotheek (`pip install cells`) | Biedt de klassen `Workbook` en `GridJs`. |
| Een voorbeeld‑Excel‑bestand (`sample.xlsx`) | Dit is de bron waarvan we de **excel workbook laden**. |
| Schrijfrechten voor de uitvoermap | Nodig voor de stap `grid.save()`. |

Als een van deze onbekend klinkt, pauzeer dan en installeer ze eerst—anders zal het script een import‑fout geven.

---

## Stap 1: Excel‑werkmap laden

Het allereerste wat je doet wanneer je **xlsx naar json wilt converteren** is de werkmap openen. Beschouw het als het ontgrendelen van de deur voordat je de kamer kunt inrichten.

```python
import cells

# Replace YOUR_DIRECTORY with the actual path on your system
workbook_path = "YOUR_DIRECTORY/sample.xlsx"

# Load the workbook – this is the entry point for all further operations
workbook = cells.Workbook(workbook_path)
print(f"Workbook loaded: {workbook_path}")
```

> **Pro tip:** Als je bestand enorm is, overweeg dan `cells.Workbook(..., read_only=True)` te gebruiken om het geheugenverbruik te verminderen.

---

## Stap 2: Een GridJs‑serverobject maken

Nu de werkmap in het geheugen staat, hebben we een **GridJs**‑object nodig dat de bladen vertaalt naar JSON die de client‑UI kan gebruiken.

```python
# Create a GridJs instance linked to the workbook
grid = cells.GridJs(workbook)
print("GridJs server object created.")
```

De variabele `grid` is in wezen een dunne wrapper rond de werkmap die weet hoe cellen, formules en zelfs opmaakinformatie geserialiseerd moeten worden.

---

## Stap 3: Spellingscontrole inschakelen (en Formule‑checker)

Hier komt het belangrijkste trefwoord tot leven. Door de vlag `enableSpellCheck` aan te zetten, geef je eindgebruikers een vangnet tegen typefouten—net zoals in Excel op de desktop.

```python
# Turn on advanced validation features
grid.options["enableFormulaChecker"] = True   # optional but handy
grid.options["enableSpellCheck"] = True       # <-- enable spell check
print("Spell check and formula checker enabled.")
```

Waarom beide inschakelen? Spellingscontrole vangt tekstuele fouten, terwijl de formule‑checker beschermt tegen kapotte berekeningen. Samen laten ze de web‑UI aanvoelen alsof het de native Excel‑ervaring is.

---

## Stap 4: Lazy Loading configureren

Als je met duizenden rijen werkt, zal het verzenden van de volledige dataset in één payload de browser overbelasten. **Configureer lazy loading** om gegevens in hapklare brokken (500 rijen per verzoek in ons voorbeeld) te versturen.

```python
# Lazy loading improves performance for large sheets
grid.options["lazyLoading"] = {"pageSize": 500}
print("Lazy loading configured: 500 rows per request.")
```

Je kunt `pageSize` aanpassen op basis van je netwerkomstandigheden. Kleinere pagina's betekenen meer round‑trips maar een soepelere UI; grotere pagina's verminderen het aantal oproepen maar kunnen vertraging veroorzaken.

---

## Stap 5: Excel JSON exporteren

Alle zware taken draaien nu op de achtergrond. De laatste stap is om **excel json te exporteren** naar een bestand dat je front‑end kan opvragen.

```python
# Destination for the generated JSON
output_path = "YOUR_DIRECTORY/grid_data.json"

# Persist the JSON representation
grid.save(output_path)
print(f"JSON exported to: {output_path}")
```

Wanneer de `save`‑methode voltooid is, heb je een nette `grid_data.json` die bevat:

* Bladnamen en ID’s  
* Rij‑data (waarden, formules en opmaak)  
* Metadata over ingeschakelde functies (spellingscontrole, lazy loading, enz.)

Je kunt de output verifiëren door het bestand te openen in een teksteditor of door het te laden in een browser‑console:

```json
{
  "sheets": [
    {
      "name": "Sheet1",
      "rows": [
        {"c": [{"v": "Hello"}, {"v": 123}]},
        {"c": [{"v": "World"}, {"v": 456}]}
      ]
    }
  ],
  "options": {
    "enableSpellCheck": true,
    "enableFormulaChecker": true,
    "lazyLoading": {"pageSize": 500}
  }
}
```

Dat is een **volledige, zelfstandige oplossing** om een Excel‑bestand om te zetten naar een JSON‑payload terwijl spellingscontrole actief blijft.

---

## Volledig script – Alles samenvoegen

Hieronder vind je het volledige programma dat je kunt kopiëren‑plakken, de paden aanpassen en uitvoeren. Geen verborgen stappen, geen externe scripts—slechts één bestand.

```python
import cells

# ----------------------------------------------------------------------
# Configuration – adjust these variables to match your environment
# ----------------------------------------------------------------------
WORKBOOK_PATH = "YOUR_DIRECTORY/sample.xlsx"
OUTPUT_JSON = "YOUR_DIRECTORY/grid_data.json"
PAGE_SIZE = 500   # rows per lazy‑load request

# ----------------------------------------------------------------------
# 1️⃣ Load the Excel workbook
# ----------------------------------------------------------------------
workbook = cells.Workbook(WORKBOOK_PATH)
print(f"[✓] Loaded workbook from {WORKBOOK_PATH}")

# ----------------------------------------------------------------------
# 2️⃣ Create GridJs server object
# ----------------------------------------------------------------------
grid = cells.GridJs(workbook)
print("[✓] GridJs instance ready")

# ----------------------------------------------------------------------
# 3️⃣ Enable spell check + formula checking
# ----------------------------------------------------------------------
grid.options["enableFormulaChecker"] = True
grid.options["enableSpellCheck"] = True
print("[✓] Spell check and formula checker enabled")

# ----------------------------------------------------------------------
# 4️⃣ Configure lazy loading for performance
# ----------------------------------------------------------------------
grid.options["lazyLoading"] = {"pageSize": PAGE_SIZE}
print(f"[✓] Lazy loading set to {PAGE_SIZE} rows per request")

# ----------------------------------------------------------------------
# 5️⃣ Export the workbook as JSON
# ----------------------------------------------------------------------
grid.save(OUTPUT_JSON)
print(f"[✓] Exported JSON to {OUTPUT_JSON}")
```

Sla dit op als `export_gridjs.py` en voer uit:

```bash
python export_gridjs.py
```

Je zou een reeks `[✓]`‑berichten moeten zien die bevestigen dat elke stap geslaagd is.

---

## Veelgestelde vragen & randgevallen

**Wat als mijn werkmap meerdere bladen bevat?**  
GridJs doorloopt automatisch elk blad, dus de resulterende JSON bevat een `sheets`‑array. Je kunt aan de client‑kant filteren als je slechts een subset nodig hebt.

**Kan ik spellingscontrole uitschakelen voor een specifiek blad?**  
Het `options`‑dictionary geldt globaal. Om per blad te schakelen, moet je aparte `GridJs`‑objecten maken of de JSON naverwerken.

**Mijn bestand is groter dan 10 MB—helpt lazy loading nog steeds?**  
Absoluut. Lazy loading werkt op API‑niveau; de server streamt alleen de gevraagde pagina. Overweeg echter `pageSize` te verhogen naar 1000 als je netwerklatentie laag is.

**Moet ik me zorgen maken over Unicode‑tekens?**  
`cells` verwerkt UTF‑8 standaard, dus tekens zoals emoji’s of niet‑Latijnse scripts overleven de round‑trip.

---

## Pro‑tips voor productie

* **Cache de JSON** – Als de werkmap zelden verandert, cache `grid_data.json` in een CDN voor bliksemsnelle laadtijden.  
* **Beveiliging** – Exposeer nooit het ruwe Excel‑bestand; serveer alleen de gegenereerde JSON.  
* **Versiebeheer** – Voeg een versienummer toe aan de JSON‑bestandsnaam (bijv. `grid_data_v2.json`) om verouderde data na updates te vermijden.  
* **Testen** – Schrijf een kleine unit‑test die de JSON laadt en controleert dat `enableSpellCheck` `true` is. Zo vang je regressies vroegtijdig.

---

## Conclusie

Je hebt nu een solide, end‑to‑end recept om **spellingscontrole in te schakelen** terwijl je **Excel JSON exporteert** met GridJs. Van **excel workbook laden** tot **lazy loading configureren** en uiteindelijk **xlsx naar json converteren**, het proces is eenvoudig en klaar voor productie.

Volgende stappen? Probeer het gegenereerde `grid_data.json` te gebruiken in een eenvoudige HTML‑pagina die de GridJs‑clientbibliotheek laadt, experimenteer met aangepaste cel‑renderers, of voeg authenticatie toe rond het JSON‑endpoint. De mogelijkheden zijn eindeloos wanneer je spellingscontrole, lazy loading en naadloze Excel‑naar‑JSON‑conversie combineert.

Heb je meer vragen of een lastige werkmap waar je mee worstelt? Laat een reactie achter, en happy coding!  

---

![Spellingscontrole inschakelen in GridJs](/images/enable-spell-check-gridjs.png "Screenshot showing spell check enabled in GridJs UI")


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Export Excel to JSON](/cells/english/java/excel-import-export/export-excel-to-json/)
- [Import JSON Data into Excel Using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [How to Efficiently Filter Data While Loading Excel Workbooks Using Aspose.Cells in Java](/cells/english/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}