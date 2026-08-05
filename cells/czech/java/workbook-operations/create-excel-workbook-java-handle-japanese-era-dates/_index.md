---
category: general
date: 2026-08-04
description: Vytvořte Excel sešit v Javě, zpracujte japonské datumy v érách a poté
  uložte sešit jako xlsx pomocí Aspose.Cells pro Javu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- java excel date conversion
- Aspose.Cells Java
- japanese era date parsing
language: cs
lastmod: 2026-08-04
og_description: Vytvořte v Javě excelový sešit a automaticky převádějte japonské datumy
  podle éry na gregoriánské, poté uložte sešit jako xlsx pomocí Aspose.Cells.
og_image_alt: Java code creating an Excel workbook and converting a Japanese era date
  to Gregorian
og_title: Vytvořte Excel sešit v Javě – Průvodce konverzí japonských dat
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create excel workbook java and parse Japanese era dates, then save
    workbook as xlsx using Aspose.Cells for Java.
  headline: 'Create excel workbook java: handle Japanese era dates'
  type: TechArticle
tags:
- java
- excel
- Aspose.Cells
- date conversion
- xlsx
title: 'Vytvořit Excel sešit v Javě: zpracovat japonské datumy podle éry'
url: /cs/java/workbook-operations/create-excel-workbook-java-handle-japanese-era-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořit excel workbook java: práce s japonskými era daty

Pokud potřebujete **create excel workbook java** a pracovat s japonskými era daty, tento tutoriál vám přesně ukáže, jak na to. Naučíte se zadat datum jako “R3/05/01”, nechat Aspose.Cells interpretovat jej jako gregoriánské datum a poté **save workbook as xlsx**.

Práce s kalendáři založenými na érách může být matoucí, zejména když výchozí parser Excelu očekává standardní gregoriánský formát. Povolením parsování japonských éráů se vyhnete ruční manipulaci s řetězci a necháte knihovnu, aby konverzi provedla za vás. Tento průvodce také pokrývá poslední krok uložení souboru jako souboru `.xlsx`.

## Požadavky

* Java 17 nebo novější nainstalována.
* Maven 3.6+ (nebo Gradle) pro správu závislostí.
* IDE, jako je IntelliJ IDEA nebo Eclipse.
* Knihovna Aspose.Cells for Java (příklad používá verzi 23.10, ale funguje jakákoli novější verze).

## Krok 1: Přidat Aspose.Cells do projektu

Knihovna poskytuje třídy `Workbook`, `Worksheet` a `WorkbookSettings`, které jsou používány v celém tomto tutoriálu.

**Maven**

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

**Gradle**

```gradle
implementation 'com.aspose:aspose-cells:23.10:jdk17'
```

> **Tip:** Použijte `javadoc` JAR pro získání inline dokumentace během kódování.

## Krok 2: Vytvořit sešit a získat první list

Nyní vytvoříme nový objekt workbook a získáme výchozí první list.

```java
import com.aspose.cells.*;

public class JapaneseEraExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();                // create an empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet (index 0)
```

*Proč je tento krok důležitý:* `Workbook` představuje celý Excel soubor, zatímco `Worksheet` je plátno, kam umisťujete buňky. Začátek s čistým workbookem zajišťuje, že žádné skryté formátování nezasahuje do parsování data.

## Krok 3: Zadání japonského era data do buňky

Japonská era data následují vzor “<EraLetter><Year>/<Month>/<Day>”. V tomto příkladu používáme “R3” (Reiwa 3 = 2021).

```java
        // Step 3: Put a Japanese era date into cell A1
        Cell dateCell = worksheet.getCells().get("A1");
        dateCell.putValue("R3/05/01");   // Reiwa 3, May 1st
```

*Proč je tento krok důležitý:* Zapsáním řetězce era přímo necháte Aspose.Cells provést konverzi později. Vyhnete se nutnosti převádět “R3” na “2021” ručně.

## Krok 4: Povolit parsování japonských éráů a přepočítat vzorce

