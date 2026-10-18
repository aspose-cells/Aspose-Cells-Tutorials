---
category: general
date: 2026-06-18
description: Rijen verwijderen in een werkblad met Aspose.Cells voor Java. Leer hoe
  je de tabelkoprij kunt verwijderen en rijen uit een Excel‑tabel veilig kunt verwijderen.
draft: false
keywords:
- delete rows in worksheet
- remove table header row
- remove rows from excel table
language: nl
og_description: Verwijder rijen in een werkblad met Aspose.Cells voor Java. Deze gids
  laat zien hoe je de tabelkoprij verwijdert en rijen uit een Excel‑tabel efficiënt
  verwijdert.
og_title: Rijen verwijderen in werkblad met Java – Stap voor stap
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Delete rows in worksheet using Aspose.Cells for Java. Learn how to
    remove table header row and delete rows from Excel table safely.
  headline: Delete rows in worksheet with Java – Complete Guide
  type: TechArticle
- description: Delete rows in worksheet using Aspose.Cells for Java. Learn how to
    remove table header row and delete rows from Excel table safely.
  name: Delete rows in worksheet with Java – Complete Guide
  steps:
  - name: '`table.unlist()` strips the table metadata, turning the block into ordinary
      cells.'
    text: '`table.unlist()` strips the table metadata, turning the block into ordinary
      cells.'
  - name: With the header now a regular row, `deleteRows(0, …)` works without complaints.
    text: With the header now a regular row, `deleteRows(0, …)` works without complaints.
  - name: If you still need a table after the cleanup, you can recreate it using `ws.getTables().add(...)`.
    text: If you still need a table after the cleanup, you can recreate it using `ws.getTables().add(...)`.
  - name: Loads a workbook.
    text: Loads a workbook.
  - name: Checks if the first table exists.
    text: Checks if the first table exists.
  - name: Deletes **all** rows *including* the header safely.
    text: Deletes **all** rows *including* the header safely.
  - name: Re‑creates the table from the remaining rows (if any).
    text: Re‑creates the table from the remaining rows (if any).
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Worksheet
title: Rijen verwijderen in werkblad met Java – Complete gids
url: /nl/java/worksheet-management/delete-rows-in-worksheet-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rijen verwijderen in werkblad – Complete Java-tutorial

Heb je ooit moeten **rijen verwijderen in een werkblad** maar liep je tegen een muur omdat de tabelkop weigert te bewegen? Je bent niet de enige. In veel Excel‑automatiseringsscenario's behoort de eerste rij tot een gestructureerde tabel, en een naïeve aanroep van `deleteRows` veroorzaakt een uitzondering of laat de kop simpelweg onaangeroerd.

In deze tutorial lopen we precies uit hoe je *de tabelkoprij kunt verwijderen* en *rijen uit een Excel‑tabel kunt verwijderen* zonder het blad te breken. Aan het einde heb je een nette, uitvoerbare code‑fragment dat werkt met de nieuwste Aspose.Cells for Java (v23.10 op het moment van schrijven).

We behandelen de vereisten, drie praktische benaderingen en een reeks tips die je wilt opslaan. Geen poespas—gewoon het soort antwoord dat je van een ervaren ontwikkelaar bij een kop koffie zou verwachten.

## Vereisten

- Java 17 of nieuwer (de code compileert met oudere versies, maar 17 wordt aanbevolen).
- Aspose.Cells for Java 23.10 of later toegevoegd aan je Maven `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
</dependency>
```

- Een voorbeeld‑Excel‑bestand (`Sample.xlsx`) dat een tabel bevat op het eerste werkblad. De kop van de tabel staat in rij 0 (Excel‑rij 1).

Dat is alles. Klaar? Laten we beginnen.

## Rijen verwijderen in werkblad – waarom de koprij belangrijk is

Wanneer je aanroept:

```java
ws.getCells().deleteRows(0, 2, true);
```

Aspose.Cells weigert rij 0 te verwijderen omdat deze deel uitmaakt van een **tabel**. De API beschermt de integriteit van de tabel; het verwijderen van de kop zou de gegevensrijen weglaten. De uitzondering die je ziet is iets als *“The specified row belongs to a table and cannot be deleted.”*

