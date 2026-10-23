---
category: general
date: 2026-10-23
description: Leer hoe je een Excel‑werkblad dupliceert in Java terwijl je draaitabellen
  behoudt. Deze gids laat ook zien hoe je draaitabellen kopieert, Excel‑bereiken kopieert
  en een werkblad met draaitabelgegevens kopieert.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- duplicate excel sheet
- how to copy pivot
- copy excel range
- copy sheet with pivot
- copy pivot to workbook
language: nl
lastmod: 2026-10-23
og_description: Dupliceer een Excel-werkblad in Java terwijl je draaitabellen behoudt.
  Volg deze volledige tutorial om draaitabellen te kopiëren, Excel-bereiken te kopiëren
  en een blad met draaitabelgegevens te kopiëren.
og_image_alt: Screenshot showing a duplicated Excel sheet with pivot tables preserved
og_title: Dupliceer een Excel-werkblad met draaitabellen in Java – stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  headline: How to duplicate an Excel sheet and keep pivot tables intact in Java
  type: TechArticle
- description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  name: How to duplicate an Excel sheet and keep pivot tables intact in Java
  steps:
  - name: Expected output
    text: 'Running the program creates `DuplicatedWithPivot.xlsx` in the target directory.
      Open the file in Excel and you will see:'
  - name: How to copy pivot to another workbook without copying the whole sheet?
    text: If you only need the pivot and its underlying data, copy the range that
      contains both the source data and the pivot, then use `setCopyPivotTable(true)`.
      The same code from **Step 4** applies; just ensure the range covers the data
      source.
  - name: What if the source workbook has multiple worksheets with pivots?
    text: 'Repeat **Step 3** for each worksheet you want to duplicate:'
  - name: Does this work with protected worksheets?
    text: 'Aspose.Cells can copy protected sheets, but you must unprotect them first
      if you need to modify the pivot after copying:'
  - name: Can I copy a pivot table to an existing workbook that already contains a
      sheet with the same name?
    text: 'Yes. Use `addCopy` with a unique name:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot tables
title: Hoe een Excel-werkblad te dupliceren en draaitabellen intact te houden in Java
url: /nl/java/excel-pivot-tables/how-to-duplicate-an-excel-sheet-and-keep-pivot-tables-intact/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een Excel-werkblad te dupliceren en draaitabellen intact te houden in Java

Als je **duplicate Excel sheet** moet dupliceren terwijl je elke draaitabel intact houdt, laat deze gids je precies zien hoe. Je ziet een beknopte oplossing die een werkblad kopieert, een specifiek bereik kopieert, en zelfs een draaitabel naar een andere werkmap kopieert—alles in pure Java met Aspose.Cells.

Het dupliceren van een Excel-werkblad is een veelvoorkomende taak wanneer je maandelijkse rapporten genereert vanuit een sjabloon of wanneer je een sandbox‑kopie nodig hebt voor testen. De onderstaande code werkt met Aspose.Cells 25.11 of later, waarin de optie `setCopyPivotTable(true)` werd geïntroduceerd.

## Wat je nodig hebt

- Java 17 (of een recente JDK) geïnstalleerd
- Aspose.Cells for Java 25.11 of nieuwer in je project (Maven‑coördinaat `com.aspose:aspose-cells:25.11`)
- Een bronwerkmap (`SourceWithPivot.xlsx`) die al een draaitabel bevat
- Een IDE of build‑tool naar keuze (IntelliJ IDEA, Eclipse, Maven, Gradle, enz.)

## Stap 1: Laad de bronwerkmap die de draaitabel bevat

De eerste handeling is het openen van de werkmap die de draaitabel bevat die je wilt behouden.

```java
import com.aspose.cells.*;

public class DuplicateExcelSheet {
    public static void main(String[] args) throws Exception {
        // Load the source workbook with the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

> **Waarom deze stap belangrijk is:** Het laden van de bronwerkmap geeft je toegang tot de werkbladobjecten, cellen en de ingebedde draaitabellen. Zonder dit kun je de draaitabelgegevens die je wilt kopiëren niet refereren.

## Stap 2: Maak een lege bestemmingswerkmap (of laad een bestaande)

Je kunt beginnen met een lege werkmap of een bestaand bestand openen dat het gedupliceerde werkblad zal ontvangen.

```java
        // Create a new, empty destination workbook
        Workbook dstWb = new Workbook();
```

> **Tip:** Als je al een rapportage‑werkmap hebt, vervang dan de bovenstaande regel door `new Workbook("ExistingReport.xlsx")` om het gedupliceerde werkblad eraan toe te voegen.

## Stap 3: Kopieer het volledige werkblad – de draaitabel wordt automatisch behouden

Het kopiëren van het volledige werkblad is de eenvoudigste manier om **sheet met draaitabel te kopiëren**. Aspose.Cells kopieert de draaitabeldefinitie en de cache automatisch.

```java
        // Access the first worksheet (index 0) from the source workbook
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Add a copy of the source worksheet to the destination workbook
        Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
