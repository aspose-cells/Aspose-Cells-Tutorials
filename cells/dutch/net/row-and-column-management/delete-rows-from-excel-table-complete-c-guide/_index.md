---
category: general
date: 2026-08-07
description: Verwijder rijen uit een Excel‑tabel met C#. Leer hoe je gegevensrijen
  in Excel veilig kunt verwijderen terwijl je de koprij beschermt, in slechts een
  paar stappen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from excel table
- remove data rows excel
- protect header row excel
language: nl
lastmod: 2026-08-07
og_description: Verwijder rijen uit een Excel‑tabel via code. Deze gids laat zien
  hoe je veilig gegevensrijen in Excel verwijdert en de koprij in Excel beschermt
  met Aspose.Cells.
og_image_alt: Screenshot of C# code that deletes rows from an Excel table while keeping
  the header intact
og_title: Rijen verwijderen uit Excel‑tabel – snelle C#‑oplossing
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Delete rows from Excel table using C#. Learn how to remove data rows
    Excel safely while protecting header row Excel in just a few steps.
  headline: Delete rows from Excel table – complete C# guide
  type: TechArticle
- description: Delete rows from Excel table using C#. Learn how to remove data rows
    Excel safely while protecting header row Excel in just a few steps.
  name: Delete rows from Excel table – complete C# guide
  steps:
  - name: Run the program with a sample workbook that has at least five data rows.
    text: Run the program with a sample workbook that has at least five data rows.
  - name: Verify that the console prints “Rows deleted and workbook saved successfully.”
    text: Verify that the console prints “Rows deleted and workbook saved successfully.”
  - name: 'Open `TableHeaderProtected.xlsx` in Excel and confirm:'
    text: 'Open `TableHeaderProtected.xlsx` in Excel and confirm:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
- Data manipulation
title: Rijen verwijderen uit Excel‑tabel – volledige C#‑gids
url: /nl/net/row-and-column-management/delete-rows-from-excel-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rijen verwijderen uit Excel-tabel – volledige C#‑gids

Als je **rijen uit Excel-tabel wilt verwijderen** in een .NET‑project, laat deze tutorial je een betrouwbare manier zien om dit te doen. Of je nu geïmporteerde gegevens wilt opschonen of een rapport wilt inkorten, je ziet hoe je gegevensrijen in Excel kunt verwijderen terwijl de API automatisch **protect header row excel** beschermt tegen accidentele verwijdering.

In de onderstaande stappen leer je hoe je een werkmap laadt, veilig rijen verwijdert en uiteindelijk de wijzigingen opslaat. De gids behandelt ook de veelvoorkomende fout van het proberen te verwijderen van de koprij en legt uit waarom de bibliotheek dit voorkomt. Aan het einde kun je **remove data rows excel** vol vertrouwen gebruiken in elke Aspose.Cells‑gebaseerde oplossing.

## Vereisten

- .NET 6.0 of later geïnstalleerd.
- Het **Aspose.Cells for .NET** NuGet‑pakket (versie 23.10 of nieuwer). Installeer het met:

  ```bash
  dotnet add package Aspose.Cells
  ```

- Een Excel‑bestand (`TableWithHeader.xlsx`) dat een gestructureerde tabel met een koprij bevat in het eerste werkblad.
- Basiskennis van C# en Visual Studio (of een andere IDE naar keuze).

## Stap 1: Laad de werkmap die een tabel met een koprij bevat

De eerste handeling is het openen van de werkmap die de tabel bevat die je wilt aanpassen. Aspose.Cells leest het bestand in het geheugen zonder dat Excel geïnstalleerd hoeft te zijn.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the workbook from disk
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\TableWithHeader.xlsx");

        // Continue with the next steps...
```

**Waarom dit belangrijk is:** Het laden van de werkmap creëert een `Workbook`‑object dat je toegang geeft tot werkbladen, tabellen en cellen. Zonder dit object kun je de Excel‑structuur niet manipuleren.

## Stap 2: Toegang tot het eerste werkblad en de eerste tabel

De meeste eenvoudige voorbeelden houden de tabel in het eerste werkblad en op index 0, maar je kunt de indexen aanpassen voor jouw scenario.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Retrieve the first ListObject (Excel table) on that worksheet
        ListObject table = worksheet.Tables[0];
```

**Waarom dit belangrijk is:** `ListObject` vertegenwoordigt een Excel‑tabel, die de koprij, gegevensrijen en eventuele opmaak omvat. Werken met het tabelobject zorgt ervoor dat je de semantiek van Excel‑tabellen respecteert, zoals het beschermen van de koprij.

## Stap 3: Probeer de koprij te verwijderen (bescherming demonstreren)

Aspose.Cells gooit een uitzondering als je probeert de koprij te verwijderen omdat de API **protect header row excel** standaard beschermt. Het tonen van dit gedrag helpt je te begrijpen waarom een directe verwijdering mislukt.

```csharp
        try
        {
            // Attempt to delete the header row (index 0) and the row below it
            table.DeleteRows(0, 2);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Deletion prevented: " + ex.Message);
        }
```

**Verwachte output**

```
Deletion prevented: Cannot delete the header row of a table.
```

**Uitleg:** De `DeleteRows`‑methode ontvangt een nul‑gebaseerde startindex en een aantal. Index 0 wijst naar de koprij, die de bibliotheek beschermt om de structuur van de tabel intact te houden.

