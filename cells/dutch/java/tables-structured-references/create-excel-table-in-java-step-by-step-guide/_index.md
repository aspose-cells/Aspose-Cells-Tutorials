---
category: general
date: 2026-08-04
description: Maak een Excel‑tabel in Java en leer hoe je autofilter uitschakelt, een
  celbereik definieert en de werkmap opslaat als xlsx met een volledig codevoorbeeld.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel table
- turn off autofilter
- define cell range
- save workbook as xlsx
- disable autofilter in excel
language: nl
lastmod: 2026-08-04
og_description: Maak een Excel‑tabel in Java, schakel autofilter uit, definieer het
  celbereik en sla het werkboek op als xlsx. Volg deze volledige tutorial om Excel‑automatisering
  onder de knie te krijgen.
og_image_alt: Image showing how to create excel table without autofilter using Java
og_title: Maak een Excel‑tabel in Java – volledige code‑uitleg
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create excel table in Java and learn how to turn off autofilter, define
    cell range, and save workbook as xlsx with a complete code example.
  headline: Create excel table in Java – step‑by‑step guide
  type: TechArticle
- description: Create excel table in Java and learn how to turn off autofilter, define
    cell range, and save workbook as xlsx with a complete code example.
  name: Create excel table in Java – step‑by‑step guide
  steps:
  - name: Define cell range for the table
    text: Next, you must specify the exact area that will become the table. The **define
      cell range** step tells Aspose.Cells which rows and columns to include.
  - name: Add the table and enable its default AutoFilter
    text: Now you add a `ListObject` (the Aspose.Cells representation of an Excel
      table). By default, a new table includes an AutoFilter dropdown for each column.
  - name: Turn off autofilter for the table
    text: If you want a clean table without filter dropdowns, you must **turn off
      autofilter** (or **disable autofilter in excel**). The API call is straightforward.
  - name: Save workbook as xlsx file
    text: Finally, persist the workbook to disk. The **save workbook as xlsx** call
      writes a standard Office Open XML file that any modern spreadsheet program can
      open.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Maak een Excel‑tabel in Java – stapsgewijze handleiding
url: /nl/java/tables-structured-references/create-excel-table-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-tabel maken in Java – stap‑voor‑stap gids

Als je een **excel-tabel** in Java moet maken, laat deze tutorial je precies zien hoe je dat doet. Je leert hoe je **celbereik definieert**, **autofilter uitschakelt**, en **werkmap opslaat als xlsx** met één enkel uitvoerbaar programma.

Het voorbeeld maakt gebruik van de Aspose.Cells for Java‑bibliotheek, die een high‑level API biedt voor Excel‑automatisering. Er zijn geen extra afhankelijkheden nodig naast de Aspose.Cells JAR. Aan het einde van de gids heb je een zelfstandige oplossing die je in elk Java‑project kunt gebruiken.

## Wat je gaat bouwen

* Een nieuwe werkmap met één werkblad.  
* Een tabel (ListObject) die een specifiek **celbereik** (A1:D5) beslaat.  
* De AutoFilter van de tabel **uitgeschakeld** (d.w.z. **autofilter uitschakelen in excel**).  
* De werkmap opgeslagen als een **xlsx**‑bestand op schijf.

## Vereisten

* Java 8 of nieuwer geïnstalleerd.  
* Aspose.Cells for Java (download van de officiële site of toevoegen via Maven).  
* Basiskennis van Java‑syntaxis en IDE’s zoals IntelliJ IDEA of Eclipse.

---

## Hoe een excel‑tabel te maken zonder autofilter in Java

De eerste belangrijke stap is het instantieren van een `Workbook` en het verkrijgen van het standaard werkblad. Dit geeft je een schoon canvas waarop je een tabel kunt plaatsen.

```java
import com.aspose.cells.*;

public class CreateExcelTable {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

**Waarom dit belangrijk is:**  
Een `Workbook` vertegenwoordigt het volledige Excel‑bestand. Het eerste werkblad (`get(0)`) wordt automatisch aangemaakt, dus je hoeft er geen handmatig toe te voegen. Beginnen met een nieuw blad garandeert dat er geen overgebleven gegevens interfereren met de tabel die je gaat maken.

### Celbereik voor de tabel definiëren

Vervolgens moet je het exacte gebied opgeven dat de tabel wordt. De stap **celbereik definiëren** vertelt Aspose.Cells welke rijen en kolommen moeten worden opgenomen.

```java
        // Step 2: Define the cell range that will become the table (A1:D5)
        CellArea tableRange = CellArea.createCellArea("A1", "D5");
```

**Waarom dit belangrijk is:**  
`CellArea` codeert de linkerboven‑ en rechteronderhoeken van het bereik. Door `"A1"` en `"D5"` te gebruiken, maak je een blok van 5 rijen × 4 kolommen, wat de typische grootte is voor een eenvoudige datatabel.

### Voeg de tabel toe en schakel de standaard AutoFilter in

Nu voeg je een `ListObject` toe (de Aspose.Cells‑representatie van een Excel‑tabel). Standaard bevat een nieuwe tabel een AutoFilter‑dropdown voor elke kolom.

```java
        // Step 3: Add a table (ListObject) to the worksheet and enable its AutoFilter
        ListObject table = worksheet.getListObjects().add("MyTable", tableRange, true);
        table.setShowAutoFilter(true); // AutoFilter is turned on by default
