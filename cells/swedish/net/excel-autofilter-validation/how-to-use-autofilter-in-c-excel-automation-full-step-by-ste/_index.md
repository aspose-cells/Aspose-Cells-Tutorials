---
category: general
date: 2026-05-30
description: Hur man använder AutoFilter i C# Excel‑automatisering. Lär dig hur du
  skapar en Excel‑arbetsbok, filtrerar rader efter värde och effektiviserar dina kalkylbladsuppgifter.
draft: false
keywords:
- how to use autofilter
- create excel workbook
- filter rows by value
- filter column b
- excel automation c#
language: sv
og_description: Hur man använder AutoFilter i C# Excel‑automatisering. Bli expert
  på att skapa Excel‑arbetsböcker, filtrera rader efter värde och automatisera kalkylblad
  med lätthet.
og_title: Hur man använder AutoFilter i C# Excel‑automatisering – Komplett guide
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  headline: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  type: TechArticle
- description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  name: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  steps:
  - name: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
    text: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
  - name: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
    text: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
  - name: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
    text: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
  - name: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
    text: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
  - name: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
    text: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
  type: HowTo
- questions:
  - answer: Yes. Aspose.Cells can save to both `.xlsx` and `.xls` by changing the
      file extension or using `SaveOptions`.
    question: Does this work with older .xls files?
  - answer: Load the file with `new Workbook("path.xlsx")`, apply the filter, then
      `Save` again.
    question: What if I need to filter *after* the workbook is already saved?
  - answer: 'Absolutely. Use `worksheet.AutoFilter.Range = "A1:C5";` and then `worksheet.AutoFilter.ApplyFilter();`.
      However, tables give you built‑in styling and easier column referencing. ---
      ## Image – Visual Confirmation ![Screenshot showing AutoFilter applied to column
      B in an Excel workbook created with C#'
    question: Can I apply a filter to a *range* that isn’t a table?
  type: FAQPage
tags:
- C#
- Excel
- Automation
title: Hur man använder AutoFilter i C# Excel‑automatisering – Fullständig steg‑för‑steg‑guide
url: /sv/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder AutoFilter i C# Excel‑automatisering – Komplett guide

Har du någonsin undrat **hur man använder AutoFilter** när du genererar Excel‑filer från C#‑kod? Du är inte ensam—många utvecklare stöter på detta problem när de behöver dölja rader som inte matchar ett visst kriterium.  

I den här handledningen går vi igenom ett konkret, körbart exempel som **skapar en Excel‑arbetsbok**, lägger till en tabell och sedan **filtrerar rader efter värde** i kolumn B. I slutet har du ett rent, återanvändbart kodsnutt som du kan lägga in i vilket C#‑projekt som helst som behöver Excel‑automatisering.

## Vad du kommer att lära dig

- Ställ in ett C#‑projekt med Aspose.Cells (eller Microsoft.Office.Interop)‑biblioteket.  
- **Skapa Excel‑arbetsbok** programatiskt och lägg till en formaterad tabell.  
- Applicera **AutoFilter** för att visa endast rader där **kolumn B** är lika med en specifik sträng.  
- Ta bort filtret helt och återställ hela datasetet.  
- Tips för att hantera kantfall som saknade kolumner eller flera filterkriterier.

Ingen tidigare Excel‑VBA‑erfarenhet krävs; bara en grundläggande förståelse för C# och NuGet‑paket.

---

## Förutsättningar

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 eller senare (eller .NET Framework 4.7+) | Moderna runtime‑miljöer ger bättre prestanda och enklare paket‑hantering. |
| Aspose.Cells för .NET (eller Microsoft.Office.Interop.Excel) installerat via NuGet | Detta bibliotek ger oss `Workbook`, `Worksheet` och `Table`‑objekten som används i koden. |
| En kodredigerare (Visual Studio, VS Code, Rider, etc.) | Du behöver kompilera och köra exemplet. |
| Grundläggande C#‑kunskaper | Handledningen förklarar *varför* varje rad finns, inte bara *vad* den gör. |

Du kan installera Aspose.Cells med:

```bash
dotnet add package Aspose.Cells
```

---

## Så använder du AutoFilter med Aspose.Cells i C#