Dit beveiligingsmechanisme begrijpen is de eerste stap naar een succesvolle oplossing.

## Benadering 1 – Rijen **onder** de kop verwijderen (meest gebruikelijk)

Als je simpelweg alle gegevens wilt wissen terwijl je de tabelstructuur behoudt, begin dan met verwijderen vanaf de rij **na** de kop.

```java
import com.aspose.cells.*;

public class DeleteRowsBelowHeader {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // Determine how many data rows the table currently has
        Table table = ws.getTables().get(0);
        int dataRowCount = table.getDataRange().getRowCount();

        // Delete all data rows (keep header)
        // startRow = 1 because row index 0 is the header
        ws.getCells().deleteRows(1, dataRowCount, true);

        // Save the result
        wb.save("Result_DeleteRowsBelowHeader.xlsx");
    }
}
```

**Waarom dit werkt:** `deleteRows` krijgt een start‑index van 1, zodat de kop onaangeroerd blijft. De `true`‑vlag verschuift de resterende rijen omhoog, waardoor eventuele formules die ernaar verwijzen behouden blijven. Na het uitvoeren van de code zie je een nette tabel met alleen de kopregel over.

### Snelle tip

Als je een *specifiek* bereik van rijen wilt verwijderen (bijv. rijen 5‑10), pas dan eenvoudig de start‑index en het aantal aan. De tabel wordt automatisch aangepast aan het nieuwe gegevensbereik.

## Benadering 2 – Converteer de tabel naar een gewoon bereik, en verwijder dan

Soms moet je echt **de tabelkoprij verwijderen** en de gegevens behandelen als een gewoon bereik. De truc is om eerst de tabel te *unlist*.

```java
import com.aspose.cells.*;

public class RemoveHeaderAndDeleteRows {
    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Table table = ws.getTables().get(0);

        // 1️⃣ Unlist the table – it becomes a normal range
        table.unlist();

        // 2️⃣ Now you can delete the header row (row 0) and any other rows
        // Delete header + first two data rows (total 3 rows)
        ws.getCells().deleteRows(0, 3, true);

        // 3️⃣ (Optional) Re‑create a table from the remaining data
        // Assuming you still have data starting at row 0
        int firstDataRow = 0;
        int lastDataRow = ws.getCells().getMaxDataRow();
        int firstCol = ws.getCells().getMaxDataColumn();
        int lastCol = ws.getCells().getMaxDataColumn();

        String range = new CellArea(firstDataRow, 0, lastDataRow, firstCol).format();
        ws.getTables().add(range, true);
        ws.getTables().get(0).setName("NewTable");

        wb.save("Result_RemoveHeaderAndDeleteRows.xlsx");
    }
}
```

**Uitleg:**  

1. `table.unlist()` verwijdert de tabel‑metadata, waardoor het blok gewone cellen wordt.  
2. Nu de kop een gewone rij is, werkt `deleteRows(0, …)` zonder klachten.  
3. Als je na de opschoning toch een tabel nodig hebt, kun je deze opnieuw aanmaken met `ws.getTables().add(...)`.

Deze benadering is handig wanneer de kop zelf onjuist is of je de volledige tabeldefinitie wilt vervangen.

## Benadering 3 – Gebruik de Table‑API om specifieke rijen te verwijderen

Aspose.Cells biedt ook een **tabel‑niveau** methode om rijen te verwijderen, die automatisch de kopbescherming afhandelt.

```java
import com.aspose.cells.*;

public class DeleteRowsViaTableAPI {
    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Table table = ws.getTables().get(0);

        // Delete the first two data rows (index 0 = first data row, not the header)
        // The Table API counts only data rows, so we don't touch the header.
        table.deleteRows(0, 2);

        wb.save("Result_DeleteRowsViaTableAPI.xlsx");
    }
}
```

**Waarom je dit zou kiezen:** Het is de meest *semantische* manier—je vertelt de tabel: “verwijder mijn gegevensrijen.” De API werkt het bereik van de tabel automatisch bij, en je hoeft nooit te rommelen met ruwe rij‑indexen.

## Randgevallen & Veelvoorkomende valkuilen

