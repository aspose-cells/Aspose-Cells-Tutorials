---
date: '2026-08-16'
description: Naučte se, jak přidat globalizaci v Javě pomocí Aspose.Cells, přizpůsobit
  chybové zprávy v Excelu a nastavit závislost Maven.
keywords:
- how to add globalization
- custom excel error messages
- aspose.cells maven dependency
lastmod: '2026-08-16'
og_description: Naučte se, jak přidat globalizaci v Javě pomocí Aspose.Cells, přizpůsobit
  chybové zprávy v Excelu a nastavit závislost Maven. Postupujte podle průvodce krok
  za krokem.
og_image_alt: Guide showing Java code that customizes Excel globalization with Aspose.Cells
og_title: Jak přidat globalizaci v Javě s Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-16'
  description: Learn how to add globalization in Java using Aspose.Cells, customize
    Excel error messages, and set up the Maven dependency.
  headline: How to add globalization in Java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. Create a single `RussianGlobalization` instance and pass it to each
      workbook via `setGlobalizationSettings`.
    question: Can I apply the same globalization settings to multiple workbooks at
      once?
  - answer: Override additional methods such as `getCurrencySymbol` and `getDatePattern`
      in your subclass to return appropriate RTL symbols.
    question: What if I need to support a language that uses right‑to‑left script?
  - answer: No. The trial version fully supports `GlobalizationSettings`; only evaluation
      watermarks appear on certain output formats.
    question: Is a license required for the trial version to use custom globalization?
  - answer: Insert `System.out.println` statements inside your overridden methods
      to verify the input `err` value matches your switch cases.
    question: How do I debug incorrect error strings?
  - answer: Negligibly. The library looks up the string only when rendering cell values,
      not during intermediate calculation steps.
    question: Does this affect formula calculation speed?
  type: FAQPage
tags:
- globalization
- Aspose.Cells
- Java internationalization
- Excel localization
title: Jak přidat globalizaci v Javě s Aspose.Cells
url: /cs/java/calculation-engine/custom-globalization-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-container >}}

