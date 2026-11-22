---
category: general
date: 2026-11-22
description: Naučte se, jak nastavit locale v Java sešitu, změnit jazyk sešitu a nastavit
  kalendář na japonský s jasnými příklady kódu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set locale
- change workbook language
- set locale to japanese
- how to set calendar
language: cs
lastmod: 2026-11-22
og_description: Jak rychle nastavit locale v Java sešitu. Postupujte podle tohoto
  tutoriálu, změňte jazyk sešitu, nastavte locale na japonštinu a nakonfigurujte japonský
  kalendář.
og_image_alt: Screenshot showing how to set locale in a Java workbook
og_title: Jak nastavit locale v Java sešitu – krok za krokem průvodce
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  headline: How to set locale in a Java workbook using Aspose.Cells
  type: TechArticle
- description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  name: How to set locale in a Java workbook using Aspose.Cells
  steps:
  - name: Run the **FullLocaleExample** class.
    text: Run the **FullLocaleExample** class.
  - name: Open the generated `FullJapaneseLocale.xlsx` in Excel.
    text: Open the generated `FullJapaneseLocale.xlsx` in Excel.
  - name: 'Verify that:'
    text: 'Verify that:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Internationalization
- Workbook
title: Jak nastavit locale v Java sešitu pomocí Aspose.Cells
url: /cs/java/workbook-operations/how-to-set-locale-in-a-java-workbook-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak nastavit locale v Java sešitu pomocí Aspose.Cells

Nastavení locale v Java sešitu je běžná potřeba, když potřebujete přizpůsobit tabulku různým regionům. V tomto průvodci se naučíte, jak nastavit locale, změnit jazyk sešitu a nastavit kalendář na japonský pomocí API Aspose.Cells.

Internacionalizace sešitu jde dál než jen překlad textu; ovlivňuje také formáty čísel, parsování dat a výchozí kalendářní systém. Na konci tohoto tutoriálu budete schopni:

* Nakonfigurovat locale sešitu na japonštinu (Japonsko) – **set locale to japanese**.  
* Změnit jazyk sešitu, aby vzorce a řetězce UI respektovaly cílovou kulturu – **change workbook language**.  
* Přepnout kalendář na japonský imperiální kalendář – **how to set calendar**.  

Postupy fungují s jakoukoli aktuální verzí Aspose.Cells pro Java (v23.9 nebo novější) a vyžadují pouze standardní vývojové prostředí Java.

## Požadavky

| Požadavek | Důvod |
|-------------|--------|
| Java 8 nebo vyšší | Knihovna cílí na Java 8+. |
| Aspose.Cells for Java (v23.9+) | Poskytuje `Workbook`, `WorkbookSettings` a nástroje pro locale. |
| IDE (IntelliJ IDEA, Eclipse nebo VS Code) | Pro kompilaci a spuštění ukázky. |
| Základní znalost Javy | Potřebná k pochopení úryvků kódu. |

Přidejte Maven závislost Aspose.Cells do svého `pom.xml` (nebo si stáhněte JAR ručně):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust for your JDK version -->
</dependency>
```

## Jak nastavit locale a kalendář v sešitu

Prvním krokem je vytvořit instanci sešitu a získat její objekt nastavení. Objekt nastavení vystavuje API pro locale a kalendář.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import java.util.Locale;
import java.util.Calendar;

public class WorkbookLocaleDemo {
    public static void main(String[] args) {
        // Step 1: Create a new workbook (empty by default)
        Workbook workbook = new Workbook();

        // Step 2: Access the workbook's settings
        WorkbookSettings settings = workbook.getSettings();

        // Step 3: Set the calendar to the Japanese calendar
        // Aspose.Cells uses java.util.Calendar; the Japanese calendar is available via Calendar.JAPANESE
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // Step 4: Set the locale to Japanese (Japan)
        // This influences number formats, date formats, and built‑in function behaviour.
        settings.setLocale(new Locale("ja", "JP"));

        // Optional: Save the workbook to verify the settings
        workbook.save("LocaleDemo.xlsx");
    }
}
```

### Proč je každý řádek důležitý

* **`new Workbook()`** – Vytvoří prázdný sešit, který můžete upravovat před uložením.  
* **`getSettings()`** – Vrací objekt `WorkbookSettings`; všechny regionální možnosti jsou zde.  
* **`setCalendar(...)`** – Nahrazuje výchozí gregoriánský kalendář japonským imperiálním kalendářem, což ovlivňuje, jak jsou data zobrazována a parsována.  
* **`setLocale(new Locale("ja","JP"))`** – Mění jazyk a regionální konvence (např. měsíce, desetinné oddělovače). Toto je jádro **how to set locale** pro sešit.  

Spuštěním programu se vytvoří `LocaleDemo.xlsx`. Otevřete jej v Excelu nebo LibreOffice a uvidíte japonské názvy měsíců, symboly japonského jenu a data formátovaná podle japonského kalendáře.

## Změna jazyka sešitu (nastavit locale na japonštinu)

Pokud je vaším hlavním cílem **change workbook language**, můžete se soustředit jen na volání `setLocale`. Následující úryvek izoluje tento krok:

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Change only the language to Japanese (Japan)
settings.setLocale(new Locale("ja", "JP"));
workbook.save("JapaneseLanguage.xlsx");
```

**Co se změní?**  
* Řetězce formátování buněk přejdou do japonštiny (např. `#,##0.00` se zobrazí s japonským znakem jenu).  
* Vestavěné názvy funkcí (jako `SUM`) zůstávají v angličtině, protože jazyk funkcí v Excelu je nezávislý, ale řetězce dat a chybové zprávy následují japonské konvence.  