Řekněte workbooku, aby zacházel s řetězci era jako s daty. Po přepnutí nastavení zavolejte `calculateFormula()`, aby jakékoli závislé vzorce (pokud je později přidáte) viděly správnou gregoriánskou hodnotu.

```java
        // Step 4: Turn on Japanese era parsing
        WorkbookSettings settings = workbook.getSettings();
        settings.setUseJapaneseEra(true);   // enable era conversion
        workbook.calculateFormula();        // refresh any formulas
```

*Proč je tento krok důležitý:* Příznak `setUseJapaneseEra(true)` instruuje Aspose.Cells, aby interpretoval řetězce jako “R3/05/01” jako gregoriánská data. Bez něj by buňka zachovala doslovný text, což by narušilo následné výpočty.

## Krok 5: Ověřit konverzi a **save workbook as xlsx**

Vytiskněte převedenou hodnotu do konzole a uložte workbook.

```java
        // Step 5: Verify conversion and save the file
        System.out.println("Converted date: " + dateCell.getStringValue()); // → 2021-05-01
        workbook.save("JapaneseEra.xlsx");   // saves as .xlsx by default
    }
}
```

**Očekávaný výstup v konzoli**

```
Converted date: 2021-05-01
```

Soubor `JapaneseEra.xlsx` nyní obsahuje gregoriánské datum `2021‑05‑01` v buňce A1, i když zdrojový řetězec použil japonský formát era.

## Krok 6: Běžné varianty a ošetření okrajových případů

| Scénář | Jak upravit kód |
|----------|-----------------------|
| Jiná era (např. Heisei) | Použijte “H30/12/31” pro Heisei 30 = 2018‑12‑31. Stejný příznak `setUseJapaneseEra(true)` funguje pro všechny podporované éry. |
| Prázdný nebo špatně formátovaný řetězec | Zabalte `putValue` do try‑catch bloku a ověřte pomocí regulárního výrazu jako `^[RHS][0-9]+/[0-9]{2}/[0-9]{2}$`. |
| Potřeba zachovat původní řetězec era pro audit | Uložte surový řetězec do skryté sloupce před konverzí a poté tento sloupec ve finálním workbooku skryjte. |
| Velké datové sady | Povolte `WorkbookSettings.setEnableThreadedCalculation(true)`, aby se urychlil přepočet vzorců při použití era dat ve velkém počtu řádků. |

> **Pozor:** Použití starší verze Aspose.Cells, která předchází podpoře japonských éráů (před‑2020), bude ignorovat příznak `setUseJapaneseEra`, takže buňka zůstane nezměněna.

## Krok 7: Spustit příklad

Zkompilujte a spusťte třídu z vašeho IDE nebo z příkazové řádky:

```bash
javac -cp "path/to/aspose-cells-23.10.jar" JapaneseEraExample.java
java -cp ".:path/to/aspose-cells-23.10.jar" JapaneseEraExample
```

Po spuštění otevřete `JapaneseEra.xlsx` v Excelu. Buňka A1 zobrazuje `2021-05-01`, což potvrzuje úspěšnou **java excel date conversion**.

## Závěr

Nyní víte, jak **create excel workbook java**, zadat japonské era datum, povolit automatické parsování éráů a **save workbook as xlsx**. Tento přístup eliminuje ruční aritmetiku dat a zajišťuje, že vaše Excel soubory zůstávají kompatibilní se standardními gregoriánskými kalendáři.

### Co zkoumat dál

* **Formatting dates** – použijte styl buňky (`Style style = workbook.createStyle(); style.setNumber(14);`), aby se data zobrazovala ve vámi preferovaném locale.
* **Bulk conversion** – iterujte přes sloupec řetězců era a konvertujte každou buňku ve smyčce.
* **Export to other formats** – Aspose.Cells také podporuje PDF, CSV a ODS; stačí změnit příponu souboru v `workbook.save(...)`.

Neváhejte experimentovat s dalšími érami, vlastními formáty nebo kombinovat tuto techniku s reporty řízenými vzorci. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/french/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}