---
category: general
date: 2026-06-21
description: Aspose Cells průvodce formátem data – naučte se, jak nastavit vlastní
  formát data, změnit lokalizaci sešitu a použít globální formát data v Javě.
draft: false
keywords:
- aspose cells date format
- set custom date format
- how to set date format
- change workbook locale
- set global date format
language: cs
og_description: 'Návod na formát data v Aspose Cells: naučte se, jak nastavit vlastní
  formát data, změnit jazyk sešitu a nastavit globální formát data pro projekty v
  Javě.'
og_title: 'Aspose Cells – Formát data: nastavení vlastního formátu data v Javě'
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Aspose Cells date format guide – learn how to set custom date format,
    change workbook locale, and apply a global date format in Java.
  headline: 'Aspose Cells Date Format: How to Set Custom Date Format in Java'
  type: TechArticle
- description: Aspose Cells date format guide – learn how to set custom date format,
    change workbook locale, and apply a global date format in Java.
  name: 'Aspose Cells Date Format: How to Set Custom Date Format in Java'
  steps:
  - name: 1. Overriding the Global Format at the Cell Level
    text: 'If a cell already has a style with a specific number format, the global
      setting is ignored for that cell. To force the global format, clear the cell’s
      style:'
  - name: 2. Changing Workbook Locale Without a Custom Pattern
    text: 'Sometimes you just want to **change workbook locale** so that built‑in
      date formats (like `14‑03‑2024`) follow regional conventions. You can do this
      without a `DateTimeFormatter`:'
  - name: 3. Using Multiple Custom Formats in One Workbook
    text: 'Aspose Cells allows you to define several custom formats and apply them
      selectively:'
  - name: 4. Resetting to the Default Format
    text: 'If you need to revert to Aspose’s default date handling, simply pass `null`:'
  type: HowTo
- questions:
  - answer: Yes—any worksheet loaded into the `Workbook` after you set the global
      format will inherit it, unless a cell already has an explicit style.
    question: Does this affect existing worksheets?
  - answer: Absolutely. The global format is applied at render time, so you can populate
      cells first and set the format later.
    question: Can I set the format after writing data?
  - answer: Use the appropriate `CultureInfo` code (`"th-TH"`), and the formatter
      will respect that calendar automatically.
    question: What if I need a locale‑specific calendar (e.g., Thai Buddhist)?
  - answer: Negligible. The formatter is cached inside `WorkbookSettings`, so the
      overhead is only incurred once per workbook.
    question: Is there a performance penalty?
  type: FAQPage
tags:
- aspose-cells
- java
- date-formatting
title: 'Formát data v Aspose Cells: Jak nastavit vlastní formát data v Javě'
url: /cs/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Cells Date Format – Kompletní průvodce pro Javu

Už jste se někdy zamýšleli, jak nastavit vlastní formát data v Aspose Cells pro Javu? Nejste v tom sami. Ať už generujete zprávy pro japonského klienta nebo jen potřebujete jednotný styl data v celém sešitu, zvládnutí **aspose cells date format** je nezbytné.

V tomto tutoriálu vás provedeme praktickým příkladem od začátku do konce, který ukazuje **jak nastavit formát data** globálně, změnit locale sešitu a použít vlastní vzor, například japonský rok éry. Na konci budete mít znovupoužitelný úryvek, který můžete vložit do libovolného projektu – bez hádání.

## Co tento průvodce pokrývá

- Vytvoření nové instance `Workbook`.
- Změna locale sešitu, aby vestavěné formáty respektovaly regionální pravidla.
- Definování **vlastního formátu data** pomocí `DateTimeFormatter`.
- Aplikace tohoto formátu globálně pomocí `WorkbookSettings`.
- Běžné úskalí (např. přepisování formátů na úrovni buňky) a jak se jim vyhnout.
- Rychlé varianty pro jiné locale nebo řetězce formátů.

Potřebujete jen vývojové prostředí Javy, Maven nebo Gradle pro stažení Aspose Cells a základní znalost syntaxe Javy. Připravení? Ponořme se.

## Krok 1: Nastavte svůj projekt a importujte Aspose Cells

Nejprve se ujistěte, že Aspose Cells pro Javu je ve vaší classpath. Pokud používáte Maven, přidejte následující závislost do svého `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

Uživatelé Gradle mohou přidat:

```gradle
implementation 'com.aspose:aspose-cells:24.9'
```

> **Tip:** Aspose nabízí bezplatnou 30‑denní zkušební licenci. Umístěte soubor `Aspose.Cells.lic` do kořenového adresáře projektu a zavolejte `License license = new License(); license.setLicense("Aspose.Cells.lic");` před vytvořením jakéhokoli sešitu.

Nyní importujte třídy, které budeme potřebovat:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import com.aspose.cells.DateTimeFormatter;
import com.aspose.cells.CultureInfo;
```