```

> **Waarom het werkt:** `addCopy` kloont de werkbladstructuur, celwaarden, stijlen en eventuele ingebedde draaitabellen. Het nieuwe werkblad in `dstWb` zal er identiek uitzien als het origineel, inclusief de draaitabel‑cache.

## Stap 4: (Optioneel) Kopieer alleen een specifiek bereik dat de draaitabel bevat

Soms wil je niet het hele werkblad—misschien heb je alleen een gedeelte nodig dat de draaitabel bevat. Hier gebruik je **Excel‑bereik kopiëren** en vraag je expliciet om de draaitabel te kopiëren.

```java
        // Define the source range that covers the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G30");

        // Define the target range in the destination worksheet
        Range dstRange = dstWs.getCells().createRange("A1");

        // Copy the range and tell Aspose.Cells to include the pivot table
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setCopyPivotTable(true); // new option in 25.11
        dstRange.copy(srcRange, copyOptions);
```

> **Hoe het helpt:** `setCopyPivotTable(true)` dwingt de engine om de draaitabeldefinitie te dupliceren, zelfs wanneer je een beperkt bereik kopieert. Zonder deze vlag zou alleen de ruwe data worden gekopieerd en zou de draaitabel verloren gaan.

## Stap 5: Sla de bestemmingswerkmap op

Schrijf tenslotte de gedupliceerde inhoud naar een nieuw bestand.

```java
        // Save the destination workbook to a new file
        dstWb.save("YOUR_DIRECTORY/DuplicatedWithPivot.xlsx");
    }
}
```

### Verwachte output

Het uitvoeren van het programma maakt `DuplicatedWithPivot.xlsx` aan in de doelmap. Open het bestand in Excel en je ziet:

- Een nieuw werkblad met de naam `Sheet1 (Copy)` (of de originele naam met “Copy” toegevoegd)
- De draaitabel verschijnt precies zoals in het bronwerkblad, volledig functioneel
- Als je de optionele bereik‑kopie hebt gebruikt, zijn alleen de cellen A1:G30 aanwezig, maar werkt de draaitabel nog steeds omdat de cache is gekopieerd

## Veelgestelde vragen en randgevallen

### Hoe kopieer je een draaitabel naar een andere werkmap zonder het hele werkblad te kopiëren?

Als je alleen de draaitabel en de onderliggende data nodig hebt, kopieer dan het bereik dat zowel de brondata als de draaitabel bevat, en gebruik vervolgens `setCopyPivotTable(true)`. Dezelfde code uit **Stap 4** is van toepassing; zorg er alleen voor dat het bereik de gegevensbron omvat.

### Wat als de bronwerkmap meerdere werkbladen met draaitabellen heeft?

Herhaal **Stap 3** voor elk werkblad dat je wilt dupliceren:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet ws = srcWb.getWorksheets().get(i);
    dstWb.getWorksheets().addCopy(ws);
}
```

### Werkt dit met beveiligde werkbladen?

Aspose.Cells kan beveiligde werkbladen kopiëren, maar je moet ze eerst ontgrendelen als je de draaitabel na het kopiëren wilt aanpassen:

```java
srcWs.unprotect("password");
dstWs.unprotect("password");
```

### Kan ik een draaitabel kopiëren naar een bestaande werkmap die al een werkblad met dezelfde naam bevat?

Ja. Gebruik `addCopy` met een unieke naam:

```java
Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
dstWs.setName("PivotCopy_" + System.currentTimeMillis());
```

## Pro‑tip: controleer de draaitabel‑cache

Na het kopiëren kun je programmatisch bevestigen dat de draaitabel‑cache bestaat:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
System.out.println("Pivot cache ID: " + pt.getCacheIndex());
```

Als de cache‑ID een niet‑negatief getal afdrukt, is de draaitabel succesvol gedupliceerd.

## Conclusie

Je weet nu hoe je een **duplicate Excel sheet** in Java kunt maken terwijl je elke draaitabel behoudt, hoe je **pivot**‑tabellen direct kunt **kopiëren**, hoe je een **Excel‑bereik** kunt **kopiëren** dat een draaitabel bevat, en hoe je een **sheet met draaitabel** of **draaientabel naar werkmap kopiëren** kunt doen met Aspose.Cells 25.11+. Pas deze patronen toe om rapportgeneratie te automatiseren, sjabloon‑klonen te maken of testomgevingen op te zetten die identieke, draaitabel‑gedreven analyses nodig hebben.

Klaar om meer te ontdekken? Probeer de gedupliceerde werkmap naar PDF te exporteren, of verfris de draaitabel‑cache programmatisch na het kopiëren om te zorgen dat de nieuwste gegevens worden weergegeven. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe een werkblad te dupliceren en draaitabellen te behouden in Java](/cells/english/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/)
- [Hoe een draaitabel te kopiëren in Java – Complete Aspose.Cells‑gids](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Hoe een bereik te kopiëren en een draaitabel te behouden in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}