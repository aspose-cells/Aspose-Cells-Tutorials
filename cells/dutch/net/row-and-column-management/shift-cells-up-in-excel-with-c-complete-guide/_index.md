---
category: general
date: 2026-07-13
description: Verplaats cellen omhoog in Excel met C#. Leer hoe je de eerste rijen
  verwijdert, meerdere rijen verwijdert en rijen uit een tabel verwijdert in één enkele,
  veilige bewerking.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- shift cells up
- remove first rows
- remove rows from table
- delete multiple rows
- how to delete rows
language: nl
lastmod: 2026-07-13
og_description: Verplaats cellen omhoog in een Excel-werkblad met C#. Deze tutorial
  laat zien hoe je de eerste rijen verwijdert, meerdere rijen verwijdert en rijen
  veilig uit een tabel verwijdert.
og_image_alt: Screenshot of C# code that shifts cells up after deleting rows in an
  Excel worksheet
og_title: Cellen omhoog verschuiven in Excel met C# – Volledige programmeerhandleiding
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Shift cells up in Excel using C#. Learn how to remove first rows, delete
    multiple rows, and remove rows from table in a single, safe operation.
  headline: Shift Cells Up in Excel with C# – Complete Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Loop through `sheet.Cells.Rows` and call `DeleteRows(rowIndex,
      1, true)` whenever the condition matches. Just remember to iterate backwards
      to avoid index shifting.
    question: Can I delete rows based on a condition instead of a fixed index?
  - answer: Yes. Aspose.Cells supports both `.xlsx` and legacy `.xls` formats. The
      same API applies.
    question: Does this work with `.xls` files?
  - answer: 'Target the specific table by name: `Table myTable = sheet.Tables["MyTable"];`
      then use `myTable.Range.StartRow` to calculate the rows to delete. --- ## Full
      Working Example Below is the complete, ready‑to‑run program that incorporates
      everything we discussed. Copy‑paste it into a console app, adjust'
    question: What if my workbook contains multiple tables and I only want to affect
      one?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cellen omhoog schuiven in Excel met C# – Complete gids
url: /nl/net/row-and-column-management/shift-cells-up-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cellen omhoog verschuiven in Excel met C# – Complete gids

Heb je je ooit afgevraagd hoe je **cell​en omhoog kunt verschuiven** na het verwijderen van rijen in een Excel‑bestand? Je bent niet de enige. Of je nu geïmporteerde gegevens opschoont of een enorm rapport inkort, de mogelijkheid om de eerste rijen te verwijderen zonder een tabel te breken is een onmisbare vaardigheid voor elke C#‑ontwikkelaar.

In deze tutorial lopen we een praktische, end‑to‑end oplossing door die laat zien **hoe je rijen verwijdert**, je header intact houdt, en automatisch de resterende cellen omhoog verschuift. Aan het einde kun je **rijen uit een tabel verwijderen**, **meerdere rijen verwijderen**, en **de eerste rijen verwijderen** in slechts een paar regels code.

---

## Wat je nodig hebt

- .NET 6+ (of .NET Framework 4.7.2 en hoger)  
- De **Aspose.Cells for .NET** bibliotheek (gratis proefversie of gelicentieerd)  
- Een basisbegrip van C# en Visual Studio (of een IDE naar keuze)  

Geen andere afhankelijkheden—alleen het NuGet‑pakket en een Excel‑bestand om mee te experimenteren.

## Stap 1: Installeer Aspose.Cells

Allereerst, voeg het Aspose.Cells‑pakket toe aan je project:

```bash
dotnet add package Aspose.Cells
```

Die ene regel haalt alles binnen wat je nodig hebt om met werkboeken, werkbladen en tabellen te werken. Als je Visual Studio gebruikt, kun je ook met de rechtermuisknop op het project klikken → **Manage NuGet Packages** → zoeken naar *Aspose.Cells* en op **Install** klikken.

*Pro tip:* Gebruik de nieuwste stabiele versie; vanaf juli 2026 is dat **23.9.0**, die de nieuwste Excel‑bestandsformaten ondersteunt.

## Stap 2: Laad het werkboek dat de tabel bevat

Nu openen we het Excel‑bestand dat de gegevens bevat die je wilt opschonen. Vervang `YOUR_DIRECTORY` door het daadwerkelijke pad op je machine.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the table
        Workbook workbook = new Workbook(@"C:\Data\table.xlsx");
        
        // Grab the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];
        
        // Optional: get a reference to the first table for context
        Table table = sheet.Tables[0];
```

