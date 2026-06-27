---
category: general
date: 2026-06-27
description: Meerdere rijen verwijderen in Word met C#. Leer hoe je tabelrijen kunt
  verwijderen, tabelrijen kunt weghalen en Word‑documenttabellen efficiënt kunt bewerken.
draft: false
keywords:
- delete multiple rows word
- how to delete table rows
- how to remove table rows
- delete rows from word table
- word document table editing
language: nl
og_description: Verwijder meerdere rijen in Word direct. Deze tutorial laat zien hoe
  je tabelrijen verwijdert, rijen uit een Word‑tabel verwijdert en het bewerken van
  tabellen in een Word‑document beheerst.
og_title: Meerdere rijen verwijderen in Word – Stap‑voor‑stap tabelbewerking
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Delete multiple rows word using C#. Learn how to delete table rows,
    remove table rows and edit Word document tables efficiently.
  headline: Delete Multiple Rows Word – Complete Guide to Removing Table Rows
  type: TechArticle
tags:
- Aspose.Words
- C#
- Word Automation
title: Meerdere rijen verwijderen in Word – Complete gids voor het verwijderen van
  tabelrijen
url: /nl/net/tables-and-lists/delete-multiple-rows-word-complete-guide-to-removing-table-r/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Meerdere rijen verwijderen in Word – Complete gids voor het verwijderen van tabelrijen

Heb je ooit meerdere rijen in Word‑documenten moeten **verwijderen**, maar wist je niet welke API‑aanroep je moest gebruiken? Je bent niet de enige—de meeste ontwikkelaars lopen tegen hetzelfde probleem aan wanneer ze een tabel willen inkorten terwijl de kop intact blijft.  

In deze tutorial lopen we een beknopte, end‑to‑end oplossing door die laat zien *hoe je tabelrijen programmatically kunt verwijderen*, *hoe je tabelrijen veilig kunt verwijderen*, en waarom de aanpak werkt voor elk **verwijderen van rijen uit een Word‑tabel** scenario dat je kunt tegenkomen.

Aan het einde heb je een herbruikbare snippet die je in elk C#‑project kunt plaatsen, plus een reeks tips voor bredere **Word‑document tabelbewerking** taken.

## Prerequisites

- .NET 6.0 of later (de code werkt ook op .NET Framework 4.6+)
- Aspose.Words voor .NET geïnstalleerd (`dotnet add package Aspose.Words`)
- Een basisbegrip van C#‑syntaxis
- Een invoer‑`.docx`‑bestand dat minstens één tabel met een koprij bevat

> **Pro tip:** Als je nog geen licentie hebt, biedt Aspose.Words een gratis evaluatiemodus die perfect is voor testen.

## Step 1: Set Up the Project and Load the Word Document

Allereerst—maak een console‑app (of integreer in een bestaande service) en voeg de benodigde `using`‑directieven toe. Laad vervolgens het bron‑document.

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Tables;

class Program
{
    static void Main()
    {
        // Load the Word document (replace YOUR_DIRECTORY with your actual path)
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        Console.WriteLine("Document loaded successfully.");
```

**Waarom dit belangrijk is:**  
`Document` is het toegangspunt voor elke Aspose.Words‑operatie. Het bestand één keer laden houdt het geheugengebruik laag en geeft je een referentie voor alle daaropvolgende tabel‑bewerkings‑aanroepen.

## Step 2: Locate the First Table (or Any Table You Need)

Als je document meerdere tabellen bevat, kun je de gewenste tabel kiezen op index of door te zoeken naar een trefwoord. Voor de eenvoud pakken we de eerste tabel, die meestal de gegevens bevat die we willen inkorten.

```csharp
        // Retrieve the first table in the document
        Table firstTable = doc.GetChild(NodeType.Table, 0, true) as Table;
        if (firstTable == null)
        {
            Console.WriteLine("No table found in the document.");
            return;
        }
        Console.WriteLine($"Table with {firstTable.Rows.Count} rows found.");
```

**Uitleg:**  
`GetChild(NodeType.Table, 0, true)` doorloopt de documentboom diepte‑eerst en retourneert de eerste `Table`‑node die hij tegenkomt. De `as Table`‑cast zet de node veilig om, zodat we later met `Rows` kunnen werken.

## Step 3: Delete Multiple Rows While Preserving the Header

Nu komen we bij de kern van de zaak: **meerdere rijen in Word‑documenten verwijderen**. Stel dat de kop in rij 0 staat en je de volgende twee rijen (indices 1 en 2) wilt verwijderen. De `DeleteRows`‑methode doet precies dat.

```csharp
        // Delete two rows starting from the second row (index 1)
        // This keeps the header row untouched while removing the following rows
        firstTable?.DeleteRows(1, 2);
        Console.WriteLine("Specified rows deleted.");
```

### Hoe tabelrijen verwijderen – Variaties

- **Verwijder één rij:** `firstTable?.DeleteRows(rowIndex, 1);`
- **Verwijder alle rijen behalve de kop:** `firstTable?.DeleteRows(1, firstTable.Rows.Count - 1);`
- **Verwijder rijen op basis van een voorwaarde:** doorloop `firstTable.Rows` en roep `DeleteRows` aan wanneer een cel aan je criteria voldoet.

Deze snippets beantwoorden de veelgestelde vraag **hoe je tabelrijen kunt verwijderen** op een flexibele manier.

## Step 4: Save the Modified Document

Nadat de rijen zijn verwijderd, schrijf je het document eenvoudigweg terug naar de schijf. Je kunt het originele bestand overschrijven of een nieuwe kopie maken.

```csharp
        // Save the modified document
        doc.Save(@"YOUR_DIRECTORY\output.docx");
        Console.WriteLine("Document saved as output.docx");
    }
}
```

**Wat je zult zien:**  
Als de originele tabel bijvoorbeeld vijf rijen had (kop + vier gegevensrijen), zal het opgeslagen `output.docx` nu slechts drie rijen bevatten (kop + de overgebleven twee gegevensrijen). Open het bestand in Word om te verifiëren dat de ongewenste rijen verdwenen zijn zonder andere inhoud te verstoren.

![voorbeeld van meerdere rijen verwijderen in Word](delete-multiple-rows-word.png)

*Afbeeldingsalt‑tekst: meerdere rijen verwijderen in Word – voor‑ en na‑screenshot van een Word‑tabel.*

## Full, Ready‑to‑Run Example

Alles bij elkaar, hier is het volledige programma dat je kunt kopiëren‑plakken:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Tables;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the Word document
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        Console.WriteLine("Document loaded.");

        // 2️⃣ Retrieve the first table
        Table firstTable = doc.GetChild(NodeType.Table, 0, true) as Table;
        if (firstTable == null)
        {
            Console.WriteLine("No table found.");
            return;
        }
        Console.WriteLine($"Found table with {firstTable.Rows.Count} rows.");

        // 3️⃣ Delete rows – this is the core of delete rows from word table
        //    Starting at index 1 (second row), delete the next two rows.
        firstTable?.DeleteRows(1, 2);
        Console.WriteLine("Rows deleted.");

        // 4️⃣ Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
        Console.WriteLine("Saved output.docx");
    }
}
```

