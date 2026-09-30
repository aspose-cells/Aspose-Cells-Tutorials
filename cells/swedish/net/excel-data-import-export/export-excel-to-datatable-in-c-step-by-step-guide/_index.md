---
category: general
date: 2026-03-25
description: Lär dig hur du snabbt exporterar Excel till DataTable i C#. Denna handledning
  täcker export av Excel med kolumnnamn och export av Excel-data som sträng för pålitlig
  databehandling.
draft: false
keywords:
- export excel to datatable
- how to export excel to datatable
- export excel with column names
- export excel data as string
language: sv
og_description: Exportera Excel till DataTable i C# med kolumnnamn och strängkonvertering.
  Följ den här kortfattade handledningen för en färdiglösning som är klar att köra.
og_title: Exportera Excel till DataTable i C# – Komplett guide
tags:
- C#
- Aspose.Cells
- DataTable
- Excel
title: Exportera Excel till DataTable i C# – Steg‑för‑steg guide
url: /sv/net/excel-data-import-export/export-excel-to-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportera Excel till DataTable i C# – Steg‑för‑steg‑guide

Har du någonsin behövt **exportera Excel till DataTable** men varit osäker på vilka flaggor du ska sätta? Du är inte ensam—många utvecklare stöter på samma hinder när de första gången försöker hämta kalkylbladsdata till en `DataTable`.  

Den goda nyheten? På bara några kodrader kan du **exportera Excel med kolumnnamn** och till och med **exportera Excel-data som sträng** för att undvika huvudvärk med typ‑mismatch. Nedan hittar du ett komplett, körbart exempel samt “varför” bakom varje inställning, så att du kan anpassa det till vilket projekt som helst utan gissningar.

## Vad den här handledningen täcker

* Hur man skapar en arbetsbok i minnet (ingen fysisk fil behövs).  
* Fyller i några exempelrader så att du kan se resultatet omedelbart.  
* Konfigurerar `ExportTableOptions` så att varje cell behandlas som en sträng.  
* Exporterar ett rektangulärt område till en `DataTable` samtidigt som den första raden behålls som kolumnrubriker.  
* Verifierar resultatet och skriver ut den första raden till konsolen.  

Inga externa dokumentationslänkar behövs—allt du behöver finns här. Om du redan har en Excel‑fil på disk, ersätt bara raden som skapar arbetsboken med `new Workbook("path/to/file.xlsx")` så är du klar.

---

## Steg 1: Ställ in projektet och lägg till Aspose.Cells NuGet‑paketet

Innan vi skriver någon kod, se till att ditt projekt refererar till **Aspose.Cells for .NET** (biblioteket som driver `Workbook`‑klassen). Du kan lägga till det via NuGet Package Manager:

```bash
dotnet add package Aspose.Cells
```

> **Proffstips:** Använd den senaste stabila versionen (från och med mars 2026 är den 22.12) för att få de senaste buggfixarna och prestandaförbättringarna.

---

## Steg 2: Skapa en arbetsbok och fyll den med exempeldata

Vi börjar med en helt ny `Workbook` och skriver några rader så att du kan se exporten i aktion. Detta steg visar också **hur man exporterar excel till datatable** när källdata endast finns i minnet.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();                 // in‑memory workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Populate a few cells – this mimics a real Excel file
        worksheet.Cells["A1"].PutValue("Name");   // column header
        worksheet.Cells["B1"].PutValue("Age");    // column header
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);
```

*Varför detta är viktigt:* Genom att först infoga rubrikraden (`A1` & `B1`) kan vi senare instruera exportören att behandla den första raden som kolumnnamn—precis vad **exportera excel med kolumnnamn** betyder.

---

## Steg 3: Berätta för Aspose.Cells att behandla varje cell som en sträng

När du exporterar numeriska eller datumceller försöker Aspose att härleda .NET‑typen. Det kan orsaka subtila buggar om din efterföljande kod förväntar sig strängar. Flaggan `ExportTableOptions.ExportAsString` tvingar en enhetlig strängkonvertering.

```csharp
        // 3️⃣ Configure export options – all values will be strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true       // <-- ensures Export Excel Data As String
        };
