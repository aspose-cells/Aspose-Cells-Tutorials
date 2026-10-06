---
date: '2026-02-22'
description: Leer hoe je Excel‑rapportage kunt automatiseren met Aspose.Cells in Java
  door CopyOptions en PasteOptions te gebruiken om formules nauwkeurig te houden en
  alleen zichtbare waarden te plakken.
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
title: Automatiseer Excel-rapportage – Beheersen van CopyOptions & PasteOptions in
  Java met Aspose.Cells
url: /nl/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Automatiseer Excel-rapportage met Aspose.Cells: CopyOptions & PasteOptions in Java

Zoek je om **Excel-rapportage te automatiseren** met Java? Met Aspose.Cells kun je programmatisch kopiëren, plakken en formules aanpassen zodat je rapporten nauwkeurig blijven en alleen de gegevens die je nodig hebt worden overgebracht. In deze tutorial lopen we twee essentiële functies door—**CopyOptions.ReferToDestinationSheet** en **PasteOptions**—die je in staat stellen formule‑referenties te behouden en alleen waarden van zichtbare cellen te plakken.

## Snelle antwoorden
- **Wat doet `CopyOptions.ReferToDestinationSheet`?** Past formules aan zodat ze naar het bestemmingsblad wijzen bij het kopiëren van gegevens.  
- **Hoe kan ik alleen zichtbare cellen plakken?** Stel `PasteOptions.setOnlyVisibleCells(true)` in met `PasteType.VALUES`.  
- **Welke bibliotheekversie is vereist?** Aspose.Cells 25.3 of hoger.  
- **Heb ik een licentie nodig voor productie?** Ja, een permanente of tijdelijke licentie verwijdert de evaluatie‑beperkingen.  
- **Kan ik Maven of Gradle gebruiken?** Beide worden ondersteund; zie de afhankelijkheidsfragmenten hieronder.

## Wat betekent “Excel-rapportage automatiseren”?
Excel-rapportage automatiseren betekent het programmatisch genereren, consolideren en opmaken van Excel-werkboeken, waardoor handmatige kopie‑plak‑stappen worden geëlimineerd en fouten worden verminderd. Aspose.Cells biedt een uitgebreide API waarmee Java‑ontwikkelaars spreadsheets op grote schaal kunnen manipuleren.

## Waarom CopyOptions en PasteOptions gebruiken voor rapportage?
- **Behoud de integriteit van formules** bij het verplaatsen van gegevens tussen bladen.  
- **Sluit verborgen rijen/kolommen uit** om rapporten schoon en gefocust te houden.  
- **Verbeter de prestaties** door alleen de benodigde gegevens te kopiëren in plaats van volledige bereiken.

## Voorvereisten
- Java 8 of hoger.  
- Maven of Gradle voor afhankelijkheidsbeheer.  
- Aspose.Cells 25.3+ (trial, tijdelijke of permanente licentie).  

## Aspose.Cells voor Java instellen

Voeg de bibliotheek toe aan je project met een van de volgende opties:

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
- **Free Trial** – Volledige functionaliteit voor evaluatie.  
- **Temporary License** – Verwijdert trial‑beperkingen tijdens het testen.  
- **Permanent License** – Aanbevolen voor productie‑workloads.

Initialiseer Aspose.Cells in je Java‑code:
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Stapsgewijze handleiding

### 1. CopyOptions met ReferToDestinationSheet

#### Overzicht
Het instellen van `CopyOptions.ReferToDestinationSheet` op `true` herschrijft formule‑referenties zodat ze na de kopie‑bewerking naar het nieuwe blad wijzen.

#### Stap 1: Werkmap en werkbladen initialiseren
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Stap 2: CopyOptions configureren
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Stap 3: Kopie‑bewerking uitvoeren
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Waarom dit belangrijk is*: Formules die oorspronkelijk `Sheet1` refereerden, zullen nu correct `DestSheet` refereren, waardoor je geautomatiseerde rapporten betrouwbaar blijven.

