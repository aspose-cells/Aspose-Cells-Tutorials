---
category: general
date: 2026-02-28
description: Ta bort rader i Excel‑tabell i C# snabbt. Lär dig hur du lägger till
  ett namngivet område i Excel, får åtkomst till kalkylbladet efter namn och undviker
  fel med dubbla namn.
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: sv
og_description: Ta bort rader i en Excel‑tabell med C#. Denna handledning visar också
  hur man lägger till ett namngivet område i Excel och får åtkomst till kalkylbladet
  efter namn.
og_title: Radera rader i Excel‑tabell med C# – Komplett guide
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: Ta bort rader i Excel‑tabell med C# – Steg‑för‑steg‑guide
url: /sv/net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ta bort rader i Excel‑tabell med C# – Komplett programmeringshandledning

Har du någonsin behövt **ta bort rader i excel‑tabell** från en arbetsbok men varit osäker på vilket API‑anrop du ska använda? Du är inte ensam – de flesta utvecklare stöter på samma hinder när de första gången försöker trimma en tabell programatiskt.  

I den här guiden går vi igenom ett komplett, körbart exempel som inte bara tar bort rader från en Excel‑tabell, utan också visar **hur man lägger till ett definierat namn** (aka ett *namngivet område*), hur man **åtkommer ett kalkylblad efter namn**, och varför ett duplicerat namn på ett annat blad kastar ett `InvalidOperationException`.  

När du är klar med artikeln kommer du att kunna:

* Hämta ett kalkylblad med hjälp av dess fliknamn.  
* På ett säkert sätt ta bort datarader från den första tabellen på det bladet.  
* Skapa ett namngivet område som pekar på en specifik adress.  
* Förstå fallgroparna med duplicerade namn över blad.

Ingen extern dokumentation behövs – allt du behöver finns här.

---

## Vad du behöver

* **DevExpress Spreadsheet** (eller vilket bibliotek som helst som exponerar `Workbook`, `Worksheet`, `ListObject` och `Names`‑objekt).  
* Ett .NET‑projekt som riktar mot **.NET 6** eller senare (koden kompilerar även med .NET Framework 4.8).  
* Grundläggande kunskap om C# – om du kan skriva en `foreach`‑loop är du redo.

> **Proffstips:** Om du använder den kostnadsfria Community‑editionen av DevExpress är API:erna som används nedan identiska med den kommersiella versionen.

---

## Steg 1 – Åtkomst till kalkylblad efter namn

Det första du måste göra är att lokalisera bladet som innehåller tabellen du vill modifiera.  
De flesta utvecklare använder `Worksheets[0]` av vana, men det kopplar din kod till bladordning och går sönder så snart någon byter namn på en flik.

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*Varför detta är viktigt:* Genom att använda bladets **namn** istället för dess index undviker du oavsiktliga redigeringar av fel blad när arbetsboken förändras.  

Om namnet du anger inte finns kastar biblioteket ett `KeyNotFoundException`, som du kan fånga för att visa ett vänligt felmeddelande.

---

## Steg 2 – Ta bort rader i Excel‑tabell (det säkra sättet)

Nu när du har rätt kalkylblad, låt oss ta bort dataraderna från den första tabellen.  
Ett vanligt misstag är att anropa `DeleteRows(1, rowCount‑1)`. Sedan **DevExpress 22.2** är den överlagringen **förbjuden** och kastar ett `InvalidOperationException`. Biblioteket förväntar sig att du tar bort rader **inom tabellens dataområde**, inte rubrikraden.

```csharp
// Grab the first table (ListObject) on the sheet
var table = worksheet.ListObjects[0];

// Calculate how many data rows we actually have (excluding the header)
int dataRowCount = table.DataRange.RowCount;

// Delete only the data rows – keep the header intact
if (dataRowCount > 0)
{
    // DeleteRows(startRow, rowCount) – startRow is zero‑based within the table
    table.DeleteRows(0, dataRowCount);
}
```

> **Vad händer om tabellen är tom?** `if`‑skyddet förhindrar ett anrop med `rowCount = 0`, vilket annars skulle ge ett undantag.

### Visuell översikt  

![delete rows excel table example](image.png "Skärmbild som visar rader som tas bort från en Excel‑tabell")  

*Alt‑text: exempel på att ta bort rader i en Excel‑tabell i C#‑kod*

---

## Steg 3 – Hur man lägger till ett definierat namn (skapa ett namngivet område)

Efter att du har rensat tabellen kanske du vill referera till ett specifikt område senare – exempelvis för ett diagram eller en datavalideringslista. Det är här **add named range excel** kommer in.

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

