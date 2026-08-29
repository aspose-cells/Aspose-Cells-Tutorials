---
category: general
date: 2026-08-20
description: Naučte se, jak s Aspose.Cells smazat řádek tabulky v Excelu při zachování
  integrity tabulky. Tento krok za krokem průvodce ukazuje bezpečné mazání řádků a
  zpracování chyb.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to delete excel table row
- delete rows aspose.cells
language: cs
lastmod: 2026-08-20
og_description: Jak smazat řádek tabulky v Excelu pomocí Aspose.Cells. Postupujte
  podle tohoto kompletního návodu, jak bezpečně odstranit řádky a řešit případné chyby.
og_image_alt: Screenshot of Java code deleting a row from an Excel table with Aspose.Cells
og_title: Jak smazat řádek tabulky v Excelu pomocí Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to delete Excel table row with Aspose.Cells while preserving
    table integrity. This step‑by‑step guide shows safe row deletion and error handling.
  headline: How to delete Excel table row safely using Aspose.Cells
  type: TechArticle
- description: Learn how to delete Excel table row with Aspose.Cells while preserving
    table integrity. This step‑by‑step guide shows safe row deletion and error handling.
  name: How to delete Excel table row safely using Aspose.Cells
  steps:
  - name: Why each step matters
    text: 1. **Load the workbook** – `Workbook` reads the `.xlsx` file into memory,
      giving you programmatic access to its sheets, tables, and cells. 2. **Access
      the worksheet** – `getWorksheets().get(0)` selects the first sheet, which is
      where the target table lives. 3. **Retrieve the table** – In Excel, a st
  - name: Expected console output
    text: '*If the deletion is allowed*:'
  - name: Deleting multiple rows
    text: 'To delete three consecutive rows starting at the second data row:'
  - name: Deleting the last data row
    text: 'Attempting to delete the final data row will also raise an exception because
      a table cannot exist without at least one data row. Handle it the same way:'
  type: HowTo
tags:
- Aspose.Cells
- Excel
- Java
title: Jak bezpečně smazat řádek tabulky v Excelu pomocí Aspose.Cells
url: /cs/java/tables-structured-references/how-to-delete-excel-table-row-safely-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak bezpečně smazat řádek tabulky Excel pomocí Aspose.Cells

Pokud potřebujete **how to delete Excel table row** bez poškození struktury tabulky, tento průvodce ukazuje spolehlivý přístup s Aspose.Cells pro Java. Uvidíte kompletní, spustitelný příklad, který zachytí výjimku bezpečnosti a uloží sešit po pokusu o smazání.

Tutoriál také pokrývá **delete rows aspose.cells** způsobem, který funguje pro jednorázové i vícenásobné řádky, takže můžete kód přizpůsobit svým projektům.

## Co tento tutoriál pokrývá

* Načtení existujícího sešitu, který obsahuje tabulku Excel (ListObject).  
* Přístup k prvnímu listu a první tabulce na tomto listu.  
* Pokus o smazání řádku, zatímco Aspose.Cells ověřuje operaci.  
* Zpracování výjimky, kterou Aspose.Cells vyhodí, pokud by smazání poškodilo tabulku.  
* Uložení sešitu po pokusu o bezpečné smazání.  

Požadavky: Java 17 nebo novější, Aspose.Cells pro Java (verze 23.12 nebo novější) a základní znalost syntaxe Java. Žádné další knihovny nejsou vyžadovány.

---

## Jak smazat řádek tabulky Excel pomocí Aspose.Cells

Níže je kompletní, samostatný program. Každý krok je vysvětlen a kód lze zkopírovat do Java projektu a okamžitě spustit.

