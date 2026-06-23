---
category: general
date: 2026-06-21
description: Aktivera stavningskontroll när du exporterar Excel JSON med GridJs. Lär
  dig konvertera xlsx till JSON, konfigurera lazy loading och ladda Excel‑arbetsboken
  effektivt.
draft: false
keywords:
- enable spell check
- export excel json
- convert xlsx to json
- configure lazy loading
- load excel workbook
language: sv
og_description: Aktivera stavningskontroll vid export av Excel JSON med GridJs. Denna
  guide visar hur du konverterar xlsx till JSON, konfigurerar lazy loading och laddar
  en Excel-arbetsbok.
og_title: Aktivera stavningskontroll och exportera Excel JSON med GridJs
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
title: Aktivera stavningskontroll och exportera Excel JSON med GridJs
url: /sv/python/import-and-export/enable-spell-check-export-excel-json-with-gridjs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aktivera stavningskontroll & exportera Excel JSON med GridJs

Har du någonsin behövt **enable spell check** i ett web‑baserat kalkylblads‑UI och undrat hur du samtidigt får ut data som JSON? Du är inte ensam. Många utvecklare stöter på samma problem när de försöker **export Excel JSON** från en arbetsbok samtidigt som avancerade funktioner som formelvalidering hålls aktiva.

I den här handledningen går vi igenom ett komplett, körbart exempel som visar hur du **load Excel workbook**, omvandlar den till en JSON‑payload med GridJs, **configure lazy loading**, och naturligtvis **enable spell check**. I slutet kan du **convert xlsx to JSON** på bara några få rader—ingen gåta, inga saknade bitar.

> **What you’ll walk away with**  
> * Ett Python‑skript som läser en `.xlsx`‑fil, startar ett GridJs‑serverobjekt och skriver `grid_data.json`.  
> * Förståelse för varför varje alternativ är viktigt (stavningskontroll, formelkontroll, lazy loading).  
> * Tips för att skala lösningen till större arbetsböcker.

---

## Förutsättningar

Innan vi dyker ner, se till att du har följande på din maskin:

| Krav | Varför det är viktigt |
|------|-----------------------|
| Python 3.9+ | Krävs för `cells`‑paketet som används nedan. |
| `cells`‑bibliotek (`pip install cells`) | Tillhandahåller klasserna `Workbook` och `GridJs`. |
| En exempel‑Excel‑fil (`sample.xlsx`) | Detta är källan vi **load excel workbook** från. |
| Skrivbehörighet till utmatningsmappen | Behövs för steget `grid.save()`. |

Om något av detta känns obekant, pausa och installera det först—annars kommer skriptet att ge ett importfel.

---

## Steg 1: Ladda Excel‑arbetsbok

Det allra första du gör när du vill **convert xlsx to json** är att öppna arbetsboken. Tänk på det som att låsa upp dörren innan du kan inreda rummet.

```python
import cells

# Replace YOUR_DIRECTORY with the actual path on your system
workbook_path = "YOUR_DIRECTORY/sample.xlsx"

# Load the workbook – this is the entry point for all further operations
workbook = cells.Workbook(workbook_path)
print(f"Workbook loaded: {workbook_path}")
```

> **Pro tip:** Om din fil är enorm, överväg att använda `cells.Workbook(..., read_only=True)` för att minska minnesförbrukningen.

---

## Steg 2: Skapa ett GridJs‑serverobjekt

Nu när arbetsboken finns i minnet behöver vi ett **GridJs**‑objekt som översätter bladen till JSON som klient‑UI‑en kan konsumera.

```python
# Create a GridJs instance linked to the workbook
grid = cells.GridJs(workbook)
print("GridJs server object created.")
```

Variabeln `grid` är i princip ett tunt skal runt arbetsboken som vet hur man serialiserar celler, formler och även stilinformation.

---

## Steg 3: Aktivera stavningskontroll (och formelkontroll)

Här kommer huvudnyckelordet i spel. Genom att slå på flaggan `enableSpellCheck` ger du slutanvändarna ett skyddsnät mot stavfel—precis som i Excel‑desktop.

```python
# Turn on advanced validation features
grid.options["enableFormulaChecker"] = True   # optional but handy
grid.options["enableSpellCheck"] = True       # <-- enable spell check
print("Spell check and formula checker enabled.")
```

Varför aktivera båda? Stavningskontrollen fångar textfel, medan formelkontrollen skyddar mot brutna beräkningar. Tillsammans får web‑UI‑en en lika polerad känsla som den inhemska Excel‑upplevelsen.

---

## Steg 4: Konfigurera lazy loading

