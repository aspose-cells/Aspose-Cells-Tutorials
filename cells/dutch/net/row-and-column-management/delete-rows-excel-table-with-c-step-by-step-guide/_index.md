---
category: general
date: 2026-02-28
description: Verwijder rijen uit een Excel‑tabel in C# snel. Leer hoe je een benoemd
  bereik in Excel toevoegt, een werkblad op naam benadert en fouten door dubbele namen
  voorkomt.
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: nl
og_description: Rijen uit een Excel‑tabel verwijderen met C#. Deze tutorial laat ook
  zien hoe je een benoemd bereik in Excel kunt toevoegen en een werkblad op naam kunt
  benaderen.
og_title: Rijen verwijderen uit Excel‑tabel met C# – Complete gids
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: Rijen verwijderen uit Excel‑tabel met C# – Stapsgewijze handleiding
url: /nl/net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Verwijder rijen uit Excel-tabel met C# – Complete programmeertutorial

Heb je ooit **delete rows excel table** uit een werkmap moeten verwijderen, maar wist je niet welke API‑aanroep je moest gebruiken? Je bent niet de enige—de meeste ontwikkelaars lopen tegen dezelfde muur aan wanneer ze voor het eerst proberen een tabel programmatisch te verkleinen.  

In deze gids lopen we een volledig, uitvoerbaar voorbeeld door dat niet alleen rijen uit een Excel‑tabel verwijdert, maar ook laat zien **how to add defined name** (ook wel een *named range* genoemd), hoe je **access worksheet by name** gebruikt, en waarom het toevoegen van een dubbele naam op een ander blad een `InvalidOperationException` veroorzaakt.  

Aan het einde van het artikel kun je:

* Een werkblad ophalen met behulp van de tabnaam.  
* Veilig gegevensrijen verwijderen uit de eerste tabel op dat blad.  
* Een named range maken die naar een specifiek adres wijst.  
* De valkuilen van dubbele namen over verschillende bladen begrijpen.

Geen externe documentatie nodig—alles wat je nodig hebt staat hier.

---

## Wat je nodig hebt

* **DevExpress Spreadsheet** (of elke bibliotheek die `Workbook`, `Worksheet`, `ListObject` en `Names` objecten blootlegt).  
* Een .NET‑project dat **.NET 6** of later targett (de code compileert ook met .NET Framework 4.8).  
* Basiskennis van C#—als je een `foreach`‑lus kunt schrijven, ben je klaar om te gaan.

> **Pro tip:** Als je de gratis Community‑edition van DevExpress gebruikt, zijn de hieronder gebruikte API’s identiek aan de commerciële versie.

---

## Stap 1 – Werkblad ophalen op naam

Het eerste wat je moet doen is het blad vinden dat de tabel bevat die je wilt aanpassen.  
De meeste ontwikkelaars grijpen uit gewoonte naar `Worksheets[0]`, maar dat koppelt je code aan de volgorde van bladen en breekt zodra iemand een tabblad een andere naam geeft.

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*Waarom dit belangrijk is:* Door de **naam** van het blad te gebruiken in plaats van de index, voorkom je per ongeluk bewerkingen op het verkeerde blad wanneer de werkmap verandert.

Als de opgegeven naam niet bestaat, gooit de bibliotheek een `KeyNotFoundException`, die je kunt opvangen om een vriendelijke foutmelding te tonen.

---

## Stap 2 – Rijen uit Excel‑tabel verwijderen (de veilige manier)

Nu je het juiste werkblad hebt, laten we de gegevensrijen uit de eerste tabel verwijderen.  
Een veelgemaakte fout is het aanroepen van `DeleteRows(1, rowCount‑1)`. Sinds **DevExpress 22.2** is die overload **verboden** en gooit een `InvalidOperationException`. De bibliotheek verwacht dat je rijen **binnen het gegevensbereik van de tabel** verwijdert, niet de koprij.

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

> **Wat als de tabel leeg is?** De `if`‑guard voorkomt een aanroep met `rowCount = 0`, wat anders een uitzondering zou veroorzaken.

### Visueel overzicht  

![voorbeeld van het verwijderen van rijen uit een Excel‑tabel](image.png "Schermafbeelding die laat zien hoe rijen uit een Excel‑tabel worden verwijderd")  