| Situatie | Waar op te letten | Aanbevolen oplossing |
|-----------|------------------|-----------------|
| **Multiple tables on the same sheet** | `ws.getTables().get(0)` kan de verkeerde tabel selecteren. | Use `ws.getTables().stream().filter(t -> t.getName().equals("MyTable")).findFirst().orElse(null)` |
| **Merged cells in the header** | Rijen verwijderen kan samengevoegde gebieden splitsen, wat layout‑fouten veroorzaakt. | Unmerge before deletion: `ws.getCells().get("A1").getMergedRange().unmerge();` |
| **Formulas referencing the header** | Het verwijderen van de kop breekt externe verwijzingen. | Update formulas after deletion or keep a placeholder row. |
| **Large worksheets (>10 000 rows)** | `deleteRows` kan trager zijn door interne verschuivingen. | Use `ws.getCells().clearRows(start, count)` if you don’t need to shift. |

## Volledig werkend voorbeeld – Combineer het beste van alle werelden

Hieronder staat een zelfstandige programma dat:

1. Laadt een werkmap.
2. Controleert of de eerste tabel bestaat.
3. Verwijdert **alle** rijen *inclusief* de kop veilig.
4. Maakt de tabel opnieuw aan vanuit de overgebleven rijen (indien aanwezig).

```java
import com.aspose.cells.*;

public class DeleteRowsInWorksheetFullDemo {
    public static void main(String[] args) throws Exception {
        // ① Load the workbook
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // ② Guard: make sure a table is present
        if (ws.getTables().getCount() == 0) {
            System.out.println("No tables found – nothing to delete.");
            return;
        }

        // ③ Grab the first table (adjust if you have a named table)
        Table table = ws.getTables().get(0);

        // ④ Unlist so we can delete the header row
        table.unlist();

        // ⑤ Determine total rows to delete (header + data)
        int totalRows = table.getRange().getRowCount(); // includes header
        ws.getCells().deleteRows(0, totalRows, true);

        // ⑥ If there are still rows left, rebuild the table
        int maxRow = ws.getCells().getMaxDataRow();
        int maxCol = ws.getCells().getMaxDataColumn();

        if (maxRow >= 0) { // there is at least one row left
            String newRange = new CellArea(0, 0, maxRow, maxCol).format();
            Table newTable = ws.getTables().add(newRange, true);
            newTable.setName("RebuiltTable");
        }

        // ⑦ Save the result
        wb.save("Result_DeleteRowsInWorksheetFullDemo.xlsx");
        System.out.println("Rows deleted and table rebuilt successfully.");
    }
}
```

**Verwachte output:** Na uitvoering vind je `Result_DeleteRowsInWorksheetFullDemo.xlsx` met de oorspronkelijke tabel verwijderd, en—als er gegevens overbleven—een nieuwe tabel genaamd `RebuiltTable`. De console geeft een beknopt succesbericht weer.

## Visuele samenvatting

![Excel-werkblad vóór en na het verwijderen van rijen](https://example.com/images/delete-rows-workbook.png "Voor en na het verwijderen van rijen in werkblad")

*Alt‑tekst:* “Voor en na het verwijderen van rijen in werkblad – kop verwijderd, gegevensrijen gewist.”

## Conclusie

We hebben drie betrouwbare manieren behandeld om **rijen te verwijderen in een werkblad** terwijl we het lastige scenario *tabelkoprij verwijderen* afhandelen en veilig **rijen uit een Excel‑tabel verwijderen**. Of je nu de voorkeur geeft aan ruwe celoperaties, de Table‑API, of een volledige unlist‑relist‑cyclus, de bovenstaande code‑fragmenten zijn klaar om in je project te gebruiken.

Volgende stappen? Probeer deze technieken te combineren met voorwaardelijke logica—verwijder rijen alleen wanneer een bepaalde kolom “Inactive” bevat, of verwerk meerdere in batches

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Efficiënt rijenbeheer in Excel met Aspose.Cells for Java: rijen invoegen en verwijderen](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)
- [Hoe lege rijen uit Excel‑bestanden te verwijderen met Aspose.Cells for Java](/cells/english/java/data-manipulation/delete-blank-rows-aspose-cells-java/)
- [Hoe rijen te verwijderen in Excel met Aspose.Cells for Java | Gids & Tutorial](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}