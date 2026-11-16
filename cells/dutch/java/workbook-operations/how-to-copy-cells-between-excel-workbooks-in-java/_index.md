---
category: general
date: 2026-11-16
description: Hoe cellen tussen Excel-werkboeken te kopiëren in Java – een werkboek
  laden, een bereik tussen werkboeken kopiëren (inclusief een draaitabel), en het
  werkboekbestand opslaan.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy cells
- copy range between workbooks
- copy pivot table workbook
- save workbook file
- load excel workbook java
language: nl
lastmod: 2026-11-16
og_description: Hoe cellen tussen Excel-werkboeken te kopiëren in Java. Leer een Excel-werkboek
  te laden, een bereik (inclusief een draaitabel) tussen werkboeken te kopiëren en
  het werkboekbestand op te slaan.
og_image_alt: Screenshot of Java code copying a cell range from one Excel workbook
  to another
og_title: Hoe cellen tussen Excel-werkboeken te kopiëren in Java – volledige gids
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  headline: How to copy cells between Excel workbooks in Java
  type: TechArticle
- description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  name: How to copy cells between Excel workbooks in Java
  steps:
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Define the range that includes the pivot table
    text: '```java // Define the cell range that you want to copy. // Adjust "A1:G20"
      to match the area that contains your data/pivot table. Range srcRange = srcWs.getCells().createRange("A1:G20");
      ```'
  - name: Create the destination workbook
    text: '```java // Create a new, empty workbook that will receive the copied range.
      Workbook destWb = new Workbook(); // defaults to a single empty sheet Worksheet
      destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range to the destination workbook
    text: '```java // Copy the source range to cell A1 of the destination worksheet.
      destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1")); ```'
  - name: Save the destination workbook
    text: '```java // Save the new workbook to disk. destWb.save("YOUR_DIRECTORY/dest.xlsx");
      } } ```'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook manipulation
title: Hoe cellen tussen Excel-werkboeken te kopiëren in Java
url: /nl/java/workbook-operations/how-to-copy-cells-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe cellen te kopiëren tussen Excel-werkboeken in Java

Als je **cellen wilt kopiëren** van het ene Excel-werkboek naar het andere met Java, laat deze gids je een betrouwbare manier zien om dit te doen. Je leert hoe je **Excel-werkboek Java laadt**, een bereik dat een draaitabel kan bevatten kopieert, en uiteindelijk **werkboekbestand opslaat** met de gekopieerde gegevens.

Deze tutorial behandelt:

* Een bron-werkboek laden en een werkblad selecteren.  
* Het exacte bereik definiëren dat je wilt verplaatsen (inclusief een draaitabel).  
* Een doel-werkboek maken en het bereik kopiëren.  
* Het doelbestand opslaan.  

Het voorbeeld maakt gebruik van de Aspose.Cells for Java bibliotheek, die werkt met Excel‑bestanden zonder Microsoft Office te vereisen. De code draait op Java 8+ en elke moderne IDE (IntelliJ IDEA, Eclipse, VS Code, enz.).

---

## Vereisten

Zorg ervoor dat je het volgende hebt voordat je begint:

| Vereiste | Reden |
|-------------|--------|
| Java Development Kit (JDK) 8 or newer | Vereist om de code te compileren en uit te voeren. |
| Maven or Gradle build tool | Vereenvoudigt het toevoegen van de Aspose.Cells‑dependency. |
| Aspose.Cells for Java library (latest version) | Biedt de `Workbook`, `Worksheet` en `Range` klassen die in het voorbeeld worden gebruikt. |
| Two Excel files (`source.xlsx` and an empty folder for `dest.xlsx`) | Het bronbestand moet de gegevens bevatten en, optioneel, een draaitabel die je wilt kopiëren. |

Voeg de Aspose.Cells‑dependency toe aan je `pom.xml` (Maven) of `build.gradle` (Gradle). Voorbeeld voor Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

---

## Hoe cellen te kopiëren met Aspose.Cells

De volgende stappen leiden je door het volledige proces. Elke stap bevat de Java‑code, een uitleg **waarom** de stap belangrijk is, en een tip om veelvoorkomende valkuilen te vermijden.

### Stap 1: Laad het bron‑werkboek

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source Excel file (replace with your actual path)
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Get the first worksheet (index 0)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Waarom?**  
`Workbook` vertegenwoordigt het volledige Excel‑bestand. Het laden geeft je toegang tot alle werkbladen, cellen en objecten zoals draaitabellen. Het gebruiken van het eerste werkblad is gebruikelijk, maar je kunt elk blad selecteren op naam (`srcWb.getWorksheets().get("Sheet2")`).

**Pro tip:**  
Als het bronbestand groot is, overweeg dan om het te laden in *geheugenefficiënte* modus: `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setMemorySetting(MemorySetting.MEMORY_PREFERENCE); }});`

### Stap 2: Definieer het bereik dat de draaitabel bevat

```java
        // Define the cell range that you want to copy.
        // Adjust "A1:G20" to match the area that contains your data/pivot table.
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Waarom?**  
Een `Range`‑object abstracteert een rechthoekig blok cellen. Door `"A1:G20"` op te geven, vertel je Aspose.Cells precies welke cellen—incl. eventuele ingesloten draaitabel—te kopiëren. De bibliotheek kopieert automatisch onderliggende gegevens, stijlen en draaitabeldefinities.

