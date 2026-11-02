---
category: general
date: 2026-07-03
description: Hoe Excel‑bestanden te stylen met Java. Leer kolomdatums in Excel op
  te maken, getalnotatie in Excel toe te passen, DataTable naar XLSX te exporteren
  en DataTable in Excel te importeren met Aspose Cells.
draft: false
keywords:
- how to style excel
- format column date excel
- apply number format excel
- export datatable to xlsx
- import datatable into excel
language: nl
og_description: Hoe Excel-bestanden te stylen in Java. Deze tutorial laat zien hoe
  je kolomdatums in Excel formatteert, getalnotaties toepast, DataTable exporteert
  naar XLSX en DataTable importeert in Excel.
og_title: Hoe Excel te stylen – Java-gids voor aangepaste kolomopmaak
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to style Excel files using Java. Learn to format column date Excel,
    apply number format Excel, export DataTable to XLSX and import DataTable into
    Excel with Aspose Cells.
  headline: How to Style Excel – Import DataTable with Custom Formatting in Java
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: Hoe Excel opmaken – DataTable importeren met aangepaste opmaak in Java
url: /nl/java/excel-import-export/how-to-style-excel-import-datatable-with-custom-formatting-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Excel Stijlen – DataTable Importeren met Aangepaste Opmaak in Java

Heb je je ooit afgevraagd **how to style Excel** bladen programmatisch te stylen zonder het bestand handmatig te openen? Je bent niet de enige. Veel ontwikkelaars moeten rapporten genereren waarbij de eerste kolom vetgedrukt is, de tweede datums toont, en de rest een nette lay-out volgt. In deze gids lopen we een volledig, uitvoerbaar voorbeeld door dat **imports a DataTable into Excel**, een vetgedrukte kop toepast, een datumkolom opmaakt, en uiteindelijk **exports DataTable to XLSX**.

We gebruiken Aspose.Cells for Java, maar de concepten zijn toepasbaar op elke bibliotheek die met stijlen werkt. Aan het einde heb je een herbruikbaar patroon voor **apply number format Excel** cellen, **format column date Excel**, en kun je een gepolijste werkmap aan je gebruikers leveren.

## Vereisten

- Java 17 (of een recente JDK)  
- Aspose.Cells for Java 23.9 of nieuwer (de gratis proefversie werkt prima)  
- Een `DataTable`‑achtige structuur (het voorbeeld gebruikt een eenvoudige mock)  
- Je favoriete IDE (IntelliJ IDEA, Eclipse, VS Code…)

Er zijn geen extra Maven-plugins nodig; voeg gewoon de Aspose.Cells JAR toe aan je classpath.

---

## Stap 1: Verkrijg de Bron DataTable – “Export DataTable to XLSX” Voorbereiding

Voordat we **import datatable into excel** kunnen, hebben we een `DataTable`‑object nodig dat de gegevens vertegenwoordigt die je wilt exporteren. In echte projecten haal je dit misschien uit een database, CSV‑bestand of een API. Voor deze tutorial mocken we een kleine tabel:

```java
import java.util.*;
import com.aspose.cells.*;

public class DemoData {
    public static DataTable getDataTable() {
        // Create a simple table with three columns: ID, Date, Amount
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("OrderDate", DataType.DATE_TIME);
        dt.getColumns().add("Total", DataType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[]{1, new Date(), 125.50});
        dt.getRows().add(new Object[]{2, new Date(System.currentTimeMillis() - 86400000L), 99.99});
        dt.getRows().add(new Object[]{3, new Date(System.currentTimeMillis() - 2*86400000L), 250.00});
        return dt;
    }
}
```

> **Waarom dit belangrijk is:** De gegevens meteen correct hebben betekent dat de rest van de stijllogica zich puur op presentatie kan richten, niet op data‑manipulatie.

---

## Stap 2: Maak een Array om Stijldefinities voor Elke Kolom Vast te Houden

