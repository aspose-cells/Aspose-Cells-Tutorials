---
category: general
date: 2026-03-30
description: Lär dig hur du använder WRAPCOLS i C# för att skapa en Excel-arbetsbok,
  lägga till data i Excel och tvinga formelberäkning samtidigt som du använder WRAPROWS.
draft: false
keywords:
- how to use wrapcols
- create excel workbook c#
- add data to excel
- force formula calculation
- how to use wraprows
language: sv
og_description: Upptäck hur du använder WRAPCOLS i C# för att bygga en Excel-arbetsbok,
  lägga till data, tvinga formelberäkning och utnyttja WRAPROWS för arrayformler.
og_title: Hur man använder WRAPCOLS i C# – Komplett guide
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Hur man använder WRAPCOLS i C# – Skapa Excel-arbetsbok med wrap-funktioner
url: /sv/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder WRAPCOLS i C# – Skapa Excel-arbetsbok med Wrap-funktioner

Har du någonsin undrat **how to use WRAPCOLS** när du automatiserar Excel med C#? Du är inte ensam—många utvecklare stöter på problem när de behöver omvandla ett horisontellt område till en vertikal array utan att skriva massor av kod. Den goda nyheten är att Aspose.Cells gör det till en barnlek.

I den här handledningen går vi igenom ett komplett, körbart exempel som visar **how to use WRAPCOLS**, hur man **create Excel workbook C#**‑style, hur man **add data to Excel**, och till och med hur man **force formula calculation** så att resultaten visas omedelbart. Vi kommer också att strö lite **how to use WRAPROWS** för den motsatta transformationen. I slutet har du ett färdigt program och en klar förståelse för varför varje steg är viktigt.

---

