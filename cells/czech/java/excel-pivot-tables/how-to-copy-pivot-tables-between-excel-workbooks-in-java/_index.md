---
category: general
date: 2026-10-01
description: Naučte se, jak pomocí Javy kopírovat kontingenční tabulky mezi sešity
  Excel. Tento krok‑za‑krokem průvodce také ukazuje, jak kopírovat rozsah mezi sešity
  a bezpečně duplikovat rozsahy v Excelu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range between workbooks
- how to copy excel
- duplicate excel range
- copy range to workbook
language: cs
lastmod: 2026-10-01
og_description: Jak kopírovat kontingenční tabulky mezi sešity Excelu pomocí Javy.
  Postupujte podle tohoto návodu pro kopírování rozsahu do sešitu, duplikování rozsahů
  v Excelu a zachování dat kontingenční tabulky.
og_image_alt: Screenshot of Java code that copies a pivot table from one Excel workbook
  to another
og_title: Jak kopírovat kontingenční tabulky mezi sešity Excel v Javě – kompletní
  průvodce
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  headline: How to copy pivot tables between Excel workbooks in Java
  type: TechArticle
- description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  name: How to copy pivot tables between Excel workbooks in Java
  steps:
  - name: Expected output
    text: '* Console: `Pivot table copied successfully.` * `destination.xlsx` opens
      in Excel with a pivot table identical to the one in `source.xlsx`. Refreshing
      the pivot shows the same data source, proving that **how to copy pivot** works
      as intended.'
  - name: Copying multiple worksheets
    text: If your project requires copying several sheets, loop through the workbook’s
      worksheets and repeat steps 2‑4 for each sheet. The pivot in each sheet will
      be preserved independently.
  - name: Preserving external data connections
    text: Pivot tables that rely on external data sources keep the connection string
      after copying. However, the destination file must have access to the same data
      source. Verify the connection by opening the pivot and checking the **Data**
      tab.
  - name: Dealing with merged cells
    text: If the source range contains merged cells, Aspose.Cells copies the merge
      layout automatically. Still, validate the result if the destination workbook
      uses a different default column width.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- Pivot table
- Data manipulation
title: Jak zkopírovat kontingenční tabulky mezi sešity Excelu v Javě
url: /cs/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak kopírovat kontingenční tabulky mezi sešity Excelu v Javě

Pokud potřebujete **how to copy pivot** tabulky z jednoho souboru Excel do druhého, tento průvodce vám poskytne připravené řešení. Na konci prvních dvou vět budete přesně vědět, které volání API zachovají definici kontingenční tabulky při kopírování datového rozsahu.

Také se naučíte, jak **copy range between workbooks**, **duplicate Excel range** objekty, a bezpečně **copy range to workbook** bez ztráty vzorců nebo formátování. Není potřeba žádné externí skripty – stačí jeden projekt v Javě, který používá Aspose.Cells for Java.

## Požadavky

* Java Development Kit 17 nebo novější.
* Maven nebo Gradle pro správu závislostí.
* Platná licence Aspose.Cells for Java (bezplatná zkušební verze funguje pro testování).
* Dva soubory Excel: `source.xlsx` (obsahuje kontingenční tabulku) a prázdný `destination.xlsx` (nebo nechte kód jej vytvořit).

## Krok 1: Nastavení Maven projektu

Vytvořte soubor `pom.xml`, který zahrnuje Aspose.Cells. Tato závislost vám poskytne třídy `Workbook`, `Worksheet` a `Range` používané v příkladu.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>excel-pivot-copy</artifactId>
    <version>1.0.0</version>
    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>24.10</version> <!-- latest at time of writing -->
        </dependency>
    </dependencies>
</project>
```

> **Tip:** Udržujte verzi Aspose.Cells aktuální; novější vydání přidávají lepší podporu pro složité struktury pivot cache.

## Krok 2: Načtení zdrojového sešitu, který obsahuje kontingenční tabulku

První blok kódu ukazuje **how to copy excel** data načtením zdrojového souboru. Konstruktor `Workbook` načte celý soubor do paměti a zachová všechny objekty listů, včetně kontingenčních tabulek.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Access the first worksheet (index 0) where the pivot resides
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Proč je to důležité:* Aspose.Cells ukládá kontingenční tabulky jako součást interního modelu listu. Načtení sešitu zajišťuje, že pivot cache je k dispozici pro pozdější kopírování.

## Krok 3: Definování rozsahu, který zahrnuje kontingenční tabulku

Kontingenční tabulka může zasahovat do více řádků a sloupců. Ve většině případů můžete zkopírovat celý použitý rozsah listu. Metoda `createRange` vytvoří objekt `Range`, který bude zpracován při operaci kopírování.

```java
        // Define the range to copy – includes the pivot table and its source data
        // Adjust the address if your pivot occupies a different block
        Range srcRange = srcWs.getCells().createRange("A1:H20");