*Alt‑tekst: voorbeeld van het verwijderen van rijen uit een Excel‑tabel in C#‑code*

---

## Stap 3 – Hoe een gedefinieerde naam toevoegen (een named range maken)

Na het opschonen van de tabel wil je later misschien naar een specifiek bereik verwijzen—bijvoorbeeld voor een grafiek of een gegevensvalidatielijst. Daar komt **add named range excel** van pas.

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

De `Names.Add`‑methode neemt twee parameters: de identifier en het A1‑stijl adres.  
Omdat we eerder **access worksheet by name** hebben gebruikt, kan de adres‑string veilig naar elk blad verwijzen zonder je zorgen te maken over indexwijzigingen.

---

## Stap 4 – Named range op een ander blad – Vermijd fouten door dubbele namen

Je zou kunnen denken dat je dezelfde identifier op een ander blad kunt hergebruiken, zoals hier:

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

Helaas is de naamgevingsscope van Excel **werkmap‑breed**, niet per blad. De bovenstaande aanroep veroorzaakt een `InvalidOperationException` met de boodschap *“A name with the same identifier already exists.”*  

### Hoe dit te omzeilen

1. **Kies een unieke naam** (`MyTable_Sheet2`).  
2. **Verwijder de bestaande naam** voordat je deze opnieuw toevoegt (alleen als je deze echt wilt vervangen).  

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

---

## Volledig, uitvoerbaar voorbeeld

Alles bij elkaar genomen, hier is een zelfstandige console‑app die je in Visual Studio kunt plaatsen en kunt uitvoeren tegen een voorbeeldbestand `sample.xlsx`.

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

**Verwacht resultaat**

* Alle gegevensrijen uit de eerste tabel op **Sheet1** verdwijnen, waardoor alleen de koprij overblijft.  
* De naam **MyTable** wijst nu naar `Sheet1!$A$1:$C$5`.  
* Een tweede naam **MyTable_Sheet2** verwijst veilig naar een bereik op **Sheet2** zonder een uitzondering te veroorzaken.

---

## Veelgestelde vragen & randgevallen

| Vraag | Antwoord |
|----------|--------|
| *Wat als de werkmap meerdere tabellen bevat?* | Haal het juiste `ListObject` op via index (`worksheet.ListObjects[1]`) of via naam (`worksheet.ListObjects["MyTable"]`). |
| *Kan ik rijen verwijderen uit een tabel die zich over meerdere werkbladen uitstrekt?* | Nee—tabellen zijn beperkt tot één blad. Je moet de verwijderlogica voor elk blad herhalen. |
| *Is er een manier om alleen een deel van de rijen te verwijderen?* | Ja—gebruik `table.DeleteRows(startRow, count)` waarbij `startRow` nul‑gebaseerd is binnen het gegevensgebied van de tabel. |
| *Blijven named ranges behouden na het opslaan?* | Absoluut. Zodra je `SaveDocument` aanroept, worden de namen onderdeel van de XML van de werkmap. |
| *Hoe lijst ik alle gedefinieerde namen in de werkmap op?* | Itereer `foreach (var name in workbook.Names) Console.WriteLine(name.Name);`. |

---

## Conclusie

We hebben **delete rows excel table** met C# behandeld, **add named range excel** gedemonstreerd, en de juiste manier laten zien om **access worksheet by name** te gebruiken, terwijl we de gevreesde duplicate‑name‑exception vermijden.  

De volledige oplossing staat in de code‑snippet hierboven—kopieer, plak en voer het uit tegen je eigen bestanden. Vanaf hier kun je de logica uitbreiden om meerdere tabellen te verwerken, dynamische bereikberekeningen uit te voeren, of zelfs te integreren met een UI.

**Volgende stappen** die je kunt verkennen:

* Gebruik **named range on another sheet** om grafiekreeksen aan te sturen.  
* Combineer de verwijderlogica met **ExcelDataReader** om gegevens te importeren voordat je ze opruimt.  
* Automatiseer bulk‑updates over tientallen werkmappen met een eenvoudige `foreach (var file in Directory.GetFiles(...))`‑lus.

Heb je meer vragen over Excel‑automatisering in C#? Laat een reactie achter, en laten we het gesprek voortzetten. Veel plezier met coderen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}