Tyto importy nám poskytují přístup k objektu sešitu, jeho nastavením a locale‑citlivému formátovači.

## Krok 2: Vytvořte nový sešit a přistupte k jeho nastavením

Nový `Workbook` začíná s výchozím (obvykle US) locale. Pro globální řízení zpracování dat musíme získat jeho objekt `WorkbookSettings`:

```java
// Step 2: Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the settings object – this is where we’ll apply the date format
WorkbookSettings settings = workbook.getSettings();
```

Objekt `settings` je centrální uzel. Cokoli zde změníte – například formát data – ovlivní každou buňku, která **nemá** již explicitní styl, který by to přepisoval.

## Krok 3: Definujte vlastní formát data/času (příklad japonské éry)

Řekněme, že potřebujete data ve formátu japonské éry, např. „令和04.10.01“. Vzor `"ggyy.MM.dd"` funguje, pokud je spárován s japonskou kulturou:

```java
// Step 3: Build a formatter for the Japanese era year
DateTimeFormatter formatter = new DateTimeFormatter(
        "ggyy.MM.dd",                // Pattern: era (gg), year (yy), month, day
        new CultureInfo("ja-JP")    // Locale: Japanese (Japan)
);
```

Pokud dáváte přednost jednoduššímu ISO stylu (`"yyyy-MM-dd"`), stačí nahradit řetězec vzoru – žádné další změny nejsou potřeba.

## Krok 4: Aplikujte vlastní formát jako globální formát data

Nyní svázeme formátovač s globálními nastaveními sešitu. Toto je krok **nastavení globálního formátu data**, který zajišťuje, že každá buňka zobrazující datum automaticky použije náš vzor:

```java
// Step 4: Apply the custom formatter globally
settings.setDateTimeFormat(formatter);
```

V tomto okamžiku se jakékoli datum, které zapíšete do listu – ať už pomocí `Cell.putValue(new Date())` nebo načtením z datového zdroje – zobrazí pomocí japonského vzoru éry.

## Krok 5: Naplňte sešit ukázkovými daty (volitelné)

Přidejme několik řádků, abyste viděli formát v akci. Tato část není striktně nutná pro logiku formátování data, ale pomáhá ověřit, že vše funguje:

```java
// Step 5: Insert sample dates into the first sheet
var sheet = workbook.getWorksheets().get(0);
var cells = sheet.getCells();

cells.get("A1").putValue(new java.util.Date()); // Today’s date
cells.get("A2").putValue(java.sql.Date.valueOf("2024-12-31")); // Specific date
cells.get("A3").putValue(java.time.LocalDateTime.now()); // Date‑time now
```

Když sešit uložíte, tyto buňky zobrazí něco jako:

```
A1: 令和05.04.21
A2: 令和06.12.31
A3: 令和05.04.21 14:37:12
```

(Přesný rok éry závisí na aktuálním japonském kalendáři.)

## Krok 6: Uložte sešit a ověřte výstup

Nakonec zapište sešit do souboru, abyste jej mohli otevřít v Excelu, LibreOffice nebo jakémkoli prohlížeči, který respektuje formát:

```java
// Step 6: Save the workbook
workbook.save("CustomDateFormatDemo.xlsx");
System.out.println("Workbook saved with custom date format.");
```

Otevřete `CustomDateFormatDemo.xlsx` a měli byste vidět data vykreslená podle nastaveného vzoru. Pokud zaznamenáte nesoulad, dvakrát zkontrolujte, že žádný styl na úrovni buňky nepřepisuje globální nastavení (viz sekce „Edge Cases“ níže).

## Okrajové případy a varianty

### 1. Přepisování globálního formátu na úrovni buňky

Pokud má buňka již styl s konkrétním číselným formátem, globální nastavení je pro tuto buňku ignorováno. Pro vynucení globálního formátu vymažte styl buňky:

```java
cells.get("A1").getStyle().setNumber(0); // Reset number format to default
```

### 2. Změna locale sešitu bez vlastního vzoru

Někdy chcete jen **změnit locale sešitu**, aby vestavěné formáty data (např. `14‑03‑2024`) dodržovaly regionální konvence. To můžete provést bez `DateTimeFormatter`:

```java
WorkbookSettings localeSettings = workbook.getSettings();
localeSettings.setCultureInfo(new CultureInfo("fr-FR")); // French (France)
```

Nyní se jakýkoli výchozí styl data zobrazí jako `21/04/2025` místo `04/21/2025`.