**Probleemtip**: Als formules nog steeds naar het oude blad verwijzen, zorg er dan voor dat `setReferToDestinationSheet(true)` **vóór** de kopie wordt aangeroepen.

### 2. PasteOptions voor alleen waarden van zichtbare cellen

#### Overzicht
`PasteOptions` stelt je in staat te definiëren wat er wordt geplakt. Het gebruik van `PasteType.VALUES` in combinatie met `onlyVisibleCells=true` kopieert alleen de weergegeven waarden, waarbij verborgen rijen/kolommen en opmaak worden genegeerd.

#### Stap 1: Werkmap en werkbladen initialiseren
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Stap 2: PasteOptions configureren
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Stap 3: Plak‑bewerking uitvoeren
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Waarom dit belangrijk is*: Ideaal voor het extraheren van gefilterde gegevens of het genereren van schone rapporten zonder verborgen rijen of opmaak‑ruis.

**Probleemtip**: Controleer of rijen/kolommen daadwerkelijk verborgen zijn in Excel voordat je kopieert; anders worden ze meegenomen.

## Praktische toepassingen
1. **Financial Consolidation** – Voeg maandelijkse bladen samen tot een master‑werkmap terwijl alle formules nauwkeurig blijven.  
2. **Filtered Data Export** – Haal alleen zichtbare rijen van een gefilterde tabel naar een samenvattend blad.  
3. **Scheduled Report Generation** – Automatiseer de nachtelijke creatie van Excel‑rapporten met precieze celwaarden en correcte referenties.

## Prestatie‑overwegingen
- **Werkboeken vrijgeven** wanneer klaar (`wb.dispose();`) om native resources vrij te maken.  
- **Batch‑bewerkingen** – Groepeer meerdere kopie‑/plak‑aanroepen om overhead te verminderen.  
- **Geheugen monitoren** – Grote werkboeken kunnen een grotere heap vereisen (`-Xmx2g`).

## Veelgestelde vragen

**Q1: Waar wordt `CopyOptions.ReferToDestinationSheet` voor gebruikt?**  
A: Het herschrijft formule‑referenties zodat ze na een kopie naar het bestemmingsblad wijzen, waardoor rapportage‑formules correct blijven.

**Q2: Hoe plak ik alleen zichtbare cellen?**  
A: Stel `PasteOptions.setOnlyVisibleCells(true)` in en kies `PasteType.VALUES`.

**Q3: Kan ik Aspose.Cells gebruiken zonder een licentie aan te schaffen?**  
A: Ja, een gratis trial of tijdelijke licentie is beschikbaar voor evaluatie, maar een permanente licentie is vereist voor productie.

**Q4: Waarom zijn sommige referenties nog steeds onjuist na het kopiëren?**  
A: Controleer dubbel of `ReferToDestinationSheet` is ingeschakeld **vóór** de kopie‑bewerking en of de bronformules geen externe werkboek‑links bevatten.

**Q5: Welke best practices voor geheugenbeheer moet ik volgen?**  
A: Geef `Workbook`‑objecten vrij wanneer ze klaar zijn, verwerk grote bestanden in delen, en houd het JVM‑heap‑gebruik in de gaten.

**Q6: Is het mogelijk om CopyOptions en PasteOptions in één bewerking te combineren?**  
A: Ja, je kunt ze combineren door eerst te kopiëren met `CopyOptions` en vervolgens `PasteOptions` toe te passen op het doelbereik.

## Bronnen
- **Documentatie**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download**: [Aspose.Cells Releases for Java](https://releases.aspose.com/cells/java/)  
- **Aankoop**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Gratis proefversie**: [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **Tijdelijke licentie**: [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Ondersteuningsforum**: [Aspose Support](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Laatst bijgewerkt:** 2026-02-22  
**Getest met:** Aspose.Cells 25.3 for Java  
**Auteur:** Aspose