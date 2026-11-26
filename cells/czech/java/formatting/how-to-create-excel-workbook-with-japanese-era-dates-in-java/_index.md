---
category: general
date: 2026-11-25
description: Naučte se, jak vytvořit sešit Excel, nastavit obecný formát buňky, aplikovat
  styl buňky v Excelu a uložit sešit ve formátu XLSX pomocí Javy a Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- format cell general
- apply style excel cell
- save workbook xlsx
language: cs
lastmod: 2026-11-25
og_description: Vytvořte sešit Excel v Javě, nastavte buňku na obecný formát, aplikujte
  styl buňky Excel a uložte sešit jako XLSX při zpracování japonských era datumů.
og_image_alt: Screenshot of a Java IDE showing code that creates an Excel workbook
  with a formatted date cell
og_title: Vytvořte sešit Excel s japonskými daty podle éry – krok za krokem průvodce
  v Javě
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to create Excel workbook, format cell general, apply style
    Excel cell, and save workbook XLSX using Java and Aspose.Cells.
  headline: How to create Excel workbook with Japanese era dates in Java
  type: TechArticle
tags:
- Java
- Excel automation
- Aspose.Cells
title: Jak vytvořit sešit Excel s japonskými daty podle japonské éry v Javě
url: /cs/java/formatting/how-to-create-excel-workbook-with-japanese-era-dates-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit Excel sešit s japonskými era daty v Javě

Pokud potřebujete **vytvořit Excel sešit**, který ukládá japonská era data, tento návod vám ukáže přesné kroky. Uvidíte, jak nastavit buňku jako General, aplikovat styl na buňku v Excelu a nakonec **uložit sešit XLSX**, aby byl datum správně interpretován.

Práce s řetězci japonských érá (např. „R3‑04‑01“) může být obtížná, protože Excel očekává skutečnou hodnotu `DateTime`, nikoli jen text. Na konci tohoto tutoriálu budete mít plně funkční soubor `.xlsx`, který zobrazuje správné gregoriánské datum a zároveň zachovává původní zápis era.

## Požadavky

- Java 17 nebo novější (kód se také kompiluje s dřívějšími verzemi)
- Aspose.Cells for Java knihovna (`aspose-cells-xx.x.jar`) – knihovna je zdarma pro evaluaci a plně vybavena pro produkci
- Základní znalost Javy a Maven/Gradle (nebo schopnost přidat JAR do classpath)
- IDE jako IntelliJ IDEA, Eclipse nebo VS Code (kterékoli bude fungovat)

## Krok 1 – Vytvořit Excel sešit

Prvním krokem je vytvořit novou instanci objektu sešitu. Tento objekt představuje celý Excel soubor v paměti a poskytuje přístup k listům, buňkám a stylům.

```java
import com.aspose.cells.*;

public class JapaneseEraExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook (an empty .xlsx file in memory)
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

**Proč je to důležité:**  
Programové vytvoření sešitu eliminuje potřebu šablonového souboru a zaručuje, že výsledný soubor začne v čistém stavu. Konstruktor `Workbook` automaticky vytvoří výchozí list, který si načteme pro další manipulaci.

## Krok 2 – Nastavit buňku jako General

Excel ukládá čísla pomocí různých formátů. Pro datum, které později převedeme z japonského era řetězce, nejprve nastavíme formát buňky na *General*, aby Excel neinterpretoval text předčasně.

```java
        // Step 2: Get the target cell (A1) where the era date will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Write the raw Japanese era string (e.g., "R3-04-01")
        targetCell.putValue("R3-04-01");

        // Ensure the cell uses the General number format
        Style cellStyle = targetCell.getStyle();
        cellStyle.setNumber(0); // 0 = General format in Aspose.Cells
        targetCell.setStyle(cellStyle);
```

**Proč je to důležité:**  
Nastavení **format cell general** zabraňuje Excelu automaticky formátovat řetězec era jako text s vlastním formátem, což by pozdější konverzi na skutečný `DateTime` zablokovalo. Volání `setNumber(0)` je ekvivalent Aspose.Cells pro Excelův formát „General“.

## Krok 3 – Aplikovat styl na buňku v Excelu

I když je hlavním cílem uložit datum, můžete chtít, aby buňka vypadala konzistentně s ostatními částmi listu – třeba tenký okraj nebo specifické písmo. Aplikace stylu také ukazuje, jak programově manipulovat s estetikou buňky.

```java
        // Step 3: Apply additional styling (optional but common)
        // Example: add a thin border around the cell
        cellStyle.setBorder(BorderType.TOP_BORDER, CellBorderType.THIN);
        cellStyle.setBorder(BorderType.BOTTOM_BORDER, CellBorderType.THIN);
        cellStyle.setBorder(BorderType.LEFT_BORDER, CellBorderType.THIN);
        cellStyle.setBorder(BorderType.RIGHT_BORDER, CellBorderType.THIN);

        // Set a light gray background to highlight the date cell
        cellStyle.setPattern(BackgroundType.SOLID);
        cellStyle.setBackgroundColor(Color.getGray());

        // Apply the updated style back to the cell
        targetCell.setStyle(cellStyle);
