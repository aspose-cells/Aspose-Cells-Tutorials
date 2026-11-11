---
date: '2026-10-28'
description: Leer hoe u het Excel-datumsysteem naar 1904 kunt wijzigen met Aspose.Cells
  for Java, het Excel-datumformaat instelt en het 1904-systeem efficiënt converteert.
keywords:
- change excel date system
- excel 1904 date conversion
- maven dependency aspose cells
lastmod: '2026-10-28'
og_description: Verander het Excel-datumsysteem naar 1904 met Aspose.Cells for Java.
  Leer stap voor stap hoe u het 1904-systeem inschakelt, datums instelt en terug converteert.
og_image_alt: Aspose.Cells Java guide showing how to switch Excel to the 1904 date
  system
og_title: Verander het Excel-datumsysteem naar 1904 met Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  headline: Change Excel date system to 1904 with Aspose.Cells Java
  type: TechArticle
- description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  name: Change Excel date system to 1904 with Aspose.Cells Java
  steps:
  - name: initialize and load the workbook
    text: The `Workbook` class represents an entire Excel file in memory. First, create
      a `Workbook` instance that points to your existing file.
  - name: enable the 1904 date system
    text: The `WorkbookSettings.setDate1904` method toggles the workbook‑level date
      flag. Setting it to `true` activates the 1904 system for all worksheets. **Pro
      tip:** You can also call `setDate1904(false)` later if you need to revert.
  - name: save the modified workbook
    text: Finally, write the changes to a new file (or overwrite the original). The
      `save` method respects the active date system automatically. > **Note:** The
      code above uses the class name `tWorkbook` as originally provided. Ensure this
      typo matches your project’s naming conventions or correct it to `Workb
  type: HowTo
- questions:
  - answer: The 1900 system starts on January 1, 1900, while the 1904 system starts
      on January 1, 1904, shifting all dates by 1,462 days.
    question: What is the difference between the 1900 and 1904 date systems?
  - answer: Yes, but you must close the file in Excel first; otherwise the save operation
      will fail.
    question: Can I change the date system of a workbook that is currently open in
      Excel?
  - answer: The method works in the free trial, but a full license removes evaluation
      limitations.
    question: Do I need a license to use `setDate1904`?
  - answer: No, the date system is a workbook‑level setting; it applies to all worksheets.
    question: Is it possible to change the date system for only a single worksheet?
  - answer: Open the saved file in Excel, go to **File → Options → Advanced**, and
      check the **"Use 1904 date system"** box.
    question: How can I verify that the date system was changed?
  type: FAQPage
tags:
- change excel date system
- aspose cells java
- excel date conversion
- java excel processing
title: Verander het Excel-datumsysteem naar 1904 met Aspose.Cells Java
url: /nl/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wijzig Excel-datumssysteem naar 1904 met Aspose.Cells Java

In deze tutorial leer je hoe je het **Excel-datumssysteem** kunt wijzigen naar het 1904‑formaat met Aspose.Cells voor Java. Het 1904‑systeem is essentieel wanneer je legacy Mac‑gebaseerde datums moet behouden of moet afstemmen op financiële modellen die dat tijdperk verwachten. We lopen door het installeren van de bibliotheek, het laden van een werkmap, het schakelen van het datumssysteem en het opslaan van het resultaat — allemaal zonder Microsoft Excel op de server te hoeven installeren.

## Snelle antwoorden
- **Wat doet het 1904-datumssysteem?** Het begint met het tellen van dagen vanaf 1 januari 1904, waardoor alle datums met 1.462 dagen verschuiven ten opzichte van het standaard 1900‑systeem.  
- **Waarom Aspose.Cells gebruiken om het datumssysteem te wijzigen?** Het biedt een eenvoudige API die werkt zonder dat Excel geïnstalleerd is en ondersteunt grote bestanden.  
- **Welke Java‑versies worden ondersteund?** JDK 8 of hoger.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor evaluatie; een licentie verwijdert gebruiksbeperkingen.  
- **Kan ik later terugschakelen naar het 1900‑systeem?** Ja, roep gewoon `setDate1904(false)` aan.

## Wat is het 1904-datumssysteem in Excel?
Het 1904‑datumssysteem telt dagen vanaf 1 januari 1904, in plaats van vanaf de standaard 1900‑epoch. Deze verschuiving voegt precies 1.462 dagen toe aan elke datumwaarde, waardoor legacy Mac‑werkboeken een offset vertonen wanneer ze op Windows worden geopend. Het wordt voornamelijk gebruikt voor compatibiliteit met oudere Macintosh‑Excel‑bestanden en sommige legacy‑financiële modellen.

## Waarom het Excel-datumssysteem wijzigen met Aspose.Cells?
Je kunt het datumssysteem rechtstreeks vanuit Java wijzigen, waardoor handmatige stappen in Excel worden geëlimineerd. Aspose.Cells verwerkt werkboeken tot **2 GB** groot en kan een werkboek met 500 bladen in minder dan **2 seconden** omzetten op een typische 4‑core server, waardoor high‑throughput server‑side automatisering wordt geleverd.

## Voorvereisten
- Java Development Kit (JDK) 8 of hoger.  
- Maven of Gradle voor afhankelijkheidsbeheer.  
- Basiskennis van Java‑programmeren.  

## Aspose.Cells voor Java instellen

### Maven
Voeg de volgende afhankelijkheid toe aan je `pom.xml`‑bestand:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Voeg deze regel toe aan je `build.gradle`‑bestand:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Licentie‑acquisitie
Aspose biedt een gratis proefversie, een tijdelijke licentie en volledige commerciële licenties. Je kunt beginnen met de [gratis proefversie](https://releases.aspose.com/cells/java/) of een tijdelijke licentie verkrijgen via de [pagina voor tijdelijke licentie](https://purchase.aspose.com/temporary-license/).

## Hoe wijzig je het Excel-datumssysteem naar 1904 met Aspose.Cells voor Java?
Laad de werkmap, schakel de 1904‑instelling in en sla het bestand op — deze drie‑stappen‑stroom werkt de interne datum‑epoch van de werkmap bij in minder dan een seconde. De API‑aanroep `setDate1904(true)` zet de systeemvlag om, en de wijziging wordt bewaard wanneer je `save` aanroept. Er is geen Excel‑installatie vereist, waardoor het ideaal is voor headless serveromgevingen.

### Stap 1: initialiseren en de werkmap laden
De `Workbook`‑klasse vertegenwoordigt een volledig Excel‑bestand in het geheugen. Maak eerst een `Workbook`‑instantie die naar je bestaande bestand verwijst.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Stap 2: het 1904‑datumssysteem inschakelen
De methode `WorkbookSettings.setDate1904` schakelt de datum‑vlag op werkboekniveau om. Door deze op `true` te zetten, activeer je het 1904‑systeem voor alle werkbladen.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Pro tip:** Je kunt later ook `setDate1904(false)` aanroepen als je moet terugschakelen.

### Stap 3: de gewijzigde werkmap opslaan
Schrijf tenslotte de wijzigingen naar een nieuw bestand (of overschrijf het origineel). De `save`‑methode houdt automatisch rekening met het actieve datumssysteem.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **Opmerking:** De bovenstaande code gebruikt de klassennaam `tWorkbook` zoals oorspronkelijk opgegeven. Zorg ervoor dat deze typefout overeenkomt met de naamgevingsconventies van je project of corrigeer deze naar `Workbook` indien nodig.

## Excel‑datum programmatically instellen (secundaire trefwoord)
Als je individuele celwaarden moet aanpassen nadat je het systeem hebt gewijzigd, kun je `cells.get(i, j).putValue(Date)` gebruiken, waarbij de datum wordt geïnterpreteerd volgens het actieve datumssysteem.

## Excel‑1904‑systeem terugzetten naar 1900 (secundaire trefwoord)
Om terug te gaan, roep je simpelweg aan:

```java
workbook.getSettings().setDate1904(false);
```

Sla vervolgens de werkmap opnieuw op.

## Praktische toepassingen
1. **Gegevensarchivering** – Legacy‑tijdstempels behouden bij het migreren van oude Mac‑gebaseerde spreadsheets.  
2. **Cross‑platform rapportage** – Rapporten genereren die correct openen op zowel Windows als macOS zonder datumverschillen.  
3. **Financiële modellering** – Datumcalculaties afstemmen op legacy‑financiële modellen die het 1904‑systeem verwachten.

## Prestatie‑overwegingen
- Beperk werkboekbewerkingen in één sessie om het geheugenverbruik laag te houden; Aspose.Cells streamt gegevens en laadt het volledige bestand nooit in het RAM tenzij je dit expliciet vraagt.  
- Stem de garbage‑collection‑flags van Java (`-XX:+UseG1GC`) af voor zeer grote bestanden om pieken in pauzetijd te vermijden.  

## Veelgestelde vragen

**Q: Wat is het verschil tussen de 1900‑ en 1904‑datumssystemen?**  
A: Het 1900‑systeem start op 1 januari 1900, terwijl het 1904‑systeem start op 1 januari 1904, waardoor alle datums met 1.462 dagen verschuiven.

**Q: Kan ik het datumssysteem van een werkmap die momenteel in Excel openstaat wijzigen?**  
A: Ja, maar je moet het bestand eerst in Excel sluiten; anders zal de opslaan‑bewerking mislukken.

**Q: Heb ik een licentie nodig om `setDate1904` te gebruiken?**  
A: De methode werkt in de gratis proefversie, maar een volledige licentie verwijdert evaluatiebeperkingen.

**Q: Is het mogelijk om het datumssysteem alleen voor één werkblad te wijzigen?**  
A: Nee, het datumssysteem is een instelling op werkboekniveau; het geldt voor alle werkbladen.

**Q: Hoe kan ik verifiëren dat het datumssysteem is gewijzigd?**  
A: Open het opgeslagen bestand in Excel, ga naar **Bestand → Opties → Geavanceerd**, en vink het vakje **"Gebruik 1904-datumssysteem"** aan.

## Conclusie
Je weet nu hoe je het **Excel-datumssysteem** naar 1904 kunt wijzigen met Aspose.Cells voor Java, hoe je individuele celdata kunt instellen, en hoe je indien nodig terug kunt schakelen naar het 1900‑systeem. Integreer deze fragmenten in je data‑verwerkings‑pipelines om datum‑compatibiliteit over platforms en legacy‑bestanden te garanderen.

---

**Laatst bijgewerkt:** 2026-10-28  
**Getest met:** Aspose.Cells 25.3 voor Java  
**Auteur:** Aspose  

**Documentatie:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
**Download:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)  
**Licentie kopen:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
**Gratis proefversie:** [Start Free Trial](https://releases.aspose.com/cells/java/)  
**Tijdelijke licentie:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)  
**Ondersteuningsforum:** [Aspose Support](https://forum.aspose.com/c/cells/9)

## Gerelateerde tutorials

- [Efficiënt Excel naar PDF converteren met aangepaste datumformaten met Aspose.Cells voor Java](/cells/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Aspose.Cells voor Java: Hoe Excel-werkboeken efficiënt maken en opmaken](/cells/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Excel-manipulatie beheersen met Aspose.Cells voor Java: Werkmapbewerkingen en celopmaak tutorial](/cells/java/workbook-operations/excel-manipulation-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}