### 3. Použití více vlastních formátů v jednom sešitu

Aspose Cells vám umožňuje definovat několik vlastních formátů a aplikovat je selektivně:

```java
// Define two formatters
DateTimeFormatter usFormatter = new DateTimeFormatter("MM/dd/yyyy", new CultureInfo("en-US"));
DateTimeFormatter jpFormatter = new DateTimeFormatter("ggyy.MM.dd", new CultureInfo("ja-JP"));

// Apply US format globally
settings.setDateTimeFormat(usFormatter);

// Later, apply Japanese format to a specific range
var style = workbook.createStyle();
style.setCustom(usFormatter.getFormatString()); // Or jpFormatter.getFormatString()
cells.get("B1").setStyle(style);
```

### 4. Resetování na výchozí formát

Pokud potřebujete vrátit se k výchozímu zpracování dat od Aspose, jednoduše předáte `null`:

```java
settings.setDateTimeFormat(null); // Clears the custom global format
```

## Často kladené otázky

- **Ovlivňuje to existující listy?**  
  Ano – každý list načtený do `Workbook` po nastavení globálního formátu jej zdědí, pokud buňka již nemá explicitní styl.

- **Mohu nastavit formát po zápisu dat?**  
  Rozhodně. Globální formát se aplikuje při vykreslování, takže můžete buňky nejprve naplnit a formát nastavit později.

- **Co když potřebuji kalendář specifický pro locale (např. thajský buddhistický)?**  
  Použijte odpovídající kód `CultureInfo` (`"th-TH"`), a formátovač bude automaticky respektovat tento kalendář.

- **Je zde nějaký výkonový dopad?**  
  Nezajímavý. Formátovač je uložen v `WorkbookSettings`, takže režie nastane jen jednou na sešit.

## Kompletní funkční příklad

Níže je kompletní, připravený k spuštění program, který zahrnuje všechny diskutované kroky:

```java
import com.aspose.cells.*;

public class AsposeCellsDateFormatDemo {
    public static void main(String[] args) throws Exception {
        // Apply license if you have one
        // License lic = new License();
        // lic.setLicense("Aspose.Cells.lic");

        // 1️⃣ Create workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 3️⃣ Define custom Japanese era format
        DateTimeFormatter jpFormatter = new DateTimeFormatter(
                "ggyy.MM.dd",
                new CultureInfo("ja-JP")
        );

        // 4️⃣ Set as global date format
        settings.setDateTimeFormat(jpFormatter);

        // 5️⃣ Add sample dates
        var sheet = workbook.getWorksheets().get(0);
        var cells = sheet.getCells();

        cells.get("A1").putValue(new java.util.Date());                     // Today
        cells.get("A2").putValue(java.sql.Date.valueOf("2024-12-31"));      // Fixed date
        cells.get("A3").putValue(java.time.LocalDateTime.now());           // Date‑time now

        // 6️⃣ Save to file
        workbook.save("AsposeCellsCustomDateFormat.xlsx");
        System.out.println("Workbook saved with custom Japanese era date format.");
    }
}
```

**Očekávaný výstup v Excelu:**

| Buňka | Zobrazená hodnota |
|------|----------------|
| A1   | 令和05.04.21   |
| A2   | 令和06.12.31   |
| A3   | 令和05.04.21 14:45:03 (time part may vary) |

Otevřete soubor a uvidíte, že data jsou formátována přesně podle definice.

## Závěr

Právě jste se naučili, jak **aspose cells date format** sešit v Javě, od změny locale po aplikaci **vlastního formátu data**, který funguje globálně. Využitím `WorkbookSettings` a `DateTimeFormatter` získáte přesnou kontrolu nad tím, jak se každé datum zobrazí – bez nutnosti ručního stylování.

Dále můžete prozkoumat **jak nastavit formát data** pouze pro konkrétní sloupce, nebo kombinovat vlastní číselné formáty s podmíněným formátováním pro vylepšenou zprávu. Stejné principy platí: definujte formátovač, připojte jej pomocí stylu a nechte Aspose, aby se postaralo o zbytek.

Šťastné programování a nebojte se experimentovat s dalšími locale – vaši uživatelé vám poděkují za vylepšené, kulturně citlivé tabulky!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným vysvětlením krok za krokem, aby vám pomohly zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Efektivně převést Excel do PDF s vlastními formáty data pomocí Aspose.Cells pro Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Mistrovství v prezentaci dat v Excelu: číselné a vlastní formátování data s Aspose.Cells pro Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Jak vytvořit a formátovat buňky v Excelu pomocí Aspose.Cells pro Java: krok za krokem průvodce](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}