Op dit moment hebben we een `Worksheet`‑object klaar voor manipulatie. Let op: we hebben de tabel nog niet aangeraakt—het behouden van de header is cruciaal wanneer we later **cell​en omhoog verschuiven**.

## Stap 3: Verwijder de eerste twee rijen terwijl je cellen omhoog verschuift

Dit is de kern van de zaak: rijen verwijderen *en* de cellen eronder automatisch laten opschuiven. Aspose.Cells biedt een `DeleteRows`‑methode die precies dat doet wanneer je `true` doorgeeft voor de `shiftCellsUp`‑vlag.

```csharp
        // Delete the first two rows (row index starts at 0)
        // The third argument ‑‑> true tells Aspose.Cells to shift cells up.
        sheet.Cells.DeleteRows(0, 2, true);
```

### Waarom de `true`‑vlag belangrijk is

Als je de `true`‑vlag weglaten, worden de rijen verwijderd maar blijft de ruimte die ze innamen leeg, waardoor er gaten in je gegevens ontstaan. Het instellen op **true** vertelt de bibliotheek om het bereik samen te trekken, effectief **cell​en omhoog te verschuiven** zodat rij 3 de nieuwe rij 1 wordt. Dit is de meest nette manier om **de eerste rijen te verwijderen** zonder formules of tabelstructuren te breken.

> **Belangrijk:** Het verwijderen van rijen die de tabelheader bevatten zal een uitzondering veroorzaken. Houd de header‑rij (meestal rij 0) intact, of verwijder deze apart nadat je de tabelheader opnieuw hebt aangemaakt.

## Stap 4: Controleer of de tabel er nog goed uitziet

Na het verwijderen is het een goed idee om dubbel te controleren of de tabelreferentie nog naar het juiste bereik wijst. Je kunt het adres van de tabel afdrukken of het vernieuwen:

```csharp
        // Refresh the table range to reflect the new data area
        table.Refresh();

        // Output the new range for debugging
        Console.WriteLine($"Table now spans: {table.Ref}");
```

Het uitvoeren van het programma zou iets moeten tonen als `Table1!A1:D8` in plaats van het oorspronkelijke `A1:D10`, wat bevestigt dat de rijen zijn verwijderd en de cellen omhoog zijn verschoven.

## Stap 5: Sla het gewijzigde werkboek op

Tot slot schrijf je de wijzigingen terug naar de schijf. Je kunt het oorspronkelijke bestand overschrijven of een nieuwe kopie maken—jouw keuze.

```csharp
        // Save the workbook with the changes
        workbook.Save(@"C:\Data\modified_table.xlsx");
    }
}
```

Open `modified_table.xlsx` in Excel, en je zult zien dat de eerste twee rijen verdwenen zijn, de resterende rijen omhoog zijn verschoven, en de tabel nog intact is. De bewerking heeft effectief **meerdere rijen verwijderd** terwijl de gegevensintegriteit behouden blijft.

## Randgevallen & Veelvoorkomende valkuilen

| Situatie | Wat gebeurt er | Hoe op te lossen |
|-----------|----------------|------------------|
| **Header‑rij maakt deel uit van het te verwijderen bereik** | Aspose.Cells gooit een `InvalidOperationException` omdat een tabel zijn header niet kan verliezen. | Verwijder alleen gegevensrijen, of maak de header opnieuw na het verwijderen met `sheet.Cells["A1"].PutValue("Header")`. |
| **Tabel strekt zich uit over meerdere werkbladen** | Het verwijderen van rijen op één blad heeft geen effect op de andere. | Loop over de tabellen van elk werkblad als je een globale opschoning nodig hebt. |
| **Grote bestanden (>100 MB)** | Het geheugenverbruik stijgt. | Gebruik `LoadOptions` met `MemoryPreference` ingesteld op `MemoryPreference.MemoryOnly` om de RAM‑voetafdruk te verkleinen. |
| **Je moet formules behouden die naar de verwijderde rijen verwijzen** | Formules kunnen `#REF!` worden. | Gebruik `sheet.Cells.DeleteRows(startRow, count, true, true)` – het vierde argument vertelt Aspose.Cells om formules bij te werken. |