Nedan är det fullständiga, fristående programmet. Spara det som `Program.cs` i ett konsolprojekt och kör – du får `FilteredWorkbook.xlsx` i utdata‑mappen.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutoFilterDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Create an Excel workbook and grab the first worksheet
            // -------------------------------------------------
            Workbook workbook = new Workbook();               // creates a new, empty workbook
            Worksheet sheet = workbook.Worksheets[0];         // the default sheet is named "Sheet1"

            // Populate the sheet with sample data (A‑C columns, 5 rows)
            sheet.Cells["A1"].PutValue("ID");
            sheet.Cells["B1"].PutValue("Fruit");
            sheet.Cells["C1"].PutValue("Quantity");

            sheet.Cells["A2"].PutValue(1);
            sheet.Cells["B2"].PutValue("Apple");
            sheet.Cells["C2"].PutValue(10);

            sheet.Cells["A3"].PutValue(2);
            sheet.Cells["B3"].PutValue("Banana");
            sheet.Cells["C3"].PutValue(15);

            sheet.Cells["A4"].PutValue(3);
            sheet.Cells["B4"].PutValue("Apple");
            sheet.Cells["C4"].PutValue(7);

            sheet.Cells["A5"].PutValue(4);
            sheet.Cells["B5"].PutValue("Cherry");
            sheet.Cells["C5"].PutValue(20);

            // -------------------------------------------------
            // Step 2: Convert the range into a ListObject (Excel table)
            // -------------------------------------------------
            // Parameters: firstRow, firstColumn, totalRows, totalColumns, hasHeaders
            int tableIdx = sheet.ListObjects.Add(0, 0, 5, 3, true);
            ListObject table = sheet.ListObjects[tableIdx];
            table.TableStyleType = TableStyleType.TableStyleMedium2; // nice built‑in styling

            // -------------------------------------------------
            // Step 3: Apply an AutoFilter to show only rows where column B = "Apple"
            // -------------------------------------------------
            // The AutoFilter is attached to the table’s range automatically.
            // We target column B (index 1) and set the criteria.
            table.AutoFilter.Filter(1, "Apple"); // 1 = zero‑based column index for B

            // -------------------------------------------------
            // Step 4: Save the filtered workbook to disk
            // -------------------------------------------------
            workbook.Save("FilteredWorkbook.xlsx");

            // -------------------------------------------------
            // Step 5: (Optional) Remove the AutoFilter completely
            // -------------------------------------------------
            // This demonstrates that you can revert to the full dataset without re‑loading.
            table.RemoveAutoFilter();   // clears the filter
            workbook.Save("UnfilteredWorkbook.xlsx");

            Console.WriteLine("Workbook created and filtered successfully.");
        }
    }
}
```

### Så fungerar koden

1. **Skapa arbetsboken** – `new Workbook()` ger dig en tom fil; `Worksheets[0]` hämtar standardbladet.  
2. **Fyll exempeldata** – Vi skriver en liten dataset så att du kan se filtret i aktion.  
3. **Lägg till en tabell** – `ListObjects.Add` konverterar området till en Excel‑tabell, som automatiskt stödjer filtrering och formatering.  
4. **Applicera AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` talar om för motorn: “Visa endast rader där den andra kolumnen (B) är lika med *Apple*.”  
5. **Spara filer** – Två filer skrivs: en filtrerad, en med filtret borttaget, vilket visar att `RemoveAutoFilter()` fungerar som förväntat.

> **Proffstips:** Om du behöver filtrera efter flera kriterier (t.ex. “Apple” *eller* “Banana”), använd överlagringen `Filter(int columnIndex, string criteria1, string criteria2)` eller skicka en array av strängar.

---

## Filtrera rader efter värde – Vanliga variationer

Även om exemplet ovan fokuserar på **filter kolumn B**, kan du vilja filtrera andra kolumner eller använda numeriska kriterier. Här är ett snabbt fuskblad:

| Desired filter | Code snippet |
|----------------|--------------|
| Textmatch i kolumn C | `table.AutoFilter.Filter(2, "Cherry");` |
| Tal större än 10 i kolumn C | `table.AutoFilter.CustomFilter(2, "10", OperatorType.GreaterThan);` |
| Flera värden i kolumn B | `table.AutoFilter.Filter(1, new[] { "Apple", "Banana" });` |

**Kantfall:** Om kolumnrubriken är felstavad eller kolumnindexet är utanför intervallet, kastar Aspose.Cells ett `ArgumentException`. Skydda dig mot detta genom att kontrollera `table.ListColumns.Count` innan du applicerar filtret.

