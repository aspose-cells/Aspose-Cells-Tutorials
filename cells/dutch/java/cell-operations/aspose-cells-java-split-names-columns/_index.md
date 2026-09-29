---
date: '2026-03-15'
description: Leer hoe je namen in aparte kolommen splitst en een werkboek xlsx opslaat
  met Aspose Cells Java in een stapsgewijze tutorial.
keywords:
- Aspose.Cells Java
- split names columns
- Excel manipulation
- text to columns Java
- Java Excel processing
title: aspose cells java – Namen splitsen in kolommen
url: /nl/java/cell-operations/aspose-cells-java-split-names-columns/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Beheersen **aspose cells java**: Namen splitsen in kolommen

Welkom bij onze uitgebreide **aspose cells java** tutorial. In deze gids leer je **hoe je namen splitst** die in één Excel‑kolom zijn opgeslagen naar twee afzonderlijke kolommen—voornaam en achternaam—met behulp van de krachtige tekst‑naar‑kolommen functie. Of je nu een contactlijst opschoont, gegevens voorbereidt voor een CRM‑import, of gewoon een snelle manier nodig hebt om spreadsheets te herstructureren, deze tutorial laat je precies zien hoe je **save workbook xlsx** uitvoert na de transformatie.

## Snelle antwoorden
- **What does this tutorial cover?** Splitsen van volledige‑naam strings in voor‑ en achternaam kolommen met Aspose.Cells voor Java.  
- **Which library version is used?** De nieuwste stabiele release (vanaf 2026).  
- **Do I need a license?** Een gratis proefversie werkt voor ontwikkeling; een commerciële licentie is vereist voor productie.  
- **Can I split on other delimiters?** Ja—verander gewoon de scheidingsteken in `TxtLoadOptions`.  
- **Is the output an .xlsx file?** Absoluut, de werkmap wordt opgeslagen in XLSX‑formaat.

## Wat is **aspose cells java**?
**Aspose.Cells java** is een high‑performance Java‑API die ontwikkelaars in staat stelt Excel‑bestanden te maken, wijzigen, converteren en renderen zonder Microsoft Office nodig te hebben. Het ondersteunt alle belangrijke Excel‑formaten en biedt geavanceerde functies zoals formules, grafieken en gegevensmanipulatie.

## Waarom **aspose cells java** gebruiken voor het splitsen van namen?
- **Zero‑install**: Werkt op elke server‑side Java‑omgeving.  
- **Speed**: Verwerkt grote spreadsheets sneller dan native Excel‑interop.  
- **Precision**: Volledige controle over scheidingstekens, kolombereiken en outputformaten.  
- **Reliability**: Geen COM‑ of Office‑afhankelijkheden, waardoor het ideaal is voor cloud‑ of container‑implementaties.

## Voorvereisten
- Java Development Kit (JDK) 8 of nieuwer.  
- Een IDE zoals IntelliJ IDEA of Eclipse (optioneel maar aanbevolen).  
- Maven of Gradle voor afhankelijkheidsbeheer.  

### Maven‑configuratie
Voeg de Aspose.Cells‑dependency toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle‑configuratie
Voeg de bibliotheek toe aan je `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

> **Pro tip:** Gebruik een tijdelijke licentie van het Aspose‑portaal om volledige functionaliteit te ontgrendelen tijdens ontwikkeling.

## Stapsgewijze implementatie

### Stap 1: Maak een Workbook aan en krijg toegang tot het eerste werkblad
Eerst importeer je de kernklassen en instantieer je een nieuw workbook. Dit geeft je een schoon Excel‑bestand klaar voor gegevensinvoer.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
```

```java
String dataDir = "YOUR_DATA_DIRECTORY"; // Define your directory path here

Workbook wb = new Workbook();
Worksheet ws = wb.getWorksheets().get(0);
```

### Stap 2: Vul het werkblad met voorbeeldnamen
Vervolgens voeg je een paar volledige‑naam strings toe aan kolom **A**. In een echt project zou je deze uit een database of CSV‑bestand lezen.

```java
import com.aspose.cells.Cell;

String outDir = "YOUR_OUTPUT_DIRECTORY"; // Define your output directory path here

ws.getCells().get("A1").putValue("John Teal");
ws.getCells().get("A2").putValue("Peter Graham");
ws.getCells().get("A3").putValue("Brady Cortez");
ws.getCells().get("A4").putValue("Mack Nick");
ws.getCells().get("A5").putValue("Hsu Lee");
```