```

**Waarom dit belangrijk is:**  
Het inschakelen van `setShowAutoFilter(true)` weerspiegelt het standaardgedrag van Excel, waardoor de tabel direct filterbaar is. Deze stap is optioneel maar verduidelijkt de status voordat je deze uitschakelt.

### AutoFilter voor de tabel uitschakelen

Als je een schone tabel zonder filter‑dropdowns wilt, moet je **autofilter uitschakelen** (of **autofilter uitschakelen in excel**). De API‑aanroep is eenvoudig.

```java
        // Step 4: Disable the AutoFilter for the table
        table.setShowAutoFilter(false);
```

**Waarom dit belangrijk is:**  
Het uitschakelen van de AutoFilter verbetert de leesbaarheid wanneer de tabel wordt gebruikt voor rapportage of afdrukken. Het vermindert ook de UI‑rommel voor eindgebruikers die geen interactieve filtering nodig hebben.

### Werkmap opslaan als xlsx‑bestand

Sla tenslotte de werkmap op schijf op. De **save workbook as xlsx**‑aanroep schrijft een standaard Office Open XML‑bestand dat elk modern spreadsheet‑programma kan openen.

```java
        // Step 5: Save the workbook to a file
        workbook.save("TableNoAutoFilter.xlsx", SaveFormat.XLSX);
    }
}
```

**Waarom dit belangrijk is:**  
Kiezen voor het `XLSX`‑formaat zorgt voor compatibiliteit met Excel 2007+ en met clouddiensten zoals Google Sheets. De bestandsnaam `TableNoAutoFilter.xlsx` geeft duidelijk weer dat de AutoFilter is uitgeschakeld.

---

## Volledige broncode samenvatting

Alle fragmenten samenvoegen levert een compleet, uitvoerbaar programma op:

```java
import com.aspose.cells.*;

public class CreateExcelTable {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the cell range that will become the table (A1:D5)
        CellArea tableRange = CellArea.createCellArea("A1", "D5");

        // Add a table (ListObject) to the worksheet and enable its AutoFilter
        ListObject table = worksheet.getListObjects().add("MyTable", tableRange, true);
        table.setShowAutoFilter(true); // AutoFilter is on by default

        // Disable the AutoFilter for the table
        table.setShowAutoFilter(false);

        // Save the workbook to a file (xlsx format)
        workbook.save("TableNoAutoFilter.xlsx", SaveFormat.XLSX);
    }
}
```

**Verwacht resultaat:**  
Wanneer je `TableNoAutoFilter.xlsx` opent in Microsoft Excel, zie je een tabel met de naam **MyTable** die de cellen A1:D5 beslaat. Er verschijnen geen filterpijlen op de kolomkoppen, wat bevestigt dat de stap **autofilter uitschakelen** geslaagd is.

---

## Veelgestelde vragen en randgevallen

| Vraag | Antwoord |
|----------|--------|
| *Kan ik gegevens toevoegen voordat ik de tabel maak?* | Ja. Vul eerst de cellen in het gedefinieerde bereik; de tabel zal de gegevens automatisch opnemen. |
| *Wat als het werkblad al gegevens bevat?* | Kies een ander **celbereik** dat niet overlapt met bestaande inhoud, of maak het gebied leeg met `worksheet.getCells().clear(A1, D5)`. |
| *Is het mogelijk om de AutoFilter alleen voor sommige kolommen te behouden?* | Aspose.Cells ondersteunt geen kolomspecifieke AutoFilter‑schakeling; je moet het voor de hele tabel aan laten staan of volledig uitschakelen. |
| *Hoe wijzig ik de tabelstijl?* | Gebruik `table.setTableStyleType( TableStyleType.TABLE_STYLE_MEDIUM_2 );` vóór het opslaan. |
| *Werkt dit op oudere Excel‑versies (xls)?* | Sla op met `SaveFormat.XLS` in plaats van `XLSX`, maar let op dat sommige nieuwere functies (zoals ListObject) beperkt kunnen zijn. |

**Pro tip:** Roep altijd `workbook.save(..., SaveFormat.XLSX)` aan nadat je alle tabelwijzigingen hebt voltooid. Meerdere keren opslaan kan de bestandsgrootte onnodig vergroten.

---

## Volgende stappen

Nu je weet hoe je een **excel‑tabel** maakt, **celbereik definieert**, **autofilter uitschakelt**, en **werkmap opslaat als xlsx**, kun je de oplossing uitbreiden:

* **Formules toevoegen** aan berekende kolommen met `table.getListColumns().get(i).setFormula("=SUM(...)")`.  
* **Voorwaardelijke opmaak toepassen** om rijen te markeren die aan bepaalde criteria voldoen.  
* **De werkmap exporteren naar PDF** met `workbook.save("Table.pdf", SaveFormat.PDF)` voor rapportagedoeleinden.  

Elk van deze onderwerpen bouwt voort op de kernconcepten die in deze tutorial behandeld zijn en toont verder hoe je **autofilter in excel** kunt **uitschakelen** wanneer nodig.

---

## Conclusie

Je hebt nu een compleet, productie‑klaar voorbeeld dat laat zien hoe je een **excel‑tabel** in Java maakt, **celbereik definieert**, **autofilter uitschakelt**, en **werkmap opslaat als xlsx**. Door de stap‑voor‑stap code en uitleg te volgen, kun je het maken van Excel‑tabellen integreren in elke Java‑applicatie en het AutoFilter‑gedrag programmatisch beheersen. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe een Excel-werkmap maken en opslaan als SVG met Aspose.Cells voor Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Excel-werkmap maken en opslaan Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Excel-werkmap maken en opslaan Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}