{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Jak přidat globalizaci v Javě s Aspose.Cells

## Úvod

Přidání globalizace do vašeho Java sešitu vám umožní zobrazovat chybové zprávy, boolean hodnoty a další řetězce specifické pro locale v jazyce, který vaši uživatelé očekávají. V tomto tutoriálu se naučíte **jak přidat globalizaci** pro ruštinu, ale stejný vzor funguje pro jakýkoli jazyk. Na konci průvodce budete schopni:

- Přepsat výchozí text chyb a reprezentace boolean hodnot.
- Použít vlastní nastavení na libovolnou instanci `Workbook`.
- Integrovat řešení do typického Maven‑založeného Java projektu.

Připraveni učinit vaše Excel soubory skutečně vícejazyčnými? Nejprve ověřme, že vaše vývojové prostředí splňuje předpoklady.

## Rychlé odpovědi
- **Co je globalizace v Aspose.Cells?** Jedná se o sadu řetězců citlivých na locale (chyby, booleany atd.), které můžete nahradit vlastním textem.  
- **Který Maven artefakt je vyžadován?** `com.aspose:aspose-cells:25.3`.  
- **Mohu cílit na jazyky jiné než ruštinu?** Ano – rozšiřte `GlobalizationSettings` a přepište potřebné metody pro každé locale.  
- **Potřebuji licenci pro vývoj?** Bezplatná zkušební verze funguje pro testování; trvalá licence odstraňuje vodotisky hodnocení.  
- **Je řešení thread‑safe?** Nastavte konfiguraci pro každý sešit; objekt `GlobalizationSettings` je po vytvoření neměnný.

## Co je globalizace v Aspose.Cells?

`GlobalizationSettings` je konfigurační objekt Aspose.Cells, který řídí řetězce specifické pro locale, jako jsou chybové zprávy, boolean hodnoty, symboly měn a formáty dat. Poskytnutím vlastní podtřídy řeknete knihovně, jaký text má zobrazovat pro každou kulturu, což vám umožní nahradit výchozí anglické řetězce překlady odpovídajícími jazyku a regionálním konvencím koncového uživatele.

## Proč přidat vlastní globalizaci?

Aspose.Cells podporuje **více než 50 vstupních a výstupních formátů** – včetně XLSX, CSV, PDF a ODS – a dokáže zpracovat sešity s **až 200 000 řádky** bez načítání celého souboru do paměti. Přizpůsobení globalizace zajišťuje, že koncoví uživatelé vidí zprávy ve svém rodném jazyce, což snižuje počet požadavků na podporu o odhadovaných **30 %** u nadnárodních nasazení.

## Předpoklady

- **Java Development Kit** 8 nebo novější.
- **IDE** jako IntelliJ IDEA nebo Eclipse.
- **Aspose.Cells for Java** verze 25.3 (nebo novější) přidaná přes Maven nebo Gradle.

### Nastavení Aspose.Cells pro Java

Přidejte Maven závislost do vašeho `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Nebo, pokud dáváte přednost Gradlu, vložte následující do `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Získání licence

Aspose nabízí několik možností licencování:

- **Bezplatná zkušební verze** – plnohodnotné hodnocení po dobu 30 dnů.  
- **Dočasná licence** – neomezené hodnocení bez vodotisků.  
- **Komerní licence** – připravená pro produkci, s prioritní podporou.

Po získání licenčního souboru jej nastavte jednou při spuštění aplikace:

```java
com.aspose.cells.License license = new com.aspose.cells.License();
license.setLicense("Aspose.Cells.lic");
```
```java
import com.aspose.cells.*;

public class InitializeAspose {
    public static void main(String[] args) {
        // Set the license if you have one
        License license = new License();
        try {
            license.setLicense("PathToYourLicenseFile.lic");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Create a new workbook instance
        Workbook workbook = new Workbook();
    }
}
```

## Jak přidat globalizaci pro ruštinu?

`Workbook` objekt představuje Excel soubor načtený do paměti, poskytující přístup k listům, buňkám a nastavením. Načtěte svůj sešit, vytvořte podtřídu `GlobalizationSettings` a připojte ji k sešitu. Přímá odpověď je: **vytvořit vlastní třídu `GlobalizationSettings`, přepsat `getErrorValueString` a `getBooleanValueString`, a poté zavolat `workbook.setGlobalizationSettings(customSettings)`**. Tento dvoustupňový přístup nahradí výchozí ruské řetězce vašimi vlastními.

### Definování vlastního nastavení

Poprvé, když v tomto průvodci odkazujete na `GlobalizationSettings`, všimněte si definice:

`GlobalizationSettings` je základní třída, kterou Aspose.Cells používá k získání řetězců specifických pro locale.  

Nyní vytvořte podtřídu, která vrací text specifický pro ruštinu:

```java
class RussianGlobalization extends GlobalizationSettings {
    @Override
    public String getErrorValueString(String err) {
        switch (err) {
            case "#DIV/0!": return "Деление на ноль";
            case "#N/A":    return "Недоступно";
            default:        return err; // fallback to original
        }
    }

    @Override
    public String getBooleanValueString(Boolean bv) {
        return bv ? "ИСТИНА" : "ЛОЖЬ";
    }
}
```
```java
import com.aspose.cells.*;

class RussianGlobalization extends GlobalizationSettings {
    public String getErrorValueString(String err) {
        switch (err.toUpperCase()) {
            case "#NAME?":
                return "#RussianName-имя?";
        }
        return "RussianError-ошибка";
    }

    public String getBooleanValueString(Boolean bv) {
        return bv ? "RussianTrue-правда" : "RussianFalse-ложный";
    }
}
```

### Aplikace nastavení na sešit

Po definování podtřídy ji připojte k libovolné instanci `Workbook`:

```java
Workbook wb = new Workbook("input.xlsx");
wb.setGlobalizationSettings(new RussianGlobalization());
wb.save("output.xlsx");
```
```java
import com.aspose.cells.*;
import AsposeCellsExamples.Utils; // Placeholder import

public void Run() throws Exception {
    String dataDir = "YOUR_DATA_DIRECTORY";
    String outDir = "YOUR_OUTPUT_DIRECTORY";

    Workbook wb = new Workbook(dataDir + "/sampleRussianGlobalization.xlsx");
    wb.getSettings().setGlobalizationSettings(new RussianGlobalization());
    
    wb.calculateFormula();
    wb.save(outDir + "/outputRussianGlobalization.pdf");
}
```

## Praktické aplikace

- **Finanční výkaznictví** – zobrazovat chybové kódy v rodném jazyce účetního, což snižuje nesprávné interpretace.  
- **Nástroje na úrovni podniku** – vložit stejnou logiku globalizace do desítek interních utilit založených na Excelu.  
- **Automatizované datové pipeline** – zajistit, aby podřízené systémy přijímaly hodnoty citlivé na locale bez dalších kroků překladu.

## Úvahy o výkonu

Když povolíte vlastní globalizaci, Aspose.Cells stále zpracovává vzorce a I/O se stejným vysokým výkonem. Pro udržení nízké spotřeby paměti:

- Uvolněte reference na sešit (`wb.dispose()`) po uložení.  
- Používejte `CalculationOptions.setEnableIterativeCalculation(true)` pouze když je to nutné.  
- Nastavte haldu JVM (`-Xmx2g`) pro sešity větší než 100 MB.

## Často kladené otázky

**Q: Mohu použít stejné nastavení globalizace na více sešitů najednou?**  
**A:** Ano. Vytvořte jedinou instanci `RussianGlobalization` a předávejte ji každému sešitu pomocí `setGlobalizationSettings`.

**Q: Co když potřebuji podporovat jazyk, který používá skript zprava doleva?**  
**A:** Přepište další metody, jako `getCurrencySymbol` a `getDatePattern`, ve vaší podtřídě, aby vracely vhodné RTL symboly.

**Q: Je licence vyžadována pro zkušební verzi k použití vlastní globalizace?**  
**A:** Ne. Zkušební verze plně podporuje `GlobalizationSettings`; pouze se na některých výstupních formátech zobrazují vodotisky hodnocení.

**Q: Jak ladit nesprávné chybové řetězce?**  
**A:** Vložte `System.out.println` výpisy do vašich přepsaných metod, abyste ověřili, že vstupní hodnota `err` odpovídá vašim případům ve switch.

**Q: Ovlivňuje to rychlost výpočtu vzorců?**  
**A:** Nezajímavě. Knihovna vyhledává řetězec pouze při vykreslování hodnot buněk, ne během mezivýpočtových kroků.

## Další zdroje

- **Dokumentace**: Prozkoumejte podrobné průvodce na [Dokumentace Aspose.Cells](https://reference.aspose.com/cells/java/)  
- **Stáhnout**: Získejte nejnovější verze na [Aspose Downloads](https://releases.aspose.com/cells/java/)  
- **Nákup**: Kupte licenci pro komerční použití na [Aspose Purchase](https://purchase.aspose.com/buy)  
- **Bezplatná zkušební verze**: Začněte s bezplatnou zkušební verzí na [Aspose Free Trial](https://releases.aspose.com/cells/java/)  
- **Dočasná licence**: Získejte dočasnou licenci prostřednictvím [Aspose Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Podpora**: Získejte pomoc od komunity na [Aspose Support Forum](https://forum.aspose.com/c/cells/9)

---

**Poslední aktualizace:** 2026-08-16  
**Testováno s:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose

## Související tutoriály

- [Aspose.Cells Java: Průvodce vlastním výpočetním enginem](/cells/java/calculation-engine/aspose-cells-java-custom-engine-guide/)
- [Jak používat Aspose Cells – Tutoriály Excel Engine pro Java](/cells/java/calculation-engine/)
- [Aspose Cells Maven závislost – Správa Excel datových spojení s Aspose.Cells v Javě](/cells/java/advanced-features/aspose-cells-java-excel-external-data-connections/)


{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

{{< /blocks/products/pf/main-container >}}

{{< blocks/products/pf/main-wrap-class >}}