Aspose.Cells laat je een **Style[]**‑array doorgeven bij het importeren van een `DataTable`. Elke entry correspondeert met een kolom en bepaalt hoe die kolom eruitziet na de import. Laten we de array toewijzen op basis van het aantal kolommen:

```java
DataTable dataTable = DemoData.getDataTable();
Style[] columnStyles = new Style[dataTable.getColumns().size()];
```

> **Tip:** Als je veel kolommen hebt, overweeg dan de array in een lus te bouwen en een enkel `Style`‑object te hergebruiken waar de opmaak identiek is. Dit vermindert het geheugenverbruik.

---

## Stap 3: Definieer de Stijlen – Vet Koptekst & Datumopmaak

Nu beantwoorden we de klassieke **format column date excel** vraag en demonstreren we ook **apply number format excel** voor andere kolommen.

```java
// --- Style for the first column (header bold) ---
columnStyles[0] = new Style();
columnStyles[0].getFont().setBold(true);          // Makes header text bold

// --- Style for the second column (date formatting) ---
columnStyles[1] = new Style();
columnStyles[1].setNumber(StyleNumberFormat.DATE); // Uses the built‑in DATE format

// --- Optional: Style for the third column (currency) ---
columnStyles[2] = new Style();
columnStyles[2].setNumber(StyleNumberFormat.CURRENCY_USD);
```

**Wat gebeurt er hier?**  
- `StyleNumberFormat.DATE` vertelt Excel de celwaarde als een korte datum te behandelen (bijv. *01/31/2024*).  
- `StyleNumberFormat.CURRENCY_USD` voegt automatisch het `$`‑symbool en twee decimalen toe.  
- Het instellen van het lettertype op vet in de eerste kolom laat de koptekst opvallen, wat vaak vereist is wanneer je **how to style excel** spreadsheets voor leesbaarheid.

> **Randgeval:** Als je brongegevens al opgemaakte strings bevatten, moet je ze mogelijk omzetten naar `java.util.Date`‑objecten vóór import; anders behandelt Excel ze als platte tekst.

---

## Stap 4: Maak een Nieuwe Werkmap en Toegang tot het Eerste Werkblad

Een nieuwe werkmap geeft ons een schoon canvas. We pakken het eerste werkblad, waar de import terechtkomt.

```java
Workbook workbook = new Workbook();               // New empty workbook
Worksheet worksheet = workbook.getWorksheets().get(0); // First sheet (index 0)
```

> **Waarom een nieuwe werkmap?** Vanaf nul beginnen garandeert dat er geen achtergebleven stijlen of verborgen rijen de uiteindelijke output beïnvloeden—essentieel wanneer je **how to style excel** bestanden consistent wilt verwerken over meerdere runs.

---

## Stap 5: Importeer de DataTable met de Kolomstijlen

Dit is het hart van de operatie: de `DataTable` in het blad voeren terwijl we de stijlarray toepassen die we hebben gebouwd.

```java
// The third argument (true) tells Aspose.Cells to include column headers.
worksheet.getCells().importDataTable(dataTable, true, columnStyles);
```

**Uitleg:**  
- `importDataTable` kopieert zowel de koprij als de gegevensrijen.  
- De `columnStyles`‑array stemt overeen met elke kolom, zodat de kop van de eerste kolom vet wordt, de tweede kolom datums toont, en de derde kolom als valuta verschijnt.  
- Deze enkele regel vervangt tientallen handmatige cel‑voor‑cel opmaakstappen, en illustreert een nette manier om **apply number format excel** programmatisch toe te passen.

> **Pro tip:** Als je oudere Excel‑versies moet ondersteunen, roep dan `workbook.save(outputPath, SaveFormat.XLS)` aan in plaats van de standaard XLSX.

---

## Stap 6: Sla de Gestylede Werkmap Op – Voltooiing van de “Export DataTable to XLSX”

