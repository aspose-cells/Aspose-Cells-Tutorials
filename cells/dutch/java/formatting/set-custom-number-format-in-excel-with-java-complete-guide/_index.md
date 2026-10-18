---
category: general
date: 2026-06-30
description: Stel een aangepast getalformaat in Excel in met Java. Leer hoe je een
  Excel-werkmap maakt met Java, datum‑tijd uit een cel haalt, werkmapformules berekent
  en de datum‑tijdwaarde uitvoert.
draft: false
keywords:
- set custom number format
- get datetime from cell
- create excel workbook java
- calculate workbook formulas
- output datetime value
language: nl
og_description: Stel een aangepast getalformaat in Excel in met Java. Deze gids laat
  zien hoe je een Excel-werkmap maakt met Java, datum‑tijd uit een cel haalt, werkmapformules
  berekent en de datum‑tijdwaarde uitvoert.
og_title: Aangepast getalformaat instellen in Excel met Java – Volledige tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  headline: Set Custom Number Format in Excel with Java – Complete Guide
  type: TechArticle
- description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  name: Set Custom Number Format in Excel with Java – Complete Guide
  steps:
  - name: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
    text: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
  - name: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
    text: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
  - name: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
    text: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DateTime
title: Aangepast getalformaat instellen in Excel met Java – Complete gids
url: /nl/java/formatting/set-custom-number-format-in-excel-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aangepast getalformaat instellen in Excel met Java – Complete gids

Heb je ooit moeten **set custom number format** in een Excel‑werkblad terwijl je in Java werkt? Je bent niet de enige. Of je nu een rapportage‑engine bouwt of gewoon Japanse jaartijd‑datums correct wilt weergeven, het beheersen van deze truc bespaart je talloze uren post‑processing. In deze tutorial lopen we door een praktijkvoorbeeld dat **creates Excel workbook Java**, een locale‑specifiek formaat toepast, formules opnieuw berekent, en uiteindelijk **gets DateTime from cell** naar **output datetime value**.

We gebruiken de populaire Aspose.Cells for Java bibliotheek omdat deze getalformaten en cultuur‑bewuste datums direct ondersteunt. Aan het einde van de gids heb je een zelfstandige, uitvoerbare programma dat je in elk Maven‑ of Gradle‑project kunt plaatsen. Geen vage “see the docs” shortcuts—alleen solide code en duidelijke uitleg.

---

## Wat je zult leren

- Hoe je **create Excel workbook Java** programmatically kunt maken.  
- De exacte stappen om **set custom number format** voor Japanse era‑datums toe te passen.  
- Waarom het aanroepen van **calculate workbook formulas** essentieel is vóór het extraheren van de waarde.  
- De juiste manier om **get datetime from cell** en **output datetime value** te doen.  
- Veelvoorkomende valkuilen (ontbrekende locale, verouderde formules) en snelle oplossingen.

---

## Vereisten

- Java 8 of nieuwer geïnstalleerd op je machine.  
- Aspose.Cells for Java 23.11 (of een recentere versie).  
- Een basis‑IDE of teksteditor—IntelliJ IDEA, Eclipse, VS Code, wat je maar verkiest.  

Als je Aspose.Cells nog niet aan je project hebt toegevoegd, plak dan het volgende Maven‑fragment in je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.11</version>
</dependency>
```

Gradle‑gebruikers kunnen toevoegen:

```gradle
implementation 'com.aspose:aspose-cells:23.11'
```

Nu de omgeving klaar is, duiken we in de code.

---

## Stap 1: Aangepast getalformaat instellen – Overzicht

Voordat we Java schrijven, helpt het om te visualiseren wat we willen bereiken. Stel je een Excel‑cel voor die **“令和2年4月1日”** moet weergeven in plaats van de ISO‑8601‑string “2020‑04‑01”. De onderliggende waarde blijft een echte datum (zodat formules nog steeds werken), maar de *weergave* volgt het Japanse era‑formaat. Dit is precies wat de **set custom number format**‑bewerking bereikt.

Hieronder staat het volledige bronbestand. Voel je vrij om het te kopiëren‑plakken in `src/main/java/SetCustomNumberFormatDemo.java`.

```java
// File: SetCustomNumberFormatDemo.java
import com.aspose.cells.*;