## Stap 4: Alleen gegevensrijen verwijderen – de juiste manier om **remove data rows excel**

Nu je weet dat de koprij beschermd is, verwijder je alleen de gegevensrijen die beginnen na de koprij. In de meeste tabellen staat de eerste gegevensrij op index 1.

```csharp
        // Delete three data rows starting after the header (index 1)
        table.DeleteRows(1, 3); // removes rows 2, 3, and 4 of the worksheet

        // Optionally, you can delete a single row:
        // table.DeleteRows(4, 1);
```

**Waarom dit werkt:** Door te beginnen op index 1 sla je de koprij over, zodat de bewerking voldoet aan de **protect header row excel**‑regel. De `DeleteRows`‑methode werkt het interne bereik van de tabel automatisch bij.

## Stap 5: Sla de aangepaste werkmap op

Sla de wijzigingen op in een nieuw bestand zodat je het origineel intact houdt.

```csharp
        // Save the workbook with the modified table
        workbook.Save(@"YOUR_DIRECTORY\TableHeaderProtected.xlsx");

        Console.WriteLine("Rows deleted and workbook saved successfully.");
    }
}
```

**Resultaat:** Na het uitvoeren van het programma bevat `TableHeaderProtected.xlsx` dezelfde koprij, maar zijn de opgegeven gegevensrijen verdwenen. Het openen van het bestand in Excel toont een schone tabel zonder de verwijderde rijen.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Valkuil | Waarom het gebeurt | Oplossing |
|---------|--------------------|-----------|
| Proberen de koprij te verwijderen | Aspose.Cells handhaaft tabelintegriteit | Begin altijd met verwijderen op index 1 of hoger |
| Meer rijen verwijderen dan bestaan | `DeleteRows` gooit `ArgumentOutOfRangeException` | Controleer `table.DataRange.RowCount` voordat je `DeleteRows` aanroept |
| Werken met een niet‑tabelbereik | `ListObject`‑methoden zijn alleen van toepassing op gestructureerde tabellen | Zet eerst een bereik om naar een tabel (`worksheet.Tables.Add`) indien nodig |

**Pro tip:** Als je de hele tabel wilt wissen maar de koprij wilt behouden, gebruik `table.DeleteRows(1, table.DataRange.RowCount - 1);`. Dit verwijdert elke gegevensrij, ongeacht hoeveel rijen de tabel momenteel heeft.

## Alternatief: Rijen verwijderen op basis van celadres

Soms ken je het exacte celadres in plaats van de rij‑index. Je kunt een adres omzetten naar een rij‑index met de `Cells`‑collectie:

```csharp
        // Example: delete rows that contain the value "Obsolete"
        for (int i = table.DataRange.FirstRow; i <= table.DataRange.LastRow; i++)
        {
            if (worksheet.Cells[i, table.DataRange.FirstColumn].StringValue == "Obsolete")
            {
                // Subtract one because DeleteRows expects a zero‑based index relative to the table
                table.DeleteRows(i - table.StartRow + 1, 1);
                i--; // Adjust loop counter after deletion
            }
        }
```

Deze aanpak is handig wanneer rijen die moeten worden verwijderd worden geïdentificeerd op basis van inhoud in plaats van een vaste telling.

## Test je implementatie

1. Voer het programma uit met een voorbeeld‑werkmap die minimaal vijf gegevensrijen bevat.  
2. Controleer of de console “Rows deleted and workbook saved successfully.” afdrukt.  
3. Open `TableHeaderProtected.xlsx` in Excel en bevestig:
   - De koprij is nog aanwezig.
   - Alleen de beoogde gegevensrijen ontbreken.

Als de koprij verdwijnt, ben je waarschijnlijk begonnen met verwijderen op index 0 — bekijk **Stap 4**.

## Conclusie

Je weet nu hoe je **rijen uit Excel-tabel** veilig kunt verwijderen met C#. De gids behandelde het laden van een werkmap, het benaderen van de tabel, het respecteren van de **protect header row excel**‑regel, het correct **remove data rows excel**, en het opslaan van het resultaat. Door deze stappen te volgen vermijd je veelvoorkomende fouten en houd je je Excel‑tabellen goed gestructureerd.

### Volgende stappen

- Verken **Aspose.Cells**‑functies zoals rijen invoegen, stijlen toepassen of gegevens filteren.  
- Combineer het verwijderen van rijen met **Excel‑formules** om opschoning te automatiseren op basis van berekeningsresultaten.  
- Bekijk gerelateerde onderwerpen zoals **exporting Excel to CSV** of **reading large workbooks efficiently**.

Voel je vrij om te experimenteren met verschillende aantallen rijen, meerdere tabellen of voorwaardelijke verwijderingen. Als je tegen randgevallen aanloopt, raadpleeg dan opnieuw de foutafhandeling die in **Stap 3** wordt getoond — de bibliotheek beschermt altijd de koprij voor je. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Meerdere rijen verwijderen in Excel met Aspose.Cells .NET: Een uitgebreide gids voor gegevensmanipulatie](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [Hoe rijen invoegen en verwijderen in Excel met Aspose.Cells voor .NET: Een uitgebreide gids](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Hoe lege rijen verwijderen in Excel met Aspose.Cells .NET voor gegevensopschoning](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}