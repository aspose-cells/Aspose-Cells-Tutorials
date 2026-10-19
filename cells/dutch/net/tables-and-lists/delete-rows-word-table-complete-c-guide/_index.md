---
category: general
date: 2026-06-08
description: Rijen uit een Word‑tabel verwijderen met Aspose.Words. Leer hoe je rijen
  verwijdert, meerdere rijen in Word verwijdert en tabelbewerking in enkele minuten
  onder de knie krijgt.
draft: false
keywords:
- delete rows word table
- how to delete rows
- delete multiple rows word
language: nl
og_description: Verwijder rijen uit een Word‑tabel met Aspose.Words. Deze tutorial
  laat zien hoe je rijen verwijdert, meerdere rijen in Word verwijdert en je tabellen
  netjes houdt.
og_title: Rijen verwijderen uit Word‑tabel – Complete C#‑gids
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Delete rows word table using Aspose.Words. Learn how to delete rows,
    delete multiple rows word, and master table editing in minutes.
  headline: Delete rows word table – Complete C# Guide
  type: TechArticle
- description: Delete rows word table using Aspose.Words. Learn how to delete rows,
    delete multiple rows word, and master table editing in minutes.
  name: Delete rows word table – Complete C# Guide
  steps:
  - name: 3.1 How to delete rows (single row)
    text: 'To remove a single row, call `DeleteRows(startIndex, count)` where `startIndex`
      is zero‑based. Skipping the header row (index 0) is common:'
  - name: 3.2 Delete multiple rows word – batch removal
    text: 'When you need to drop a range—say rows 2‑6—you pass the start index and
      the number of rows to erase. This is the **delete multiple rows word** pattern:'
  - name: Expected output
    text: '- `output.docx` contains the original table **without** rows 2‑6. - All
      remaining rows shift up, preserving cell formatting and column widths. - The
      header row stays intact, keeping your column titles visible.'
  type: HowTo
- questions:
  - answer: Absolutely. Loop through `table.Rows`, inspect `row.Cells[i].GetText()`,
      and collect matching indices. Then call `DeleteRows` with the smallest index
      and total count, or delete rows in reverse order to avoid re‑indexing.
    question: Can I delete rows based on cell content instead of index?
  - answer: Yes. Aspose.Words supports both `.doc` and `.docx`. Just change the file
      extension in the `Document` constructor and `Save` call.
    question: Does this work with .doc files?
  - answer: 'Retrieve it via `doc.FirstSection.HeadersFooters` collection, then apply
      the same `DeleteRows` logic. ## Conclusion You now have a solid, end‑to‑end
      solution for **delete rows word table** using C#. The example shows *how to
      delete rows* individually and how to **delete multiple rows word** in a sin'
    question: What if the table is inside a header/footer?
  type: FAQPage
tags:
- C#
- Aspose.Words
- Word automation
title: Rijen uit Word‑tabel verwijderen – Complete C#‑gids
url: /nl/net/tables-and-lists/delete-rows-word-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Verwijder rijen Word‑tabel – Complete C#‑gids

Ever needed to **delete rows word table** but weren’t sure where to start? You’re not alone; many developers hit this snag when cleaning up generated reports or trimming data‑driven tables. The good news? With a few lines of C# and Aspose.Words you can easily remove unwanted rows, whether it’s a single line or a batch of them. In this guide we’ll walk through *how to delete rows* and even cover the trickier case of **delete multiple rows word** in one go.

We’ll cover everything you need to know: the exact code, why each step matters, common pitfalls, and a ready‑to‑run example. By the end you’ll be able to drop rows from any Word table without breaking the document structure. No fluff, just practical, battle‑tested techniques.

## Vereisten

Before we dive in, make sure you have:

- **Aspose.Words for .NET** (versie 23.12 of nieuwer). Je kunt het ophalen via NuGet: `Install-Package Aspose.Words`.
- Een .NET‑ontwikkelomgeving (Visual Studio, Rider, of VS Code met de C#‑extensie).
- Een invoer‑Word‑bestand (`input.docx`) dat minstens één tabel met een koprij bevat.

That’s it—no extra libraries, no COM interop, just pure managed code.

## Stap 1: Laad het Word‑document

The first thing you do is open the document. Aspose.Words treats a Word file as a `Document` object, which gives you full access to sections, bodies, tables, and more.

```csharp
using Aspose.Words;

class TableCleaner
{
    static void Main()
    {
        // Load the source .docx file
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        // Continue with table manipulation…
```

*Waarom dit belangrijk is:* Loading the document creates an in‑memory representation, so any changes you make are fast and don’t touch the file system until you explicitly save.

## Stap 2: Haal de doel‑tabel op

In most scenarios you know which table you want to edit—often the first one. Aspose.Words makes it trivial to fetch it via the `FirstSection` property.

```csharp
        // Access the first table in the first section
        Table table = doc.FirstSection.Body.Tables[0];
```

If your document has multiple tables, you can loop through `doc.GetChildNodes(NodeType.Table, true)` and pick the right one based on index or a custom marker.

## Stap 3: Verwijder rijen – enkel of meerdere

### 3.1 Hoe rijen te verwijderen (enkele rij)

To remove a single row, call `DeleteRows(startIndex, count)` where `startIndex` is zero‑based. Skipping the header row (index 0) is common:

```csharp
        // Delete just the second row (index 1)
        table.DeleteRows(1, 1);
```

### 3.2 Delete multiple rows word – batchverwijdering

When you need to drop a range—say rows 2‑6—you pass the start index and the number of rows to erase. This is the **delete multiple rows word** pattern:

```csharp
        // Delete rows 2‑6 (skip header at index 0)
        // startIndex = 1 (second row), count = 5 rows
        table.DeleteRows(1, 5);
```

*Waarom een enkele oproep gebruiken?* Deleting rows one‑by‑one forces the table to re‑index after each removal, which can be error‑prone and slower. The bulk method keeps the table’s internal structure consistent.

#### Randgeval: Verwijderen buiten de tabelgrootte

If `startIndex + count` exceeds the actual row count, Aspose.Words throws an `ArgumentOutOfRangeException`. A defensive guard looks like this:

```csharp
        int rowsToDelete = Math.Min(5, table.Rows.Count - 1); // never delete the header
        if (rowsToDelete > 0)
            table.DeleteRows(1, rowsToDelete);
```

That snippet ensures you never attempt to delete more rows than exist.

## Stap 4: Sla het gewijzigde document op

Once the rows are gone, persisting the changes is a single line:

```csharp
        // Save the cleaned document
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

The `Save` method automatically chooses the format based on the file extension, so you could output to PDF, HTML, or even ODT with a different suffix.

## Volledig Werkend Voorbeeld

Putting it all together, here’s the complete, ready‑to‑run program:

```csharp
using System;
using Aspose.Words;

class TableCleaner
{
    static void Main()
    {
        // 1️⃣ Load the Word document
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // 2️⃣ Access the first table (adjust index if needed)
        Table table = doc.FirstSection.Body.Tables[0];

        // 3️⃣ Delete rows 2‑6 (skip header row at index 0)
        //    This demonstrates delete multiple rows word in one call.
        if (table.Rows.Count > 1) // ensure there is at least a header + one data row
        {
            int rowsToDelete = Math.Min(5, table.Rows.Count - 1);
            table.DeleteRows(1, rowsToDelete);
        }

        // 4️⃣ Save the modified document
        doc.Save(@"YOUR_DIRECTORY\output.docx");

        Console.WriteLine("Rows removed successfully. Output saved to output.docx");
    }
}
```

### Verwachte output

- `output.docx` contains the original table **without** rows 2‑6.
- All remaining rows shift up, preserving cell formatting and column widths.
- The header row stays intact, keeping your column titles visible.

## Waarom deze aanpak beter is dan de alternatieven

| Aanpak | Voordelen | Nadelen |
|----------|------|------|
| **Aspose.Words `DeleteRows`** | Eenregelige bulkverwijdering, behoudt stijlen, geen COM‑afhankelijkheden | Vereist een commerciële bibliotheek (gratis proefversie beschikbaar) |
| Office Interop | Werkt met native Word | Vereist Word geïnstalleerd op de server, traag, COM‑opruimingsproblemen |
| Open XML SDK | Gratis, open source | Handmatige XML‑manipulatie; rijen veilig verwijderen is omslachtig |

## Pro‑tips & veelvoorkomende valkuilen

- **Pro tip:** Houd de koprij (index 0) altijd onaangeroerd tenzij je deze echt wilt verwijderen. Het verwijderen van de koprij kan downstream‑verwerking die kolomnamen verwacht breken.
- **Let op samengevoegde cellen.** Als een rij een verticaal samengevoegde cel bevat die zich uitstrekt tot de rij die je verwijdert, past Aspose.Words automatisch het samenvoegbereik aan, maar controleer het visuele resultaat.
- **Prestatie‑opmerking:** Het verwijderen van veel rijen uit een enorme tabel (duizenden rijen) is nog steeds snel, maar als je honderden documenten in een lus verwerkt, overweeg dan om het `Document`‑object waar mogelijk te hergebruiken om toewijzings‑overhead te verminderen.

## Veelgestelde vragen

**Q: Kan ik rijen verwijderen op basis van celinhoud in plaats van index?**  
A: Absoluut. Loop door `table.Rows`, inspecteer `row.Cells[i].GetText()`, en verzamel overeenkomende indices. Roep vervolgens `DeleteRows` aan met de kleinste index en het totale aantal, of verwijder rijen in omgekeerde volgorde om herindexering te vermijden.

**Q: Werkt dit met .doc‑bestanden?**  
A: Ja. Aspose.Words ondersteunt zowel `.doc` als `.docx`. Verander gewoon de bestandsextensie in de `Document`‑constructor en de `Save`‑aanroep.

**Q: Wat als de tabel zich in een header/footer bevindt?**  
A: Haal deze op via de `doc.FirstSection.HeadersFooters`‑collectie en pas vervolgens dezelfde `DeleteRows`‑logica toe.

## Conclusie

You now have a solid, end‑to‑end solution for **delete rows word table** using C#. The example shows *how to delete rows* individually and how to **delete multiple rows word** in a single, efficient call. With Aspose.Words you get a clean API, no COM hassles, and full control over Word documents.

Ready for the next challenge? Try adding a new row with calculated totals, or export the trimmed table to CSV using `Table.ToTxt`. The sky’s the limit when you master table manipulation.

Happy coding, and may your Word tables stay tidy!

## Wat moet je hierna leren?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step‑by‑step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Hoe rijen te verwijderen in Excel met Aspose.Cells voor Java | Gids & Tutorial](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)
- [Hoe lege rijen te verwijderen in Excel met Aspose.Cells .NET voor data‑opschoning](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)
- [Hoe rijen in te voegen en te verwijderen in Excel met Aspose.Cells voor .NET&#58; Een uitgebreide gids](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}