```

**Proč je to důležité:**  
Krok **apply style excel cell** ukazuje, jak obohatit vizuální prezentaci, aniž by to ovlivnilo podkladová data. Okraje a barvy pozadí jsou uloženy jako součást objektu stylu buňky, což zajišťuje, že finální sešit bude po otevření v Excelu vypadat upraveně.

## Krok 4 – Převést japonský era řetězec na objekt DateTime

Nyní nahradíme surový text skutečnou hodnotou `DateTime`. Aspose.Cells dokáže parsovat řetězec pomocí specifického `CultureInfo`. Předáním japonské kultury (`ja-JP`) knihovna správně interpretuje „R3‑04‑01“ jako 3. rok éry Reiwa, což odpovídá 2021‑04‑01 v gregoriánském kalendáři.

```java
        // Step 4: Convert the era string to a DateTime using Japanese culture
        // The fromString method respects the culture’s calendar (Japanese Imperial)
        DateTime japaneseDate = DateTime.fromString(
                "R3-04-01", // era string
                CultureInfo.createSpecificCulture("ja-JP") // Japanese locale
        );

        // Overwrite the cell value with the parsed DateTime
        targetCell.setValue(japaneseDate);
```

**Proč je to důležité:**  
Bez určení kultury by byl „R3‑04‑01“ považován za prostý text a ztratil by datumovou semantiku. Objekt `CultureInfo` říká Aspose.Cells, aby použil japonský kalendářní systém, a automaticky provádí konverzi era. Výsledná buňka nyní obsahuje pravý Excel datum, což umožňuje řazení, filtrování a datumové výpočty.

## Krok 5 – Uložit sešit jako XLSX

Nakonec zapíšeme sešit z paměti do fyzického souboru. Použití formátu `.xlsx` zaručuje kompatibilitu s moderními verzemi Excelu, Google Sheets a dalšími tabulkovými nástroji.

```java
        // Step 5: Save the workbook to the desired location
        String outputPath = "JapaneseEra.xlsx"; // adjust the path as needed
        workbook.save(outputPath, SaveFormat.XLSX);

        System.out.println("Workbook saved successfully to " + outputPath);
    }
}
```

**Proč je to důležité:**  
Operace **save workbook xlsx** finalizuje všechny změny. Aspose.Cells zapisuje sešit ve formátu Open XML, zachovává jak data, tak styly aplikované v předchozích krocích. Výsledný soubor lze otevřít přímo v Excelu, kde buňka zobrazí `2021‑04‑01` (gregoriánský ekvivalent), ale původní řetězec era lze stále získat přes Excel „Formát buněk → Číslo → Vlastní“, pokud bude potřeba.

## Očekávaný výstup

Po otevření `JapaneseEra.xlsx` v Microsoft Excel:

- Buňka **A1** zobrazuje datum `2021‑04‑01` (výchozí formát data v Excelu).  
- Buňka má tenký šedý okraj a světle šedé pozadí, což potvrzuje úspěšné provedení kroku **apply style excel cell**.  
- Pokud změníte formát buňky na „General“, podkladová hodnota zůstane pravým datem, nikoli původním řetězcem.

Konzole vypíše:

```
Workbook saved successfully to JapaneseEra.xlsx
```

## Běžné varianty a okrajové případy

| Situace | Co změnit |
|-----------|----------------|
| **Jiná era (např. Heisei)** | Použijte odpovídající předponu era (`H` pro Heisei) ve vstupním řetězci. Stejný `CultureInfo` provede konverzi. |
| **Více dat** | Procházejte rozsah buněk a aplikujte stejnou konverzní logiku na každou z nich. |
| **Vlastní formát data** | Po `setValue(japaneseDate)` zavolejte `cellStyle.setNumber(14)` (nebo libovolné ID Excel formátu) pro zobrazení dat jako `yyyy/MM/dd`. |
| **Velké sešity** | Pro výkon znovu použijte jeden objekt `Style` nebo použijte `StyleFlag` k úpravě jen potřebných atributů. |
| **Ukládání do proudu** | Nahraďte `workbook.save(outputPath, SaveFormat.XLSX)` voláním `workbook.save(outputStream, SaveFormat.XLSX)` při odesílání souboru přes HTTP. |

## Tipy z praxe

- **Pro tip:** Vždy nastavujte formát čísla buňky *před* přiřazením `DateTime`. Změna formátu později může způsobit špatné vizuální zobrazení v Excelu.
- **Dejte si pozor na:** Použití `CultureInfo("ja-JP")` bez `createSpecificCulture` může přejít na gregoriánský kalendář a vést k nesprávným datům.
- **Poznámka k výkonu:** Při vytváření mnoha stylovaných buněk klonujte existující `Style` místo volání `getStyle()` pro každou buňku; tím se sníží interní kopírovací režie.

## Závěr

V tomto tutoriálu jste se naučili, jak **vytvořit Excel sešit** v Javě, **nastavit buňku jako General**, **aplikovat styl na buňku v Excelu** a **uložit sešit XLSX**, přičemž správně zacházíte s japonskými era daty. Kompletní ukázkový kód je připraven ke zkopírování, vložení a spuštění, což vám poskytne spolehlivý základ pro jakoukoliv automatizaci Excelu zahrnující ne‑gregoriánské kalendáře.

Dále můžete zkusit:

- Přidat vzorce odkazující na převedená data (např. `=YEAR(A1)`).
- Exportovat sešit do PDF pomocí `workbook.save("output.pdf", SaveFormat.PDF)`.
- Integrovat tuto logiku do Spring Boot REST endpointu pro generování reportů na vyžádání.

Neváhejte experimentovat s různými kulturami, vlastními číselnými formáty nebo hromadnými importy dat. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Excel Workbook Initialization & Cell Styling using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/formatting/excel-workbook-initialization-cell-styling-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}