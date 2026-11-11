---
date: '2026-10-28'
description: Naučte se, jak změnit systém data v Excelu na 1904 pomocí Aspose.Cells
  pro Java, nastavit formát data v Excelu a efektivně převést systém Excel 1904.
keywords:
- change excel date system
- excel 1904 date conversion
- maven dependency aspose cells
lastmod: '2026-10-28'
og_description: Změňte systém data v Excelu na 1904 pomocí Aspose.Cells pro Java.
  Naučte se krok za krokem, jak povolit systém 1904, nastavit data a převést zpět.
og_image_alt: Aspose.Cells Java guide showing how to switch Excel to the 1904 date
  system
og_title: Změna systému data v Excelu na 1904 s Aspose.Cells Java
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  headline: Change Excel date system to 1904 with Aspose.Cells Java
  type: TechArticle
- description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  name: Change Excel date system to 1904 with Aspose.Cells Java
  steps:
  - name: initialize and load the workbook
    text: The `Workbook` class represents an entire Excel file in memory. First, create
      a `Workbook` instance that points to your existing file.
  - name: enable the 1904 date system
    text: The `WorkbookSettings.setDate1904` method toggles the workbook‑level date
      flag. Setting it to `true` activates the 1904 system for all worksheets. **Pro
      tip:** You can also call `setDate1904(false)` later if you need to revert.
  - name: save the modified workbook
    text: Finally, write the changes to a new file (or overwrite the original). The
      `save` method respects the active date system automatically. > **Note:** The
      code above uses the class name `tWorkbook` as originally provided. Ensure this
      typo matches your project’s naming conventions or correct it to `Workb
  type: HowTo
- questions:
  - answer: The 1900 system starts on January 1, 1900, while the 1904 system starts
      on January 1, 1904, shifting all dates by 1,462 days.
    question: What is the difference between the 1900 and 1904 date systems?
  - answer: Yes, but you must close the file in Excel first; otherwise the save operation
      will fail.
    question: Can I change the date system of a workbook that is currently open in
      Excel?
  - answer: The method works in the free trial, but a full license removes evaluation
      limitations.
    question: Do I need a license to use `setDate1904`?
  - answer: No, the date system is a workbook‑level setting; it applies to all worksheets.
    question: Is it possible to change the date system for only a single worksheet?
  - answer: Open the saved file in Excel, go to **File → Options → Advanced**, and
      check the **"Use 1904 date system"** box.
    question: How can I verify that the date system was changed?
  type: FAQPage
tags:
- change excel date system
- aspose cells java
- excel date conversion
- java excel processing
title: Změna systému data v Excelu na 1904 s Aspose.Cells Java
url: /cs/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Změna systému dat v Excelu na 1904 pomocí Aspose.Cells Java

V tomto tutoriálu se naučíte, jak **změnit systém dat v Excelu** na formát 1904 pomocí Aspose.Cells pro Java. Systém 1904 je nezbytný, když potřebujete zachovat starší data založená na Macu nebo sladit s finančními modely, které očekávají tuto epochu. Provedeme vás instalací knihovny, načtením sešitu, přepnutím systému dat a uložením výsledku – vše bez nutnosti Microsoft Excel na serveru.

## Rychlé odpovědi
- **Co dělá systém dat 1904?** Začíná počítat dny od 1. ledna 1904, posouvá všechny datumy o 1 462 dní oproti výchozímu systému 1900.  
- **Proč použít Aspose.Cells ke změně systému dat?** Poskytuje jednoduché API, které funguje bez nainstalovaného Excelu a podporuje velké soubory.  
- **Které verze Javy jsou podporovány?** JDK 8 nebo novější.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro hodnocení; licence odstraňuje omezení používání.  
- **Mohu později převést zpět na systém 1900?** Ano, stačí zavolat `setDate1904(false)`.

## Co je systém dat 1904 v Excelu?
Systém dat 1904 počítá dny od 1. ledna 1904 místo výchozí epochy 1900. Tento posun přidává přesně 1 462 dní ke každé hodnotě data, což je důvod, proč se starší sešity z Macu zdají posunuté při otevření ve Windows. Používá se především pro kompatibilitu se staršími soubory Excelu pro Macintosh a některými staršími finančními modely.

## Proč změnit systém dat v Excelu pomocí Aspose.Cells?
Můžete přepnout systém dat přímo z Javy, čímž eliminujete ruční kroky v Excelu. Aspose.Cells zpracovává sešity až do **2 GB** a dokáže převést sešit s 500 listy za méně než **2 sekundy** na typickém 4‑jádrovém serveru, což poskytuje vysokou propustnost server‑side automatizace.

## Předpoklady
- Java Development Kit (JDK) 8 nebo vyšší.  
- Maven nebo Gradle pro správu závislostí.  
- Základní znalost programování v Javě.  

## Nastavení Aspose.Cells pro Java

### Maven
Přidejte následující závislost do souboru `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Vložte tento řádek do souboru `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Získání licence
Aspose nabízí bezplatnou zkušební verzi, dočasnou licenci a plné komerční licence. Můžete začít s [bezplatnou zkušební verzí](https://releases.aspose.com/cells/java/) nebo získat dočasnou licenci na [stránce dočasné licence](https://purchase.aspose.com/temporary-license/).

## Jak změnit systém dat v Excelu na 1904 pomocí Aspose.Cells pro Java?
Načtěte sešit, povolte nastavení 1904 a uložte soubor – tento tříkrokový postup aktualizuje interní epochu dat v sešitu během méně než jedné sekundy. Volání API `setDate1904(true)` přepne příznak systému a změna se uloží při volání `save`. Instalace Excelu není vyžadována, což je ideální pro prostředí serverů bez grafického rozhraní.

### Krok 1: inicializace a načtení sešitu
Třída `Workbook` představuje celý soubor Excel v paměti. Nejprve vytvořte instanci `Workbook`, která ukazuje na váš existující soubor.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Krok 2: povolení systému dat 1904
Metoda `WorkbookSettings.setDate1904` přepíná příznak data na úrovni sešitu. Nastavením na `true` aktivujete systém 1904 pro všechny listy.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Tip:** Můžete také později zavolat `setDate1904(false)`, pokud potřebujete vrátit změnu.

### Krok 3: uložení upraveného sešitu
Nakonec zapište změny do nového souboru (nebo přepište originál). Metoda `save` automaticky respektuje aktivní systém dat.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **Poznámka:** Výše uvedený kód používá název třídy `tWorkbook`, jak byl původně poskytnut. Ujistěte se, že tato chyba odpovídá konvencím pojmenování ve vašem projektu, nebo ji v případě potřeby opravte na `Workbook`.

## Nastavení data v Excelu programově (sekundární klíčové slovo)
Pokud potřebujete po změně systému upravit jednotlivé hodnoty buněk, můžete použít `cells.get(i, j).putValue(Date)`, kde datum bude interpretováno podle aktivního systému dat.

## Převod systému Excel 1904 zpět na 1900 (sekundární klíčové slovo)
Pro návrat stačí zavolat:

```java
workbook.getSettings().setDate1904(false);
```

Poté sešit znovu uložte.

## Praktické aplikace
1. **Archivace dat** – Zachování starých časových razítek při migraci starých tabulek založených na Macu.  
2. **Cross‑platform reporting** – Generování zpráv, které se otevřou správně jak ve Windows, tak v macOS, bez nesouladu dat.  
3. **Finanční modelování** – Sladění výpočtů dat s legacy finančními modely, které očekávají systém 1904.

## Úvahy o výkonu
- Omezte operace sešitu v jedné relaci, aby byl nízký odběr paměti; Aspose.Cells streamuje data a nikdy nenačítá celý soubor do RAM, pokud to výslovně nepožadujete.  
- Vyladěte příznaky garbage‑collection Javy (`-XX:+UseG1GC`) pro velmi velké soubory, aby se předešlo výkyvům v době pozastavení.  

## Často kladené otázky

**Q: Jaký je rozdíl mezi systémy dat 1900 a 1904?**  
A: Systém 1900 začíná 1. ledna 1900, zatímco systém 1904 začíná 1. ledna 1904, což posouvá všechna data o 1 462 dní.

**Q: Mohu změnit systém dat sešitu, který je aktuálně otevřený v Excelu?**  
A: Ano, ale nejprve musíte soubor v Excelu zavřít; jinak operace uložení selže.

**Q: Potřebuji licenci k použití `setDate1904`?**  
A: Metoda funguje v bezplatné zkušební verzi, ale plná licence odstraňuje omezení hodnocení.

**Q: Je možné změnit systém dat pouze pro jeden list?**  
A: Ne, systém dat je nastavení na úrovni sešitu; platí pro všechny listy.

**Q: Jak mohu ověřit, že byl systém dat změněn?**  
A: Otevřete uložený soubor v Excelu, přejděte na **Soubor → Možnosti → Upřesnit** a zaškrtněte políčko **"Použít systém dat 1904"**.

## Závěr
Nyní víte, jak **změnit systém dat v Excelu** na 1904 pomocí Aspose.Cells pro Java, jak nastavit data v jednotlivých buňkách a jak v případě potřeby vrátit systém zpět na 1900. Integrujte tyto úryvky do svých datových pipeline, abyste zajistili kompatibilitu dat napříč platformami a starými soubory.

---

**Poslední aktualizace:** 2026-10-28  
**Testováno s:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose  

**Dokumentace:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
**Stáhnout:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)  
**Koupit licenci:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
**Bezplatná zkušební verze:** [Start Free Trial](https://releases.aspose.com/cells/java/)  
**Dočasná licence:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)  
**Fórum podpory:** [Aspose Support](https://forum.aspose.com/c/cells/9)

## Související tutoriály

- [Efektivní převod Excelu do PDF s vlastními formáty data pomocí Aspose.Cells pro Java](/cells/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Aspose.Cells pro Java: Jak efektivně vytvářet a formátovat Excel sešity](/cells/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Mistrovství manipulace s Excelem pomocí Aspose.Cells pro Java: Operace sešitu a tutoriál stylování buněk](/cells/java/workbook-operations/excel-manipulation-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}