---
category: general
date: 2026-08-20
description: Naučte se exportovat Excel do TXT při omezení počtu desetinných míst,
  zachování významných číslic a uložení sešitu jako TXT pomocí Javy.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- limit decimal places
- keep significant digits
- save workbook as txt
language: cs
lastmod: 2026-08-20
og_description: Exportujte Excel do TXT pomocí Aspose.Cells. Tento průvodce ukazuje,
  jak omezit počet desetinných míst, zachovat významné číslice a uložit sešit jako
  TXT v Javě.
og_image_alt: Result of export excel to txt showing limited decimal places and kept
  significant digits
og_title: Export Excel do TXT v Javě – kontrola desetinných míst a významných číslic
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to export Excel to TXT while limiting decimal places, keeping
    significant digits, and saving workbook as TXT using Java.
  headline: How to export Excel to TXT with Aspose.Cells and control decimal precision
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Text export
title: Jak exportovat Excel do TXT pomocí Aspose.Cells a řídit desetinnou přesnost
url: /cs/java/excel-import-export/how-to-export-excel-to-txt-with-aspose-cells-and-control-dec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak exportovat Excel do TXT pomocí Aspose.Cells a řídit desetinnou přesnost

Pokud potřebujete **exportovat Excel do TXT** a zajistit, aby výstup respektoval konkrétní počet desetinných míst, tento návod poskytuje kompletní řešení. Uvidíte, jak omezit desetinná místa, zachovat významné číslice a **uložit sešit jako TXT** pomocí knihovny Aspose.Cells pro Java.

Tutoriál provádí tvorbu sešitu, vložení hodnoty s vysokou přesností, nastavení možností uložení TXT a zápis souboru na disk. Na konci budete schopni vygenerovat textový soubor, který obsahuje přesně požadovanou přesnost, bez ručního post‑zpracování.

## Co budete potřebovat

- Java 17 (nebo jakýkoli podporovaný JDK)
- Aspose.Cells pro Java 23.10 nebo novější
- IDE nebo nástroj pro sestavení (Maven/Gradle) pro správu závislostí
- Oprávnění k zápisu do výstupního adresáře

## Krok 1: Vytvořte sešit a přistupte k prvnímu listu

Vytvoření sešitu je prvním krokem, když chcete **exportovat Excel do TXT**. Třída `Workbook` představuje celý soubor Excel a `Worksheet` vám dává přístup k buňkám.

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*Proč je to důležité*: Objekt sešitu obsahuje všechna data, styly a metadata. Začít s čistým sešitem zaručuje, že žádné skryté formátování neovlivní export do textu.

## Krok 2: Přidejte číselnou hodnotu a omezte desetinná místa

Vložte číslo s mnoha desetinnými místy, abyste mohli demonstrovat, jak **omezit desetinná místa** během exportu.

```java
        // Put a high‑precision number into cell A1
        sheet.getCells().putValue("A1", 0.000123456789);
```

*Proč je to důležité*: Excel ukládá plnou přesnost, ale při exportu můžete chtít hodnotu oříznout nebo zaokrouhlit. Nastavení `limit decimal places` to provede automaticky.

## Krok 3: Nastavte možnosti uložení TXT tak, aby zachovaly významné číslice

Aspose.Cells poskytuje `TxtSaveOptions`. Nastavením `significantDigits` řeknete exportéru, aby zachoval jen požadovaný počet smysluplných číslic a ignoroval úvodní nuly.

```java
        // Configure TXT export options
        TxtSaveOptions txtOptions = new TxtSaveOptions();

        // Keep exactly 5 significant digits (e.g., 0.00012346)
        txtOptions.setSignificantDigits(5);
```

*Proč je to důležité*: Volba **keep significant digits** zajišťuje, že výstupní soubor obsahuje předvídatelný počet přesnosti, což je nezbytné pro downstream systémy očekávající formát s pevnou šířkou čísel.

## Krok 4: Uložte sešit jako TXT

Nakonec zapíšete sešit do textového souboru. Metoda `save` respektuje nastavené možnosti, takže výsledný soubor bude obsahovat omezenou desetinnou reprezentaci.

```java
        // Define the output path (replace with your own directory)
        String outputPath = "output/SignificantDigits.txt";

        // Export the workbook to TXT using the configured options
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

*Proč je to důležité*: Použití **save workbook as txt** s připraveným `TxtSaveOptions` zaručuje, že exportovaný soubor splňuje omezení přesnosti, která jste nastavili v předchozím kroku.

### Očekávaný obsah souboru `SignificantDigits.txt`

```
0.00012346
```

Hodnota ukazuje pět významných číslic (`12346`) po zaokrouhlení a úvodní nuly jsou zachovány podle formátu TXT.

## Varianty a okrajové případy

| Scénář | Úprava |
|----------|------------|
| **Různý počet významných číslic** | Zavolejte `txtOptions.setSignificantDigits(n)`, kde `n` je 1‑15. |
| **Export rozsahu místo celého listu** | Použijte `txtOptions.setExportRange("A1:B10")` před uložením. |
| **Zachování oddělovačů sloupců** | Nastavte `txtOptions.setSeparator('\t')` pro výstup oddělený tabulátorem. |
| **Velké listy** | Zvyšte `txtOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCES)`, aby se předešlo `OutOfMemoryError`. |

## Časté problémy a tipy

- **Nemíchejte významné číslice s desetinnými místy**. Úvodní nuly se nepočítají jako významné; použijte `setSignificantDigits` pro smysluplnou přesnost a `setDecimalPlaces`, pokud potřebujete pevný počet číslic za desetinnou čárkou.
- **Vždy zadejte absolutní výstupní cestu**, když spouštíte z IDE, abyste se vyhnuli chybám oprávnění.
- **Ověřte vygenerovaný soubor** pomocí jednoduchého volání `java.nio.file.Files.readAllLines(Paths.get(outputPath))`, abyste se ujistili, že obsah odpovídá očekáváním před předáním downstream procesům.

## Kompletní zdrojový kód pro referenci

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 2: Insert a high‑precision number (will be limited later)
        sheet.getCells().putValue("A1", 0.000123456789);

        // Step 3: Set TXT options – keep 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(5);   // keep significant digits

        // Step 4: Save the workbook as TXT
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

Spuštěním programu vznikne `SignificantDigits.txt` obsahující jediný řádek `0.00012346`, což demonstruje, že proces **export excel to txt** respektuje jak **limit decimal places**, tak **keep significant digits** požadavky.

## Závěr

Nyní víte, jak **exportovat Excel do TXT** pomocí Aspose.Cells pro Java a zároveň řídit číselnou přesnost. Nastavením `TxtSaveOptions` můžete **omezit desetinná místa**, **zachovat významné číslice** a spolehlivě **uložit sešit jako txt** bez dalšího post‑zpracování.

Dále můžete zkusit:

- Export více listů do samostatných TXT souborů (`save workbook as txt` pro každý list)
- Použití `setSeparator` k vytvoření CSV‑kompatibilního výstupu
- Automatizaci hromadných konverzí pro velké datové sady

Neváhejte experimentovat s různými počty číslic a oddělovači, aby vyhovovaly přesně potřebám vašeho projektu. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobným krok za krokem vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vlastních projektech.

- [Jak vytvořit a exportovat Excel do HTML pomocí Aspose.Cells Java \| Průvodce operacemi se sešitem](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Uložit Excel jako Text – Kompletní C# průvodce exportem Excel do TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Exportovat Excel sešit jako obrázek pomocí Aspose.Cells pro Java: krok za krokem](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}