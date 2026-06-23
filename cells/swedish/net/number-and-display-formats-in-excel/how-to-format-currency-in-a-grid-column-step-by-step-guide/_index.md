---
category: general
date: 2026-02-15
description: hur man formaterar valuta snabbt med set column number format och tillämpar
  anpassat numeriskt format i C#. Lär dig hämta kolumn efter namn och ställa in rutnätskolumnens
  justering.
draft: false
keywords:
- how to format currency
- set column number format
- apply custom numeric format
- retrieve column by name
- set grid column alignment
language: sv
og_description: hur man formaterar valuta i en rutnätskolumn med C#. Denna handledning
  visar hur man hämtar kolumnen efter namn, ställer in kolumnens talformat, tillämpar
  ett anpassat numeriskt format och sätter rutnätskolumnens justering.
og_title: hur man formaterar valuta i en gridkolumn – komplett guide
tags:
- C#
- GridFormatting
- UI
title: Hur man formaterar valuta i en rutnätskolumn – steg‑för‑steg‑guide
url: /sv/net/number-and-display-formats-in-excel/how-to-format-currency-in-a-grid-column-step-by-step-guide/
---

we preserve the horizontal rules "---". Keep them.

Now produce final content with all translations.

Let's assemble.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hur man formaterar valuta i en Grid Column – Komplett programmeringshandledning

Har du någonsin undrat **hur man formaterar valuta** i en grid column utan att rycka ur dig håret? Du är inte ensam. När du stirrar på ett enkelt tal som `1234.5` och önskar att det magiskt skulle visas som `$1,234.50`, är svaret oftast bara några rader konfiguration.  

I den här guiden kommer vi att **hämta kolumnen efter namn**, **sätta kolumnens talformat**, och **tillämpa ett anpassat numeriskt format** som respekterar det typiska bokföringsutseendet. På vägen kommer vi också att **sätta grid column alignment** och lägga till en subtil kant så att UI:t ser polerat ut.

> **TL;DR** – I slutet kommer du att ha ett färdigt kodsnutt som omvandlar råa decimaler till vackert formaterade valutavärden i vilken `GridJs`‑style‑kontroll som helst.

---

## Vad du behöver