```

*Varför använda detta?* Föreställ dig en kolumn som ibland innehåller siffror och ibland text (t.ex. “00123” vs. “ABC”). Genom att exportera allt som en sträng undviker du att förlora inledande nollor eller utlösa typ‑konverteringsundantag.

---

## Steg 4: Exportera önskat område till en DataTable

Nu **exporterar vi excel till datatable** på riktigt. Metoden `ExportDataTable` tar startrad/kolumn, antalet rader/kolumner, en flagga för extrahering av kolumnnamn och de alternativ vi just byggt.

```csharp
        // 4️⃣ Export rows 0‑9 and columns 0‑4 (adjust as needed)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,   // <-- uses the first row as headers
            exportOptions: exportOptions);
```

*Vad händer under huven?*  
- `startRow: 0` pekar på den första Excel‑raden (rubrikraden).  
- `exportColumnNames: true` instruerar Aspose att lyfta “Name” och “Age” till `DataTable`‑kollektionskolumnerna.  
- `totalRows`/`totalColumns` kan vara större än den faktiska datan; överflödiga celler blir tomma strängar på grund av `ExportAsString`.

---

## Steg 5: Verifiera resultatet – skriv ut den första raden

En snabb utskrift till konsolen visar att konverteringen lyckades och att kolumnnamnen är intakta.

```csharp
        // 5️⃣ Show the first data row (if any)
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

**Förväntad utskrift**

```
First row: Alice, 30
```

Om du ändrar exempeldata kommer konsolen att återspegla dessa förändringar automatiskt—ingen extra kod behövs.

---

## Vanliga frågor & kantfall

| Fråga | Svar |
|----------|--------|
| **Kan jag exportera ett blad som redan finns på disk?** | Ja—ersätt `new Workbook()` med `new Workbook("myFile.xlsx")`. Resten av stegen förblir identiska. |
| **Vad händer om min Excel‑fil har sammanslagna celler?** | Sammanslagna celler avpackas; värdet i den översta vänstra cellen används för hela det sammanslagna området. |
| **Behöver jag oroa mig för kulturspecifika talformat?** | Inte när `ExportAsString = true`; allt kommer som den råa sträng som visas i Excel. |
| **Hur många rader kan jag exportera på en gång?** | Aspose.Cells kan hantera miljontals rader, men minnesanvändningen växer med storleken på `DataTable`. Överväg sidindelning om du når gränser. |
| **Vad händer med dolda kolumner?** | Dolda kolumner exporteras om du inte sätter `ExportHiddenColumns = false` i `ExportTableOptions`. |

---

## Bonus: Exportera till CSV istället för en DataTable

Ibland kan du föredra en platt fil. Samma `ExportTableOptions` kan återanvändas med `ExportDataTableToCSV`:

```csharp
        string csvPath = "output.csv";
        worksheet.Cells.ExportDataTableToCSV(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            csvPath,
            exportColumnNames: true,
            exportOptions);
        Console.WriteLine($"CSV written to {csvPath}");
```

Den enkla raden ger dig en färdig‑att‑importera CSV samtidigt som den **exporterar excel-data som sträng**.

---

## Fullt fungerande exempel (klar att kopiera‑klistra in)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate sample data (header + two rows)
        worksheet.Cells["A1"].PutValue("Name");
        worksheet.Cells["B1"].PutValue("Age");
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);

        // Export everything as strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true
        };

        // Export range to DataTable (first row = column names)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,
            exportOptions: exportOptions);

        // Display first row
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

Kör programmet (`dotnet run`) så ser du resultatet av **export excel to datatable** skrivet till konsolen. Byt ut exempeldata, ändra `totalRows`/`totalColumns`, eller peka arbetsboken på en riktig fil—allt skalar.

---

## Slutsats

Du har nu en **komplett, självständig lösning för att exportera Excel till DataTable** i C#. Genom att konfigurera `ExportTableOptions.ExportAsString` garanterar du att **exportera excel-data som sträng**, och genom att sätta `exportColumnNames: true` får du de välbekanta kolumnrubrikerna du förväntar dig när du **exporterar excel med kolumnnamn**.  

Från och med nu kan du:

* Mata `DataTable` i Entity Framework eller Dapper för massinsättningar.  
* Skicka den till en rapportmotor som **FastReport** eller **RDLC**.  
* Konvertera den till JSON för ett API‑svar (`JsonConvert.SerializeObject(table)`).

Känn dig fri att experimentera—kanske prova att exportera ett större blad, eller kombinera detta med **how to export excel to datatable** från en nätverksdelning. Mönstret förblir detsamma, och koden är klar för produktion.

![Diagram of Excel → DataTable conversion flow – export excel to datatable](https://example.com/placeholder.png "export excel to datatable diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}