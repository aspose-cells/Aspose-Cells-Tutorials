---
category: general
date: 2026-11-16
description: Skapa villkorsstyrd formatering i Excel med Python. Lär dig att lägga
  till ett villkorsstyrt formateringsområde, markera datum och bygga en arbetsbok
  programatiskt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: sv
lastmod: 2026-11-16
og_description: Skapa villkorsstyrd formatering i Excel med Python. Denna handledning
  visar hur man lägger till ett område för villkorsstyrd formatering, markerar datum
  och genererar en arbetsbok.
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: Skapa villkorsstyrd formatering i Excel med Python – steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Hur man skapar villkorsstyrd formatering i Excel med Python
url: /sv/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar villkorsstyrd formatering i Excel med Python

Om du behöver **skapa villkorsstyrd formatering** i en Excel‑fil medan du arbetar i Python visar den här guiden exakt hur du gör det. Du kommer att lära dig att **skapa excel workbook python**‑stil, definiera ett formateringsområde och markera datum utan att lämna IDE:n.

Villkorsstyrd formatering låter dig visuellt flagga celler som uppfyller specifika kriterier – perfekt för instrumentpaneler, rapporter eller datavalideringsblad. När du är klar med den här handledningen har du en fullt fungerande arbetsbok som färgar celler med datumet “Yesterday” i rosa medan resten av området förblir grönt.

## Vad du kommer att åstadkomma

* Bygga en ny arbetsbok från grunden.  
* Lägga till en villkorsstyrd‑format‑samling för ett specifikt cellblock.  
* Applicera en **TIME_PERIOD**‑regel som markerar datum (scenariot “hur man markerar datum”).  
* Spara filen som en XLSX‑arbetsbok redo för vidare bearbetning.

**Förutsättningar**  
* Python 3.8+  
* `aspose-cells` Python‑paket (`pip install aspose-cells`)  
* Grundläggande kunskap om Pythons `datetime`‑modul  

---

## Hur man skapar villkorsstyrd formatering i Python

Det första steget är att konfigurera arbetsboken och kalkylbladet som ska hysa formateringsreglerna.

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**Varför detta är viktigt** – `Workbook` är ingångspunkten för alla Excel‑operationer. Att skapa arbetsboken programatiskt ersätter det manuella steget “File → New” och möjliggör automatiserade rapportpipelines.

---

## Förbereda samlingen för villkorsstyrd formatering – lägg till formateringsområde

Nästa steg är att definiera cellblocket som ska få regeln. I detta exempel är området **I19:K20**.

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**Förklaring** – `conditional_formattings.add` registrerar en ny samling knuten till adresssträngen. Det första villkoret (`conds[0]`) fungerar som en “standard”‑stil; det senare villkoret kommer att åsidosätta det när dess kriterier uppfylls.

---

## Lägga till ett TIME_PERIOD‑villkor – hur man markerar datum

Nu lägger vi till den faktiska logiken som identifierar “Yesterday”‑datum och färgar dem rosa.

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**Varför använda TIME_PERIOD?** – Aspose.Cells tillhandahåller inbyggda uppräkningar som `YESTERDAY`, `TODAY` och `LAST_WEEK`. De utvärderar cellens datumvärde mot det aktuella systemdatumet och eliminerar behovet av anpassade formler.

---

## Fyll i exempeldata – demonstrera regeln

För att se formateringen i aktion infogar vi ett datum som matchar regeln och ett annat som inte gör det.

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**Obs om kantfall** – `TIME_PERIOD`‑regeln fungerar endast med *verkliga* datum. Om en cell innehåller text (t.ex. “N/A”) ignoreras regeln, vilket förhindrar oväntade färgändringar.

---

## Spara arbetsboken – add conditional formatting python

Till sist skriver vi arbetsboken till disk. Filen kan öppnas i vilket kalkylprogram som helst för att verifiera färgerna.

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**Förväntat resultat**  

| I19 (grön → rosa) | J19 (grön) | K19 (grön) |
|--------------------|------------|------------|
| 7/30/2008 (igår) | – | – |
| **I20**: “Igår”‑etikett | – | – |
| I21‑K21 (grön) | – | – |

Cellen **I19** visas med en rosa bakgrund eftersom dess datum matchar “Yesterday”‑perioden, medan **K20** förblir grön.

---

## Vanliga frågor och praktiska tips

* **Kan jag använda ett eget datumintervall istället för en inbyggd period?**  
  Ja. Ersätt `condition.time_period` med `condition.formula1 = "TODAY()-1"` och sätt `condition.type = FormatConditionType.FORMULA`.

* **Vad händer om min arbetsbok redan innehåller data?**  
  Använd `worksheet.cells.import_data` för att massladda data innan du lägger till samlingen för villkorsstyrd formatering.

* **Prestanda med stora blad?**  
  Att lägga till många villkor kan sakta ner rendering. Gruppera celler med samma regel i ett enda område (t.ex. “A1:C1000”) för att hålla antalet villkor lågt.

* **Plattformsoberoende kompatibilitet?**  
  Den genererade XLSX‑filen följer Office Open XML‑standarden, så den fungerar på Windows, macOS och Linux‑kalkylprogram.

---

## Slutsats

Du vet nu hur du **skapar villkorsstyrd formatering** i en Excel‑arbetsbok med Python. Handledningen täckte hur man skapar arbetsboken, definierar ett **add conditional formatting range**, applicerar en **how to highlight dates**‑regel och sparar filen – allt med **add conditional formatting python**‑metoden som tillhandahålls av Aspose.Cells.

Härifrån kan du:

* Utöka regelsetet med andra `TimePeriodType`‑värden (t.ex. `TODAY`, `LAST_MONTH`).  
* Kombinera flera villkor på samma område för rikare visuella ledtrådar.  
* Integrera detta arbetsflöde i automatiserade rapportpipelines eller webbtjänster.

Lycka till med kodandet, och experimentera gärna med olika färger, områden och datumlogik för att passa dina rapportbehov!

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Create Excel workbook Python date conditional formatting](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [How to apply time period conditional formatting in Excel using Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}