```

Pokud se kontingenční tabulka rozšiřuje za `H20`, stačí změnit řetězec adresy. Tento krok je jádrem zpracování **duplicate excel range**; objekt rozsahu zná vzorce, styly a skryté řádky.

## Krok 4: Vytvoření nového sešitu, který přijme zkopírovaný rozsah

Můžete začít s prázdným sešitem nebo načíst existující cílový soubor. Zde vytvoříme nový sešit, což je nejčistší způsob, jak **copy range to workbook**.

```java
        // Create a new workbook for the destination
        Workbook destWb = new Workbook(); // starts with one default sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

> **Poznámka:** Pokud potřebujete zkopírovat kontingenční tabulku do konkrétního názvu listu, přejmenujte `destWs` pomocí `destWs.setName("Report")` před vložením.

## Krok 5: Kopírování rozsahu – Aspose.Cells automaticky zachovává kontingenční tabulku

Metoda `copy` přenese vše uvnitř zdrojového rozsahu, včetně definice kontingenční tabulky, cache a formátování. Není potřeba žádný další kód k zachování funkčnosti kontingenční tabulky.

```java
        // Copy the range to the destination worksheet; pivot tables are preserved automatically
        srcRange.copy(destWs.getCells().createRange("A1"));
```

*Proč to funguje:* Aspose.Cells považuje kontingenční tabulku za kolekci skrytých buněk a metadat připojených k rozsahu. Když zavoláte `copy`, knihovna replikuje tato metadata v cílovém sešitu.

## Krok 6: Uložení cílového sešitu

Nakonec výsledek zapíšete na disk. Uložený soubor obsahuje identickou kontingenční tabulku, kterou můžete aktualizovat nebo upravit stejně jako originál.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");

        System.out.println("Pivot table copied successfully.");
    }
}
```

Spuštění programu vypíše potvrzení a vytvoří `destination.xlsx` s plně funkční kontingenční tabulkou.

## Kompletní, spustitelný příklad

Spojením všech kroků dohromady vypadá kompletní třída Java takto:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load source workbook with pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot and its source data
        Range srcRange = srcWs.getCells().createRange("A1:H20");

        // 3️⃣ Prepare destination workbook (blank by default)
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // 4️⃣ Copy range – pivot table is kept intact
        srcRange.copy(destWs.getCells().createRange("A1"));

        // 5️⃣ Save the new file
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

### Očekávaný výstup

* Konzole: `Pivot table copied successfully.`
* `destination.xlsx` se otevře v Excelu s kontingenční tabulkou identickou s tou v `source.xlsx`. Aktualizace kontingenční tabulky ukáže stejný zdroj dat, což dokazuje, že **how to copy pivot** funguje podle očekávání.

## Řešení běžných variant

### Kopírování více listů

Pokud váš projekt vyžaduje kopírování několika listů, projděte smyčkou listy sešitu a opakujte kroky 2‑4 pro každý list. Kontingenční tabulka v každém listu bude zachována nezávisle.

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet src = srcWb.getWorksheets().get(i);
    Worksheet dest = destWb.getWorksheets().add();
    src.getCells().copy(dest.getCells());
}
```

### Zachování externích datových připojení

Kontingenční tabulky, které závisí na externích zdrojích dat, si po kopírování zachovají řetězec připojení. Cílový soubor však musí mít přístup ke stejnému datovému zdroji. Ověřte připojení otevřením kontingenční tabulky a kontrolou záložky **Data**.

### Práce se sloučenými buňkami

Pokud zdrojový rozsah obsahuje sloučené buňky, Aspose.Cells automaticky zkopíruje rozložení sloučení. Přesto výsledek ověřte, pokud cílový sešit používá jinou výchozí šířku sloupce.

## Nejlepší postupy pro spolehlivé kopírování

| Postup | Důvod |
|----------|--------|
| Použijte přesný použitý rozsah (`srcWs.getCells().getMaxDisplayRange()`) místo pevně zadané adresy | Zaručuje, že je zahrnuta celá kontingenční tabulka i její zdrojová data. |
| Aplikujte licenci před náročnými operacemi | Zabrání vodoznaku z hodnocení a zlepšuje výkon. |
| Obnovte kontingenční tabulku po kopírování (`pivotTable.refresh()`), pokud se zdrojová data změnila | Zajišťuje, že cíl odráží nejnovější hodnoty. |
| Napište jednotkové testy, které otevřou cílový sešit a ověří, že `pivotTable.getPivotFields().size()` odpovídá zdroji | Detekuje náhodnou ztrátu polí během budoucích změn kódu. |

## Závěr

Nyní víte, jak **how to copy pivot** tabulky mezi sešity Excelu v Javě, stejně jako jak **copy range between workbooks**, **duplicate excel range** a **copy range to workbook** při zachování veškerého formátování a vzorců. Příklad používá Aspose.Cells, který abstrahuje nízkoúrovňové zpracování XML vyžadované OpenXML SDK.

Dále prozkoumejte související témata, jako je **updating pivot cache programmatically**, **exporting pivot data to CSV** nebo **creating pivot tables from scratch**. Každé z nich staví na stejných konceptech předvedených zde.

Šťastné programování a neváhejte experimentovat s většími rozsahy, více kontingenčními tabulkami nebo vlastním stylingem – stejný vzor platí ve všech scénářích.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java: A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}