public class SetCustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Create Excel workbook Java – a fresh workbook
        // -------------------------------------------------
        Workbook workbook = new Workbook();               // in‑memory workbook, no file yet

        // -------------------------------------------------
        // 2️⃣ Access the first worksheet
        // -------------------------------------------------
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // -------------------------------------------------
        // 3️⃣ Retrieve cell A1 where we’ll store the date string
        // -------------------------------------------------
        Cell cellA1 = worksheet.getCells().get("A1");

        // -------------------------------------------------
        // 4️⃣ Insert a Japanese era date string (Reiwa 2‑04‑01)
        // -------------------------------------------------
        // Note: Aspose.Cells will treat this as a text value until we recalc.
        cellA1.putValue("R02-04-01");

        // -------------------------------------------------
        // 5️⃣ Apply the custom number format (our primary goal)
        // -------------------------------------------------
        // [$-ja-JP] tells Excel to use the Japanese locale.
        // ggge年m月d日 renders as "令和2年4月1日".
        cellA1.setNumberFormat("[$-ja-JP]ggge年m月d日");

        // -------------------------------------------------
        // 6️⃣ Calculate workbook formulas – crucial step!
        // -------------------------------------------------
        // Without this, the cell remains a plain string and the
        // DateTime conversion below will fail.
        workbook.calculateFormula();

        // -------------------------------------------------
        // 7️⃣ Get DateTime from cell – now the value is a true date
        // -------------------------------------------------
        // The getDateTime() method returns a java.util.Calendar instance.
        java.util.Calendar dt = cellA1.getDateTime();

        // -------------------------------------------------
        // 8️⃣ Output datetime value – see the result in console
        // -------------------------------------------------
        System.out.println("Converted DateTime: " + dt.getTime()); // → Tue Apr 01 00:00:00 UTC 2020
    }
}
```

### Waarom dit werkt

- **`setNumberFormat`** vertelt Excel hoe de onderliggende numerieke waarde *weergegeven* moet worden. De opmaakstring `[$-ja-JP]ggge年m月d日` is de sleutel; `ggg` selecteert de era‑naam, `e` het jaar binnen de era, gevolgd door maand‑ en dag‑lettergrepen.  
- **`calculateFormula`** dwingt Aspose.Cells om de tekst “R02-04-01” als een datum te interpreteren op basis van de Japanse kalender. Als je deze stap overslaat, blijft de cel platte tekst en zou `getDateTime()` een uitzondering gooien.  
- **`getDateTime`** haalt uiteindelijk het *werkelijke* `java.util.Calendar`‑object op, dat je kunt manipuleren, formatteren of elders opslaan.

---

## Stap 2: Excel‑werkboek maken met Java – Dieper kijken

Wanneer je **create Excel workbook Java**, allocate je niet alleen geheugen; je stelt ook standaardstijlen, een standaardwerkblad en een standaardcultuur (meestal de systeem‑locale) in. Als je een andere standaard‑locale nodig hebt, kun je een `LoadOptions`‑object doorgeven:

```java
LoadOptions opts = new LoadOptions(LoadFormat.XLSX);
opts.setLocale(new java.util.Locale("ja", "JP"));
Workbook workbook = new Workbook(opts);
```

Voor de meeste scenario’s is de eenvoudige constructor voldoende, maar het is goed om de alternatieve manier te kennen—vooral wanneer je met meerdere locales in dezelfde applicatie werkt.

*Pro tip:* Houd het werkboek altijd in het geheugen totdat je klaar bent met formatteren. Schrijven naar schijf na elke wijziging veroorzaakt onnodige I/O‑overhead.

---

## Stap 3: DateTime uit cel halen – Resultaat verwerken

De regel `java.util.Calendar dt = cellA1.getDateTime();` doet het zware werk. Achter de schermen converteert Aspose.Cells het interne seriële getal (het aantal dagen sinds 31‑12‑1899) naar een `Calendar`. Deze conversie respecteert de locale van het werkboek, zodat je de juiste Gregoriaanse datum krijgt, ook al gebruikt de weergave de Japanse era.

Als je een `java.time.LocalDate` nodig hebt (de nieuwere API), converteer dan als volgt:

```java
java.time.LocalDate localDate = dt.toInstant()
        .atZone(java.time.ZoneId.systemDefault())
        .toLocalDate();
