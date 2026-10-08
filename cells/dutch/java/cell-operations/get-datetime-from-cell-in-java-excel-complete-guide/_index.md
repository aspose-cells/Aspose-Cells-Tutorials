---
category: general
date: 2026-06-08
description: Haal datum en tijd op uit een cel met Aspose.Cells Java en leer hoe je
  een waarde in een Excel-cel schrijft in slechts een paar stappen.
draft: false
keywords:
- get datetime from cell
- write value to excel cell
- Aspose.Cells Java date parsing
- Japanese era calendar Excel
- Excel formula recalculation Java
language: nl
og_description: Haal datum en tijd op uit een cel met Aspose.Cells Java. Deze tutorial
  laat ook zien hoe je efficiënt een waarde naar een Excel-cel schrijft.
og_title: Datum en tijd uit cel halen in Java Excel – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  headline: Get datetime from cell in Java Excel – Complete Guide
  type: TechArticle
- description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  name: Get datetime from cell in Java Excel – Complete Guide
  steps:
  - name: What if the cell already contains a true Excel date?
    text: 'If `cell.getType()` returns `CellValueType.IS_DATE_TIME`, you can skip
      the recalculation step and read the value directly:'
  - name: How to process a whole column of era strings?
    text: 'Loop through the used range and apply the same settings once:'
  - name: Can I disable the Japanese era handling later?
    text: 'Yes—just flip the flag back:'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
title: Datum en tijd uit cel halen in Java Excel – Complete gids
url: /nl/java/cell-operations/get-datetime-from-cell-in-java-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Datum en tijd ophalen uit cel in Java Excel – Complete gids

Heb je ooit **datum en tijd uit een cel moeten halen** maar ziet de waarde eruit als een Japanse jaartelling? Je bent niet de enige. In veel legacy‑spreadsheets worden datums opgeslagen als “Reiwa 3/04/01”, en het extraheren van een juiste `java.time.LocalDateTime` voelt soms als het ontcijferen van een geheime boodschap.  

Gelukkig kan Aspose.Cells for Java de conversie voor je afhandelen, en daarnaast laten we je zien hoe je **waarde naar een Excel‑cel kunt schrijven** zodat je data heen‑en‑terug kunt sturen zonder de logica van het blad te breken.

In deze tutorial leer je:

* Hoe je een workbook maakt en een specifiek werkblad selecteert.  
* De exacte stappen om de Japanse jaartelling in te schakelen voor het parseren.  
* Waarom je formules moet herberekenen voordat je de datum leest.  
* Hoe je een nieuwe waarde terugschrijft naar een cel zonder opmaak te verliezen.  

Geen externe tools, geen magie—alleen gewone Java‑code die je vandaag nog in elk Maven‑project kunt gebruiken.

---

## Prerequisites

* **Java 8+** (het voorbeeld gebruikt de moderne `java.time`‑API).  
* **Aspose.Cells for Java** ≥ 23.9.0 – voeg de dependency toe via Maven of Gradle.  
* Basiskennis van Excel‑concepten (werkbladen, cellen, formules).  

Als je de bibliotheek mist, haal deze dan op uit de officiële Aspose‑repository:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9.0</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Step 1: Create a new workbook and access the first worksheet

Om te beginnen hebben we een nieuw `Workbook`‑object nodig. Beschouw het als het openen van een nieuw Excel‑bestand in het geheugen.

```java
// Step 1: Initialize workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

*Waarom dit belangrijk is:*  
Het programmatically aanmaken van het workbook geeft je volledige controle over instellingen voordat er data op het bestandssysteem wordt geschreven. Het eerste werkblad (`index 0`) is waar we zowel lezen als schrijven demonstreren.

---

## Step 2: Write a Japanese era date string into cell A1

Nu **schrijven we een waarde naar een Excel‑cel** A1. Dit spiegelt een real‑world scenario waarin een gebruiker handmatig “Reiwa 3/04/01” invoert.

```java
// Step 2: Write the era date string into A1
Cell cell = worksheet.getCells().get("A1");
cell.putValue("Reiwa 3/04/01"); // raw string, not yet a date
```

*Snel tip:* `putValue` is veelzijdig—het accepteert strings, getallen, datums en zelfs formules. Wanneer je een gewone string doorgeeft, slaat Aspose deze exact op zoals hij is, wat perfect is voor onze demo.

---

## Step 3: Enable the Japanese era calendar for date parsing

Standaard gebruikt Aspose.Cells de gregoriaanse kalender. Om “Reiwa” te kunnen interpreteren, schakelen we een instelling in.

```java
// Step 3: Turn on Japanese era calendar support
WorkbookSettings settings = workbook.getSettings();
settings.setUseJapaneseEraCalendar(true);
```

*Waarom dit inschakelen?*  
De Japanse jaartelling koppelt era‑namen (Reiwa, Heisei, Showa) aan hun gregoriaanse equivalenten. Zonder deze vlag zou de bibliotheek de string als platte tekst behandelen, en zou je nooit een juiste `DateTime`‑object krijgen.

---

## Step 4: Recalculate formulas so the era string converts to a Gregorian date

Aspose parseert de string niet automatisch naar een datum. In plaats daarvan behandelt het de cel als een formule‑resultaat na een berekeningsstap.

```java
// Step 4: Force a recalculation to convert the era string
workbook.calculateFormula(); // processes all cells, including A1
System.out.println(cell.getDateTime()); // → 2021‑04‑01
```

Wanneer `calculateFormula()` wordt uitgevoerd, herkent de engine het era‑patroon, past de Japanse kalender toe en slaat de resulterende gregoriaanse datum intern op. De `getDateTime()`‑aanroep retourneert vervolgens een `java.util.Date` (of je kunt converteren naar `java.time`).

**Verwachte output**

```
2021-04-01T00:00:00.000+00:00
```

---

## Step 5: Write a new value back to the same cell (or another cell)

Stel dat je de oorspronkelijke string wilt overschrijven met een nette ISO‑8601‑datum. Hier zie je hoe je **waarde naar een Excel‑cel** veilig schrijft, terwijl je de stijl van de cel behoudt.

```java
// Step 5: Overwrite A1 with a formatted date string
java.time.LocalDateTime now = java.time.LocalDateTime.now();
cell.putValue(now); // Aspose will store it as a proper Excel date
// Optional: apply a date format style
Style style = cell.getStyle();
style.setNumber(14); // built‑in "m/d/yyyy" format
cell.setStyle(style);
```

*Wat gebeurt er?*  
`putValue` detecteert het `LocalDateTime`‑type en zet het om naar de seriële getalrepresentatie van Excel. Het instellen van het getalformaat zorgt ervoor dat de cel de datum exact weergeeft zoals je verwacht wanneer je het bestand in Excel opent.

---

## Full Working Example

Alles bij elkaar, hier is een enkele Java‑klasse die je kunt compileren en uitvoeren. Het maakt een workbook, schrijft een era‑string, converteert deze en slaat uiteindelijk het bestand op.

```java
import com.aspose.cells.*;

