---
category: general
date: 2026-07-23
description: Vytvořte nový sešit v Javě a naučte se během několika minut zkopírovat
  kontingenční tabulku, zkopírovat oblast v Excelu a exportovat kontingenční tabulku
  pomocí Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- how to copy pivot
- copy excel range
- export pivot table
language: cs
lastmod: 2026-07-23
og_description: Vytvořte nový sešit v Javě a okamžitě zkopírujte kontingenční tabulku,
  zkopírujte oblast v Excelu a poté exportujte kontingenční tabulku pomocí Aspose.Cells.
  Sledujte tento kompletní návod.
og_image_alt: Screenshot of Java code copying a pivot table from one workbook to another
og_title: Vytvořte nový sešit v Javě – Kopírování kontingenční tabulky krok za krokem
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Create new workbook in Java and learn how to copy pivot table, copy
    excel range, and export pivot table with Aspose.Cells in minutes.
  headline: Create New Workbook in Java – Full Guide to Copy Pivot Table
  type: TechArticle
- questions:
  - answer: You’ll need to copy each relevant range separately, then recreate the
      pivot on the destination sheet using `PivotTable` APIs.
    question: What if the source pivot spans more than one worksheet?
  - answer: Set `sourceRange.setCopyDataOnly(false)` before the copy. This tells Aspose
      to keep the cache but not the underlying source data.
    question: Can I copy only the pivot layout without the data?
  - answer: CSV doesn’t support pivots, but you can export the pivot’s *result* by
      calling `pivotTable.calculate()` and then saving the sheet as CSV.
    question: Is there a way to copy the pivot to a CSV file?
  - answer: Formatting lives in the style collection. After copying, you can call
      `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())`
      to transfer styles.
    question: Why does the copied pivot lose its formatting?
  type: FAQPage
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Vytvoření nového sešitu v Javě – Kompletní průvodce kopírováním kontingenční
  tabulky
url: /cs/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření nového sešitu v Javě – Kompletní průvodce kopírováním kontingenční tabulky

Chtěli jste někdy vědět, jak **create new workbook** v Javě při zachování složité kontingenční tabulky? Nejste jediní, kdo se nad tím trápí. V mnoha reportovacích aplikacích potřebujete přesunout kontingenční tabulku ze zdrojového souboru do nového sešitu, možná pro odeslání klientovi nebo pro další výpočty. Dobrá zpráva? S několika řádky kódu to můžete udělat – bez ručního kopírování a vkládání.

V tomto tutoriálu projdeme celý proces: načtení zdrojového souboru, definování oblasti, která obsahuje kontingenční tabulku, **copying the Excel range**, vytvoření **new workbook** a nakonec **exporting the pivot table** do nového souboru. Na konci budete mít samostatný spustitelný Java program, který odpovídá na otázku „**how to copy pivot**“ bez hádání.

## Požadavky

- Java 17 nebo novější (kód funguje s jakýmkoli recentním JDK)
- Knihovna Aspose.Cells pro Java (bezplatná zkušební verze nebo licencovaná verze)
- Ukázkový soubor `source.xlsx`, který obsahuje kontingenční tabulku v rozsahu `A1:G20`
- IDE nebo nástroj pro sestavení (Maven/Gradle) pro správu JAR souboru Aspose.Cells

Máte je? Skvělé – pojďme začít.

## Krok 1: Nastavení projektu a import Aspose.Cells

Nejprve je potřeba přidat Aspose.Cells do vašeho projektu. Pokud používáte Maven, vložte tuto závislost do souboru `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.8</version> <!-- check for the latest version -->
</dependency>
```

Pokud dáváte přednost Gradle, ekvivalent je:

```groovy
implementation 'com.aspose:aspose-cells:24.8'
```

Jakmile je knihovna na classpath, importujte třídy, které budete potřebovat:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **Pro tip:** Aspose.Cells je komerční knihovna, ale nabízí plně funkční 30‑denní zkušební verzi, která na výstupu umístí vodoznak – ideální pro vyzkoušení.

## Krok 2: Načtení zdrojového sešitu

Nyní vytvoříme objekty **create new workbook**, ale nejprve potřebujeme zdroj, který obsahuje kontingenční tabulku. Tento krok je základem pro jakoukoli operaci **copy excel range**, protože objekt oblasti přesně ví, které buňky (včetně cache kontingenční tabulky) mají být přeneseny.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0) – adjust if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Proč nečíst oblast přímo? Protože metadata kontingenční tabulky jsou uložena v pivot cache listu a Aspose.Cells je automaticky zahrne při kopírování oblasti.

## Krok 3: Definování oblasti, která obsahuje kontingenční tabulku

V mnoha reálných souborech kontingenční tabulka zabírá obdélníkový blok. Pro tento příklad předpokládáme, že se nachází v `A1:G20`. Samozřejmě můžete adresu upravit tak, aby odpovídala vašemu skutečnému rozložení.

```java
// Define the exact area that includes the pivot table
Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

Pokud si nejste jisti přesnou adresou, můžete použít `sourceSheet.getCells().getMaxDataRow()` a `getMaxDataColumn()` k dynamickému výpočtu hranic. Je to užitečný trik, když se velikost kontingenční tabulky v průběhu času mění.

## Krok 4: **Create New Workbook** a cílový list

Nyní nastává okamžik, kdy skutečně **create new workbook**, který přijme zkopírovaný obsah. Považujte ho za prázdné plátno, na které vložíte kontingenční tabulku.

```java
// Create an empty workbook – this is our destination
Workbook destinationWorkbook = new Workbook();

