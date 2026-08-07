---
category: general
date: 2026-07-16
description: Stel een aangepast scheidingsteken voor cellen in bij het exporteren
  van een Excel‑tabel naar TXT met Aspose.Cells. Leer hoe je Excel‑formules naar tekst
  exporteert en een werkblad opslaat als txt‑bestand.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom cell separator
- export excel table to txt
- export excel formulas to text
- save worksheet as txt file
- export excel data as plain text
language: nl
lastmod: 2026-07-16
og_description: Stel een aangepaste celseparator in Aspose.Cells in, zodat u een Excel‑tabel
  naar TXT kunt exporteren met exacte opmaak. Exporteer Excel‑formules naar tekst
  en sla het werkblad eenvoudig op als txt‑bestand.
og_image_alt: Screenshot showing set custom cell separator option in Aspose.Cells
  export settings
og_title: Aangepast cel‑scheidingsteken instellen – Exporteer Excel‑tabel naar TXT
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Set custom cell separator when exporting Excel table to TXT using Aspose.Cells.
    Learn how to export Excel formulas to text and save worksheet as txt file.
  headline: Set Custom Cell Separator – Export Excel Table to TXT
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Export
title: Aangepaste celseparator instellen – Excel‑tabel exporteren naar TXT
url: /nl/java/excel-import-export/set-custom-cell-separator-export-excel-table-to-txt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aangepaste cel‑scheidingsteken instellen – Excel‑tabel exporteren naar TXT

Aangepaste cel‑scheidingsteken is de geheime saus die je nodig hebt wanneer je een nette tekst‑dump uit een Excel‑blad wilt. Heb je je ooit afgevraagd hoe je **excel‑tabel naar txt kunt exporteren** zonder te eindigen met een wirwar van komma’s en regeleinden? In deze tutorial lopen we het volledige proces door met Aspose.Cells for Java, van het laden van een werkmap tot **werkblad opslaan als txt‑bestand** met een door jou gekozen scheidingsteken.

## Wat je zult leren

- Hoe je **aangepaste cel‑scheidingsteken kunt instellen** voor tekst‑exporten.
- De exacte stappen om **excel‑formules naar tekst te exporteren** zodat de geëvalueerde waarden mee worden genomen.
- Manieren om **excel‑gegevens als platte tekst te exporteren** terwijl de lay‑out behouden blijft.
- Een complete, kant‑klaar code‑voorbeeld dat je kunt copy‑pasten in je project.

Aan het einde van deze gids kun je elke Excel‑werkmap nemen, een pipe (`|`), een tab (`\t`) of elk ander teken kiezen, en een schoon, gescheiden tekstbestand produceren dat downstream‑systemen waarderen.

### Vereisten

- Java 8 of hoger geïnstalleerd.
- Maven (of een ander build‑tool) om de Aspose.Cells for Java‑bibliotheek binnen te halen.
- Een voorbeeld‑werkmap (`TableDemo.xlsx`) die een tabel met formules bevat.

Als je deze zaken hebt, duiken we erin — geen extra poespas, alleen praktische stappen.

## Stap 1: Aspose.Cells aan je project toevoegen

Voordat je **aangepaste cel‑scheidingsteken kunt instellen**, heb je de Aspose.Cells‑JAR op de classpath nodig. De makkelijkste manier is via Maven:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Als je liever Gradle gebruikt, vervang dan de XML door het equivalent `implementation 'com.aspose:aspose-cells:24.10'`. Zodra de afhankelijkheid is opgehaald, ben je klaar om Java‑code te schrijven die met Excel‑bestanden werkt.

## Stap 2: De werkmap laden – Voorbereiden op exporteren van Excel‑tabel naar TXT

De eerste echte code‑regel is altijd dezelfde: open de werkmap die de tabel bevat die je wilt exporteren.