**Randgeval:**  
Als de draaitabel zich uitstrekt buiten het gedefinieerde bereik, breid dan het adres uit (bijv. `"A1:Z100"`). Je kunt ook `srcWs.getCells().getMaxDataColumn()` en `getMaxDataRow()` gebruiken om het gebruikte gebied dynamisch te berekenen.

### Stap 3: Maak het doel‑werkboek

```java
        // Create a new, empty workbook that will receive the copied range.
        Workbook destWb = new Workbook();               // defaults to a single empty sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Waarom?**  
Een nieuw werkboek zorgt ervoor dat geen ongewenste opmaak of verborgen bladen interfereren met de gekopieerde inhoud. Het standaard werkboek bevat al één werkblad, dat we als doel zullen gebruiken.

### Stap 4: Kopieer het bereik naar het doel‑werkboek

```java
        // Copy the source range to cell A1 of the destination worksheet.
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));
```

**Waarom?**  
`copyRange` behandelt alle cel‑attributen: waarden, formules, opmaak en zelfs draaitabel‑caches. Door naar `"A1"` te kopiëren, plaats je het bereik in de linkerbovenhoek van het doelblad, waardoor de oorspronkelijke lay-out behouden blijft.

**Veelgestelde vraag:** *Blijft de draaitabel functioneel?*  
Ja. Aspose.Cells kopieert de draaitabeldefinitie en de cache, zodat de draaitabel exact werkt zoals in het bron‑werkboek.

### Stap 5: Sla het doel‑werkboek op

```java
        // Save the new workbook to disk.
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Waarom?**  
Het aanroepen van `save` schrijft het in‑geheugen werkboek naar een fysiek `.xlsx`‑bestand. Je kunt ook opslaan naar andere formaten (`.xls`, `.csv`, `.pdf`) door de bestandsextensie te wijzigen of `SaveOptions` te gebruiken.

**Tip:**  
Als je het bestand moet streamen naar een web‑respons, gebruik dan `destWb.save(OutputStream, SaveFormat.XLSX);` in plaats van een bestandspad.

---

## Bereik kopiëren tussen werkboeken – volledige broncode

Hieronder staat de volledige, kant‑klaar Java‑klasse. Vervang `YOUR_DIRECTORY` door de daadwerkelijke map op jouw machine.

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Define the range that includes the data and pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Create a new destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Copy the defined range to the destination workbook
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Verwacht resultaat:**  
`dest.xlsx` bevat een exacte replica van het bereik `A1:G20` uit `source.xlsx`. Als het bronbereik een draaitabel bevatte, toont het doelbestand dezelfde draaitabel met de gegevensbron correct gekoppeld aan de gekopieerde cellen.

Je kunt `dest.xlsx` openen in Excel, LibreOffice of een andere viewer die `.xlsx` ondersteunt om te verifiëren dat de waarden, opmaak en draaitabelfunctionaliteit behouden blijven.

---

## Draaientabel‑werkboek kopiëren – wat je moet weten

* **Pivot‑cache wordt automatisch gekopieerd.** De bibliotheek draagt de onderliggende cache over, zodat de draaitabel niet handmatig ververst hoeft te worden.
* **Externe gegevensbronnen worden niet overgedragen.** Als de draaitabel gegevens uit een externe database haalt, moet je ervoor zorgen dat het doel‑werkboek dezelfde bron kan benaderen, of de cache lokaal opnieuw aanmaken.
* **Grote draaitabellen kunnen het geheugenverbruik verhogen.** Voor zeer grote werkboeken, overweeg het JVM‑heap te vergroten (`-Xmx2g`) om `OutOfMemoryError` te voorkomen.

---

## Werkboekbestand opslaan in verschillende formaten

Aspose.Cells laat je het resultaat opslaan in veel formaten zonder extra code‑aanpassingen:

```java
// Save as XLS (Excel 97-2003)
destWb.save("dest.xls");

// Save as CSV (first worksheet only)
destWb.save("dest.csv");

// Save as PDF (visual representation)
destWb.save("dest.pdf");
```

Kies het formaat dat past bij je downstream‑proces. Dezelfde `copyRange`‑logica werkt ongeacht het uiteindelijke formaat.

---

## Excel‑werkboek Java laden – extra tips

* **Versleutelde bestanden laden:** Use `LoadOptions` with a password:  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setPassword("myPassword");
  Workbook wb = new Workbook("encrypted.xlsx", opt);
  ```
* **Alleen specifieke bladen lezen:**  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setLoadDataOnly(true); // faster if you only need values
  Workbook wb = new Workbook("file.xlsx", opt);
  ```

Deze opties kunnen de **load excel workbook java** stap versnellen, vooral voor grote bestanden.

---

## Conclusie

Je weet nu **hoe je cellen** tussen Excel‑werkboeken in Java kunt kopiëren, hoe je **bereik tussen werkboeken** kunt kopiëren dat een **draaientabel** bevat, en hoe je **werkboekbestand** kunt opslaan in het gewenste formaat. Door de bovenstaande stappen te volgen, kun je Excel‑datamanipulatie integreren in elke Java‑applicatie—of je nu een rapportage‑engine, een ETL‑pipeline of een eenvoudige bestands‑conversie‑tool bouwt.

**Volgende stappen** die je kunt verkennen:

* Use **copy range between workbooks** to merge multiple reports into

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Opslaan nieuw werkboek in Java – Kopieer bereik tussen werkboeken tutorial](/cells/english/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/)
- [Hoe draaitabellen te kopiëren tussen Excel-werkboeken in Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/)
- [Hoe bereik te kopiëren in Java – Kopieer draaitabel met Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}