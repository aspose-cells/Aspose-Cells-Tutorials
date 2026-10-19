---
category: general
date: 2026-10-07
description: Čtení data z Excelu v Javě s Aspose.Cells. Tento průvodce vám ukáže,
  jak parsovat japonské datumové éry, číst datum z buněk Excelu a rychle extrahovat
  datum a čas z buněk Excelu.
draft: false
keywords:
- read date from excel
- extract datetime from excel
- java excel date conversion
- japanese era date parsing
- aspose.cells java
lastmod: 2026-10-07
og_description: Čtení data z Excelu v Javě s Aspose.Cells. Tento průvodce vám ukáže,
  jak parsovat japonské datumové éry, číst datum z buněk Excelu a extrahovat datum
  a čas z buněk Excelu během několika kroků.
og_image_alt: 'Developer guide: Read date from Excel in Java using Aspose.Cells'
og_title: Čtení data z Excelu v Javě s Aspose.Cells – úplný průvodce
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Read date from Excel in Java with Aspose.Cells. This guide shows you
    how to parse Japanese era dates, read date from Excel cells, and extract datetime
    from Excel cells quickly.
  headline: Read date from Excel in Java with Aspose.Cells – full guide
  type: TechArticle
- description: Read date from Excel in Java with Aspose.Cells. This guide shows you
    how to parse Japanese era dates, read date from Excel cells, and extract datetime
    from Excel cells quickly.
  name: Read date from Excel in Java with Aspose.Cells – full guide
  steps:
  - name: Multiple Eras
    text: Japan has had several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa). The `setParseDateUsingJapaneseEra(true)`
      flag covers all of them automatically, but be aware that older dates may fall
      outside the library’s supported range (typically 1868‑present). If you encounter
      a date like “昭和45年12月31日”, the sam
  - name: Blank or Invalid Cells
    text: 'If a cell is empty or contains a malformed string, `cell.getDateTime()`
      throws a `CellsException`. Guard against this with a simple check:'
  - name: Time Component
    text: The example only includes a date, but if your Excel file also stores time
      (e.g., “令和3年5月10日 14:30”), Aspose.Cells will preserve the time portion. The
      `LocalDateTime` you receive will include hours, minutes, and seconds.
  type: HowTo
tags:
- Java
- Excel
- DateTime
- read date from excel
- java excel date conversion
title: Čtení data z Excelu v Javě s Aspose.Cells – úplný průvodce
url: /cs/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Číst datum z Excelu v Javě s Aspose.Cells – kompletní průvodce

Pokud potřebujete **číst datum z Excelu** v tabulkách, které obsahují řetězce japonských éry, jste na správném místě. V mnoha starších účetních nebo vládních tabulkách je datum uloženo jako „令和3年5月10日“ a jeho převod na standardní gregoriánské `LocalDateTime` může být náchylný k chybám. Tento tutoriál vám krok za krokem ukáže, jak povolit parsování s ohledem na éry, přečíst hodnotu buňky a **extrahovat datum a čas z Excelu** pomocí Aspose.Cells pro Javu.

## Rychlé odpovědi
- **Která knihovna zpracovává japonské éry datum?** Aspose.Cells for Java.
- **Jaká verze Javy je vyžadována?** Java 17 nebo novější (Java 8 také funguje).
- **Potřebuji licenci pro testování?** Bezplatná zkušební verze stačí pro vývoj.
- **Může stejný kód číst gregoriánská data?** Ano, API automaticky rozpozná formát.
- **Je zachována časová informace?** Rozhodně – hodiny, minuty a sekundy přežijí konverzi.

## Co je čtení data z Excelu?
Fráze „read date from Excel“ označuje získání hodnoty data z buňky a její převod do objektu datum‑čas v Javě, například `java.time.LocalDateTime`. Aspose.Cells abstrahuje nízkoúrovňový binární formát Excelu, takže můžete pracovat s daty bez ručního parsování řetězců.

## Proč použít Aspose.Cells pro parsování japonských era datumů?
Aspose.Cells podporuje **více než 50 vstupních a výstupních formátů** a dokáže zpracovat sešity o stovkách stránek, aniž by načítal celý soubor do paměti. Jeho vestavěný parser s ohledem na éry převádí každou japonskou éru (Meiji, Taishō, Shōwa, Heisei, Reiwa) na gregoriánské datum jedním voláním API, čímž eliminuje křehký kód založený na regulárních výrazech.

