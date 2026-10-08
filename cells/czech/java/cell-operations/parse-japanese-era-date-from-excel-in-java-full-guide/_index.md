---
category: general
date: 2026-06-18
description: Analyzujte japonské datum podle éry v Javě pomocí Aspose.Cells. Naučte
  se, jak rychle načíst datum z buňky Excelu a extrahovat datum a čas z buňky Excelu.
draft: false
keywords:
- parse japanese era date
- read date from excel cell
- extract datetime from excel cell
language: cs
og_description: Rozparsujte japonské datum éry v Javě pomocí Aspose.Cells. Tento průvodce
  vám ukáže, jak přečíst datum z buňky Excelu a extrahovat datum a čas z buňky Excelu
  během několika kroků.
og_title: Rozparsování japonského data éry z Excelu v Javě – kompletní tutoriál
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  headline: Parse Japanese Era Date from Excel in Java – Full Guide
  type: TechArticle
- description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  name: Parse Japanese Era Date from Excel in Java – Full Guide
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
title: Rozparsování japonského data podle éry z Excelu v Javě – úplný průvodce
url: /cs/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rozparsování japonského data éry z Excelu v Javě – Kompletní průvodce

Už jste někdy potřebovali **rozparsovat japonské datum éry** uložené v sešitu Excel, ale nebyli jste si jisti, jak ho převést na běžné gregoriánské `DateTime`? Nejste v tom sami — mnoho vývojářů narazí na tento problém při práci se staršími japonskými účetními listy nebo vládními formuláři. Dobrou zprávou je, že s několika řádky Javy a správnou knihovnou můžete **číst datum z buňky Excelu** a **extrahovat datum‑čas z buňky Excelu** bez ručního zpracování řetězců.

V tomto tutoriálu projdeme kompletní, spustitelný příklad, který ukazuje, jak **rozparsovat japonské datum éry** jako např. „令和3年5月10日“ do Java `java.time.LocalDateTime`. Popíšeme potřebnou Maven závislost, vysvětlíme, proč je nutné povolit parsování s ohledem na éru, a upozorníme na běžné úskalí. Na konci budete mít robustní, produkčně připravený úryvek, který můžete vložit do libovolného Java projektu.

## Požadavky

- Java 17 nebo novější (kód funguje i na Java 8+)
- Maven nebo Gradle build systém
- Základní znalost práce se soubory Excel
- Knihovna **Aspose.Cells for Java** (zdarma zkušební verze stačí pro testování)

Pokud vám některá z těchto položek není známá, nebojte se — ukážu vám, jak knihovnu přidat a začít pracovat.

## Krok 1: Přidejte Aspose.Cells do svého projektu

Nejprve potřebujete knihovnu, která rozumí japonským datům éry. Aspose.Cells za vás udělá těžkou práci.

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

Jakmile je závislost vyřešena, můžete začít psát kód, který *čte datum z buňky Excelu* a *extrahuje datum‑čas z buňky Excelu*.

## Krok 2: Vytvořte sešit a zaměřte se na první list

Začneme vytvořením nového sešitu v paměti a získáním prvního listu. Toto odpovídá prvním dvěma řádkům původního příkladu.

```java
import com.aspose.cells.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize workbook and worksheet
        Workbook workbook = new Workbook();               // creates a blank workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

Proč začínat s čistým sešitem? Zajišťuje to čisté prostředí, kde můžeme kontrolovat každé nastavení — což je klíčové, když později povolíme parsování s ohledem na éru.

## Krok 3: Vložte japonský řetězec data éry do buňky A1

Nyní simulujeme soubor Excel, který již obsahuje japonské datum éry. Ve skutečnosti byste pravděpodobně načítali existující `.xlsx`, ale pro ilustraci **zapíšeme** hodnotu sami.

```java
        // Step 3: Insert a Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日"); // Reiwa 3rd year = 2021-05-10
```

Řetězec následuje standardní japonskou notaci: *Éra* + *Rok* + *Měsíc* + *Den*. Bez další konfigurace by Aspose.Cells považoval tento řetězec za prostý text, ne za datum.

## Krok 4: Povolení parsování s ohledem na éru

Tady je klíčová část: říct sešitu, aby **rozparsoval japonské datum éry**, když na něj narazí. Dělá se to pomocí příznaku `ParseDateUsingJapaneseEra`.

```java
        // Step 4: Turn on era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);
```

Proč je to nutné? Ve výchozím nastavení Aspose.Cells předpokládá gregoriánský kalendář, takže „令和3年5月10日“ zůstane jako řetězec. Povolení příznaku instruuje engine, aby ho pod kapotou převedl na `java.util.Date` (nebo ekvivalent v `java.time`).

## Krok 5: Získejte rozparsovanou hodnotu DateTime

Nyní, když sešit ví, jak interpretovat éru, můžeme od buňky požádat o její `DateTime` reprezentaci.

```java
        // Step 5: Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime(); // returns java.util.Date
        // Convert to java.time.LocalDateTime for modern APIs
        java.time.Instant instant = javaDate.toInstant();
        java.time.ZoneId zone = java.time.ZoneId.systemDefault();
        java.time.LocalDateTime dateTime = java.time.LocalDateTime.ofInstant(instant, zone);
