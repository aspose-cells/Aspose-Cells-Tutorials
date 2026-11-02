---
category: general
date: 2026-10-10
description: Leer hoe je een volledige rij in een Excel‑werkmap kunt verwijderen met
  C#. Deze stapsgewijze gids behandelt ook hoe je een rij op index kunt verwijderen
  en een rij op index kunt weghalen met Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete entire row
- how to delete row
- remove row by index
- delete row excel
- delete row c#
language: nl
lastmod: 2026-10-10
og_description: Verwijder een volledige rij in een Excel-werkmap met C#. Volg deze
  gids om te leren hoe je een rij op index kunt verwijderen, een rij op index kunt
  weghalen en het bestand veilig kunt opslaan.
og_image_alt: Screenshot of an Excel worksheet before and after deleting an entire
  row with C# code
og_title: Verwijder volledige rij in Excel met C# – volledige programmeergids
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to delete entire row in an Excel workbook with C#. This step‑by‑step
    guide also covers how to delete row by index and remove row by index using Aspose.Cells.
  headline: How to delete entire row in an Excel file using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Hoe een volledige rij in een Excel‑bestand te verwijderen met C#
url: /nl/net/row-and-column-management/how-to-delete-entire-row-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Verwijder volledige rij in een Excel‑bestand met C#

Als je een **verwijder volledige rij** in een Excel‑werkmap moet uitvoeren, laat deze gids je precies zien hoe je dat doet met C#. Of je nu geïmporteerde gegevens opschoont of een rapportagetool bouwt, de onderstaande stappen laten je een rij op basis van zijn index verwijderen en het resultaat opslaan zonder andere gegevens te verliezen.

Je ziet ook hoe dezelfde aanpak de vraag beantwoordt **how to delete row** op index, hoe je **remove row by index** uitvoert, en waarom dit werkt voor **delete row excel** scenario’s in C#.

## Vereisten

Voordat je begint, zorg dat je het volgende hebt:

* .NET 6.0 of later (de code werkt ook met .NET Framework 4.6+)  
* De **Aspose.Cells for .NET**‑bibliotheek (beschikbaar via NuGet: `Install-Package Aspose.Cells`)  
* Basiskennis van C#‑console‑ of desktop‑projecten  

Er zijn geen extra Excel‑interop‑ of COM‑componenten nodig, waardoor de oplossing lichtgewicht en veilig is voor server‑side uitvoering.

## Stap 1: Het project opzetten en namespaces importeren