![Exempel på hur man använder WRAPCOLS i C#](alt="Skärmbild som visar Excel-arbetsbok efter att ha använt WRAPCOLS i C#")

## Vad den här guiden täcker

* Att skapa en ny arbetsbok med Aspose.Cells.
* Att fylla celler programatiskt (**add data to Excel**).
* Att tillämpa `WRAPCOLS`‑funktionen för att omvandla en rad till en kolumn.
* Att använda `WRAPROWS` för att vända en kolumn tillbaka till en rad (**how to use wraprows**).
* Att tvinga motorn att utvärdera formler omedelbart (**force formula calculation**).
* Att spara filen och kontrollera resultatet.

Ingen extern dokumentation behövs—allt du behöver finns här.

---

## Hur man använder WRAPCOLS i C# – Steg‑för‑steg-implementation

Nedan är den fullständiga källfilen. Kopiera‑klistra in den i ett nytt konsolprojekt, lägg till Aspose.Cells NuGet‑paketet och tryck **F5**.

```csharp
// ------------------------------------------------------------
// How to Use WRAPCOLS in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.Cells;

namespace WrapFunctionsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a fresh workbook (this is how we **create excel workbook c#** style)
            Workbook workbook = new Workbook();

            // 2️⃣ Grab the first worksheet – it's created by default
            Worksheet sheet = workbook.Worksheets[0];

            // 3️⃣ **Add data to Excel**: place two numbers side‑by‑side
            sheet.Cells["A1"].PutValue(1);   // first value
            sheet.Cells["B1"].PutValue(2);   // second value

            // 4️⃣ **How to use WRAPCOLS** – turn the horizontal range A1:B1 into a vertical array
            //    The second argument (1) tells WRAPCOLS to create 1 column per element.
            sheet["C1"].Formula = "WRAPCOLS(A1:B1, 1)";

            // 5️⃣ **How to use WRAPROWS** – the opposite; turn the same range into a horizontal array
            //    Here we ask for 2 rows per element, which produces a single row with both values.
            sheet["C2"].Formula = "WRAPROWS(A1:B1, 2)";

            // 6️⃣ **Force formula calculation** so the workbook reflects the results immediately
            workbook.CalculateFormula();

            // 7️⃣ Save the workbook to disk – change the path to a folder you own
            string outputPath = @"WrapFunctions.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
            Console.WriteLine("Check cells C1 and C2 for the WRAPCOLS / WRAPROWS results.");
        }
    }
}
```

### Varför varje rad är viktig

| Steg | Förklaring |
|------|------------|
| **1️⃣ Skapa en ny arbetsbok** | Detta är grunden. Aspose.Cells behandlar ett `Workbook`‑objekt som hela Excel‑filen, så du effektivt **creating an Excel workbook C#**‑style. |
| **2️⃣ Hämta det första kalkylbladet** | En ny arbetsbok innehåller alltid minst ett kalkylblad (`Worksheets[0]`). Att komma åt det tidigt undviker null‑reference‑överraskningar. |
| **3️⃣ Lägg till data i Excel** | Genom att använda `PutValue` **add data to Excel** utan att oroa dig för cellformatering. Siffrorna `1` och `2` är våra testdata för wrap‑funktionerna. |
| **4️⃣ Hur man använder WRAPCOLS** | `WRAPCOLS(A1:B1, 1)` instruerar Excel att ta området `A1:B1` och sprida dess värden vertikalt, ett per rad. Resultatet hamnar i `C1` och sprids nedåt (`C1`, `C2`, …). |
| **5️⃣ Hur man använder WRAPROWS** | `WRAPROWS(A1:B1, 2)` gör motsatsen: den skapar en horisontell spill, placerar de två värdena i en enda rad som börjar på `C2`. |
| **6️⃣ Tvinga formelberäkning** | Som standard kan Aspose.Cells skjuta upp beräkning tills filen öppnas i Excel. Genom att anropa `CalculateFormula()` **forces formula calculation** så kan du läsa resultaten omedelbart efter sparning. |
| **7️⃣ Spara arbetsboken** | Det sista steget skriver allt till disk. Öppna den resulterande `WrapFunctions.xlsx` för att se resultatet. |

---

## Skapa Excel-arbetsbok C# – Ställa in miljön

Innan du kör koden, se till att du har rätt verktyg:

1. **.NET 6.0+** – Den senaste LTS‑versionen fungerar bäst.
2. **Visual Studio 2022** (eller VS Code med C#‑tillägget).
3. **Aspose.Cells for .NET** – Installera via NuGet:  
   ```bash
   dotnet add package Aspose.Cells
   ```
4. En skrivbar mapp för utdatafilen.

Dessa förutsättningar är minimala; ingen COM‑interop eller Office‑installation krävs, vilket är anledningen till att Aspose.Cells är ett populärt val för server‑sidig Excel‑generering.

---

## Lägg till data i Excel – Bästa praxis

När du **add data to Excel** programatiskt, överväg dessa tips:

* **Use `PutValue`** för råa tal eller strängar; den upptäcker automatiskt datatypen.
* **Avoid hard‑coding cell addresses** i stora projekt—använd loopar eller namngivna områden för skalbarhet.
* **Set cell styles sparingly**; varje stiländring medför overhead. Om du behöver formatering, skapa ett enda stilobjekt och applicera det på flera celler.

I vårt lilla exempel infogar vi bara två siffror, men samma mönster kan skalas till tusentals rader.

---

## Hur man använder WRAPROWS – Horisontellt array‑exempel

Om du behöver motsatsen till `WRAPCOLS`, är `WRAPROWS` ditt val. Syntaxen är:

```
WRAPROWS(source_range, [rows_per_item])
```

* `source_range` – området du vill transformera.
* `rows_per_item` – valfri; talar om för Excel hur många rader varje element upptar. I vår demo använde vi `2` för att tvinga båda värdena till en enda rad.

Du kan experimentera genom att ändra det andra argumentet:

```csharp
// Example: split each value into its own column, three rows per item
sheet["D1"].Formula = "WRAPROWS(A1:B1, 3)";
```

Öppna arbetsboken så ser du att värdena sprids över tre kolumner, där varje kolumn innehåller de ursprungliga siffrorna upprepade efter behov.

---

## Tvinga formelberäkning – När och varför

Du kanske undrar, “Behöver jag verkligen anropa `CalculateFormula()`?” Svaret är **ja**, om:

* Du planerar att läsa beräknade värden **programmatically** efter sparning.
* Du vill säkerställa att filen öppnas i Excel med de korrekta resultaten redan visade.
* Du kör i en **headless environment** (t.ex. ett web‑API) där ingen användare manuellt triggar en omberäkning.

Att hoppa över detta steg förstör inte arbetsboken, men cellerna kommer att visa formeltexten (`=WRAPCOLS(...)`) istället för de beräknade värdena tills Excel omberäknar.

---

## Förväntat resultat – Vad du ska leta efter

Efter att ha kört programmet och öppnat `WrapFunctions.xlsx`:

| Cell | Formel | Visat värde |
|------|--------|-------------|
| **C1** | `=WRAPCOLS(A1:B1, 1)` | `1` (i C1) och `2` (i C2) – en vertikal lista |
| **C2** | `=WRAPROWS(A1:B1, 2)` | `1` i C2 och `2` i D2 – en horisontell lista |

Så du kommer att se en kolumn med värden som börjar på **C1** och en rad med värden som börjar på **C2**. Detta bekräftar att båda wrap‑funktionerna fungerade som förväntat.

---

## Edge Cases & Variationer

| Scenario | Vad förändras? | Föreslagen justering |
|----------|----------------|----------------------|
| **Stort område (A1:Z1)** | Fler värden att spilla vertikalt | Öka det andra argumentet för `WRAPCOLS` om du vill ha flera kolumner per grupp. |
| **Icke‑numerisk data** | Strängar hanteras på samma sätt | Ingen kodändring; `PutValue` accepterar vilket objekt som helst. |
| **Dynamiskt område** | Du vet inte storleken vid kompileringstid | Använd `sheet.Cells.MaxDataColumn` och `MaxDataRow` för att bygga adresssträngen. |
| **Flera kalkylblad** | Behöver tillämpa wrap‑funktioner på olika blad | Referera till rätt kalkylblad (`workbook.Worksheets["Sheet2"]`). |

---

## Pro‑tips från frontlinjen

* **Pro tip:** Wrappa skapandet av arbetsboken i ett `using`‑block om du riktar dig mot .NET Core 3.1+ för att säkerställa att alla resurser frigörs snabbt.
* **Watch out for:** Att sätta samma formel i ett stort område utan att anropa `CalculateFormula()` kan orsaka prestandaproblem. Batch‑processa formler när det är möjligt.
* **Tip:** If you need to read back the calculated values in code, call `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}