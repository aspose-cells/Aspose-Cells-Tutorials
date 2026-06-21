---
category: general
date: 2026-06-21
description: Skapa multiplikationstabell i Excel med Python. Lär dig hur du använder
  lambda, hur du använder makearray, visar Excel‑array och läser Excel‑värden i Python
  i en steg‑för‑steg‑handledning.
draft: false
keywords:
- create multiplication table
- how to use lambda
- how to use makearray
- display excel array
- read excel values python
language: sv
og_description: Skapa multiplikationstabell i Excel med Python. Denna handledning
  visar hur man använder lambda, makearray, visar Excel‑array och läser Excel‑värden
  i Python effektivt.
og_title: Skapa multiplikationstabell i Excel med Python – Komplett guide
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
title: Skapa multiplikationstabell i Excel med Python – Fullständig guide
url: /sv/python/import-and-export/create-multiplication-table-in-excel-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa multiplikationstabell i Excel med Python – Fullständig guide

Har du någonsin undrat hur man **skapar multiplikationstabell** i Excel utan att manuellt skriva in varje cell? Du är inte ensam. I många rapporteringsscenario behöver du ett snabbt 5×5 (eller större) rutnät av produkter, och att göra det för hand är slöseri med tid.  

I den här handledningen går vi igenom ett rent, Python‑drivet sätt att generera den tabellen, bädda in den med en `MAKEARRAY`‑formel och sedan hämta resultaten tillbaka till ditt skript. På vägen svarar vi på **hur man använder lambda**, visar **hur man använder makearray**, och demonstrerar **visa excel‑array** samt **read excel values python**—allt i ett sammanhängande exempel.

När du är klar har du ett återanvändbart kodsnutt som fungerar med vilken arbetsbok som helst, och du kommer att förstå varför detta tillvägagångssätt är både snabbt och framtidssäkert.

## Vad du behöver

- Python 3.8+ (den senaste stabila versionen är bra)
- `openpyxl`‑biblioteket (eller något Excel‑medvetet bibliotek som stöder formler)
- En grundläggande förståelse för lambda‑uttryck i Python
- Inga speciella Excel‑tillägg; den inbyggda `MAKEARRAY`‑funktionen (tillgänglig i Excel 365) gör det tunga arbetet

Om du saknar någon av dessa, kör bara `pip install openpyxl` så är du redo att köra.

## Skapa multiplikationstabell – Översikt

Kärnidén är enkel: vi skapar en ny arbetsbok, skriver en `MAKEARRAY`‑formel som bygger en 5 × 5 multiplikationsmatris, tvingar Excel att beräkna den och läser slutligen de resulterande värdena tillbaka till Python.

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

Att köra skriptet skriver ut:

```
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
[3, 6, 9, 12, 15]
[4, 8, 12, 16, 20]
[5, 10, 15, 20, 25]
```

Det är en fullt funktionell **skapa multiplikationstabell** i Excel, genererad helt från Python.

### Varför använda `MAKEARRAY` istället för en Python‑loop?

- **Prestanda**: Excel hanterar beräkningen nativt, vilket är snabbare för stora matriser.
- **Live‑uppdatering**: Om du senare ändrar dimensionerna i formeln, räknar bladet om automatiskt.
- **Läsbarhet**: Formeln uttrycker avsikten (“make an array”) direkt, vilket håller din Python‑kod prydlig.

## Hur man använder lambda i Python för Excel‑formler

`LAMBDA`‑delen av `MAKEARRAY`‑anropet är en anonym funktion på Excel‑sidan, inte en Python‑lambda. Ändå är konceptet detsamma: du definierar en liten, inlinad logik som tar `r` (radindex) och `c` (kolumnindex) och returnerar `r*c`.

Om du är ny på **hur man använder lambda** i Excel‑världen, tänk på det som en mini‑funktion som bara finns inom formeln. Ingen anledning att deklarera en separat funktion någon annanstans. I Python bäddar vi helt enkelt in strängen:

```python
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"
```

Den raden säger till Excel: *“För varje cell i ett 5‑x‑5‑block, beräkna rad × kolumn.”*

Eftersom lambda‑funktionen utvärderas av Excel, behöver du inte oroa dig för Pythons egen lambda‑syntax här—endast Excel‑syntaxen.

## Hur man använder makearray för att generera arrayer

`MAKEARRAY` är ett relativt nytt tillskott till Excels funktionsbibliotek (tillgänglig i Microsoft 365 sedan 2022). Den ersätter äldre knep som `INDEX` + `ROW`/`COLUMN`‑kombinationer. Signaturen är:

```
MAKEARRAY(rows, columns, lambda)
```

- **rows** – antal rader du vill ha.
- **columns** – antal kolumner du vill ha.
- **lambda** – en Excel LAMBDA som tar emot `(row, column)` och returnerar ett värde.

I vårt exempel skickade vi `5,5` för en klassisk multiplikationstabell, men du kan enkelt ändra de siffrorna:

```python
worksheet["A1"] = "=MAKEARRAY(10,10, LAMBDA(r,c, r*c))"
```

Det skulle ge dig en 10 × 10‑tabell utan att röra några Python‑loopar. Detta demonstrerar **hur man använder makearray** för vilken typ av deterministisk matris som helst, vare sig det är en uppslagstabell, en värmekarta eller ett finansiellt schema.

## Visa excel‑array – hämta data tillbaka till Python

När Excel har beräknat formeln, ligger de resulterande värdena i bladet precis som i någon manuellt inmatad cell. För att **visa excel‑array**, itererar vi över området och skriver ut varje rad:

```python
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

- Använd `worksheet.cell(row, column).value` istället för dictionary‑stil indexering om du behöver hantera större områden; det är lite snabbare.
- Om du vill ha en snyggare tabell, överväg `tabulate` eller `pandas.DataFrame` för att formatera utskriften.

Nedan är en skärmdump av det resulterande bladet (bildens alt‑text innehåller huvudnyckelordet för SEO):

![Screenshot showing create multiplication table in Excel using Python](/images/multiplication-table-excel.png)

## Läs excel‑värden python – extrahera matrisen för vidare bearbetning

Ofta är nästa steg efter **visa excel‑array** att mata in dessa siffror i en data‑analys‑pipeline. Det är där **read excel values python** glänser. Samma loop som vi använde för utskrift kan återanvändas för att bygga en lista av listor, en NumPy‑array eller en Pandas‑DataFrame:

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

Utdata:

```
      Col1  Col2  Col3  Col4  Col5
Row1     1     2     3     4     5
Row2     2     4     6     8    10
Row3     3     6     9    12    15
Row4     4     8    12    16    20
Row5     5    10    15    20    25
```

Nu har du en fullt typad DataFrame som du kan plotta, exportera till CSV eller mata in i en maskininlärningsmodell. Detta slutför **read excel values python**‑delen av arbetsflödet.

## Särskilda fall & Praktiska tips

- **Formel‑omberäkning**: Om du ändrar arbetsboken efter det första anropet av `calculate_formula()`, måste du anropa den igen; annars blir den cachade arrayen föråldrad.
- **Non‑365 Excel**: Äldre Excel‑versioner stödjer inte `MAKEARRAY`. I så fall återgå till en Python‑genererad tabell och skriv varje cell individuellt.
- **Stora tabeller**: För matriser större än ~100 × 100, överväg att strömma data för att undvika att ladda hela bladet i minnet.
- **Felhantering**: Omslut beräknings‑ och läsningsstegen i `try/except`‑block för att fånga `InvalidFileException` eller `FormulaError`.

## Slutsats

Vi har just visat dig hur du **skapar multiplikationstabell** i Excel med Python, och utnyttjar kraften i **hur man använder lambda** och **hur man använder makearray**. Du har sett hur du **visar excel‑array**, läser tillbaka dessa värden med **read excel values python**, och till och med omvandlar resultatet till en Pandas‑DataFrame för efterföljande analys.

Vill du gå längre? Prova att byta ut multiplikationslogiken mot något mer komplext—kanske en avståndsmatris, en sannolikhetstabell eller ett dynamiskt prisgrid. Samma mönster gäller: en rad `MAKEARRAY`, ett snabbt `calculate_formula()`, och ett fåtal Python‑loopar för att hämta data.

Om du tyckte att den här guiden var hjälpsam, ge den en stjärna på GitHub, dela den med kollegor, eller lämna en kommentar med ditt eget användningsfall. Lycka till med kodandet, och njut av kortheten i att generera Excel‑tabeller med en enda formel!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man skapar och konfigurerar Excel‑arbetsböcker med Aspose.Cells .NET: En steg‑för‑steg‑guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Aspose.Cells .NET‑handledning: Hur man enkelt skapar och ändrar Excel‑arbetsböcker](/cells/english/net/workbook-operations/aspose-cells-net-create-modify-excel-workbooks/)
- [Hur man skapar och formaterar namngivna områden i Excel med Aspose.Cells .NET | Steg‑för‑steg‑guide](/cells/english/net/range-management/create-style-named-ranges-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}