## Veelgestelde vragen

**Q: Kan ik rijen verwijderen op basis van een voorwaarde in plaats van een vaste index?**  
A: Absoluut. Loop door `sheet.Cells.Rows` en roep `DeleteRows(rowIndex, 1, true)` aan telkens wanneer de voorwaarde overeenkomt. Vergeet niet achterwaarts te itereren om indexverschuiving te voorkomen.

**Q: Werkt dit met `.xls`‑bestanden?**  
A: Ja. Aspose.Cells ondersteunt zowel `.xlsx` als de oudere `.xls`‑formaten. Dezelfde API is van toepassing.

**Q: Wat als mijn werkboek meerdere tabellen bevat en ik slechts één wil aanpassen?**  
A: Richt je op de specifieke tabel op naam: `Table myTable = sheet.Tables["MyTable"];` en gebruik vervolgens `myTable.Range.StartRow` om de te verwijderen rijen te berekenen.

## Volledig werkend voorbeeld

Hieronder staat het volledige, kant‑klaar programma dat alles wat we hebben besproken bevat. Kopieer‑plak het in een console‑app, pas de bestandspaden aan, en druk op **F5**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"C:\Data\table.xlsx");
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ (Optional) Reference the first table for context
        Table table = sheet.Tables[0];

        // 3️⃣ Delete the first two rows and shift cells up
        //    Row index starts at 0, delete 2 rows, shift up = true
        sheet.Cells.DeleteRows(0, 2, true);

        // 4️⃣ Refresh the table range so it reflects the new data area
        table.Refresh();

        // 5️⃣ Show the new table reference (useful for debugging)
        Console.WriteLine($"Table now spans: {table.Ref}");

        // 6️⃣ Save the modified workbook
        workbook.Save(@"C:\Data\modified_table.xlsx");

        Console.WriteLine("Rows removed and cells shifted up successfully!");
    }
}
```

**Verwacht resultaat:**  
- Rijen 1‑2 verdwijnen van het blad.  
- Rij 3 wordt de nieuwe rij 1, rij 4 wordt rij 2, enz.  
- Het bereik van de tabel wordt automatisch bijgewerkt, wat bevestigt dat **cell​en omhoog verschuiven** werkt zoals bedoeld.

## Conclusie

We hebben zojuist behandeld hoe je **cell​en omhoog verschuift** in een Excel‑werkblad met C#. Door gebruik te maken van Aspose.Cells’ `DeleteRows`‑methode met de `true`‑vlag, kun je veilig **de eerste rijen verwijderen**, **meerdere rijen verwijderen**, en **rijen uit een tabel verwijderen** zonder je datamodel te breken. De aanpak is snel, betrouwbaar, en werkt met alle moderne Excel‑formaten.

Klaar voor de volgende stap? Probeer deze techniek te combineren met een voorwaardelijke filter om rijen met lege of dubbele waarden te verwijderen. Of verken Aspose.Cells’ styling‑API’s om opmaak opnieuw toe te passen na de verschuiving. De mogelijkheden zijn eindeloos als je rij‑manipulatie in Excel onder de knie hebt.

Heb je vragen of een cool use‑case die je wilt delen? Laat een reactie achter hieronder, en happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Meerdere rijen verwijderen in Excel met Aspose.Cells .NET: Een uitgebreide gids voor gegevensmanipulatie](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [Hoe rijen in Excel in te voegen en te verwijderen met Aspose.Cells voor .NET: Een uitgebreide gids](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Hoe lege rijen te verwijderen in Excel met Aspose.Cells .NET voor gegevensopschoning](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}