## Požadavky
- Java 17 (nebo Java 8+) nainstalovaná na vašem počítači.
- Systém sestavení Maven nebo Gradle.
- Základní znalost souborů Excel.
- Knihovna Aspose.Cells for Java (zkušební nebo licencovaná verze).

Pokud jsou některé z těchto položek neznámé, nebojte se – v dalším kroku ukážeme, jak knihovnu přidat.

## Jak číst datum z Excelu v Javě?

Načtěte svůj sešit, povolte parsování s ohledem na éry a požádejte buňku o její hodnotu `DateTime`. Celý proces zabere **dvě řádky funkčního kódu**, jakmile je knihovna na classpath.

### Krok 1: přidat Aspose.Cells do vašeho projektu

**Maven**:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for latest version -->
</dependency>
```

**Gradle**:

```groovy
implementation 'com.aspose:aspose-cells:24.9'
```

Po vyřešení závislosti můžete začít používat API k **čtení data z Excelu** v buňkách.

### Krok 2: vytvořit sešit a zaměřit se na první list

Třída `Workbook` představuje celý soubor Excel v paměti. Vytvoření nové instance zaručuje čisté prostředí pro následné kroky parsování.

```java
import com.aspose.cells.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize workbook and worksheet
        Workbook workbook = new Workbook();               // creates a blank workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

### Krok 3: vložit řetězec japonské éry do buňky A1

Pro demonstraci zapíšeme řetězec éry sami; ve výrobě byste načetli existující `.xlsx`.

```java
        // Step 3: Insert a Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日"); // Reiwa 3rd year = 2021-05-10
```

Text následuje konvenční japonský vzor: *Éra* + *Rok* + *Měsíc* + *Den*.

### Krok 4: povolit parsování datumů s ohledem na éry

Řekněte Aspose.Cells, aby zacházel s řetězci éry jako s daty nastavením příznaku `ParseDateUsingJapaneseEra`.  
`ParseDateUsingJapaneseEra` je vlastnost, která při nastavení na true umožňuje automatický převod japonských řetězců éry na gregoriánská data.

```java
        // Step 4: Turn on era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);
```

Bez tohoto příznaku by knihovna považovala „令和3年5月10日“ za prostý text a automatický převod by chyběl.

### Krok 5: získat parsovanou hodnotu DateTime

Nyní požádejte buňku o její datumovou reprezentaci. `cell.getDateTime()` vrací hodnotu buňky jako objekt `java.util.Date`. Metoda vrací `java.util.Date`, který okamžitě převedeme na moderní `java.time.LocalDateTime`. `LocalDateTime` je třída Javy představující datum a čas bez časové zóny.

```java
        // Step 5: Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime(); // returns java.util.Date
        // Convert to java.time.LocalDateTime for modern APIs
        java.time.Instant instant = javaDate.toInstant();
        java.time.ZoneId zone = java.time.ZoneId.systemDefault();
        java.time.LocalDateTime dateTime = java.time.LocalDateTime.ofInstant(instant, zone);
```

Tím splňujeme požadavek **extrahovat datum a čas z Excelu** typově bezpečným způsobem.

### Krok 6: ověřit výsledek

Vytiskněte gregoriánské datum pro potvrzení úspěšné konverze.

```java
        // Step 6: Output the Gregorian date
        System.out.println(dateTime); // Expected output: 2021-05-10T00:00
    }
}
```

Po spuštění programu byste měli vidět:

```
2021-05-10T00:00
```

Výstup dokazuje, že jsme úspěšně **četli datum z Excelu**, parsovali japonskou éru a **extrahovali datum a čas z Excelu** v jednom toku.

## Řešení reálných okrajových případů

### Více era

Japonsko mělo několik era (Meiji, Taishō, Shōwa, Heisei, Reiwa). Příznak `setParseDateUsingJapaneseEra(true)` pokrývá všechny automaticky, ale mějte na paměti, že starší data mohou spadat mimo podporovaný rozsah knihovny (typicky 1868‑současnost). Pokud narazíte na datum jako „昭和45年12月31日“, stejný kód jej převede na 1970‑12‑31.

