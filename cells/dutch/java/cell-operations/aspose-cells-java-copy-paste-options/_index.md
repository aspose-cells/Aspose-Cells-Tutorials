---
date: '2026-10-28'
description: Leer hoe u waarden kunt plakken met de kopieer‑ en plakopties van Aspose.Cells
  in Java, met stapsgewijze code, Maven‑afhankelijkheidsconfiguratie en licentietips.
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: Leer hoe u waarden kunt plakken met de kopieer‑ en plakopties van
  Aspose.Cells in Java, met stapsgewijze code, Maven‑afhankelijkheidsconfiguratie
  en licentietips.
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: Hoe waarden plakken met de kopieer‑ en plakopties van Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: Hoe waarden plakken met de kopieer‑ en plakopties van Aspose.Cells
url: /nl/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe waarden plakken met Aspose.Cells kopieer‑ en plakopties

Automatiseren van Excel‑rapportage in Java betekent dat je werkboeken kunt genereren, consolideren en opmaken zonder Excel handmatig te openen. Met **Aspose.Cells** krijg je volledige controle over formules, verborgen rijen en celwaarden, zodat je rapporten nauwkeurig en lichtgewicht blijven. In deze tutorial leer je hoe je **CopyOptions.ReferToDestinationSheet** gebruikt om formules correct te houden en **PasteOptions** om alleen de zichtbare waarden die je nodig hebt te plakken.

## Snelle antwoorden
- **Wat doet `CopyOptions.ReferToDestinationSheet`?** Het herschrijft formules zodat ze naar het bestemmingsblad wijzen na een kopieerbewerking.  
- **Hoe kan ik alleen zichtbare cellen plakken?** Roep `PasteOptions.setOnlyVisibleCells(true)` aan samen met `PasteType.VALUES`.  
- **Welke bibliotheekversie is vereist?** Aspose.Cells 25.3 of later.  
- **Heb ik een licentie nodig voor productie?** Ja – een permanente of tijdelijke licentie verwijdert evaluatielimieten.  
- **Kan ik Maven of Gradle gebruiken?** Beide worden ondersteund; zie de afhankelijkheidsfragmenten hieronder.

## Wat is “automatiseren van Excel-rapportage”?
Automatiseren van Excel-rapportage betekent het programmatisch genereren en bijwerken van Excel-werkboeken, waardoor je rapporten kunt maken, samenvoegen en opmaken zonder handmatig kopiëren‑plakken, wat fouten vermindert en uren repetitief werk bespaart. Deze aanpak is ideaal voor geplande batchtaken, data‑gedreven dashboards en financiële consolidatie‑pijplijnen.

## Waarom CopyOptions en PasteOptions gebruiken voor rapportage?
Deze twee klassen laten je formule‑referenties intact houden tijdens het kopiëren van gegevens **en** alleen de cellen extraheren die zichtbaar zijn na filteren of verbergen van rijen. Ze samen gebruiken vermindert de hoeveelheid overgedragen data met tot 80 % in typische gefilterde‑tabelscenario's en garandeert dat formules correct blijven berekenen in het bestemmingsblad.

## Vereisten
- Java 8 of hoger.  
- Maven of Gradle voor afhankelijkheidsbeheer.  
- Aspose.Cells 25.3+ (trial, tijdelijke of permanente licentie).  

## Aspose.Cells voor Java instellen
Voeg de bibliotheek toe aan je project met een van de volgende:

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Licentie‑acquisitie
- **Free trial** – volledige functionaliteit voor evaluatie.  
- **Temporary license** – verwijdert trial‑limieten tijdens het testen.  
- **Permanent license** – aanbevolen voor productie‑workloads.

Initialiseer Aspose.Cells in je Java‑code:  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Stapsgewijze handleiding

### 1. copyOptions met referToDestinationSheet

#### Overzicht
`CopyOptions` is het configuratie‑object van Aspose.Cells dat bepaalt hoe formules en cel‑referenties worden behandeld tijdens een kopieerbewerking. Het instellen van `CopyOptions.ReferToDestinationSheet` op `true` herschrijft formule‑referenties zodat ze naar het nieuwe blad wijzen na de kopieerbewerking.

#### Stap 1: werkmap en werkbladen initialiseren  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Stap 2: copyOptions configureren  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Stap 3: kopieerbewerking uitvoeren  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Waarom dit belangrijk is*: Formules die oorspronkelijk `Sheet1` refereerden, zullen nu correct `DestSheet` refereren, waardoor je geautomatiseerde rapporten betrouwbaar blijven.

