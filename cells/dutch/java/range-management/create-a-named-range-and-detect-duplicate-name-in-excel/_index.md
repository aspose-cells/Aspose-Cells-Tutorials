---
category: general
date: 2026-09-27
description: Maak een benoemd bereik in Excel met Aspose.Cells, stel de tabelnaam
  in, voeg een benoemd bereik toe, maak een Excel‑tabel en detecteer fouten bij dubbele
  namen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create named range
- set table name
- create excel table
- add named range
- detect duplicate name
language: nl
lastmod: 2026-09-27
og_description: Maak een benoemd bereik in Excel met Aspose.Cells, stel vervolgens
  de tabelnaam in, voeg een benoemd bereik toe, maak een Excel-tabel en detecteer
  fouten bij dubbele namen.
og_image_alt: Screenshot showing how to create a named range in Excel with Aspose.Cells
og_title: Maak een benoemd bereik en detecteer dubbele naam in Excel
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Create a named range in Excel using Aspose.Cells, set table name, add
    named range, create Excel table, and detect duplicate name errors.
  headline: Create a named range and detect duplicate name in Excel
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Maak een benoemd bereik en detecteer dubbele naam in Excel
url: /nl/java/range-management/create-a-named-range-and-detect-duplicate-name-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak een named range en detecteer duplicate name in Excel

Als je een **named range** moet **maken** in een Excel-werkmap en naamconflicten wilt vermijden, laat deze gids je precies zien hoe je dat doet met Aspose.Cells for Java. Je leert **add named range**, **create Excel table**, **set table name**, en **detect duplicate name** fouten in één zelf‑bevat voorbeeld.

Werken met named ranges is een veelvoorkomende eis wanneer je rapportagetools, data‑validatiebladen of dynamische dashboards bouwt. Aan het einde van deze tutorial heb je een uitvoerbaar programma dat veilig een named range maakt, een tabel bouwt en op elegante wijze eventuele name‑conflict‑exceptions afhandelt.

## Vereisten

- Java 17 of later geïnstalleerd
- Maven of Gradle voor afhankelijkheidsbeheer
- Aspose.Cells for Java (nieuwste versie; Maven‑coördinaat `com.aspose:aspose-cells:23.9` op het moment van schrijven)
- Basiskennis van Excel-concepten zoals werkbladen, bereiken en tabellen

## Stap 1: Maak een named range in de werkmap

De eerste stap is het instantieren van een `Workbook`‑object en het toevoegen van een named range die naar een specifiek celblok wijst.

```java
import com.aspose.cells.*;

public class NamedRangeDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the default first worksheet (named "Sheet1")
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Define a named range called "MyRange" that covers A1:C5
        // This demonstrates the "add named range" operation.
        workbook.getNames().add("MyRange", "'Sheet1'!$A$1:$C$5");
```

**Waarom dit belangrijk is:**  
Een named range fungeert als een herbruikbare referentie waar formules en tabellen naar kunnen verwijzen. Het vroeg toevoegen zorgt ervoor dat latere stappen dezelfde identifier kunnen hergebruiken zonder celadressen hard‑gecodeerd te gebruiken.

## Stap 2: Maak een Excel‑tabel die de named range gebruikt

Vervolgens maken we een gestructureerde tabel (ListObject) die hetzelfde gebied beslaat als de named range. Dit illustreert het **create excel table**‑concept.

```java
        // Create an Excel table (ListObject) that spans the same area as the named range.
        // The parameters (0,0,4,2) represent the top‑left cell (A1) and bottom‑right cell (C5).
        ListObject table = sheet.getListObjects().add(0, 0, 4, 2, true);
```

**Waarom dit belangrijk is:**  
Tabellen bieden ingebouwde sortering, filteren en opmaak. Door de tabel op één lijn te brengen met de named range houd je het datamodel consistent.

## Stap 3: Stel tabelnaam in en behandel een mogelijk conflict

Nu proberen we de tabel een naam te geven die overeenkomt met de eerder gemaakte named range. Deze stap demonstreert **set table name** en veroorzaakt opzettelijk een naamconflict.

```java
        try {
            // Attempt to set the table name to "MyRange".
            // Because a named range with the same identifier already exists,
            // Aspose.Cells will throw an exception.
            table.setName("MyRange"); // <-- conflict expected
        } catch (Exception e) {
            // Step 4: Detect duplicate name and respond appropriately
            System.out.println("Name conflict detected: " + e.getMessage());
        }
```