```

Všimněte si, že **čteme datum z buňky Excelu** pomocí `cell.getDateTime()`. Metoda vrací `java.util.Date`, který okamžitě převedeme na `LocalDateTime` pro vyšší typovou bezpečnost. Tím splníme požadavek **extrahovat datum‑čas z buňky Excelu** čistým, idiomatickým způsobem.

## Krok 6: Ověřte výsledek

Nakonec vytiskneme gregoriánské datum, abychom potvrdili úspěšnou konverzi.

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

Tento výstup dokazuje, že jsme úspěšně **rozparsovali japonské datum éry**, **četli datum z buňky Excelu** a **extrahovali datum‑čas z buňky Excelu** v jedné posloupnosti.

## Řešení reálných okrajových případů

### Více epoch

Japonsko mělo několik epoch (Meiji, Taishō, Shōwa, Heisei, Reiwa). Příznak `setParseDateUsingJapaneseEra(true)` je pokrývá automaticky, ale mějte na paměti, že starší data mohou spadat mimo podporovaný rozsah knihovny (typicky 1868‑současnost). Pokud narazíte na datum jako „昭和45年12月31日“, stejný kód jej převede na 1970‑12‑31.

### Prázdné nebo neplatné buňky

Pokud je buňka prázdná nebo obsahuje špatně formátovaný řetězec, `cell.getDateTime()` vyhodí `CellsException`. Ochráníte se tím jednoduchou kontrolou:

```java
if (cell.getType() == CellValueType.IS_DATE) {
    // safe to call getDateTime()
} else {
    System.out.println("Cell does not contain a parsable date.");
}
```

### Časová složka

Příklad zahrnuje jen datum, ale pokud váš Excel obsahuje i čas (např. „令和3年5月10日 14:30“), Aspose.Cells zachová i časovou část. `LocalDateTime`, který získáte, bude obsahovat hodiny, minuty i sekundy.

## Kompletní funkční příklad

Sestavte vše dohromady, zde je kompletní program připravený ke zkopírování a vložení:

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

Uložte jej jako `JapaneseEraDateParser.java`, zkompilujte pomocí `javac` a spusťte pomocí `java`. Pokud je vše nastaveno správně, na konzoli se zobrazí gregoriánské datum.

## Profesionální tipy a časté úskalí

- **Tip:** Vždy nastavte `setParseDateUsingJapaneseEra(true)` **před** načtením jakýchkoli hodnot buněk. Změna příznaku po načtení buňky neprovádí retroaktivní konverzi.
- **Dejte pozor na locale:** Knihovna parsuje řetězce epoch na základě Unicode znaků, takže není nutné explicitně nastavovat japonské locale.
- **Poznámka k výkonu:** Povolení parsování epoch přidává malé zatížení. Pokud jej potřebujete jen pro několik buněk, můžete příznak dočasně zapnout, přečíst buňky a pak jej zase vypnout.
- **Testování:** Využijte bezplatnou zkušební verzi Aspose k ověření proti reálnému Excel souboru, který obsahuje více epoch. Tím zajistíte, že váš produkční kód se chová podle očekávání.

## Závěr

Ukázali jsme, jak **rozparsovat japonské datum éry** přímo ze sešitu Excel pomocí Javy a Aspose.Cells. Povolením parsování s ohledem na éru můžete **číst datum z buňky Excelu** a **extrahovat datum‑čas z buňky Excelu** čistým, typově bezpečným způsobem. Přístup funguje pro jakoukoli moderní japonskou epochu, zvládá časové složky a elegantně zachází s neplatnými daty.

Jste připraveni na další výzvu? Zkuste načíst skutečný `.xlsx` soubor, který obsahuje směs gregoriánských a japonských epoch, nebo experimentujte s formátováním výsledného `LocalDateTime` do řetězců podle vašeho locale. Můžete také zkusit zapsat převedená data zpět do Excelu pro systémy, které rozumí jen gregoriánským datům.

Máte otázky nebo jste narazili na podivný okrajový případ? Zanechte komentář níže a šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným krok‑za‑krokem vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Ovládněte systém dat 1904 v Excelu pomocí Aspose.Cells Java pro efektivní operace s buňkami](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Efektivně převádějte Excel do PDF s vlastními formáty dat pomocí Aspose.Cells for Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Jak vybrat rozsahy buněk v Excelu pomocí Aspose.Cells for Java (průvodce 2023)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}