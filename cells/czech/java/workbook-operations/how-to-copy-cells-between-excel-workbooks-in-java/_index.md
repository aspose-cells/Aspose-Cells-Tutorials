---
category: general
date: 2026-11-16
description: Jak kopírovat buňky mezi sešity Excel v Javě – načíst sešit, zkopírovat
  oblast mezi sešity (včetně kontingenční tabulky) a uložit soubor sešitu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy cells
- copy range between workbooks
- copy pivot table workbook
- save workbook file
- load excel workbook java
language: cs
lastmod: 2026-11-16
og_description: Jak kopírovat buňky mezi sešity Excel v Javě. Naučte se načíst sešit
  Excel, zkopírovat oblast (včetně kontingenční tabulky) mezi sešity a uložit soubor
  sešitu.
og_image_alt: Screenshot of Java code copying a cell range from one Excel workbook
  to another
og_title: Jak kopírovat buňky mezi sešity Excel v Javě – kompletní průvodce
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
title: Jak kopírovat buňky mezi sešity Excelu v Javě
url: /cs/java/workbook-operations/how-to-copy-cells-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak kopírovat buňky mezi sešity Excel v Javě

Pokud potřebujete **kopírovat buňky** z jednoho sešitu Excel do druhého pomocí Javy, tento průvodce vám ukáže spolehlivý způsob, jak to provést. Naučíte se, jak **načíst Excel workbook Java**, zkopírovat oblast, která může obsahovat kontingenční tabulku, a nakonec **uložit soubor sešitu** s zkopírovanými daty.

Tento tutoriál pokrývá:

* Načtení zdrojového sešitu a výběr listu.  
* Definování přesné oblasti, kterou chcete přesunout (včetně kontingenční tabulky).  
* Vytvoření cílového sešitu a kopírování oblasti.  
* Uložení cílového souboru.  

Příklad používá knihovnu Aspose.Cells for Java, která pracuje se soubory Excel bez nutnosti Microsoft Office. Kód běží na Java 8+ a v jakémkoli moderním IDE (IntelliJ IDEA, Eclipse, VS Code, atd.).

---

## Požadavky

Než začnete, ujistěte se, že máte:

| Požadavek | Důvod |
|-------------|--------|
| Java Development Kit (JDK) 8 nebo novější | Vyžadováno pro kompilaci a spuštění kódu. |
| Maven nebo Gradle nástroj pro sestavení | Zjednodušuje přidání závislosti Aspose.Cells. |
| Aspose.Cells for Java library (latest version) | Poskytuje třídy `Workbook`, `Worksheet` a `Range` použité v příkladu. |
| Two Excel files (`source.xlsx` a prázdná složka pro `dest.xlsx`) | Zdrojový soubor musí obsahovat data a volitelně kontingenční tabulku, kterou chcete kopírovat. |

Přidejte závislost Aspose.Cells do vašeho `pom.xml` (Maven) nebo `build.gradle` (Gradle). Příklad pro Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

---

## Jak kopírovat buňky pomocí Aspose.Cells

Následující kroky vás provedou celým procesem. Každý krok obsahuje Java kód, vysvětlení **proč** je krok důležitý, a tip, jak se vyhnout běžným úskalím.

### Krok 1: Načíst zdrojový sešit

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source Excel file (replace with your actual path)
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Get the first worksheet (index 0)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Proč?**  
`Workbook` představuje celý soubor Excel. Načtením získáte přístup ke všem listům, buňkám a objektům, jako jsou kontingenční tabulky. Použití prvního listu je běžné, ale můžete vybrat libovolný list podle názvu (`srcWb.getWorksheets().get("Sheet2")`).

**Tip:**  
Pokud je zdrojový soubor velký, zvažte načtení v *paměťově‑efektivním* režimu: `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setMemorySetting(MemorySetting.MEMORY_PREFERENCE); }});`

### Krok 2: Definovat oblast, která zahrnuje kontingenční tabulku

```java
        // Define the cell range that you want to copy.
        // Adjust "A1:G20" to match the area that contains your data/pivot table.
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Proč?**  
Objekt `Range` abstrahuje obdélníkový blok buněk. Zadáním `"A1:G20"` řeknete Aspose.Cells přesně, které buňky – včetně vložené kontingenční tabulky – mají být zkopírovány. Knihovna automaticky kopíruje podkladová data, styly i definice kontingenčních tabulek.

**Speciální případ:**  
Pokud kontingenční tabulka zasahuje mimo definovanou oblast, rozšiřte adresu (např. `"A1:Z100"`). Můžete také použít `srcWs.getCells().getMaxDataColumn()` a `getMaxDataRow()` pro dynamické vypočtení použité oblasti.

### Krok 3: Vytvořit cílový sešit

```java
        // Create a new, empty workbook that will receive the copied range.
        Workbook destWb = new Workbook();               // defaults to a single empty sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Proč?**  
