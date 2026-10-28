---
category: general
date: 2026-06-18
description: Odstraňte řádky v listu pomocí Aspose.Cells pro Javu. Naučte se, jak
  bezpečně odstranit řádek záhlaví tabulky a smazat řádky z Excelové tabulky.
draft: false
keywords:
- delete rows in worksheet
- remove table header row
- remove rows from excel table
language: cs
og_description: Smazání řádků v listu pomocí Aspose.Cells pro Java. Tento průvodce
  ukazuje, jak efektivně odstranit řádek záhlaví tabulky a smazat řádky z Excelové
  tabulky.
og_title: Smazat řádky v listu pomocí Javy – krok za krokem
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
title: Smazání řádků v listu pomocí Javy – kompletní průvodce
url: /cs/java/worksheet-management/delete-rows-in-worksheet-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Delete rows in worksheet – Kompletní Java tutoriál

Už jste někdy potřebovali **delete rows in worksheet**, ale narazili na překážku, protože záhlaví tabulky odmítá ustoupit? Nejste jediní. V mnoha scénářích automatizace Excelu první řádek patří strukturované tabulce a naivní volání `deleteRows` vyvolá výjimku nebo jednoduše ponechá záhlaví nedotčené.  

V tomto tutoriálu vás provedeme přesně tím, jak *remove table header row* a *remove rows from Excel table* bez poškození listu. Na konci budete mít čistý, spustitelný úryvek, který funguje s nejnovější verzí Aspose.Cells for Java (v23.10 v době psaní).  

Probereme předpoklady, tři praktické přístupy a několik tipů, které si budete chtít uložit. Žádné zbytečnosti—pouze odpověď, jakou byste očekávali od zkušeného vývojáře u šálku kávy.

## Požadavky

- Java 17 nebo novější (kód se kompiluje i se staršími verzemi, ale 17 je doporučená).
- Aspose.Cells for Java 23.10 nebo novější přidaný do vašeho Maven `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
</dependency>
```

- Ukázkový soubor Excel (`Sample.xlsx`), který obsahuje tabulku na prvním listu. Záhlaví tabulky je v řádku 0 (Excel řádek 1).

To je vše. Připravení? Pojďme na to.

## Delete rows in worksheet – proč je řádek záhlaví důležitý

When you call:

```java
ws.getCells().deleteRows(0, 2, true);
```

Aspose.Cells odmítá smazat řádek 0, protože je součástí **table**. API chrání integritu tabulky; odstranění záhlaví by ponechalo datové řádky osiřelé. Výjimka, kterou uvidíte, bude něco jako *„The specified row belongs to a table and cannot be deleted.“*  

Pochopení tohoto omezení je prvním krokem k úspěšnému řešení.

## Přístup 1 – Delete rows **below** the header (nejčastější)

Pokud chcete jednoduše vymazat data a zachovat strukturu tabulky, začněte mazat od řádku **po** záhlaví.

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

**Proč to funguje:** `deleteRows` dostane počáteční index 1, takže záhlaví zůstane nedotčeno. Příznak `true` posune zbývající řádky nahoru a zachová všechny vzorce, které na ně odkazují. Po spuštění kódu uvidíte čistou tabulku pouze se zbylým řádkem záhlaví.

### Rychlý tip

Pokud potřebujete smazat *specifický* rozsah řádků (např. řádky 5‑10), stačí upravit počáteční index a počet podle toho. Tabulka se automaticky přizpůsobí novému datovému rozsahu.

## Přístup 2 – Convert the table to a plain range, then delete

Někdy skutečně potřebujete **remove table header row** a zacházet s daty jako s běžným rozsahem. Trik je nejprve *unlist* tabulku.

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

**Vysvětlení:**  

1. `table.unlist()` odebere metadata tabulky a převádí blok na běžné buňky.  
2. S tím, že je záhlaví nyní běžným řádkem, `deleteRows(0, …)` funguje bez problémů.  
3. Pokud po úklidu stále potřebujete tabulku, můžete ji znovu vytvořit pomocí `ws.getTables().add(...)`.

Tento přístup je užitečný, když je samotné záhlaví špatné nebo chcete nahradit celou definici tabulky.

## Přístup 3 – Use the Table API to delete specific rows

Aspose.Cells také nabízí **table‑level** metodu pro mazání řádků, která automaticky řeší ochranu záhlaví.

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

**Proč byste si mohli vybrat tuto možnost:** Je to nejvíce *semantic* způsob—říkáte tabulce: „odstraň moje datové řádky.“ API automaticky aktualizuje rozsah tabulky a nikdy nemusíte manipulovat s čistými indexy řádků.

## Okrajové případy a běžné úskalí

| Situace | Na co si dát pozor | Doporučené řešení |
|-----------|------------------|-----------------|
| **Více tabulek na stejném listu** | `ws.getTables().get(0)` může cílit na špatnou tabulku. | Použijte `ws.getTables().stream().filter(t -> t.getName().equals("MyTable")).findFirst().orElse(null)` |
| **Sloučené buňky v záhlaví** | Mazání řádků může rozdělit sloučené oblasti, což způsobí vizuální chyby. | Odstraňte sloučení před mazáním: `ws.getCells().get("A1").getMergedRange().unmerge();` |
| **Vzorce odkazující na záhlaví** | Odstranění záhlaví rozbije externí odkazy. | Aktualizujte vzorce po smazání nebo ponechte zástupný řádek. |
| **Velké listy (>10 000 řádků)** | `deleteRows` může být pomalejší kvůli internímu posunu. | Použijte `ws.getCells().clearRows(start, count)`, pokud nepotřebujete posun. |

## Kompletní funkční příklad – kombinace nejlepších přístupů

Níže je samostatný program, který:

1. Načte sešit.
2. Zkontroluje, zda první tabulka existuje.
3. Bezpečně smaže **všechny** řádky *včetně* záhlaví.
4. Znovu vytvoří tabulku ze zbývajících řádků (pokud nějaké jsou).

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

**Očekávaný výstup:** Po spuštění najdete `Result_DeleteRowsInWorksheetFullDemo.xlsx` s původní tabulkou odstraněnou a—pokud nějaká data přežily—novou tabulku nazvanou `RebuiltTable`. Konzole vypíše stručnou zprávu o úspěchu.

## Vizualizovaný přehled

![Excel list před a po smazání řádků](https://example.com/images/delete-rows-workbook.png "Před a po smazání řádků v listu")

*Alt text:* „Před a po smazání řádků v listu – záhlaví odstraněno, datové řádky vymazány.“

## Závěr

Představili jsme tři spolehlivé způsoby, jak **delete rows in worksheet**, přičemž řešíme obtížný scénář *remove table header row* a bezpečně **remove rows from Excel table**. Ať už dáváte přednost přímým operacím s buňkami, Table API, nebo kompletnímu cyklu unlist‑relist, výše uvedené úryvky kódu jsou připraveny k nasazení ve vašem projektu.  

Další kroky? Zkuste kombinovat tyto techniky s podmíněnou logikou—mazat řádky jen tehdy, když určitý sloupec obsahuje „Inactive“, nebo hromadně zpracovávat více

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která navazují na techniky předvedené v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Efektivní správa řádků v Excelu pomocí Aspose.Cells for Java: Vkládání a mazání řádků](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)
- [Jak odstranit prázdné řádky z Excel souborů pomocí Aspose.Cells for Java](/cells/english/java/data-manipulation/delete-blank-rows-aspose-cells-java/)
- [Jak smazat řádky v Excelu pomocí Aspose.Cells for Java | Průvodce a tutoriál](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}