**Kdy to použít?**  
* Když potřebujete tabulku, která zobrazuje čísla a data pro japonské publikum, ale výchozí kalendář může zůstat gregoriánský.  
* Pro zprávy exportované do PDF nebo tištěné, aby vizuální jazyk odpovídal cílovému trhu.

## Jak nastavit kalendář na japonský kalendář

Někdy je požadavek **how to set calendar** oddělený od locale. Pro starší systémy, které ukládají data v japonské imperiální éře, musíte kalendář nastavit explicitně a volitelně si ponechat výchozí locale.

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Set only the calendar; keep the default (US) locale
settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

// Verify the calendar by creating a date cell
int row = 0, column = 0;
workbook.getWorksheets().get(0).getCells().putValue(row, column, new java.util.Date());

// Save to see the Japanese era (e.g., "R3/04/01" for Reiwa 3)
workbook.save("JapaneseCalendar.xlsx");
```

**Klíčové body:**

* `Calendar.getInstance(Locale.JAPAN)` vrací `java.util.Calendar` nakonfigurovaný pro japonskou éru.  
* Sešit nyní bude zobrazovat data pomocí symbolů éry (R pro Reiwa, H pro Heisei atd.).  
* Toto nastavení **neovlivňuje** formátování čísel ani jazyk UI; pokud potřebujete obojí, kombinujte jej s `setLocale`.

## Kompletní end‑to‑end příklad

Níže je kompletní, spustitelný program, který demonstruje **how to set locale**, **change workbook language** a **set the calendar** v jednom koherentním toku. Přidává také ukázkovou buňku pro ilustraci efektu.

```java
import com.aspose.cells.*;
import java.util.*;

public class FullLocaleExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 1️⃣ Set the locale to Japanese (Japan) – changes language & number formats
        settings.setLocale(new Locale("ja", "JP"));

        // 2️⃣ Set the calendar to the Japanese imperial calendar
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // 3️⃣ Add a sample date and number to visualize the changes
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Date cell – will show Japanese era after applying the calendar
        cells.putValue(0, 0, new Date());

        // Number cell – will use Japanese Yen symbol and comma separator
        cells.putValue(1, 0, 1234567.89);

        // Apply a style to the number cell for currency formatting
        Style style = cells.getRows().get(1).getStyle();
        style.setNumber(3); // Built‑in currency format
        cells.getRows().get(1).setStyle(style);

        // Save the workbook
        workbook.save("FullJapaneseLocale.xlsx");
        System.out.println("Workbook created with Japanese locale and calendar.");
    }
}
```

**Očekávaný výstup:**  
Otevřením `FullJapaneseLocale.xlsx` uvidíte první buňku s datem jako `R3/04/01` (Reiwa 3) a druhou buňku formátovanou jako `¥1,234,567.89`. To potvrzuje, že **how to set locale**, **change workbook language** a **how to set calendar** fungují společně.

## Časté úskalí a jak se jim vyhnout

| Úskalí | Proč se to děje | Řešení |
|---------|----------------|-----|
| Použití `Locale.CHINA` místo `new Locale("ja","JP")` | `Locale.CHINA` nastaví čínský jazyk, ne japonský. | Vždy vytvářejte `Locale` s `"ja", "JP"` pro japonštinu. |
| Zapomenutí zavolat `settings.setCalendar(...)` po `setLocale` | Kalendář zůstane gregoriánský, takže data se zobrazí ve špatné éře. | Zavolejte `setCalendar` **po** nastavení locale, nebo nastavte obojí najednou, jak je ukázáno. |
| Uložení sešitu před aplikací nastavení | Nastavení se aplikuje na objekt v paměti; předčasné uložení zapíše výchozí locale. | Aplikujte všechny změny locale/kalendáře **před** voláním `workbook.save()`. |
| Použití zastaralé verze Aspose.Cells | Starší verze postrádají přetížení `setCalendar`. | Upgradujte na v23.9+ nebo zkontrolujte poznámky k vydání ohledně podpory locale. |

## Testování vaší konfigurace

1. Spusťte třídu **FullLocaleExample**.  
2. Otevřete vygenerovaný soubor `FullJapaneseLocale.xlsx` v Excelu.  
3. Ověřte, že:  
   * Sloupec s daty zobrazuje japonské symboly éry (`R`, `H` atd.).  
   * Sloupec s čísly používá znak jenu a čárkové oddělovače.  
   * Jakékoli vestavěné chybové zprávy (např. `#DIV/0!`) se zobrazují v japonštině, pokud sešit obsahuje chyby.  

Pokud některá z těchto kontrol selže, zkontrolujte, že objekt `WorkbookSettings`, který jste upravili, je stejná instance použitá při ukládání.

## Další kroky

* **Lokalizace vzorců** – Zatímco locale řídí formátování, můžete také přeložit vlastní názvy funkcí pomocí `FormulaParser`.  
* **Aplikace locale na existující sešity** – Načtěte sešit pomocí `new Workbook`  

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich projektech.

- [Aspose Cells Date Format: How to Set Custom Date Format in Java](/cells/english/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/)
- [How to Set Language in Excel Files Using Aspose.Cells .NET for Multilingual Support](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [How to set cell number format and convert Japanese dates in C# using Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}