### Stap 3: Configureer Text Load Options voor kolomsplitsing
De `TxtLoadOptions`‑klasse vertelt Aspose.Cells hoe de tekst geïnterpreteerd moet worden. Hier gebruiken we een spatie (`' '`) als scheidingsteken.

```java
import com.aspose.cells.TxtLoadOptions;

TxtLoadOptions opts = new TxtLoadOptions();
opts.setSeparator(' ');
```

### Stap 4: Splits de tekst in twee kolommen
Roep nu `textToColumns()` aan op het celgebied dat de namen bevat. De parameters `(0, 0, 5, opts)` betekenen *begin bij rij 0, kolom 0, verwerk 5 rijen, met de opties die we zojuist hebben gedefinieerd*.

```java
ws.getCells().textToColumns(0, 0, 5, opts);
```

Na deze aanroep bevat kolom A de voornamen en kolom B de achternamen.

### Stap 5: Sla het Workbook op als een XLSX‑bestand
Schrijf tenslotte het aangepaste workbook naar schijf. De `SaveFormat`‑enum zorgt ervoor dat het bestand wordt opgeslagen in het moderne XLSX‑formaat.

```java
import com.aspose.cells.SaveFormat;

wb.save(outDir + "outputTextToColumns.xlsx");
```

> **Waarom dit belangrijk is:** Door **save workbook xlsx** te gebruiken, garandeer je compatibiliteit met de nieuwste versies van Excel, Google Sheets en andere spreadsheet‑tools.

## Praktische toepassingen
- **Data Cleaning:** Snel samengevoegde velden scheiden voordat ze in analytics‑pijplijnen worden geladen.  
- **CRM Integration:** Transformeer een platte contactlijst naar een gestructureerde tabel voor import.  
- **HR Systems:** Splits volledige namen van werknemers voor loonadministratie of voordelenverwerking.

## Prestatie‑overwegingen
Bij het werken met duizenden rijen:

1. **Batch Updates:** Gebruik `ws.getCells().setRowHeight()` of vergelijkbare batch‑methoden om overhead te verminderen.  
2. **Memory Management:** Roep `wb.calculateFormula()` alleen aan wanneer nodig, en maak grote objecten snel vrij.  
3. **Garbage Collection:** Start de JVM met geschikte heap‑instellingen (`-Xmx2g` voor grote bestanden) om OutOfMemory‑fouten te voorkomen.

## Veelvoorkomende problemen en oplossingen

| Issue | Solution |
|-------|----------|
| **Namen bevatten middelste initialen** (bijv. “John A. Doe”) | Pas de scheidingsteken aan of verwerk de tweede kolom nadien om de achternaam te extraheren. |
| **Onverwacht lege cellen** | Controleer of het bronbereik (`textToColumns`‑parameters) overeenkomt met de werkelijke gegevensrijen. |
| **Licentie niet gevonden** | Plaats het tijdelijke licentiebestand (`Aspose.Cells.lic`) in de project‑root of stel de licentie programmatisch in. |

## Veelgestelde vragen

**Q: What is Aspose.Cells Java?**  
A: Een krachtige bibliotheek die je in staat stelt Excel‑bestanden programmatisch te maken, wijzigen en converteren met Java.

**Q: Can I split columns based on delimiters other than spaces?**  
A: Ja, pas de `TxtLoadOptions`‑scheidingsteken aan zoals nodig voor je gegevens.

**Q: How do I handle large datasets with Aspose.Cells?**  
A: Optimaliseer de prestaties door geheugenbeheer en het minimaliseren van workbook‑operaties, zoals hierboven beschreven.

**Q: Is there support available if I encounter issues?**  
A: Bezoek het [Aspose Forum](https://forum.aspose.com/c/cells/9) voor community‑hulp of neem rechtstreeks contact op met het Aspose‑ondersteuningsteam.

**Q: What formats can Aspose.Cells save workbooks in?**  
A: Ondersteunt een breed scala aan Excel‑bestandsformaten, waaronder XLSX, XLS, CSV en meer.

## Bronnen

- **Documentatie**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Download**: [Aspose.Cells Java Releases](https://releases.aspose.com/cells/java/)
- **Aankoop**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Gratis proefversie**: [Try Aspose.Cells for Free](https://releases.aspose.com/cells/java/)
- **Tijdelijke licentie**: [Request a Temporary License](https://purchase.aspose.com/temporary-license/)

Veel programmeerplezier, en geniet van het benutten van de volledige kracht van **aspose cells java** in je projecten!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Laatst bijgewerkt:** 2026-03-15  
**Getest met:** Aspose.Cells 25.3 for Java  
**Auteur:** Aspose