---
category: general
date: 2026-02-09
description: Skapa en ny Excel‑arbetsbok och lär dig hur du enkelt kopierar pivottabeller.
  Denna guide visar hur du duplicerar en pivottabell och sparar arbetsboken som en
  ny.
draft: false
keywords:
- create new excel workbook
- how to copy pivot
- duplicate pivot table
- save workbook as new
- how to copy worksheet
language: sv
og_description: Skapa en ny Excel‑arbetsbok i C# och kopiera en pivottabell omedelbart.
  Lär dig hur du duplicerar pivottabellen och sparar arbetsboken som en ny med ett
  komplett kodexempel.
og_title: Skapa ny Excel‑arbetsbok – Steg‑för‑steg Pivot‑kopia
tags:
- excel
- csharp
- aspose.cells
- automation
title: Skapa ny Excel‑arbetsbok – Kopiera & duplicera pivottabell
url: /sv/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa ny Excel-arbetsbok – Kopiera & duplicera pivottabell

Har du någonsin behövt **skapa ny Excel-arbetsbok** som behåller en komplex pivottabell från en befintlig fil? Du är inte ensam—många utvecklare stöter på detta hinder när de automatiserar rapporteringspipelines. Den goda nyheten är att med några rader C# och Aspose.Cells‑biblioteket kan du **hur man kopierar pivottabell** snabbt, **duplicera pivottabell**, och **spara arbetsbok som ny** utan att öppna Excel manuellt.

I den här guiden går vi igenom hela processen, från att ladda källarbetsboken till att spara den duplicerade versionen. I slutet har du ett färdigt kodexempel som du kan klistra in i vilket .NET‑projekt som helst. Inga onödiga utsvävningar, bara en praktisk lösning du kan testa idag.

## Vad den här tutorialen täcker

* **Förutsättningar** – .NET 6+ (eller .NET Framework 4.6+), Visual Studio och Aspose.Cells for .NET NuGet‑paketet.
* Steg‑för‑steg‑kod som **skapar ny Excel-arbetsbok**, kopierar pivottabellen och skriver resultatet till disk.
* Förklaringar till **varför** varje rad är viktig, inte bara **vad** den gör.
* Tips för att hantera kantfall som dolda kalkylblad eller stora dataintervall.
* En snabb titt på **hur man kopierar kalkylblad** om du någonsin behöver hela bladet istället för bara pivottabellen.

Klar? Låt oss dyka in.

![create new excel workbook illustration](image.png "Diagram showing source workbook, pivot copy, and destination workbook")

## Steg 1: Ställ in projektet och installera Aspose.Cells

Innan vi kan **skapa ny Excel-arbetsbok** behöver vi ett projekt som refererar rätt bibliotek.

```csharp
// Install the Aspose.Cells package via NuGet:
//   dotnet add package Aspose.Cells
using Aspose.Cells;   // Provides Workbook, Worksheet, Range, etc.
using System;        // For basic .NET types
```

*Varför detta är viktigt:* Aspose.Cells kör helt i minnet, så du behöver aldrig starta Excel på servern. Det bevarar också pivottabellens cache‑information, vilket är avgörande för en sann **duplicera pivottabell**.

> **Proffstips:** Om du riktar dig mot .NET Core, se till att projektets runtime‑identifierare (RID) matchar den plattform du ska distribuera till; annars kan du stöta på fel vid inläsning av native‑bibliotek.

## Steg 2: Ladda källarbetsboken som innehåller pivottabellen

Nu ska vi **hur man kopierar pivottabell** från en befintlig fil. Källarbetsboken kan ligga var som helst på disken, i en ström eller till och med i en byte‑array.

```csharp
// Step 2: Load the source workbook that contains the pivot table
string sourcePath = @"C:\Reports\source.xlsx";
Workbook sourceWorkbook = new Workbook(sourcePath);

// Grab the first worksheet (adjust the index if your pivot lives elsewhere)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that encloses the pivot table – A1:D20 in this example
Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");
```

*Varför vi väljer ett intervall:* En pivottabell lever i ett vanligt cellintervall, men den har också dold cache‑data kopplad till bladet. Genom att kopiera intervallet **inklusive pivottabellen** säkerställer Aspose.Cells att cachen följer med, vilket ger dig en funktionell **duplicera pivottabell** i destinationsfilen.

## Steg 3: Skapa en ny Excel-arbetsbok för att ta emot den kopierade datan

Här skapar vi faktiskt **skapa ny Excel-arbetsbok** som ska hålla den duplicerade pivottabellen.

```csharp
// Step 3: Create a fresh workbook (empty) for the destination
Workbook destinationWorkbook = new Workbook(); // Starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

// Destination starts at A1 – you could offset if you need space for other data
Range destinationRange = destinationSheet.Cells.CreateRange("A1");
```