Maak een nieuwe console‑applicatie (of voeg de code toe aan een bestaand project) en voeg de benodigde `using`‑directieven toe:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the tutorial code lives here.
        }
    }
}
```

*Waarom dit belangrijk is*: Het importeren van `Aspose.Cells` geeft je toegang tot `Workbook`, `Worksheet` en de `DeleteRows`‑methode die de daadwerkelijke rijverwijdering uitvoert.

## Stap 2: Laad de werkmap en selecteer het werkblad

Je moet het bronbestand (`input.xlsx`) laden en het werkblad verkrijgen dat je wilt aanpassen. Het eerste werkblad wordt benaderd met index `0`.

```csharp
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Get the first worksheet (you can also use workbook.Worksheets["SheetName"])
Worksheet ws = workbook.Worksheets[0];
```

> **Tip**: Als je met een specifiek blad wilt werken, vervang dan de index door de bladnaam: `workbook.Worksheets["Data"]`.

## Stap 3: Verwijder de volledige rij op basis van zijn nul‑gebaseerde index

Aspose.Cells gebruikt nul‑gebaseerde indexering, dus de eerste rij is `0`. Om rij 5 (de zesde visuele rij) te verwijderen, roep je `DeleteRows` aan met `DeleteOptions.DeleteEntireRow`.

```csharp
// Delete one row starting at index 5 (zero‑based) and remove the whole row
ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
```

*Uitleg*:

* `ws.Cells[5, 0]` wijst naar de eerste cel van de rij die je wilt verwijderen.  
* `DeleteRows(1, DeleteOptions.DeleteEntireRow)` vertelt Aspose.Cells om **1** rij te verwijderen, en de `DeleteEntireRow`‑vlag zorgt ervoor dat **de hele rij** verdwijnt, waarbij de rijen eronder omhoog verschuiven.

### Hoe een rij op index te verwijderen in andere scenario’s

* **Meerdere opeenvolgende rijen verwijderen** – wijzig het eerste argument naar het aantal rijen dat je wilt wissen:

  ```csharp
  // Remove rows 5, 6 and 7 (three rows total)
  ws.Cells[5, 0].DeleteRows(3, DeleteOptions.DeleteEntireRow);
  ```

* **De laatste rij verwijderen** – gebruik `ws.Cells.MaxDataRow` om de index van de onderste gevulde rij te verkrijgen:

  ```csharp
  int lastRow = ws.Cells.MaxDataRow;
  ws.Cells[lastRow, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
  ```

Deze fragmenten beantwoorden de **remove row by index**‑vereiste terwijl de code overzichtelijk blijft.

## Stap 4: Sla de werkmap op met de verwijderde rij

Na de verwijdering schrijf je de aangepaste werkmap terug naar de schijf. Je kunt het oorspronkelijke bestand overschrijven of een nieuw bestand aanmaken.

```csharp
// Save the workbook to a new file (or overwrite the original)
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

Als je het originele bestand ongewijzigd wilt laten, wijzig dan simpelweg het uitvoerpad. De `Save`‑methode ondersteunt vele formaten (`.xls`, `.csv`, `.pdf`, enz.) – wijzig gewoon de bestandsextensie.

## Volledig werkend voorbeeld

Alles samengevoegd, hier is een compleet, kant‑klaar programma:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Select the first worksheet
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Delete the entire row at index 5 (sixth visual row)
            ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);

            // 4️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Row deleted successfully. Output saved to output.xlsx");
        }
    }
}
```

**Verwachte output**: Na het uitvoeren van het programma bevat `output.xlsx` alle oorspronkelijke rijen behalve die die begon op visuele rij 6. Alle gegevens onder de verwijderde rij schuiven automatisch omhoog, waardoor formules en opmaak behouden blijven.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| **Index out of range** | Proberen een rij‑index te verwijderen die niet bestaat (bijv. `ws.Cells[1000,0]` in een blad met 200 rijen) | Gebruik `ws.Cells.MaxDataRow` om de hoogste geldige index te verifiëren vóór het aanroepen van `DeleteRows`. |
| **Partial row deletion** | Het weglaten van `DeleteOptions.DeleteEntireRow` leidt tot alleen het wissen van celinhoud | Geef altijd `DeleteOptions.DeleteEntireRow` door wanneer je de hele rij wilt verwijderen. |
| **Unexpected formula changes** | Rijen die deel uitmaken van een formule‑bereik verwijderen kan referenties breken | Evalueer formules opnieuw na het verwijderen (`workbook.CalculateFormula()`) als je werkmap afhankelijk is van dynamische bereiken. |
| **Saving to a read‑only location** | De `Save`‑aanroep gooit een uitzondering als de map beschermd is | Zorg dat de doelmap beschrijfbaar is of voer het programma uit met de juiste rechten. |

Het aanpakken van deze punten maakt de oplossing robuust voor productie en beantwoordt de **delete row excel**‑ en **delete row c#**‑vragen.

## Geavanceerd: Rijen verwijderen op basis van een voorwaarde

Soms moet je rijen verwijderen die aan een bepaald criterium voldoen (bijv. rijen waarbij kolom A leeg is). De volgende lus toont een veilige manier om van onder naar boven te scannen en overeenkomende rijen te verwijderen:

```csharp
int lastRow = ws.Cells.MaxDataRow;
for (int row = lastRow; row >= 0; row--)
{
    // Check if column A (index 0) is empty
    if (ws.Cells[row, 0].StringValue == string.Empty)
    {
        ws.Cells[row, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
    }
}
workbook.Save("YOUR_DIRECTORY/cleaned.xlsx");
```

Naar boven scannen voorkomt het index‑verschuivingsprobleem dat optreedt wanneer je rijen verwijdert terwijl je vooruit iterereert.

## Conclusie

Je weet nu hoe je een **delete entire row** in een Excel‑werkmap kunt uitvoeren met C#. De gids besprak:

* Het laden van een werkmap en selecteren van een werkblad  
* Het gebruik van `DeleteRows` met `DeleteOptions.DeleteEntireRow` om **how to delete row** op index uit te voeren  
* Het veilig opslaan van het gewijzigde bestand  
* Afhandeling van randgevallen, prestatietips en een voorbeeld van conditionele verwijdering  

Met deze kennis kun je vol vertrouwen **remove row by index** functionaliteit implementeren, data‑opschoning automatiseren en Excel‑manipulatie integreren in elke C#‑applicatie.  

**Volgende stappen**: verken andere Aspose.Cells‑functies zoals rijen invoegen, bereiken kopiëren, of de werkmap naar PDF converteren — elk bouwt voort op dezelfde `Workbook`‑ en `Worksheet`‑objecten die je zojuist onder de knie hebt. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementaties in je eigen projecten te verkennen.

- [Hoe een Excel‑rij te verwijderen met Aspose.Cells .NET: Een uitgebreide gids](/cells/english/net/worksheet-management/delete-excel-row-aspose-cells-net-tutorial/)
- [Aspose Cells rijen verwijderen – Koprij beschermen in Excel](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [Efficiënt rijen beheren in Excel met Aspose.Cells voor Java: Rijen invoegen en verwijderen](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}