```java
import com.aspose.cells.*;

public class SafeTableDeletion {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the workbook containing the table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Retrieve the first table (ListObject) on the worksheet
        ListObject table = worksheet.getListObjects().get(0);

        // Step 4: Attempt to delete a row that would break the table structure
        //         The operation is wrapped in a try‑catch to demonstrate the safety check
        try {
            // Row index is zero‑based; this tries to delete the third data row.
            table.deleteRows(2, 1);
            System.out.println("Row deleted successfully.");
        } catch (Exception ex) {
            // Aspose.Cells throws an exception if the deletion would leave the table invalid.
            System.out.println("Partial‑deletion prevented: " + ex.getMessage());
        }

        // Step 5: Save the workbook after the safe‑deletion attempt
        workbook.save("YOUR_DIRECTORY/TableSafeDelete.xlsx");
    }
}
```

### Proč je každý krok důležitý

1. **Load the workbook** – `Workbook` načte soubor `.xlsx` do paměti a poskytne vám programový přístup k listům, tabulkám a buňkám.  
2. **Access the worksheet** – `getWorksheets().get(0)` vybere první list, kde se nachází cílová tabulka.  
3. **Retrieve the table** – V Excelu je strukturovaná tabulka reprezentována objektem `ListObject`. Tento objekt poskytuje metody jako `deleteRows`.  
4. **Safe deletion** – `deleteRows` kontroluje integritu tabulky. Pokud by odstranění řádku poškodilo tabulku (např. zanechalo hlavičku bez dat), Aspose.Cells vyhodí výjimku. Blok `try‑catch` demonstruje bezpečnostní zpracování **delete rows aspose.cells**.  
5. **Save the workbook** – `workbook.save` zapíše změny zpět na disk a vytvoří nový soubor, který odráží pokus o smazání.  

### Očekávaný výstup v konzoli

*Pokud je smazání povoleno*:

```
Row deleted successfully.
```

*Pokud by smazání poškodilo tabulku* (běžné, když tabulka má jen jeden datový řádek):

```
Partial‑deletion prevented: Deleting the specified rows would break the table structure.
```

---

## Načtení sešitu (krok 1)

Konstruktor `Workbook` přijímá cestu k souboru. Ujistěte se, že cesta ukazuje na existující soubor Excel, který obsahuje alespoň jednu tabulku. Pokud soubor chybí, Aspose.Cells vyhodí `FileNotFoundException`, kterou můžete zachytit podobně jako výjimku při mazání tabulky.

```java
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

**Tip:** Používejte během vývoje absolutní cestu, abyste se vyhnuli záměně relativních cest, zejména při spouštění z IDE.

---

## Přístup k listu (krok 2)

Sešit může obsahovat mnoho listů. Příklad používá první (`index 0`). Pokud potřebujete konkrétní list podle názvu, nahraďte volání tímto:

```java
Worksheet worksheet = workbook.getWorksheets().get("SheetName");
```

---

## Získání tabulky (krok 3)

`ListObject` představuje tabulku Excel. Pokud list nemá žádné tabulky, `getListObjects().size()` vrátí `0` a volání `get(0)` by vyvolalo `IndexOutOfBoundsException`. Obranná kontrola vypadá takto:

```java
if (worksheet.getListObjects().getCount() == 0) {
    System.out.println("No tables found on the worksheet.");
    return;
}
ListObject table = worksheet.getListObjects().get(0);
```

---

## Mazání řádků pomocí Aspose.Cells (krok 4)

Jádrem **how to delete Excel table row** je metoda `deleteRows`:

```java
table.deleteRows(startIndex, count);
```

* `startIndex` – nulový index (zero‑based) prvního řádku k smazání v datovém rozsahu tabulky.  
* `count` – počet řádků k odstranění.

Aspose.Cells ověřuje operaci vůči hlavičce tabulky, celkovému počtu řádků a jakýmkoli vzorcům, které odkazují na tabulku. Pokud by smazání zanechalo tabulku v neplatném stavu, je vyhozena výjimka, proto je vzor `try‑catch` nezbytný.

### Mazání více řádků

Pro smazání tří po sobě jdoucích řádků počínaje druhým datovým řádkem:

```java
table.deleteRows(1, 3);
```

### Mazání posledního datového řádku

Pokud se pokusíte smazat poslední datový řádek, také dojde k výjimce, protože tabulka nemůže existovat bez alespoň jednoho datového řádku. Zacházejte s tím stejným způsobem:

```java
try {
    table.deleteRows(table.getDataRows().getCount() - 1, 1);
} catch (Exception ex) {
    System.out.println("Cannot delete the last row: " + ex.getMessage());
}
```

---

## Uložení sešitu (krok 5)

Po pokusu o bezpečné smazání jsou změny snadno uloženy:

```java
workbook.save("YOUR_DIRECTORY/TableSafeDelete.xlsx");
```

Můžete zvolit libovolný podporovaný formát (`.xlsx`, `.xls`, `.csv`, atd.) změnou přípony souboru.

---

## Běžné úskalí a jak se jim vyhnout

| Problém | Proč k tomu dochází | Řešení |
|---------|----------------------|--------|
| **Žádná tabulka na listu** | `getListObjects().get(0)` vyvolá `IndexOutOfBoundsException`. | Zkontrolujte `getCount()` před přístupem. |
| **Špatný index řádku** | `deleteRows` používá nulové indexování relativně k tabulce, ne k listu. | Ověřte index výpisem `table.getDataRows().getCount()`. |
| **Mazání jediného datového řádku** | Aspose.Cells chrání integritu tabulky a vyhodí výjimku. | Buď nejprve přidejte zástupný řádek, nebo odstraňte celou tabulku pomocí `table.remove()`. |
| **Problémy s cestou k souboru** | Relativní cesty se mohou rozpoznat jako pracovní adresář IDE, což způsobí `FileNotFoundException`. | Používejte absolutní cesty nebo nastavte pracovní adresář IDE. |

---

## Přehled kompletního funkčního příkladu

Níže je celý program znovu pro rychlé zkopírování. Obsahuje obranné kontroly zmíněné výše.

```java
import com.aspose.cells.*;