Voer het programma uit, open `output.docx`, en je zult zien dat de kop nog steeds aanwezig is terwijl de gekozen rijen verdwenen zijn. Dat is **meerdere rijen verwijderen in Word** in actie.

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Probleem | Waarom het gebeurt | Oplossing |
|----------|-------------------|-----------|
| **NullReferenceException** wanneer `firstTable` `null` is | Het document heeft geen tabellen of de index is onjuist | Controleer altijd `firstTable != null` voordat je `DeleteRows` aanroept. |
| **Rijen niet verwijderd** | Het gebruiken van een verkeerde startindex (Word‑tabellen zijn nul‑gebaseerd) | Onthoud dat de kop rij 0 is; begin bij 1 om deze te behouden. |
| **Opslaan over een alleen‑lezen bestand** | Bestandsrechten verhinderen overschrijven | Sla op een ander pad op of pas de bestandsattributen aan. |
| **Onverwachte lay‑out wijzigingen** | Rijen met samengevoegde cellen verwijderen kan de tabel beschadigen | Zorg ervoor dat samengevoegde cellen worden afgehandeld—splits eerst of verwijder hele rijen zorgvuldig. |

## De oplossing uitbreiden – Meer Word‑document tabelbewerking

Als je geïnteresseerd bent in bredere **Word‑document tabelbewerking**, overweeg dan de volgende stappen:

- **Nieuwe rijen invoegen**: `firstTable?.Rows.Add(new Row(doc));`
- **Celtekst bijwerken**: `firstTable.Rows[rowIndex].Cells[colIndex].Paragraphs[0].AppendText("New value");`
- **Stijlen toepassen**: Gebruik `CellFormat` of `RowFormat` om schaduwen, randen of lettertype‑eigenschappen in te stellen.
- **Exporteren naar PDF**: `doc.Save("output.pdf", SaveFormat.Pdf);`

Al deze bewerkingen bouwen voort op hetzelfde objectmodel dat we voor het verwijderen van rijen gebruikten, waardoor je codebasis consistent blijft.

## Conclusie

We hebben je zojuist laten zien hoe je **meerdere rijen in Word‑documenten kunt verwijderen** met een handvol regels C#‑code. De aanpak behandelt *hoe je tabelrijen kunt verwijderen*, *hoe je tabelrijen kunt weghalen*, en het bredere onderwerp van **Word‑document tabelbewerking**.  

Je hebt nu een solide, herbruikbaar patroon: laad het document, vind de tabel, roep `DeleteRows` aan met de juiste indices, en sla op. Vanaf hier kun je het rijenbereik aanpassen, over tabellen itereren, of combineren met andere bewerkingsfuncties om elke automatiseringstaak aan te pakken.

Klaar om verder te gaan? Probeer factuurgeneratie te automatiseren, rapporttemplates op te schonen, of een bulk‑update tool te bouwen die tientallen Word‑bestanden in één keer verwerkt. De mogelijkheden zijn eindeloos, en de API maakt het moeiteloos.

Als je tegen problemen aanloopt, laat dan een reactie achter—veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe rijen in Excel in te voegen en te verwijderen met Aspose.Cells voor .NET: Een uitgebreide gids](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Meerdere rijen in Excel verwijderen met Aspose.Cells .NET: Een uitgebreide gids voor gegevensmanipulatie](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [Meerdere rijen verwijderen in Aspose.Cells .NET](/cells/english/net/row-and-column-management/delete-multiple-rows-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}