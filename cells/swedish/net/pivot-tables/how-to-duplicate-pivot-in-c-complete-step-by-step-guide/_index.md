---
category: general
date: 2026-03-22
description: Lär dig hur du duplicerar pivottabell i C# med Aspose.Cells. Den här
  guiden visar också hur du kopierar rader och laddar en Excel-arbetsbok i C# för
  sömlös Excel‑automatisering av radkopiering.
draft: false
keywords:
- how to duplicate pivot
- how to copy rows
- load excel workbook c#
- excel automation copy rows
language: sv
og_description: Hur du duplicerar pivottabell i C#? Följ den här koncisa handledningen
  för att ladda en Excel-arbetsbok i C#, kopiera rader och bemästra Excel‑automation
  för att kopiera rader.
og_title: Hur man duplicerar pivot i C# – Komplett guide
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Hur man duplicerar Pivot i C# – Komplett steg‑för‑steg‑guide
url: /sv/net/pivot-tables/how-to-duplicate-pivot-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man duplicerar pivot i C# – Komplett steg‑för‑steg‑guide

Har du någonsin undrat **hur man duplicerar pivot** tabeller programatiskt utan att manuellt dra dem i Excel? Du är inte ensam. I många rapporteringspipeline behövs samma pivottlayout på en ny uppsättning rader, och att göra det för hand är slöseri med tid.  

Den goda nyheten? Med några rader C# kan du ladda en Excel‑arbetsbok, definiera området som innehåller pivoten, och **how to copy rows** så att pivoten visas på en ny plats — allt i ett automatiserat körning. I den här handledningen kommer vi också att gå igenom grunderna för **load excel workbook c#** och ge dig en solid grund för **excel automation copy rows**‑uppgifter.

> **What you’ll walk away with**  
> • Ett komplett, körbart exempel som duplicerar en pivottabell.  
> • En förklaring av varför varje rad är viktig.  
> • Tips för att hantera kantfall som dolda arbetsblad eller flera pivoter.

---

## Förutsättningar

Innan vi dyker ner, se till att du har:

- **.NET 6.0** (eller någon nyare .NET‑version) installerad.  
- **Aspose.Cells for .NET** – biblioteket vi använder för att manipulera Excel‑filer. Du kan hämta det via NuGet:  

```bash
dotnet add package Aspose.Cells
```  

- En källarbetsbok (`Source.xlsx`) som redan innehåller en pivottabell i området **A1:J20** (området vi ska duplicera).  
- Grundläggande kunskap om C#‑syntax – inget avancerat, bara de vanliga `using`‑satserna och `Main`‑metoden.

Om någon av dessa punkter känns obekanta, pausa ett ögonblick och installera paketet; resten av guiden förutsätter att biblioteket är redo att användas.