public class SafeTableDeletion {
    public static void main(String[] args) throws Exception {

        // Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Ensure a table exists
        if (worksheet.getListObjects().getCount() == 0) {
            System.out.println("No tables found on the worksheet.");
            return;
        }

        // Retrieve the first table
        ListObject table = worksheet.getListObjects().get(0);

        // Attempt safe deletion
        try {
            table.deleteRows(2, 1); // zero‑based index
            System.out.println("Row deleted successfully.");
        } catch (Exception ex) {
            System.out.println("Partial‑deletion prevented: " + ex.getMessage());
        }

        // Save the result
        workbook.save("YOUR_DIRECTORY/TableSafeDelete.xlsx");
    }
}
```

Spuštěním tohoto programu se vytiskne buď zpráva o úspěchu, nebo ochranná zpráva o výjimce a poté se zapíše `TableSafeDelete.xlsx` do určené složky.

---

## Závěr

Nyní víte **how to delete Excel table row** bezpečně pomocí Aspose.Cells pro Java. Průvodce ukázal načtení sešitu, vyhledání tabulky, provedení chráněného smazání řádku, zpracování výjimky **delete rows aspose.cells** a uložení aktualizovaného souboru.

Odtud můžete:

* Smazat více řádků jedním voláním.  
* Iterovat přes seznam indexů řádků a provádět hromadné mazání.  
* Nahradit `try‑catch` vlastním logováním pro produkční prostředí.  

Experimentujte s různými rozvrženími tabulek, vzorci a pravidly pro ověřování dat, abyste viděli, jak Aspose.Cells vynucuje integritu. Když potřebujete programově manipulovat se soubory Excel, vzor zde ukázaný poskytuje solidní, chybově‑vědomý základ.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy ve vlastních projektech.

- [Jak vkládat a mazat řádky v Excelu pomocí Aspose.Cells pro .NET: Kompletní průvodce](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Jak smazat prázdné řádky v Excelu pomocí Aspose.Cells .NET pro čištění dat](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)
- [Jak smazat sloupec v Excelu pomocí Aspose.Cells .NET v C# – Kompletní průvodce](/cells/english/net/worksheet-management/delete-column-aspose-cells-dotnet-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}