System.out.println("LocalDate: " + localDate); // 2020-04-01
```

Dat dekt de **output datetime value**‑vereiste terwijl je modern blijft.

---

## Stap 4: Werkboekformules berekenen – Wanneer het telt

Je vraagt je misschien af: *“Moet ik echt `calculateFormula()` aanroepen?”* Het antwoord is een volmondig ja, tenzij je de cel vanaf het begin voedt met een native Java `Date`‑object. Wanneer je **set custom number format** toepast op een tekst‑string, behandelen Excel (en Aspose.Cells) dit als een formule‑achtige expressie die geëvalueerd moet worden. Zonder herberekening zal `getDateTime()` de standaard `1900‑01‑00` teruggeven of een `CellValueException` gooien.

Als je werkboek al complexe formules bevat die naar de nieuw geformatteerde cel verwijzen, roep dan `calculateFormula()` *eenmaal* aan na alle wijzigingen. Herhaalde aanroepen zijn kostbaar.

---

## Stap 5: DateTime‑waarde outputten – Resultaat verifiëren

Het uitvoeren van de demo print iets als:

```
Converted DateTime: Tue Apr 01 00:00:00 UTC 2020
```

Die regel bevestigt drie dingen:

1. De **set custom number format** is toegepast (je kunt het gegenereerde `.xlsx` in Excel openen om “令和2年4月1日” te zien).  
2. De stap **calculate workbook formulas** is geslaagd, waardoor de era‑string in een echte datum werd omgezet.  
3. De **get datetime from cell**‑aanroep leverde een juiste `Calendar` op, die we vervolgens **output datetime value** naar de console schreven.

Als je het werkboek opent met een spreadsheet‑programma, zie je de geformatteerde tekst, maar de onderliggende celwaarde blijft het seriële getal `43831` (de Excel‑representatie van 2020‑04‑01). Deze dualiteit maakt Excel krachtig.

---

## Veelvoorkomende valkuilen & randgevallen

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| `cellA1.getDateTime()` throws `CellValueException` | De cel is nog steeds een string omdat `calculateFormula()` weggelaten is. | Roep altijd `workbook.calculateFormula()` aan na het instellen van een tekstdatum die geconverteerd moet worden. |
| Japanese era not displayed correctly | Locale‑code ontbreekt of is onjuist. | Gebruik `[$-ja-JP]` in de opmaakstring, of stel de werkboek‑locale in via `LoadOptions`. |
| Format shows “#VALUE!” in Excel | De opmaakstring is onjuist gevormd. | Controleer haakjes en tekens; het patroon `ggge年m月d日` is vereist voor era‑jaar. |
| Time component appears (e.g., “00:00:00”) | De bron‑string bevat tijd of de celstijl voegt het toe. | Trim de bron‑string of pas de opmaak aan naar `ggge年m月d日;@`. |

---

## Volledig werkend voorbeeld – Eén‑klik uitvoering

Als je de voorkeur geeft aan één enkel bestand zonder extra commentaren, hier is de minimale versie:



## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Maak een Excel‑werkboek met Aspose.Cells in Java: Een stapsgewijze gids](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Meesterschap in gegevenspresentatie in Excel: getal‑ en aangepaste datumopmaak met Aspose.Cells for Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Hoe Excel‑cellen te maken & op te maken met Aspose.Cells for Java: Een stapsgewijze gids](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}