Tot slot slaan we de werkmap op op schijf. Pas het pad aan naar een schrijfbare map op je machine.

```java
String outputPath = "C:/temp/styledImport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Open het bestand in Excel en je zou moeten zien:

- Kolom **ID** koptekst in vet.  
- Kolom **OrderDate** opgemaakt als datums (bijv. *04/27/2024*).  
- Kolom **Total** weergegeven met een dollarteken en twee decimalen.

> **Pro tip:** Als je oudere Excel‑versies moet ondersteunen, roep dan `workbook.save(outputPath, SaveFormat.XLS)` aan in plaats van de standaard XLSX.

---

## Stap 7: Verifieer het Resultaat & Optionele Aanpassingen

Het is een goede gewoonte om het gegenereerde bestand dubbel te controleren, vooral bij het automatiseren van rapporten voor belanghebbenden.

```java
// Quick verification: read the first cell's style
Cell firstHeader = worksheet.getCells().get(0, 0);
boolean isBold = firstHeader.getStyle().getFont().isBold();
System.out.println("Header bold? " + isBold);
```

Als `isBold` `true` afdrukt, heeft je **how to style excel** routine gewerkt zoals bedoeld. Vanaf hier kun je:

- Voorwaardelijke opmaak toevoegen (bijv. totalen > $200 markeren).  
- De bovenste rij bevriezen voor gemakkelijker scrollen.  
- Een grafiek invoegen die verwijst naar de geïmporteerde gegevens.

Al deze uitbreidingen volgen hetzelfde patroon: definieer een `Style`, pas deze toe, en sla op.

## Veelgestelde Vragen & Randgevallen

| Vraag | Antwoord |
|----------|--------|
| **Kan ik meer dan één kolom op dezelfde manier stijlen?** | Ja—hergebruik een enkele `Style`‑instance voor alle kolommen die dezelfde opmaak delen. |
| **Wat als mijn DataTable meer kolommen heeft dan stijlen?** | Elke kolom zonder een overeenkomstige entry in `columnStyles` zal de standaardstijl gebruiken. |
| **Hoe wijzig ik het datumformaat naar “dd‑MMM‑yyyy”?** | Gebruik `columnStyles[1].setCustom("#dd-MMM-yyyy#");` in plaats van de ingebouwde `DATE`. |
| **Is er een manier om kolommen automatisch te schalen na import?** | Roep `worksheet.autoFitColumns();` aan na `importDataTable`. |
| **Werkt dit op Linux/macOS?** | Absoluut—Aspose.Cells is platform‑onafhankelijk zolang je een compatibele JDK hebt. |

## Conclusie

Je hebt nu een solide, end‑to‑end voorbeeld van **how to style Excel** werkboeken door **importing datatable into excel**, **format column date excel**, en **apply number format excel** te gebruiken met Java. De code toont de volledige stroom van **export datatable to xlsx** tot het openen van het bestand in Excel, en behandelt zowel het *wat* als het *waarom* achter elke stap.

Probeer het: pas de stijlarray aan, voeg meer kolommen toe, of koppel een echte database‑query. Hetzelfde patroon stelt je in staat om professioneel uitziende rapporten te genereren met één klik, zonder handmatige opmaak.

![Styled Excel worksheet created using Java and Aspose.Cells, showing bold header and formatted date column](https://example.com/images/styled-worksheet.png "Screenshot of styled Excel worksheet created using Java and Aspose.Cells")

*Afbeelding alt‑tekst: “Gestylede Excel-werkblad gemaakt met Java en Aspose.Cells, met vet koptekst en opgemaakte datumkolom.”*

## Wat Moet Je Hierna Leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe Excel‑cellen te Maken & Op te Maken met Aspose.Cells for Java: Een Stapsgewijze Gids](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Hoe Excel‑cellen te Stijlen en Hyperlinks Toe te Voegen met Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Aspose.Cells for Java: Hoe Excel‑werkboeken Efficiënt te Maken en Op te Maken](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}