`Names.Add`‑metoden tar två parametrar: identifieraren och adressen i A1‑stil.  
Eftersom vi tidigare använde **åtkomst till kalkylblad efter namn**, kan adresssträngen säkert referera till vilket blad som helst utan att oroa sig för indexändringar.

---

## Steg 4 – Namngivet område på ett annat blad – undvik fel med duplicerade namn

Du kanske tror att du kan återanvända samma identifierare på ett annat blad, så här:

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

Tyvärr är Excels namngivningsomfång **arbetsboks‑brett**, inte per blad. Anropet ovan triggar ett `InvalidOperationException` med meddelandet *“A name with the same identifier already exists.”*  

### Så här löser du det

1. **Välj ett unikt namn** (`MyTable_Sheet2`).  
2. **Ta bort det befintliga namnet** innan du lägger till det igen (endast om du verkligen vill ersätta det).  

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

---

## Fullt, körbart exempel

När allt sätts ihop får du en fristående konsolapp som du kan klistra in i Visual Studio och köra mot en exempel‑fil `sample.xlsx`.

```csharp
using System;
using DevExpress.Spreadsheet;

class Program
{
    static void Main()
    {
        // Load an existing workbook (replace with your file path)
        Workbook workbook = new Workbook();
        workbook.LoadDocument("sample.xlsx");

        // -------------------------------------------------
        // Step 1 – Access the worksheet by its tab name
        // -------------------------------------------------
        Worksheet worksheet = workbook.Worksheets["Sheet1"]; // primary sheet

        // -------------------------------------------------
        // Step 2 – Delete rows excel table (safe method)
        // -------------------------------------------------
        var table = worksheet.ListObjects[0];
        int dataRows = table.DataRange.RowCount;
        if (dataRows > 0)
            table.DeleteRows(0, dataRows); // removes only data rows

        // -------------------------------------------------
        // Step 3 – Add a defined name (named range) on Sheet1
        // -------------------------------------------------
        workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

        // -------------------------------------------------
        // Step 4 – Demonstrate duplicate‑name handling
        // -------------------------------------------------
        try
        {
            workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine("Duplicate name error: " + ex.Message);
            // Use a unique identifier instead
            workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");
        }

        // Save the modified workbook
        workbook.SaveDocument("sample_modified.xlsx");
        Console.WriteLine("Workbook updated successfully.");
    }
}
```

**Förväntat resultat**

* Alla datarader från den första tabellen på **Sheet1** försvinner, endast rubrikraden blir kvar.  
* Namnet **MyTable** pekar nu på `Sheet1!$A$1:$C$5`.  
* Ett andra namn **MyTable_Sheet2** refererar säkert till ett område på **Sheet2** utan att kasta ett undantag.

---

## Vanliga frågor & kantfall

| Fråga | Svar |
|----------|--------|
| *Vad händer om arbetsboken har flera tabeller?* | Hämta rätt `ListObject` efter index (`worksheet.ListObjects[1]`) eller efter namn (`worksheet.ListObjects["MyTable"]`). |
| *Kan jag ta bort rader från en tabell som sträcker sig över flera kalkylblad?* | Nej – tabeller är begränsade till ett enda blad. Du måste upprepa raderingslogiken för varje blad. |
| *Finns det ett sätt att bara ta bort ett delmängd av rader?* | Ja – använd `table.DeleteRows(startRow, count)` där `startRow` är nollbaserat inom tabellens dataområde. |
| *Behåller namngivna områden sig efter sparning?* | Absolut. När du anropar `SaveDocument` blir namnen en del av arbetsbokens XML. |
| *Hur listar jag alla definierade namn i arbetsboken?* | Iterera `foreach (var name in workbook.Names) Console.WriteLine(name.Name);`. |

---

## Slutsats

Vi har gått igenom **delete rows excel table** med C#, demonstrerat **add named range excel**, och visat det rätta sättet att **access worksheet by name** samtidigt som vi undviker den fruktade duplicate‑name‑exceptionen.  

Den kompletta lösningen finns i kodsnutten ovan – kopiera, klistra in och kör den mot dina egna filer. Därefter kan du utöka logiken för att hantera flera tabeller, dynamiska områdesberäkningar eller till och med integrera med ett UI.

**Nästa steg** du kan utforska:

* Använd **named range on another sheet** för att driva diagramserier.  
* Kombinera raderingslogiken med **ExcelDataReader** för att importera data innan du rensar den.  
* Automatisera massuppdateringar i dussintals arbetsböcker med en enkel `foreach (var file in Directory.GetFiles(...))`‑loop.

Har du fler frågor om Excel‑automation i C#? Lämna en kommentar, så fortsätter vi samtalet. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}