Om du hanterar tusentals rader kommer det att kväva webbläsaren att skicka hela datasetet i en enda payload. **Configure lazy loading** för att skicka data i bit‑stora portioner (500 rader per begäran i vårt exempel).

```python
# Lazy loading improves performance for large sheets
grid.options["lazyLoading"] = {"pageSize": 500}
print("Lazy loading configured: 500 rows per request.")
```

Du kan justera `pageSize` baserat på dina nätverksförhållanden. Mindre sidor betyder fler rundresor men mjukare UI; större sidor minskar anrop men kan orsaka fördröjning.

---

## Steg 5: Exportera Excel JSON

All tungt arbete är nu bakom kulisserna. Den sista akten är att **export excel json** till en fil som ditt front‑end kan begära.

```python
# Destination for the generated JSON
output_path = "YOUR_DIRECTORY/grid_data.json"

# Persist the JSON representation
grid.save(output_path)
print(f"JSON exported to: {output_path}")
```

När `save`‑metoden är klar har du en prydlig `grid_data.json` som innehåller:

* Bladnamn och ID:n  
* Raddata (värden, formler och formatering)  
* Metadata om aktiverade funktioner (stavningskontroll, lazy loading, osv.)

Du kan verifiera utdata genom att öppna filen i en textredigerare eller ladda den i en webbläsarkonsol:

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

Det är en **complete, self‑contained solution** för att omvandla en Excel‑fil till en JSON‑payload samtidigt som stavningskontrollen förblir aktiv.

---

## Fullt skript – Sätt ihop allt

Nedan är hela programmet som du kan kopiera‑klistra, justera sökvägarna och köra. Inga dolda steg, inga externa skript—bara en fil.

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

Spara detta som `export_gridjs.py` och kör:

```bash
python export_gridjs.py
```

Du bör se en rad `[✓]`‑meddelanden som bekräftar att varje steg lyckades.

---

## Vanliga frågor & kantfall

**Vad händer om min arbetsbok innehåller flera blad?**  
GridJs itererar automatiskt över varje blad, så den resulterande JSON‑en får en `sheets`‑array. Du kan filtrera på klientsidan om du bara behöver ett delmängd.

**Kan jag inaktivera stavningskontroll för ett specifikt blad?**  
`options`‑dictionaryn gäller globalt. För att växla per blad måste du skapa separata `GridJs`‑objekt eller efterbearbeta JSON‑en.

**Min fil är större än 10 MB—hjälper lazy loading fortfarande?**  
Absolut. Lazy loading fungerar på API‑nivå; servern strömmar bara den begärda sidan. Överväg dock att öka `pageSize` till 1000 om din nätverkslatens är låg.

**Måste jag oroa mig för Unicode‑tecken?**  
`cells` hanterar UTF‑8 direkt, så tecken som emojis eller icke‑latinska skript klarar rundresan.

---

## Pro‑tips för produktion

* **Cachea JSON** – Om arbetsboken sällan förändras, cachea `grid_data.json` i ett CDN för blixtsnabb laddning.  
* **Säkerhet** – Exponera aldrig den råa Excel‑filen; servera bara den genererade JSON‑en.  
* **Versionering** – Inkludera ett versionsnummer i JSON‑filnamnet (t.ex. `grid_data_v2.json`) för att undvika föråldrad data efter uppdateringar.  
* **Testning** – Skriv ett litet enhetstest som laddar JSON och kontrollerar att `enableSpellCheck` är `true`. Det fångar regressioner tidigt.

---

## Slutsats

Du har nu ett robust, end‑to‑end‑recept för att **enable spell check** medan du **export Excel JSON** med GridJs. Från **load excel workbook** till **configure lazy loading** och slutligen **convert xlsx to json**, är processen enkel och redo för produktion.

Nästa steg? Prova att plugga in den genererade `grid_data.json` i en enkel HTML‑sida som använder GridJs‑klientbiblioteket, experimentera med egna cell‑renderare, eller lägg till autentisering kring JSON‑endpointen. Himlen är gränsen när du kombinerar stavningskontroll, lazy loading och sömlös Excel‑till‑JSON‑konvertering.

Har du fler frågor eller en knepig arbetsbok du kämpar med? Lämna en kommentar nedan, och lycka till med kodandet!  

---

![Aktivera stavningskontroll i GridJs](/images/enable-spell-check-gridjs.png "Skärmbild som visar stavningskontroll aktiverad i GridJs UI")


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Export Excel to JSON](/cells/english/java/excel-import-export/export-excel-to-json/)
- [Import JSON Data into Excel Using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [How to Efficiently Filter Data While Loading Excel Workbooks Using Aspose.Cells in Java](/cells/english/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}