public class JapaneseEraDateDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first sheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ Write Japanese era date string to A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue("Reiwa 3/04/01");

        // 3️⃣ Enable Japanese era calendar
        WorkbookSettings settings = workbook.getSettings();
        settings.setUseJapaneseEraCalendar(true);

        // 4️⃣ Recalculate so the string becomes a Gregorian date
        workbook.calculateFormula();
        System.out.println("Converted date: " + cell.getDateTime());

        // 5️⃣ Overwrite with a clean LocalDateTime (optional)
        java.time.LocalDateTime now = java.time.LocalDateTime.now();
        cell.putValue(now);
        Style style = cell.getStyle();
        style.setNumber(14); // m/d/yyyy
        cell.setStyle(style);

        // 6️⃣ Save the workbook
        workbook.save("output.xlsx");
        System.out.println("Workbook saved as output.xlsx");
    }
}
```

Voer dit uit met `java -cp aspose-cells-23.9.jar;. JapaneseEraDateDemo` en open **output.xlsx**. Je ziet cel A1 met de huidige datum, terwijl de console de geconverteerde “2021‑04‑01” waarde logt.

---

## Handling Edge Cases & Common Questions

### What if the cell already contains a true Excel date?

Als `cell.getType()` `CellValueType.IS_DATE_TIME` retourneert, kun je de herberekeningsstap overslaan en de waarde direct lezen:

```java
if (cell.getType() == CellValueType.IS_DATE_TIME) {
    System.out.println("Already a date: " + cell.getDateTime());
}
```

### How to process a whole column of era strings?

Loop door het gebruikte bereik en pas dezelfde instellingen één keer toe:

```java
Range used = worksheet.getCells().getMaxDisplayRange();
for (int row = 0; row < used.getRowCount(); row++) {
    Cell c = used.getCell(row, 0); // column A
    c.putValue(c.getStringValue()); // re‑assign to trigger parsing
}
workbook.calculateFormula();
```

### Can I disable the Japanese era handling later?

Ja—schakel de vlag gewoon weer uit:

```java
settings.setUseJapaneseEraCalendar(false);
```

Vergeet niet opnieuw te herberekenen als je de instelling wijzigt nadat je data hebt geschreven.

---

## Pro Tips & Gotchas

* **Performance:** Het inschakelen van de Japanse jaartelling voegt een kleine overhead toe. Als je het slechts voor een paar cellen nodig hebt, overweeg dan de instelling in te schakelen, te verwerken, en daarna weer uit te schakelen.  
* **Locale awareness:** De era‑string moet exact het patroon “EraName yy/MM/dd” volgen. Een typefout in “Reiwa” (bijv. “Rewa”) laat de cel als platte tekst staan.  
* **Saving format:** `Workbook.save("output.xlsx")` schrijft een XLSX‑bestand. Gebruik `"output.xls"` als je het oudere binaire formaat nodig hebt, maar let op dat sommige functies (zoals era‑parsing) beperkt kunnen zijn.

---

## Conclusion

Je weet nu hoe je **datum en tijd uit een cel** kunt halen wanneer de bron een Japanse era‑notatie gebruikt, en je hebt ook een nette manier gezien om **waarde naar een Excel‑cel** te schrijven met de juiste opmaak. Door `setUseJapaneseEraCalendar(true)` in te schakelen en een formule‑herberekening af te dwingen, overbrugt Aspose.Cells de kloof tussen legacy‑era‑strings en moderne gregoriaanse datums—allemaal met een handvol Java‑regels.

Wat nu? Probeer dit patroon uit te breiden naar andere culturele kalenders (Thai, Hijri) of verwerk grote workbooks in batch met dezelfde aanpak. Dezelfde principes—de juiste kalender inschakelen, herberekenen, dan lezen/schrijven—gelden overal.

Heb je een lastig datumformaat dat je niet kunt kraken? Laat een reactie achter hieronder, en laten we samen het probleem oplossen. Happy coding!  

![Get datetime from cell example](https://example.com/images/get-datetime-from-cell.png "Get datetime from cell example")


## What Should You Learn Next?


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende codevoorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementaties in je eigen projecten te verkennen.

- [Master the 1904 Date System in Excel Using Aspose.Cells Java for Effective Cell Operations](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [How to Implement Recursive Cell Calculation in Aspose.Cells Java for Enhanced Excel Automation](/cells/english/java/calculation-engine/aspose-cells-java-recursive-cell-calculations/)
- [How to Convert Excel Cell Names to Indices Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}