### Prázdné nebo neplatné buňky

Pokud je buňka prázdná nebo obsahuje poškozený řetězec, `cell.getDateTime()` vyhodí `CellsException`. Ochráníte se tím jednoduchou kontrolou:

```java
if (cell.getType() == CellValueType.IS_DATE) {
    // safe to call getDateTime()
} else {
    System.out.println("Cell does not contain a parsable date.");
}
```

### Časová složka

Příklad zahrnuje jen datum, ale pokud váš Excel soubor také ukládá čas (např. „令和3年5月10日 14:30“), Aspose.Cells zachová časovou část. `LocalDateTime`, který získáte, bude obsahovat hodiny, minuty i sekundy.

## Kompletní funkční příklad

Spojením všech částí získáte kompletní, připravený ke zkopírování a vložení program:

```java
import com.aspose.cells.*;
import java.time.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Insert Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日");

        // Enable era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);

        // Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime();
        LocalDateTime dateTime = javaDate.toInstant()
                                         .atZone(ZoneId.systemDefault())
                                         .toLocalDateTime();

        // Output the Gregorian date
        System.out.println(dateTime); // 2021-05-10T00:00
    }
}
```

Uložte jej jako `JapaneseEraDateParser.java`, zkompilujte pomocí `javac` a spusťte pomocí `java`. Pokud je vše nastaveno správně, uvidíte v konzoli vytištěné gregoriánské datum.

## Profesionální tipy a běžné úskalí

- **Pro tip:** Povolte `setParseDateUsingJapaneseEra(true)` **před** čtením jakýchkoli hodnot buněk. Změna příznaku později nepřevádí buňky, které už byly načteny.
- **Locale note:** Parser pracuje přímo s Unicode znaky, takže není nutné explicitně nastavovat japonskou locale.
- **Performance:** Parsování éry přidává zanedbatelný overhead. Pokud jej potřebujete jen pro několik buněk, přepněte příznak jen během těchto čtení.
- **Testing:** Využijte bezplatnou zkušební verzi Aspose k ověření na reálném sešitu, který kombinuje gregoriánská i era data. To zajistí, že produkční kód se chová podle očekávání.

## Často kladené otázky

**Q: Mohu použít tento přístup s existujícím souborem .xlsx?**  
A: Ano. Načtěte soubor pomocí `new Workbook("path/to/file.xlsx")` a stejný příznak parsuje všechny nalezené řetězce éry.

**Q: Co se stane, pokud buňka obsahuje gregoriánské datum?**  
A: Knihovna vrátí gregoriánskou hodnotu beze změny; parsování éry ovlivní jen řetězce, které odpovídají vzoru éry.

**Q: Podporuje Aspose.Cells data starší než Meiji (1868)?**  
A: Ne. Data před rokem 1868 jsou mimo podporovaný rozsah a budou považována za prostý text.

**Q: Jak mohu zpracovat velké sešity, aniž bych vyčerpával paměť?**  
A: Použijte konstruktor `Workbook`, který přijímá `LoadOptions` s nastavením `setMemorySetting(MemorySetting.MemoryPreference)`, aby se data streamovala místo načítání celého souboru najednou.

**Q: Je pro produkční použití vyžadována komerční licence?**  
A: Ano, platná licence Aspose.Cells odstraňuje omezení evaluace a umožňuje plný výkon.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Ovládněte datumový systém 1904 v Excelu pomocí Aspose.Cells Java pro efektivní operace s buňkami](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Efektivně převést Excel do PDF s vlastním formátem data pomocí Aspose.Cells pro Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Jak vybrat rozsahy buněk v Excelu pomocí Aspose.Cells pro Java (průvodce 2023)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

---

**Last Updated:** 2026-10-07  
**Tested With:** Aspose.Cells 24.12 for Java  
**Author:** Aspose

## Související tutoriály

- [Parsování japonského data z Excelu v Javě – kompletní průvodce](/cells/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/)
- [Čtení souboru Excel v Javě s Aspose.Cells – kompletní průvodce](/cells/java/automation-batch-processing/aspose-cells-java-excel-manipulation/)
- [Uložení sešitu Excel s Aspose.Cells pro Java – kompletní průvodce](/cells/java/automation-batch-processing/excel-workbook-automation-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}