![illustration av hur man duplicerar pivot i C# med Aspose.Cells](https://example.com/duplicate-pivot.png "illustration av hur man duplicerar pivot i C#")

*Bildtext: "illustration av hur man duplicerar pivot i C# exempel som visar käll‑ och duplicerade pivotrader".*

---

## Steg 1: Load Excel Workbook C# – Öppna filen

Det allra första du behöver göra när du vill **load excel workbook c#** är att skapa en `Workbook`‑instans som pekar på din fil. Detta objekt ger dig åtkomst till varje arbetsblad, cell och pivot i filen.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Load the source workbook
        string sourcePath = @"C:\Data\Source.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // From here on we can work with worksheets, ranges, and pivots.
```

**Varför detta är viktigt:**  
`Workbook` abstraherar hela Excel‑filen till en modell i minnet. Utan att ladda den först kan du inte inspektera pivotens placering eller kopiera rader. Dessutom upptäcker konstruktorn automatiskt filformatet (XLS, XLSX, CSV osv.), så du behöver ingen extra kod för formatdetektering.

---

## Steg 2: How to Copy Rows – Definiera pivotområdet

Nu när arbetsboken är i minnet måste vi tala om för Aspose.Cells vilka rader som innehåller pivoten. I vårt exempel ligger pivoten i **A1:J20**, vilket motsvarar raderna **0‑19** (nollbaserad indexering). Vi omsluter detta i en `CellArea`‑struktur.

```csharp
        // Step 2: Define the cell area that contains the pivot table (A1:J20)
        // Row indices are zero‑based, column indices are also zero‑based.
        CellArea copyRange = new CellArea(startRow: 0, startColumn: 0, endRow: 19, endColumn: 9);
```

**Varför vi använder `CellArea`:**  
Det är ett lättviktigt sätt att beskriva ett rektangulärt block. När du senare anropar `CopyRows` läser metoden detta objekt för att exakt veta vilka rader som ska dupliceras. Om du någonsin behöver justera intervallet (t.ex. om pivoten växer till kolumn K) ändrar du bara värdet för `endColumn`.

---

## Steg 3: Åtkomst till målbladet

De flesta arbetsböcker har bara ett blad, men API‑et fungerar likadant för flera blad. Hämta det första arbetsbladet (index 0) – det är där den ursprungliga pivoten finns.

```csharp
        // Step 3: Get the first worksheet from the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Pro tip:**  
Om du har namngivna blad kan du även hämta dem med namn: `workbook.Worksheets["Sheet1"]`. Detta hjälper dig undvika hårdkodade index när arbetsbokens struktur förändras.

---

## Steg 4: How to Copy Rows – Duplicera pivottabellen

Här är kärnan i **how to duplicate pivot**: vi kopierar raderna som innehåller pivoten till en ny plats. I vårt fall börjar vi på rad 31 (nollbaserad index 30). Metoden `CopyRows` kopierar *både* data och den underliggande pivot‑cachen, så de nya raderna beter sig exakt som originalet.

```csharp
        // Step 4: Copy the rows of the defined range to a new location (starting at row 31)
        // The third argument is the destination start row (zero‑based).
        worksheet.Cells.CopyRows(copyRange.StartRow, copyRange.EndRow, destinationRow: 30);
```

**Vad som händer under huven?**  
`CopyRows` klonar varje rad och bevarar formler, format och pivottdefinitioner. Eftersom pivotens cache finns på arbetsboksnivå refererar den duplicerade pivoten automatiskt till samma datakälla – ingen extra konfiguration behövs.

**Kantfall – dolda rader:**  
Om någon av raderna i källintervallet är dolda, förblir de dolda efter kopieringen. Vill du visa dem, anropa `worksheet.Rows[destRow].IsHidden = false` efter kopieringen.

---

## Steg 5: Spara arbetsboken – Verifiera duplikatet

Till sist skriver du tillbaka ändringarna till disk. Du kan skriva över originalfilen eller, för säkerhets skull, spara till ett nytt namn så att du kan jämföra före/efter.

```csharp
        // Step 5: Save the workbook – the pivot table is now duplicated in the new rows
        string outputPath = @"C:\Data\CopyWithPivot.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine("Pivot duplicated successfully! Check " + outputPath);
    }
}
```

**Resultat du bör se:**  
Öppna `CopyWithPivot.xlsx`. Du hittar den ursprungliga pivoten i **A1:J20** och en identisk kopia som börjar på **A31:J50**. Båda pivoterna kan uppdateras oberoende, och eventuella slicers som är kopplade till originalet fungerar fortfarande för kopian eftersom de delar samma cache.

---

## Vanliga frågor & variationer

### Kan jag duplicera flera pivoter samtidigt?

Absolut. Loopa igenom alla pivottabeller (`worksheet.PivotTables`) och kopiera varje intervall till en annan destination. Se bara till att destinationsintervallen inte överlappar.

### Vad händer om källarbetsboken är lösenordsskyddad?

Aspose.Cells låter dig öppna en skyddad fil genom att skicka lösenordet till `Workbook`‑konstruktorn:

```csharp
Workbook workbook = new Workbook(sourcePath, new LoadOptions { Password = "mySecret" });
```

### Hur kopierar man rader utan att påverka formler?

Om du bara behöver *värdena* (inga formler), använd `CopyRows` med flaggan `CopyOptions`:

```csharp
worksheet.Cells.CopyRows(sourceStart, sourceEnd, destStart, new CopyOptions { CopyValues = true });
```

### Finns det ett sätt att kopiera rader till en *annan* arbetsbok?

Ja. Efter att ha kopierat rader i källbladet kan du klona bladet till en annan `Workbook`‑instans via `targetWorkbook.Worksheets.AddCopy(worksheet)`.

---

## Proffstips för pålitlig Excel Automation Copy Rows

- **Validera intervallet** innan du kopierar. En snabb `if (copyRange.EndRow >= worksheet.Cells.MaxDataRow)` förhindrar out‑of‑range‑fel.  
- **Stäng av beräkning** medan du kopierar stora områden: `workbook.Settings.CalcMode = CalcMode.Manual;` – detta snabbar upp operationen avsevärt.  
- **Disposera objekt** (`workbook.Dispose()`) om du bearbetar många filer i en loop för att frigöra inhemska resurser.  
- **Logga operationen** – särskilt i produktionspipeline – så att du kan spåra vilka filer som bearbetats och fånga fel tidigt.

---

## Slutsats

Du vet nu **how to duplicate pivot** tabeller i C# med Aspose.Cells, och du har sett hela arbetsflödet från **load excel workbook c#** till **excel automation copy rows** och slutligen sparandet av resultatet. Exemplet är självständigt, körs direkt och kan utökas för att hantera flera pivoter, skyddade filer eller kopiering mellan arbetsböcker.

Nästa steg? Prova att anpassa skriptet för att:

- Uppdatera den duplicerade pivoten programatiskt (`pivotTable.RefreshData();`).  
- Exportera det duplicerade området till en CSV för vidare bearbetning.  
- Integrera koden i ett ASP.NET Core‑API så att användare kan ladda upp en fil och få en version med duplicerad pivot direkt.

Lycka till med kodandet, och må din Excel‑automation alltid vara smidig!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}