```java
import com.aspose.cells.*;

public class ExportTableWithOptions {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableDemo.xlsx");
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Hier halen we het eerste werkblad op (`get(0)`). Als je gegevens zich op een ander blad bevinden, wijzig dan de index of gebruik `get("SheetName")`. Dit deel is essentieel voor **excel‑tabel naar txt exporteren** omdat de exporter op werkbladniveau werkt.

## Stap 3: Aangepaste cel‑scheidingsteken instellen – De kern van exporteren

Nu komt het sterpunt van de show: het configureren van `ExportTableOptions`. Dit object laat je precies bepalen hoe elke cel eruitziet in het uiteindelijke tekstbestand.

```java
        // Define how the table should be exported
        ExportTableOptions exportTableOptions = new ExportTableOptions();

        // 1️⃣ Export cell contents as plain strings (no rich formatting)
        exportTableOptions.setExportAsString(true);

        // 2️⃣ Include the evaluated formula result, not the formula itself
        exportTableOptions.setFormulaValueInCell(true);

        // 3️⃣ Set the custom separator – this is where we set custom cell separator
        exportTableOptions.setCellValueSeparator("|"); // you can use any char you like
```

Waarom **aangepaste cel‑scheidingsteken instellen**? Omdat de standaard scheidingsteken een tab is, wat kan conflicteren met data die al tabs bevat. Door een pipe (`|`) of een puntkomma te kiezen, zorg je ervoor dat elke kolom distinct blijft wanneer een downstream‑parser het bestand leest.

### Excel‑formules naar tekst exporteren

De regel `setFormulaValueInCell(true)` vertelt Aspose.Cells om de **excel‑formules naar tekst te exporteren** als het *resultaat* van de formule, niet als de formule‑tekst zelf. Als je dit weglaten zou een cel met `=SUM(A1:A5)` verschijnen als `=SUM(A1:A5)` in de TXT, wat zelden gewenst is.

## Stap 4: Exportopties koppelen aan TXT‑opslaan‑opties

Nu binden we die tabelopties aan de algemene TXT‑exportconfiguratie.

```java
        // Attach the table export options to TXT save options
        TxtSaveOptions txtSaveOptions = new TxtSaveOptions();
        txtSaveOptions.setExportTableOptions(exportTableOptions);
```

`TxtSaveOptions` is het overkoepelende object dat bepaalt hoe het volledige werkblad wordt weggeschreven. Door `exportTableOptions` erin te pluggen, zorg je dat elke tabel op het blad de **aangepaste cel‑scheidingsteken**‑regel respecteert.

## Stap 5: Het werkblad opslaan als TXT‑bestand – Export afronden

Tot slot schrijven we het bestand naar schijf.

```java
        // Save the worksheet as a TXT file using the configured options
        workbook.save("YOUR_DIRECTORY/TableExported.txt", txtSaveOptions);
    }
}
```

Het uitvoeren van dit programma maakt `TableExported.txt`. Elke rij van de oorspronkelijke Excel‑tabel verschijnt nu als een regel met door pipes gescheiden waarden, bijvoorbeeld:

```
Name|Quantity|Price|Total
Apple|10|0.50|5.00
Banana|5|0.30|1.50
```

Merk op hoe de formule in de **Total**‑kolom werd geëvalueerd voordat deze werd weggeschreven — dankzij `setFormulaValueInCell(true)`. Dat is de essentie van **excel‑gegevens als platte tekst exporteren** terwijl berekende resultaten behouden blijven.

## Stap 6: Output verifiëren – Ziet het er goed uit?

Open het gegenereerde `TableExported.txt` in een willekeurige teksteditor. Je zou moeten zien:

- Eén regel per Excel‑rij.
- Kolommen gescheiden door het pipe‑teken dat je hebt ingesteld met `setCellValueSeparator`.
- Geen vreemde komma’s of tabs, tenzij ze deel uitmaakten van de oorspronkelijke celwaarden.
- Formule‑resultaten, niet de formules zelf.

Als je onverwachte tekens tegenkomt, controleer dan het door jou gekozen scheidingsteken. Sommige tekens (zoals de pipe) zijn veilig voor de meeste CSV‑achtige parsers, maar als je data al pipes bevat, overweeg dan een ander scheidingsteken zoals `~` of een tab (`\t`).

## Tips, randgevallen en best practices – Excel‑gegevens als platte tekst exporteren

| Situatie | Wat te doen |
|-----------|------------|
| **Data bevat al het door jou gekozen scheidingsteken** | Schakel over naar een minder vaak gebruikt teken (`^`, `~` of Unicode‑niet‑printbare tekens). |
| **Je hebt UTF‑8‑codering nodig** |  |

## Wat kun je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Excel opslaan als tekstbestand met aangepast scheidingsteken met Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Excel‑tekst aangepast scheidingsteken Aspose Cells Net](/cells/german/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Excel‑tekst aangepast scheidingsteken Aspose Cells Net](/cells/french/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}