Čerstvý sešit zajišťuje, že žádné nechtěné formátování nebo skryté listy neovlivní kopírovaný obsah. Výchozí sešit již obsahuje jeden list, který použijeme jako cíl.

### Krok 4: Zkopírovat oblast do cílového sešitu

```java
        // Copy the source range to cell A1 of the destination worksheet.
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));
```

**Proč?**  
`copyRange` zpracovává všechny atributy buněk: hodnoty, vzorce, formátování a dokonce i cache kontingenčních tabulek. Kopírováním do `"A1"` umístíte oblast do levého horního rohu cílového listu a zachováte původní rozložení.

**Častá otázka:** *Zůstane kontingenční tabulka funkční?*  
Ano. Aspose.Cells kopíruje definici kontingenční tabulky i její cache, takže tabulka funguje přesně jako ve zdrojovém sešitu.

### Krok 5: Uložit cílový sešit

```java
        // Save the new workbook to disk.
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Proč?**  
Volání `save` zapíše sešit v paměti do fyzického souboru `.xlsx`. Můžete také uložit do jiných formátů (`.xls`, `.csv`, `.pdf`) změnou přípony souboru nebo použitím `SaveOptions`.

**Tip:**  
Pokud potřebujete soubor streamovat do webové odpovědi, použijte `destWb.save(OutputStream, SaveFormat.XLSX);` místo cesty k souboru.

---

## Kopírování oblasti mezi sešity – kompletní zdrojový kód

Níže je kompletní, připravená ke spuštění Java třída. Nahraďte `YOUR_DIRECTORY` skutečnou složkou na vašem počítači.

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

**Očekávaný výsledek:**  
`dest.xlsx` obsahuje přesnou repliku oblasti `A1:G20` ze `source.xlsx`. Pokud zdrojová oblast obsahovala kontingenční tabulku, cílový soubor zobrazí stejnou tabulku s datovým zdrojem správně propojeným na zkopírované buňky.

Soubor `dest.xlsx` můžete otevřít v Excelu, LibreOffice nebo jakémkoli prohlížeči podporujícím `.xlsx` a ověřit, že hodnoty, formátování i funkčnost kontingenční tabulky jsou zachovány.

---

## Kopírování sešitu s kontingenční tabulkou – co byste měli vědět

* **Pivot cache is copied automatically.** Knihovna přenáší podkladovou cache, takže kontingenční tabulka nevyžaduje ruční obnovení.
* **External data sources are not transferred.** Pokud kontingenční tabulka čerpá data z externí databáze, musíte zajistit, aby cílový sešit měl přístup ke stejnému zdroji, nebo cache vytvořit lokálně.
* **Large pivot tables may increase memory usage.** U velmi velkých sešitů zvažte zvýšení haldy JVM (`-Xmx2g`), aby nedošlo k `OutOfMemoryError`.

---

## Ukládání souboru sešitu v různých formátech

Aspose.Cells vám umožňuje uložit výsledek do mnoha formátů bez dalších úprav kódu:

```java
// Save as XLS (Excel 97-2003)
destWb.save("dest.xls");

// Save as CSV (first worksheet only)
destWb.save("dest.csv");

// Save as PDF (visual representation)
destWb.save("dest.pdf");
```

Vyberte formát, který odpovídá vašemu následnému procesu. Stejná logika `copyRange` funguje bez ohledu na finální formát.

---

## Načítání Excel sešitu v Javě – další tipy

* **Loading encrypted files:** Použijte `LoadOptions` s heslem:  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setPassword("myPassword");
  Workbook wb = new Workbook("encrypted.xlsx", opt);
  ```
* **Reading only specific sheets:**  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setLoadDataOnly(true); // faster if you only need values
  Workbook wb = new Workbook("file.xlsx", opt);
  ```

Tyto možnosti mohou urychlit krok **load excel workbook java**, zejména u velkých souborů.

---

## Závěr

Nyní víte, **jak kopírovat buňky** mezi sešity Excel v Javě, **jak kopírovat oblast mezi sešity**, která obsahuje **kontingenční tabulku**, a **jak uložit soubor sešitu** ve formátu, který potřebujete. Dodržením výše uvedených kroků můžete integrovat manipulaci s Excel daty do jakékoli Java aplikace – ať už vytváříte reporting engine, ETL pipeline nebo jednoduchý nástroj pro konverzi souborů.

**Další kroky**, které můžete prozkoumat:

* Použít **copy range between workbooks** k sloučení více reportů do

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným krok‑za‑krokem vysvětlením, které vám pomůže zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Uložit nový sešit v Javě – tutoriál Kopírování oblasti mezi sešity](/cells/english/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/)
- [Jak kopírovat kontingenční tabulky mezi sešity Excel v Javě](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/)
- [Jak kopírovat oblast v Javě – Kopírování kontingenční tabulky s Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}