**Probleemtip**: Als formules nog steeds naar het oude blad verwijzen, zorg ervoor dat `setReferToDestinationSheet(true)` **voor** de kopie wordt aangeroepen.

### 2. pasteOptions voor alleen‑waarden van zichtbare cellen

#### Overzicht
`PasteOptions` is het instellingen‑object van Aspose.Cells dat bepaalt wat er wordt geplakt. Het gebruik van `PasteType.VALUES` samen met `onlyVisibleCells=true` kopieert alleen de weergegeven waarden, waarbij verborgen rijen/kolommen en opmaak worden genegeerd.

#### Stap 1: werkmap en werkbladen initialiseren  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Stap 2: pasteOptions configureren  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Stap 3: plakbewerking uitvoeren  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Waarom dit belangrijk is*: Ideaal voor het extraheren van gefilterde data of het genereren van schone rapporten zonder verborgen rijen of opmaakruis.

**Probleemtip**: Controleer of rijen/kolommen daadwerkelijk verborgen zijn in Excel vóór het kopiëren; anders worden ze meegenomen.

## Praktische toepassingen
1. **Financial consolidation** – voeg maandelijkse bladen samen tot een master‑werkmap terwijl alle formules nauwkeurig blijven.  
2. **Filtered data export** – haal alleen zichtbare rijen van een gefilterde tabel op naar een samenvattend blad.  
3. **Scheduled report generation** – automatiseer de nachtelijke Excel‑rapportcreatie met precieze celwaarden en correcte referenties.

## Prestatie‑overwegingen
- **Werkboeken vrijgeven** wanneer klaar (`wb.dispose();`) om native resources vrij te maken.  
- **Batch‑bewerkingen** – groepeer meerdere kopieer‑/plak‑aanroepen om overhead te verminderen.  
- **Geheugen monitoren** – grote werkboeken kunnen een grotere heap vereisen (`-Xmx2g`).  
- Aspose.Cells ondersteunt **50+ in‑ en uitvoerformaten** en kan werkboeken verwerken met **tot 2 miljoen rijen** zonder het volledige bestand in het geheugen te laden, waardoor hoge‑doorvoersnelheid wordt geleverd voor enterprise‑workloads.

## Veelgestelde vragen

**Q: Waar wordt `CopyOptions.ReferToDestinationSheet` voor gebruikt?**  
A: Het herschrijft formule‑referenties zodat ze naar het bestemmingsblad wijzen na een kopie, waardoor rapportage‑formules correct blijven.

**Q: Hoe plak ik alleen zichtbare cellen?**  
A: Stel `PasteOptions.setOnlyVisibleCells(true)` in en kies `PasteType.VALUES`.

**Q: Kan ik Aspose.Cells gebruiken zonder een licentie aan te schaffen?**  
A: Ja, een gratis trial of tijdelijke licentie is beschikbaar voor evaluatie, maar een permanente licentie is vereist voor productie.

**Q: Waarom zijn sommige referenties nog steeds onjuist na het kopiëren?**  
A: Controleer nogmaals dat `ReferToDestinationSheet` **voor** de kopie‑bewerking is ingeschakeld en dat de bronformules geen externe werkboek‑links bevatten.

**Q: Welke best practices voor geheugenbeheer moet ik volgen?**  
A: Geef `Workbook`‑objecten vrij wanneer ze niet meer nodig zijn, verwerk grote bestanden in delen, en monitor het JVM‑heap‑gebruik.

**Q: Is het mogelijk om CopyOptions en PasteOptions te combineren in één bewerking?**  
A: Ja, je kunt ze achter elkaar uitvoeren door eerst te kopiëren met `CopyOptions` en vervolgens `PasteOptions` toe te passen op het doelbereik.

## Bronnen
- **Documentatie**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download**: [Aspose.Cells releases for Java](https://releases.aspose.com/cells/java/)  
- **Aankoop**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Gratis trial**: [Aspose.Cells free trial](https://releases.aspose.com/cells/java/)  
- **Tijdelijke licentie**: [Apply for a temporary license](https://purchase.aspose.com/temporary-license/)  
- **Supportforum**: [Aspose support](https://forum.aspose.com/c/cells)

---

**Laatst bijgewerkt:** 2026-10-28  
**Getest met:** Aspose.Cells 25.3 for Java  
**Auteur:** Aspose

## Gerelateerde tutorials

- [Excel‑bestand lezen Java – Master Workbook celmanipulatie met Aspose.Cells](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [Gegevens toevoegen aan cel in Excel met Aspose.Cells voor Java](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Excel‑cel rij‑kolom indexen converteren met Aspose.Cells Java](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}