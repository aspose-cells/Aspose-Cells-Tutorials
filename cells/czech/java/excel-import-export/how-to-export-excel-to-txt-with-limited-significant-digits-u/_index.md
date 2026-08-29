---
category: general
date: 2026-08-17
description: Exportujte Excel do TXT při omezení významných číslic – zjistěte, jak
  nastavit číslice a převést Excel na text v Javě s kompletním příkladem Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set digits
- convert excel to text
- how to limit decimals
- limit significant digits
language: cs
lastmod: 2026-08-17
og_description: Exportujte Excel do TXT s omezením významných číslic. Tento tutoriál
  ukazuje, jak nastavit počet číslic a převést Excel na text pomocí Aspose.Cells pro
  Javu.
og_image_alt: Java code exporting Excel to TXT with 4 significant digits
og_title: Export Excel do TXT s omezeným počtem významných číslic – Java průvodce
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  headline: How to export Excel to TXT with limited significant digits using Java
  type: TechArticle
- description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  name: How to export Excel to TXT with limited significant digits using Java
  steps:
  - name: Prerequisites
    text: '- Java 17 or later (the code compiles with Java 8 as well). - Aspose.Cells
      for Java 25.10 or newer. Download the JAR from the [Aspose website](https://products.aspose.com/cells/java)
      and add it to your project’s classpath. - An IDE or a simple text editor and
      command‑line build tool (Maven/Gradle).'
  - name: How the setting differs from “limit decimals”
    text: '- **limit decimals** (`setDecimalPlaces`) trims digits *after* the decimal
      point, regardless of the integer part. - **significant digits** (`setSignificantDigits`)
      counts digits from the first non‑zero digit, which is useful when numbers vary
      in magnitude.'
  - name: Expected output
    text: '| Cell | Original value | Exported (4 significant digits) | |------|----------------|---------------------------------|
      | A1 | 123.456789 | 123.5 |'
  - name: Exporting a whole range
    text: 'If you want to export more than one cell, simply fill the range before
      saving:'
  - name: Handling locale‑specific decimal separators
    text: 'Aspose.Cells respects the system locale when writing text. To force a dot
      (`.`) as the decimal separator, set the `TxtSaveOptions` culture:'
  - name: Overwriting existing files
    text: 'The `save` method overwrites the target file by default. If you need to
      avoid accidental data loss, check for file existence first:'
  - name: Large workbooks and memory usage
    text: 'When exporting very large worksheets, consider streaming the output:'
  - name: Next steps
    text: "- Explore other `TxtSaveOptions` properties such as `setDelimiter('\t')`
      to customize column separators. - Combine the exporter with `CsvSaveOptions`
      if you need comma‑separated values instead of plain text. - Integrate the routine
      into a web service that accepts uploaded Excel files and returns tri"
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel export
- TXT conversion
title: Jak exportovat Excel do TXT s omezeným počtem významných číslic v Javě
url: /cs/java/excel-import-export/how-to-export-excel-to-txt-with-limited-significant-digits-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportovat Excel do TXT s omezeným počtem významných číslic pomocí Javy

Pokud potřebujete **exportovat Excel do TXT** a zároveň řídit počet významných číslic, tento návod poskytuje připravené řešení. Uvidíte, jak nastavit číslice, převést Excel na text a udržet výstup přehledný pomocí jediné změny konfigurace.

Ukázka používá Aspose.Cells pro Java 25.10, který zavádí možnost `setSignificantDigits`. Na konci tutoriálu budete schopni vygenerovat TXT soubor, který obsahuje jen požadované číslice, bez dalšího kódu pro zaokrouhlování.

## Co dosáhnete

- Vytvořit sešit programově.
- Vložit číselnou hodnotu do buňky.
- Nastavit možnosti uložení TXT tak, aby omezily významné číslice.
- Uložit sešit jako soubor prostého textu.
- Pochopit, jak funguje nastavení `significantDigits` a jak jej přizpůsobit pro jiné scénáře.

### Požadavky

- Java 17 nebo novější (kód se také kompiluje s Java 8).
- Aspose.Cells pro Java 25.10 nebo novější. Stáhněte JAR ze [stránky Aspose](https://products.aspose.com/cells/java) a přidejte jej do classpath vašeho projektu.
- IDE nebo jednoduchý textový editor a nástroj pro sestavení z příkazové řádky (Maven/Gradle).

## Krok 1: Nastavení projektu a import Aspose.Cells

Vytvořte nový Java projekt a přidejte JAR Aspose.Cells do cesty pro sestavení. Pokud používáte Maven, přidejte následující závislost do `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Tip:** Použijte klasifikátor `jdk17` pro nejnovější Java runtime; snižuje riziko varování o kompatibilitě.

## Krok 2: Vytvořit sešit a zapsat hodnotu

Sešit představuje Excel soubor v paměti. Data můžete přidat do libovolné buňky pomocí metody `putValue`.

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Put a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(123.456789);
```

Číslo `123.456789` bude zdrojem pro náš export do TXT. Ve výchozím nastavení by Aspose.Cells zapisoval všechny desetinné místa, což často vede k hlučným textovým souborům.

## Krok 3: Nastavit možnosti uložení TXT tak, aby omezily významné číslice

Aspose.Cells poskytuje `TxtSaveOptions` pro detailní kontrolu výstupu prostého textu. Metoda `setSignificantDigits` říká exportéru, kolik číslic má zachovat **celkově**, nejen za desetinnou čárkou.

```java
        // Configure TXT save options to keep only 4 significant digits
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4); // new option in 25.10
```

Když je `significantDigits` nastaveno na `4`, exportér zaokrouhlí hodnotu `123.456789` na `123.5`. Toto chování odpovídá matematické definici významných číslic: první čtyři nenulové číslice jsou zachovány.

### Jak se nastavení liší od „limit decimals“

- **limit decimals** (`setDecimalPlaces`) ořízne číslice *za* desetinnou čárkou, bez ohledu na celočíselnou část.
- **significant digits** (`setSignificantDigits`) počítá číslice od první nenulové číslice, což je užitečné, když se čísla liší velikostí.

Pokud místo toho potřebujete pevný počet desetinných míst, nahraďte výše uvedený řádek tímto:

```java
saveOptions.setDecimalPlaces(2); // keeps two digits after the decimal point
```

## Krok 4: Uložit sešit jako TXT soubor

Nyní zapište sešit na disk pomocí nakonfigurovaných možností.

```java
        // Save the workbook as a TXT file using the configured options
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Spuštěním programu se vytvoří `significant_digits.txt` v pracovním adresáři. Soubor obsahuje jediný řádek:

```
123.5
```

### Očekávaný výstup

| Buňka | Původní hodnota | Exportováno (4 významné číslice) |
|------|----------------|-----------------------------------|
| A1   | 123.456789     | 123.5                             |

Pokud změníte `setSignificantDigits(4)` na `6`, výstup bude `123.457`. Experimentujte s různými hodnotami a sledujte, jak se zaokrouhlování přizpůsobuje.

## Krok 5: Běžné varianty a okrajové případy

### Export celého rozsahu

Pokud chcete exportovat více než jednu buňku, jednoduše před uložením vyplňte rozsah:

```java
worksheet.getCells().get("B1").putValue(0.0012345);
worksheet.getCells().get("C1").putValue(98765.4321);
```

Stejné nastavení `significantDigits` se použije na každou číselnou buňku, čímž zajistí konzistentní přesnost v celém souboru.

### Zpracování lokálně specifických desetinných oddělovačů

Aspose.Cells respektuje systémové locale při zápisu textu. Pro vynucení tečky (`.`) jako desetinného oddělovače nastavte kulturu `TxtSaveOptions`:

```java
saveOptions.setCultureInfo(java.util.Locale.US);
```

To je užitečné, když cílová aplikace očekává konkrétní formát, například CSV parsery, které akceptují jen `.`.

### Přepisování existujících souborů

Metoda `save` ve výchozím nastavení přepíše cílový soubor. Pokud chcete předejít neúmyslné ztrátě dat, nejprve zkontrolujte existenci souboru:

```java
java.io.File outFile = new java.io.File("significant_digits.txt");
if (outFile.exists()) {
    throw new IllegalStateException("File already exists. Choose a different name or delete the existing file.");
}
workbook.save(outFile.getPath(), saveOptions);
```

### Velké sešity a využití paměti

Při exportu velmi velkých listů zvažte streamování výstupu:

```java
saveOptions.setEnableMemorySaving(true);
```

Tato možnost snižuje spotřebu haldy tím, že zapisuje řádky postupně.

## Kompletní funkční příklad

Níže je kompletní program, který můžete okamžitě zkopírovat, vložit a spustit:

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 2: Put numeric values into cells
        worksheet.getCells().get("A1").putValue(123.456789);
        worksheet.getCells().get("B1").putValue(0.0012345);
        worksheet.getCells().get("C1").putValue(98765.4321);

        // Step 3: Configure TXT save options
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4);          // limit to 4 significant digits
        saveOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator
        saveOptions.setEnableMemorySaving(true);      // optional for large files

        // Step 4: Save the workbook as a TXT file
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Spuštěním tohoto kódu se vytvoří `significant_digits.txt` s následujícím obsahem (sloupce oddělené tabulátorem):

```
123.5	0.001235	98770
```

Každé číslo dodržuje pravidlo **4 významné číslice**, což dokazuje, že nastavení funguje napříč různými velikostmi.

## Závěr

Nyní víte, jak **exportovat Excel do TXT** a zároveň řídit počet významných číslic. Pomocí `TxtSaveOptions.setSignificantDigits` můžete **nastavit číslice**, **omezit desetinná místa** a **omezit významné číslice** v jediném, udržovatelném řádku kódu. Přístup funguje pro jednotlivé buňky, celé rozsahy i velké sešity.

### Další kroky

- Prozkoumejte další vlastnosti `TxtSaveOptions`, například `setDelimiter('\t')`, pro přizpůsobení oddělovačů sloupců.
- Kombinujte exportér s `CsvSaveOptions`, pokud potřebujete hodnoty oddělené čárkou místo prostého textu.
- Integrujte tuto rutinu do webové služby, která přijímá nahrané Excel soubory a vrací oříznutý TXT výstup v reálném čase.

Neváhejte experimentovat s různými limity číslic a locale. Pokud narazíte na situaci, kdy vestavěné možnosti nesplňují speciální požadavek, můžete vždy provést následné zpracování vygenerovaného TXT souboru pomocí standardních Java I/O utilit.

Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto návodu. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak převést text na čísla v Excelu pomocí Aspose.Cells pro Java](/cells/english/java/cell-operations/convert-text-to-numbers-excel-aspose-cells-java/)
- [Jak vytvořit a exportovat Excel do HTML pomocí Aspose.Cells Java \| Průvodce operacemi sešitu](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Jak exportovat vlastní vlastnosti Excelu do PDF pomocí Aspose.Cells pro Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}