> **Varför en ny arbetsbok?** Att börja med en tom arbetsbok garanterar att ingen kvarvarande formatering eller dolda objekt stör den kopierade pivottabellen. Det gör också den resulterande filen mindre, vilket är praktiskt för automatiserade e‑postbilagor.

## Steg 4: Kopiera pivottabellens intervall till den nya arbetsboken

Nu utför vi själva **hur man kopierar pivottabell**‑operationen.

```csharp
// Step 4: Copy the range (including the pivot) from source to destination
sourceRange.Copy(destinationRange);
```

Den där enda raden gör det tunga lyftet:

* Cellvärden, formler och formatering överförs.
* Pivottabellens cache dupliceras, så den nya pivottabellen förblir fullt funktionell.
* Eventuella relativa referenser i pivottabellen justeras automatiskt till den nya platsen.

### Hantera kantfall

* **Dolda kalkylblad:** Om källbladet är dolt kopieras pivottabellen fortfarande utan problem, men du kanske vill göra destinationsbladet synligt för användaren:
  ```csharp
  destinationSheet.IsVisible = true;
  ```
* **Stora datamängder:** För intervall som är större än några tusen rader, överväg att använda `CopyTo` med `CopyOptions` för att strömma operationen och minska minnesbelastningen.

## Steg 5: Spara destinationsarbetsboken som en ny fil

Till sist **spara arbetsbok som ny** och verifiera resultatet.

```csharp
// Step 5: Save the destination workbook with the duplicated pivot table
string destPath = @"C:\Reports\copied.xlsx";
destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

// Quick verification – open the file manually or read a cell value
Console.WriteLine($"Workbook saved to {destPath}");
```

Om du öppnar `copied.xlsx` ser du en exakt kopia av den ursprungliga pivottabellen, redo för vidare manipulation eller distribution.

### Valfritt: Hur man kopierar kalkylblad istället för bara pivottabellen

Ibland vill du ha hela bladet, inte bara pivottabellen. Samma API gör det enkelt:

```csharp
// Copy the whole worksheet (including all charts, tables, etc.)
sourceSheet.CopyTo(destinationWorkbook, 0); // Inserts at index 0
destinationWorkbook.Save(@"C:\Reports\full_copy.xlsx");
```

Detta svarar på frågan **hur man kopierar kalkylblad** och kan vara praktiskt när du behöver bevara ytterligare blad‑nivåinställningar.

## Fullständigt fungerande exempel

Sätter vi ihop allt får vi en självständig konsolapp som du kan kompilera och köra:

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load source workbook
        string sourcePath = @"C:\Reports\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");

        // 2️⃣ Create destination workbook
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
        Range destinationRange = destinationSheet.Cells.CreateRange("A1");

        // 3️⃣ Copy the pivot (range)
        sourceRange.Copy(destinationRange);

        // 4️⃣ Save as new file
        string destPath = @"C:\Reports\copied.xlsx";
        destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Successfully created new Excel workbook with duplicated pivot table at {destPath}");
    }
}
```

**Förväntad output:** Konsolen skriver ut ett lyckat meddelande, och `copied.xlsx` dyker upp i `C:\Reports` med en funktionell pivottabell som är identisk med den i `source.xlsx`.

## Vanliga frågor & fallgropar

* **Kommer formler i pivottabellen gå sönder?** Nej—eftersom pivottabellens cache följer med intervallet förblir alla beräknade fält intakta.
* **Vad händer om källpivottabellen använder externa datakopplingar?** Dessa kopplingar *kopieras inte*. Du måste återupprätta dem i destinationsarbetsboken eller konvertera pivottabellen till en statisk tabell först.
* **Kan jag kopiera flera pivottabeller samtidigt?** Absolut—definiera bara ett större intervall som omfattar alla pivottabeller, eller loopa igenom varje `PivotTable`‑objekt i `sourceSheet.PivotTables` och kopiera dem individuellt.
* **Måste jag disponera `Workbook`‑objekten?** De implementerar `IDisposable`, så att omsluta dem i `using`‑satser är en god vana, särskilt i hög‑trafik‑tjänster.

## Slutsats

Du vet nu **hur man skapar ny Excel-arbetsbok**, kopierar en pivottabell, **duplicera pivottabell**, och **spara arbetsbok som ny** med C# och Aspose.Cells. Stegen är enkla: ladda, skapa, kopiera och spara. Med det valfria **hur man kopierar kalkylblad**‑exemplet har du också ett alternativ för fullständig bladduplication.

Nästa steg kan vara att utforska:

* Lägga till anpassad formatering i den duplicerade pivottabellen.
* Uppdatera pivottabellens cache programatiskt efter datakörningar.
* Exportera arbetsboken till PDF eller CSV för downstream‑system.

Prova, justera intervallet och låt automatiseringen ta bort det tråkiga arbetet i din rapporteringsprocess. Lycka till med kodningen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}