---

## Ta bort AutoFilter – När du ska återställa

Ibland behöver du visa hela datasetet igen (t.ex. efter att en användare har rensat ett sökfält). Att anropa `table.RemoveAutoFilter()` löser det med en enda rad. Om du använder Microsoft.Office.Interop istället, skulle du anropa `worksheet.AutoFilterMode = false;`.

---

## Fullständigt fungerande exempel – Sammanfattning

Nedan är det *hela* programmet igen, utan kommentarer för dem som föredrar en koncis vy:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("ID");
        ws.Cells["B1"].PutValue("Fruit");
        ws.Cells["C1"].PutValue("Quantity");

        ws.Cells["A2"].PutValue(1); ws.Cells["B2"].PutValue("Apple");  ws.Cells["C2"].PutValue(10);
        ws.Cells["A3"].PutValue(2); ws.Cells["B3"].PutValue("Banana"); ws.Cells["C3"].PutValue(15);
        ws.Cells["A4"].PutValue(3); ws.Cells["B4"].PutValue("Apple");  ws.Cells["C4"].PutValue(7);
        ws.Cells["A5"].PutValue(4); ws.Cells["B5"].PutValue("Cherry"); ws.Cells["C5"].PutValue(20);

        int idx = ws.ListObjects.Add(0, 0, 5, 3, true);
        ListObject tbl = ws.ListObjects[idx];
        tbl.TableStyleType = TableStyleType.TableStyleMedium2;

        tbl.AutoFilter.Filter(1, "Apple");
        wb.Save("FilteredWorkbook.xlsx");

        tbl.RemoveAutoFilter();
        wb.Save("UnfilteredWorkbook.xlsx");
    }
}
```

Kör detta ger två filer:

- **FilteredWorkbook.xlsx** – endast rader med *Apple* synliga.  
- **UnfilteredWorkbook.xlsx** – den ursprungliga datan återställd.

---

## Vanliga frågor

**Q: Fungerar detta med äldre .xls‑filer?**  
A: Ja. Aspose.Cells kan spara både som `.xlsx` och `.xls` genom att ändra filändelsen eller använda `SaveOptions`.

**Q: Vad händer om jag behöver filtrera *efter* att arbetsboken redan är sparad?**  
A: Ladda filen med `new Workbook("path.xlsx")`, applicera filtret, och spara sedan igen med `Save`.

**Q: Kan jag applicera ett filter på ett *område* som inte är en tabell?**  
A: Absolut. Använd `worksheet.AutoFilter.Range = "A1:C5";` och sedan `worksheet.AutoFilter.ApplyFilter();`. Dock ger tabeller inbyggd formatering och enklare kolumnreferenser.

---

## Bild – Visuell bekräftelse

![Skärmbild som visar AutoFilter tillämpat på kolumn B i en Excel‑arbetsbok skapad med C#](/images/autofilter-column-b.png "AutoFilter på kolumn B")

*(Bilden illustrerar den filtrerade vyn där endast rader som innehåller “Apple” återstår.)*

---

## Slutsats

Vi har just gått igenom **hur man använder AutoFilter** i ett C#‑styrt Excel‑automatiseringsscenario, från **att skapa en Excel‑arbetsbok** till **att filtrera rader efter värde** i **kolumn B**, och slutligen **ta bort filtret** när det inte längre behövs. De grundläggande stegen—initiera, lägga till en tabell, applicera filtret och städa upp—är återanvändbara i alla projekt som behöver **excel automation c#**.

Klar för nästa utmaning? Prova:

- Lägga till villkorsstyrd formatering för att markera filtrerade rader.  
- Exportera de filtrerade data till en CSV för vidare bearbetning.  
- Kombinera flera filter (t.ex. “Apple” *och* kvantitet > 8).

---

## Vad du bör lära dig härnäst?

- [Hur man implementerar AutoFilter i Excel med Aspose.Cells för .NET (Dataanalysguide)](/cells/english/net/data-analysis/implement-autofilter-excel-aspose-cells-dotnet/)
- [Hur man använder Autofilter Not Contains i Aspose.Cells .NET för Excel‑dataanalys](/cells/english/net/data-analysis/master-autofilter-not-contains-aspose-cells-net/)
- [Hur man implementerar Excel‑Autofilter 'EndsWith' med Aspose.Cells för .NET](/cells/english/net/data-analysis/implement-autofilter-endswith-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}