// By default a new workbook comes with one worksheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Proč začít s prázdným sešitem? Zajišťuje, že žádné skryté styly nebo předchozí kontingenční tabulky nebudou zasahovat do kopírování, což vám poskytne čistý výsledek připravený pro **export pivot table**.

## Krok 5: Kopírování kontingenční tabulky (a její podkladové oblasti)

Nyní jádro tutoriálu: **copy pivot table**. Aspose.Cells považuje kopírování oblasti za hlubokou kopii, což znamená, že pivot cache cestuje spolu s buňkami. Proto tato jediná řádka provádí těžkou práci.

```java
// Copy the defined range (including the pivot) to the destination sheet at A1
sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

Pokud jste se někdy ptali **how to copy pivot** bez ztráty funkčnosti, toto je odpověď. Cílový list nyní obsahuje plně funkční kontingenční tabulku, kterou můžete aktualizovat, upravit nebo jednoduše exportovat.

### Okrajový případ: Zachování nastavení obnovy

Někdy je zdrojová kontingenční tabulka nastavena na obnovu při otevření. Pro zachování tohoto chování můžete explicitně zkopírovat možnosti pivotu:

```java
// Optional: retain the original pivot's refresh settings
PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
PivotTable destPivot = destinationSheet.getPivotTables().get(0);
destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
```

Tento úryvek zajistí, že zkopírovaný pivot se chová přesně jako originál.

## Krok 6: Uložení cílového sešitu – **Export Pivot Table**

Nakonec **export pivot table** uložením nového sešitu na disk. Můžete zvolit libovolný formát, který Aspose podporuje: XLSX, XLS, CSV, PDF atd. Pro tento návod zůstaneme u XLSX.

```java
// Save the workbook that now contains the copied pivot
destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);
```

Pokud potřebujete soubor odeslat přes webovou službu, můžete jej zapsat do `ByteArrayOutputStream` místo cesty k souboru – Aspose to dělá jednoduchým.

## Kompletní funkční příklad

Spojením všech částí získáte kompletní, připravený k spuštění program. Klidně jej zkopírujte, vložte a spusťte ve svém IDE.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 3️⃣ Copy the range (pivot table included) to the destination sheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Optional: Preserve refresh settings if needed
        if (!sourceSheet.getPivotTables().isEmpty()) {
            PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
            PivotTable destPivot = destinationSheet.getPivotTables().get(0);
            destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
        }

        // 4️⃣ Save the result – this effectively **export pivot table**
        destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);

        System.out.println("Pivot table copied successfully!");
    }
}
```

### Očekávaný výstup

Po spuštění programu vypíše konzole:

```
Pivot table copied successfully!
```

A soubor `copied_with_pivot.xlsx` se objeví v `YOUR_DIRECTORY`. Otevřete jej v Excelu a uvidíte, že kontingenční tabulka je zachována, připravena k aktualizaci nebo úpravě.

## Časté otázky a řešení problémů

- **Co když zdrojová kontingenční tabulka zasahuje do více listů?**  
  Budete muset zkopírovat každou relevantní oblast zvlášť a poté na cílovém listu znovu vytvořit pivot pomocí API `PivotTable`.

- **Mohu zkopírovat jen rozložení pivotu bez dat?**  
  Před kopírováním nastavte `sourceRange.setCopyDataOnly(false)`. Tím říkáte Aspose, aby zachoval cache, ale ne podkladová zdrojová data.

- **Je možné zkopírovat pivot do CSV souboru?**  
  CSV nepodporuje pivoty, ale můžete exportovat *výsledek* pivotu voláním `pivotTable.calculate()` a následným uložením listu jako CSV.

- **Proč zkopírovaný pivot ztrácí formátování?**  
  Formátování je uloženo ve sbírce stylů. Po kopírování můžete zavolat `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())` pro přenos stylů.

## Závěr

Právě jsme vám ukázali, jak **create new workbook** v Javě, **copy pivot table** a **export pivot table** – vše s čistým, reprodukovatelným ukázkovým kódem. Definováním přesného **copy excel range**, využitím hlubokých kopií v Aspose.Cells a zachováním volitelných nastavení můžete automatizovat prakticky jakýkoli úkol migrace pivotu.

Jste připraveni na další krok? Zkuste změnit výstupní formát na PDF nebo projít více zdrojových souborů a hromadně zpracovat desítky pivotů. Stejný vzor platí – stačí upravit cesty k souborům a adresy oblastí.

Pokud narazíte na problém, zanechte komentář níže nebo si prohlédněte dokumentaci Aspose.Cells pro pokročilé manipulace s pivoty. Šťastné programování a užijte si čas, který jste ušetřili automatizací těch nudných úkolů kopírování‑vkládání!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak vytvořit kontingenční tabulky v Excelu pomocí Aspose.Cells pro Java: Kompletní průvodce](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Jak aktualizovat zdroj kontingenční tabulky v Excelu pomocí Aspose.Cells pro Java: Kompletní průvodce](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Jak vytvořit a exportovat Excel do HTML pomocí Aspose.Cells Java \| Průvodce operacemi se sešitem](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}