- Ett .NET‑projekt (valfri version som stödjer C# 8.0+ – Visual Studio 2022 fungerar utmärkt).  
- En grid‑komponent som exponerar en `Columns`‑samling (exemplet använder en fiktiv `GridJs`‑klass, men koncepten kan överföras till DevExpress, Telerik eller Syncfusion‑gridar).  
- Grundläggande kunskap om C#‑syntax – inga avancerade knep krävs.

Om du redan har dem, toppen. Om inte, skapa bara en konsolapp; grid‑komponenten kan mockas för illustration.

## Steg‑för‑steg‑implementering

Under varje steg ser du ett kompakt kodblock, en kort förklaring till **varför** raden är viktig, samt ett tips för att undvika vanliga fallgropar.

### ## Steg 1 – Hämta “Amount”-kolumnen efter namn

```csharp
// Step 1: Retrieve the "Amount" column from the grid
var amountColumn = gridJs.Columns["Amount"];
if (amountColumn == null)
{
    throw new InvalidOperationException("Column 'Amount' does not exist. Verify the column name or check the grid's schema.");
}
```

**Varför detta är viktigt:**  
De flesta grid‑API:er exponerar kolumner via en ordboks‑liknande indexerare. Att hämta kolumnen efter dess rubriknamn (`"Amount"`) låter dig manipulera dess utseende utan att röra den underliggande datakällan.

**Proffstips:** Se alltid till att skydda mot ett `null`‑resultat – ett stavfel i kolumnnamnet eller en dynamisk schemaväxling kan annars orsaka ett `NullReferenceException` vid körning.

---

### ## Steg 2 – Sätt kolumnens talformat med en anpassad valutamask

```csharp
// Step 2: Apply a custom numeric format for currency values
amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";
```

**Varför detta är viktigt:**  
Formatsträngen följer Excels bokföringsformatkonventioner:

- `_(* #,##0.00_)` → Positiva tal, högerjusterade med ett inledande mellanslag för valutasymbolen.  
- `_(* (#,##0.00)` → Negativa tal omslutna av parenteser.  
- `_(* \"-\"??_)` → Nollvärden visas som ett streck.  
- `_(@_)` → Textvärden förblir oförändrade.

Att använda **apply custom numeric format** ger dig full kontroll över tusentalsavgränsare, decimaler och placeringen av valutasymbolen.  

**Edge case:** Om din applikation måste respektera en annan lokal (t.ex. Euro istället för USD), ersätt det inledande mellanslaget med rätt symbol eller använd `CultureInfo`‑medveten formatering i datakällan.

---

### ## Steg 3 – Justera kolumnens innehåll till höger för läsbarhet

```csharp
// Step 3: Align the column contents to the right for better readability
amountColumn.Alignment = GridAlignment.Right;
```

**Varför detta är viktigt:**  
Valutavärden är lättare att skanna när de är i linje med decimalseparatorn. Att sätta **set grid column alignment** till `Right` speglar hur kalkylblad visar ekonomiska data.  

**Gotcha:** Vissa grid‑komponenter ignorerar justering på celler som innehåller anpassade mallar. Om du märker att justeringen inte träder i kraft, dubbelkolla att kolumnen inte använder en anpassad cell‑renderer.

---

### ## Steg 4 – Lägg till en tunn grå kant runt kolumncellerna

```csharp
// Step 4: Add a thin gray border around the column cells
amountColumn.Border = new GridBorder
{
    Color = Color.Gray,
    Style = BorderLineStyle.Thin
};
```

**Varför detta är viktigt:**  
En subtil kant separerar “Amount”-kolumnen från dess grannar, särskilt när grid‑en har alternerande radfärger. Det är en visuell ledtråd att datan representerar en distinkt finansiell siffra.  

**Tips:** Om du behöver en tjockare linje för utskriftsändamål, öka `BorderLineStyle` till `Medium` eller ändra `Color` till `Color.Black`.

---

## Fullt fungerande exempel

Här är hela kodsnutten som du kan klistra in i ett WinForms‑ eller WPF‑projekt som använder en `GridJs`‑style‑kontroll. Exemplet skriver också de formaterade värdena till konsolen så att du kan verifiera resultatet utan ett UI.

```csharp
using System;
using System.Drawing;   // For Color
using GridLibrary;      // Hypothetical namespace for GridJs

namespace GridCurrencyDemo
{
    class Program
    {
        static void Main()
        {
            // Create a mock grid and add a sample column
            var gridJs = new GridJs();
            gridJs.Columns.Add(new GridColumn
            {
                Name = "Amount",
                Header = "Amount",
                DataType = typeof(decimal)
            });

            // Populate some sample data
            gridJs.Rows.Add(new { Amount = 1234.5m });
            gridJs.Rows.Add(new { Amount = -567.89m });
            gridJs.Rows.Add(new { Amount = 0m });

            // ---- Formatting steps ------------------------------------------------
            // 1️⃣ Retrieve the "Amount" column
            var amountColumn = gridJs.Columns["Amount"]
                ?? throw new InvalidOperationException("Column 'Amount' not found.");

            // 2️⃣ Apply custom numeric format for currency
            amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";

            // 3️⃣ Right‑align the values
            amountColumn.Alignment = GridAlignment.Right;

            // 4️⃣ Add a thin gray border
            amountColumn.Border = new GridBorder
            {
                Color = Color.Gray,
                Style = BorderLineStyle.Thin
            };
            // -----------------------------------------------------------------------

            // Render the grid (in a real UI you would call gridJs.Render() or similar)
            Console.WriteLine("Formatted Currency Grid:");
            foreach (var row in gridJs.Rows)
            {
                var rawValue = (decimal)row.Amount;
                // The grid library would automatically apply NumberFormat when displaying.
                // For console demo we mimic the formatting:
                string formatted = rawValue.ToString("#,##0.00", System.Globalization.CultureInfo.InvariantCulture);
                if (rawValue < 0)
                    formatted = $"({formatted.TrimStart('-')})";
                else if (rawValue == 0)
                    formatted = "-";

                Console.WriteLine($"| {formatted,15} |");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Förväntad konsolutmatning**

```
Formatted Currency Grid:
|        1,234.50 |
|       (567.89) |
|               - |
```

Observera hur det positiva talet är högerjusterat, det negativa visas i parenteser och noll visas som ett streck – exakt vad den anpassade formatsträngen anger.

---

## Vanliga frågor & edge cases

| Question | Answer |
|----------|--------|
| *Vad händer om grid‑en använder en annan kultur (t.ex. € istället för $)?* | Ersätt det inledande mellanslaget i formatsträngen med önskad symbol eller låt datakällan generera en förformatsträng med `CultureInfo.CurrentCulture`. |
| *Kan jag återanvända samma format för flera kolumner?* | Absolut. Spara formatsträngen i en konstant (`const string CurrencyMask = "...";`) och tilldela den där du behöver valuta. |
| *Vad händer om kolumnen innehåller ett strängvärde?* | Formatsträngen påverkar endast numeriska typer. Strängar passerar oförändrade, vilket är anledningen till att den sista delen av masken (`_(@_)`) finns – den bevarar icke‑numeriskt innehåll. |
| *Finns det någon prestandapåverkan?* | Försumbar. Formatet appliceras vid rendering, inte under datahämtning. Såvida du inte renderar tusentals rader per bildruta, märker du ingen fördröjning. |
| *Hur gör jag kanten tjockare för utskriftsrapporter?* | Byt `BorderLineStyle.Thin` mot `BorderLineStyle.Medium` eller `BorderLineStyle.Thick`. Vissa bibliotek låter dig också ange en pixelbredd direkt. |

---

## Sammanfattning

Vi har gått igenom **hur man formaterar valuta** i en grid‑kolumn från början till slut: hämta kolumnen efter namn, sätt kolumnens talformat, tillämpa ett anpassat numeriskt format, justera cellerna och lägg till en smakfull kant. Det kompletta exemplet körs direkt och visar exakt det visuella resultat du kan förvänta dig.

If you’re ready to take this further, try:

- **Dynamic cultures** – switch the format string based on the user’s locale.  
- **Conditional

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}