---
category: general
date: 2026-02-15
description: Maak een nieuw werkboek in C# en leer hoe je een tabel toevoegt, een
  filter inschakelt en het werkboek opslaat als xlsx. Snelle, volledige gids voor
  Excel‑automatisering.
draft: false
keywords:
- create new workbook
- save workbook as xlsx
- how to create workbook
- how to add table
- how to enable filter
language: nl
og_description: Maak een nieuw werkboek in C# en voeg direct een tabel toe, schakel
  filters in/uit, en sla het werkboek vervolgens op als xlsx. Volg deze beknopte,
  praktische tutorial.
og_title: Maak een nieuw werkboek in C# – Complete programmeergids
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Nieuw werkboek maken in C# – Stapsgewijze handleiding
url: /nl/net/excel-workbook/create-new-workbook-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak een nieuw werkboek in C# – Complete programmeergids

Heb je ooit een **nieuw werkboek maken** in C# moeten, maar wist je niet welke objecten je eerst moest aanraken? Je bent niet de enige; veel ontwikkelaars lopen tegen die muur aan bij het automatiseren van Excel‑bestanden. In deze tutorial lopen we stap voor stap door het maken van een nieuw werkboek, het invoegen van een tabel, het schakelen van de auto‑filter, en uiteindelijk **werkboek opslaan als xlsx**—alles met duidelijke, uitvoerbare code.

We zullen ook de blijvende “how to add table” en “how to enable filter” vragen beantwoorden die meestal opduiken na de eerste werkboekcreatie. Tegen het einde heb je een zelfstandige voorbeeld die je in elk .NET‑project kunt plaatsen, zonder extra poespas.

## Vereisten & Installatie

- **.NET 6** (of een recente .NET‑versie) geïnstalleerd.
- Het **Aspose.Cells for .NET** NuGet‑pakket (`Install-Package Aspose.Cells`) – deze bibliotheek levert de `Workbook`, `Worksheet` en `ListObject`‑klassen die hieronder worden gebruikt.
- Een ontwikkelomgeving naar keuze (Visual Studio, VS Code, Rider – kies wat je wilt).

Er is geen extra configuratie nodig; de code werkt direct zodra het pakket is verwezen.

![Schermafbeelding van een nieuw aangemaakt werkboek in Excel – create new workbook](image.png)

*Afbeeldingsalt‑tekst: “create new workbook screenshot in Excel”*

## Stap 1: Nieuw werkboek maken en toegang tot het eerste werkblad

Het allereerste wat je moet doen is een `Workbook`‑object instantieren. Beschouw dit als het openen van een gloednieuw Excel‑bestand dat momenteel één standaardblad bevat. Daarna haal je een referentie naar het werkblad op zodat je het kunt gaan vullen.

```csharp
using Aspose.Cells;

public class WorkbookDemo
{
    public static void Main()
    {
        // Step 1: Create a new workbook (this is the "create new workbook" part)
        Workbook workbook = new Workbook();

        // Access the first worksheet – by default it is named "Sheet1"
        Worksheet worksheet = workbook.Worksheets[0];
```

**Waarom dit belangrijk is:** Het maken van het werkboek geeft je een schoon canvas; toegang tot het eerste werkblad zorgt ervoor dat je een doel hebt voor de komende tabel. Als je dit overslaat, zullen latere `ListObject`‑aanroepen een null‑referentie veroorzaken.

## Stap 2: Hoe een tabel aan het werkblad toevoegen

Nu we een werkblad hebben, laten we een tabel invoegen die zich uitstrekt over de cellen **A1:C5**. In Aspose.Cells beheert de `ListObjects`‑collectie tabellen (ook wel *list objects* genoemd). Het toevoegen van een tabel is een tweestapsproces: roep `Add` aan om deze te maken, en wikkel vervolgens het resultaat in een `ListObject`‑variabele voor gemakkelijke manipulatie.

```csharp
        // Step 2: Add a table named "MyTable" covering the range A1:C5
        int tableIndex = worksheet.ListObjects.Add("MyTable", "A1:C5", true);
        ListObject table = worksheet.ListObjects[tableIndex];
```

**Wat er onder de motorkap gebeurt:** De `Add`‑methode registreert de tabel bij de interne tabelengine van Excel en kent een unieke index toe. Door die index op te slaan in `tableIndex` kunnen we de daadwerkelijke `ListObject`‑instantie ophalen, wat ons volledige controle over de tabel‑eigenschappen geeft.

### Pro‑tip
Als je van plan bent meerdere tabellen te maken, bewaar hun indexen in een lijst – dit maakt latere updates een fluitje van een cent.

## Stap 3: Hoe filter op de tabel inschakelen

Tabellen in Excel hebben standaard een auto‑filterrij, maar afhankelijk van hoe je de tabel hebt gemaakt, moet je deze mogelijk expliciet inschakelen. De `ShowAutoFilter`‑eigenschap schakelt die rij aan of uit.

```csharp
        // Step 3: Enable the auto‑filter for the table
        table.ShowAutoFilter = true;
```

Zodra ingeschakeld, kunnen gebruikers op de vervolgkeuzepijlen in de koprij klikken om rijen op basis van waarden te filteren. Dit is vooral handig voor grote datasets.

### Wat als je geen filter wilt?
Stel simpelweg `ShowAutoFilter` in op `false` en de pijlen verdwijnen. De volgende regel toont de tegenovergestelde actie:

```csharp
        // Disable (remove) the auto‑filter
        table.ShowAutoFilter = false;
```

## Stap 4: Werkboek opslaan als XLSX

Alle zware taken zijn voltooid; nu slaan we het werkboek op schijf op. De `Save`‑methode accepteert een volledig pad en bepaalt automatisch het bestandsformaat aan de hand van de extensie. Hier slaan we expliciet **werkboek opslaan als xlsx** op.

```csharp
        // Step 4: Save the workbook to a file
        string outputPath = @"C:\Temp\NoFilter.xlsx"; // Change to your desired folder
        workbook.Save(outputPath);
    }
}
```

Wanneer je `NoFilter.xlsx` opent, zie je één blad met een tabel genaamd **MyTable** die A1:C5 beslaat, en — omdat we `ShowAutoFilter` op `false` hebben gezet — zullen er geen filterpijlen zichtbaar zijn.

### Verwacht resultaat
- Een bestand genaamd `NoFilter.xlsx` in de map die je hebt opgegeven.
- Sheet1 bevat een tabel van 5 rijen en 3 kolommen met standaardgegevens (lege cellen tenzij je ze vult).
- Er wordt geen auto‑filterrij weergegeven.

## Variaties & Randgevallen

### De filter ingeschakeld houden
Als jouw scenario vereist dat de filter aan blijft, laat dan simpelweg de regel weg die `ShowAutoFilter = false` zet. De tabel verschijnt met filterpijlen klaar voor gebruikersinteractie.

### Meerdere tabellen toevoegen
Je kunt **Stap 2** herhalen met verschillende bereiken en namen:

```csharp
int secondTableIdx = worksheet.ListObjects.Add("SecondTable", "E1:G10", true);
ListObject secondTable = worksheet.ListObjects[secondTableIdx];
secondTable.ShowAutoFilter = true;
```

### Tabelgegevens vullen
Aspose.Cells laat je direct naar cellen schrijven vóór of na het maken van de tabel. Bijvoorbeeld, om de eerste kolom met getallen te vullen:

```csharp
for (int i = 0; i < 5; i++)
{
    worksheet.Cells[i, 0].PutValue(i + 1); // A1‑A5 = 1‑5
}
```

### Compatibiliteitsopmerking
De code werkt met **Aspose.Cells 23.9** en later. Als je een oudere versie gebruikt, kan de signatuur van de `Add`‑methode iets anders zijn — controleer de release‑notes van de bibliotheek.

## Veelvoorkomende valkuilen & hoe ze te vermijden

- **Vergeten Aspose.Cells te refereren** – de compiler klaagt over onbekende types. Zorg ervoor dat het NuGet‑pakket is geïnstalleerd en dat `using Aspose.Cells;` bovenaan staat.
- **Onjuiste bereik‑string** – Excel‑bereiken zijn niet hoofdlettergevoelig, maar moeten wel geldig zijn (bijv. `"A1:C5"` in plaats van `"A1:C"`). Een typefout zal een `CellsException` veroorzaken.
- **Bestandspad‑rechten** – proberen op te slaan in een beschermde map (zoals `C:\Program Files`) veroorzaakt een `UnauthorizedAccessException`. Gebruik een schrijfbare directory zoals `%TEMP%` of je gebruikersprofiel.

## Volledig werkend voorbeeld (klaar om te kopiëren en plakken)

```csharp
using Aspose.Cells;

public class WorkbookDemo
{
    public static void Main()
    {
        // 1️⃣ Create new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Add a table named "MyTable" covering A1:C5
        int tableIdx = worksheet.ListObjects.Add("MyTable", "A1:C5", true);
        ListObject table = worksheet.ListObjects[tableIdx];

        // 3️⃣ Enable auto‑filter (you can skip this if you don't need it)
        table.ShowAutoFilter = true;

        // OPTIONAL: Disable the filter if you don't want it visible
        // table.ShowAutoFilter = false;

        // 4️⃣ Save workbook as xlsx
        string outputPath = @"C:\Temp\NoFilter.xlsx";
        workbook.Save(outputPath);
    }
}
```

Voer het programma uit, open het gegenereerde bestand, en je zult het exacte resultaat zien dat eerder is beschreven.

## Samenvatting

We begonnen met **nieuw werkboek maken**, daarna leerden we **hoe een tabel toe te voegen**, schakelden we de **hoe filter in te schakelen**‑functie, en uiteindelijk **werkboek opslaan als xlsx**. Elke stap werd uitgelegd met *waarom* het belangrijk is, niet alleen *wat* je moet typen, zodat je het patroon kunt aanpassen aan complexere scenario's.

## Wat volgt?

- **De tabel stijlen** – verken `TableStyleType` om je gegevens een professionele uitstraling te geven.
- **Formules invoegen** – gebruik `Cells[i, j].Formula = "=SUM(A2:A5)"` om berekeningen toe te voegen.
- **Exporteren naar PDF** – Aspose.Cells kan het werkboek ook als PDF renderen met één `Save`‑aanroep.
- **Bestaande werkboeken lezen** – vervang `new Workbook()` door `new Workbook("ExistingFile.xlsx")` om bestanden on‑the‑fly te wijzigen.

Voel je vrij om met deze ideeën te experimenteren, en aarzel niet om een reactie achter te laten als iets niet duidelijk is. Veel plezier met coderen, en geniet van het automatiseren van Excel met C#!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}