**Waarom dit belangrijk is:**  
Excel staat niet toe dat een tabel en een named range dezelfde identifier delen. Het vroeg detecteren van het conflict voorkomt corrupte werkmappen en maakt debuggen eenvoudiger.

## Stap 4: Detecteer duplicate name en los het op

Wanneer de uitzondering wordt opgevangen, kun je de tabel hernoemen of de conflicterende named range verwijderen. Hieronder staat een eenvoudige oplossingsstrategie die de tabel een suffix geeft.

```java
            // Resolve the conflict by appending a numeric suffix
            String baseName = "MyRange";
            int suffix = 1;
            String newName;
            do {
                newName = baseName + "_" + suffix;
                suffix++;
            } while (workbook.getNames().get(newName) != null);

            table.setName(newName);
            System.out.println("Table renamed to: " + newName);
        }

        // Save the workbook to verify the result
        workbook.save("NamedRangeDemo.xlsx");
    }
}
```

**Belangrijke punten van de oplossing:**

- **detect duplicate name** – het `catch`‑blok bevestigt het conflict.
- De lus controleert de naamcollectie van de werkmap om te verzekeren dat de nieuwe identifier uniek is.
- Ten slotte wordt de werkmap opgeslagen zodat je deze in Excel kunt openen en kunt verifiëren dat de tabel een aparte naam heeft terwijl de oorspronkelijke named range intact blijft.

## Volledig, uitvoerbaar voorbeeld

Alle onderdelen samenvoegend ziet het volledige programma er als volgt uit:

```java
import com.aspose.cells.*;

public class NamedRangeDemo {
    public static void main(String[] args) throws Exception {
        // Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Add a named range called "MyRange" covering A1:C5
        workbook.getNames().add("MyRange", "'Sheet1'!$A$1:$C$5");

        // Create an Excel table that occupies the same cells
        ListObject table = sheet.getListObjects().add(0, 0, 4, 2, true);

        try {
            // Try to set the table name to the same identifier
            table.setName("MyRange");
        } catch (Exception e) {
            // Detect duplicate name and resolve it
            System.out.println("Name conflict detected: " + e.getMessage());

            String baseName = "MyRange";
            int suffix = 1;
            String newName;
            do {
                newName = baseName + "_" + suffix;
                suffix++;
            } while (workbook.getNames().get(newName) != null);

            table.setName(newName);
            System.out.println("Table renamed to: " + newName);
        }

        // Save the file for inspection
        workbook.save("NamedRangeDemo.xlsx");
    }
}
```

**Verwachte output wanneer je het programma uitvoert:**

```
Name conflict detected: A name with the specified identifier already exists.
Table renamed to: MyRange_1
```

Het openen van `NamedRangeDemo.xlsx` in Excel toont:

- Een named range **MyRange** dat verwijst naar cellen A1:C5.
- Een tabel genaamd **MyRange_1** die dezelfde cellen beslaat.
- Geen naamfout wanneer je formules toevoegt die `MyRange` refereren.

## Veelvoorkomende valkuilen en best practices

- **Herbruik geen identifiers**: Controleer altijd of een naam nog niet bestaat voordat je deze aan een tabel toewijst.  
- **Geef de voorkeur aan expliciete controles**: `workbook.getNames().get("Name")` retourneert `null` als de naam beschikbaar is, wat veiliger is dan een algemene uitzondering opvangen.  
- **Houd naamgevingsconventies consistent**: Het gebruik van een prefix zoals `tbl_` voor tabellen en `rng_` voor bereiken vermindert de kans op conflicten.  
- **Versie‑compatibiliteit**: De code werkt met Aspose.Cells 23.9 en later; eerdere versies kunnen andere exceptiemeldingen hebben.

## Conclusie

Je weet nu hoe je **create a named range**, **add named range**, **create Excel table**, **set table name**, en **detect duplicate name** conflicten kunt behandelen met Aspose.Cells for Java. Door naamconflicten proactief af te handelen, houd je je werkmappen schoon en je automatiseringsscripts robuust.

**Volgende stappen**

- Verken de **set table name**‑API verder om stijlopties toe te passen.  
- Gebruik het **detect duplicate name**‑patroon bij het programmatisch genereren van meerdere tabellen.  
- Combineer named ranges met formules of gegevensvalidatie voor dynamische rapportage.

Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Maak stijl named range Excel Aspose Cells Java](/cells/hindi/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)
- [Maak stijl named range Excel Aspose Cells Java](/cells/german/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)
- [Maak stijl named range Excel Aspose Cells Java](/cells/french/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}