---
category: general
date: 2026-07-03
description: Rozparsujte datum s locale pomocí Java java.time API. Naučte se zacházet
  s formátem japonské éry, konverzí dat podle locale a robustními technikami parsování
  dat v Javě.
draft: false
keywords:
- parse date with locale
- java date parsing
- japanese era format
- locale date conversion
- java time API
language: cs
og_description: Rozparsujte datum s locale v Javě pomocí API java.time. Tento průvodce
  ukazuje zpracování formátu japonské éry, konverzi data podle locale a osvědčené
  postupy pro spolehlivé parsování data.
og_title: Rozparsování data s locale v Javě – Kompletní programovací tutoriál
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Parse date with locale using Java’s java.time API. Learn Japanese era
    format handling, locale date conversion, and robust java date parsing techniques.
  headline: Parse Date with Locale in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Parse date with locale using Java’s java.time API. Learn Japanese era
    format handling, locale date conversion, and robust java date parsing techniques.
  name: Parse Date with Locale in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Define the Era Date String
    text: First, store the Japanese era string exactly as you receive it (e.g., from
      a CSV file or UI).
  - name: Build a Locale‑Aware Formatter
    text: Java’s **java.time API** lets you tie a `DateTimeFormatter` to a specific
      chronology (calendar system) and `Locale`. For the Japanese era we use `JapaneseChronology`.
  - name: Parse and Convert to Gregorian `LocalDate`
    text: Now we actually parse the string and transform the result into a classic
      `LocalDate` that any Java library can consume.
  - name: What if the input uses a different era symbol?
    text: Japanese eras change roughly every few decades. The formatter automatically
      recognises `M` (Meiji), `T` (Taisho), `S` (Showa), `H` (Heisei), and `R` (Reiwa).
      If you receive an older era not covered by the default `JapaneseChronology`,
      you’ll get a `DateTimeParseException`. In that case, verify the s
  - name: How to support other non‑Gregorian calendars?
    text: 'The pattern is identical; you just swap the chronology and locale. For
      example, Thai Buddhist dates (`BuddhistChronology`) look like this:'
  - name: Can I parse without an era symbol (pure year‑month‑day)?
    text: Yes—simply omit `G` from the pattern and use the default `ISO_LOCAL_DATE`
      formatter. That’s the classic *java date parsing* route for Gregorian strings.
  - name: What about lenient parsing (e.g., missing leading zeros)?
    text: Switch `ResolverStyle.STRICT` to `ResolverStyle.LENIENT`. Be aware that
      lenient mode may silently roll over invalid dates (e.g., `R5/13/40` becomes
      `2024‑02‑09`). For production code, strict mode is usually safer.
  type: HowTo
tags:
- java
- date-time
- localization
title: Parsování data s locale v Javě – Kompletní krok‑za‑krokem průvodce
url: /cs/java/advanced-features/parse-date-with-locale-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Parsování data s locale v Javě – Kompletní krok‑za‑krokem průvodce

Už jste někdy potřebovali **parsovat datum s locale** v Javě, ale nebyli jste si jisti, které třídy použít? Nejste v tom sami — práce s ne‑gregoriánskými kalendáři nebo regionálními formáty může připomínat dešifrování tajného jazyka. V tomto tutoriálu si projdeme reálný příklad: převod japonského řetězce éry jako `R5/04/01` na standardní gregoriánské `2023‑04‑01` `Date` objekt. Na konci budete mít znovupoužitelný vzor pro jakýkoli locale‑specifický formát data.

Probereme vše od potřebných importů po zpracování okrajových případů a přidáme několik souvisejících konceptů — *java date parsing*, *japanese era format*, *locale date conversion* a moderní *java time API* — abyste mohli řešení přizpůsobit svým projektům. Žádné externí knihovny, jen čistá Java 8+.

---

## Co tento tutoriál pokrývá

- Nastavení formátového řetězce **Japanese era** (`Reiwa`).
- Použití `DateTimeFormatter` s `JapaneseChronology` a `Locale`.
- Převod výsledného `JapaneseDate` na `LocalDate` (gregoriánské).
- Vytištění konečného data ve formátu ISO‑8601.
- Běžné úskalí, jako jsou nepodporované éry nebo neodpovídající vzory.
- Rychlé varianty pro jiné locale (Thai Buddhist, Islamic, atd.).

**Požadavky**  
JDK 8 nebo novější, základní znalost `java.time` a IDE nebo CLI pro spuštění Java kódu. To je vše — žádné další Maven závislosti.

---

## Parsování data s locale – Krok‑za‑krokem

Níže rozdělujeme řešení do tří přirozených kroků. Každý krok obsahuje přesný kód, který potřebujete, stručné vysvětlení *proč* je důležitý a tip, který v oficiální dokumentaci nenajdete.

### Krok 1: Definujte řetězec data s érou

Nejprve uložte japonský řetězec éry přesně tak, jak jej obdržíte (např. z CSV souboru nebo UI).

```java
// Step 1: Define a date string using the Japanese era format (Reiwa 5)
String eraDateString = "R5/04/01";
```

> **Proč je to důležité:**  
> Úvodní `R` označuje *Reiwa*, současnou japonskou éru. Pokud ignorujete značku éry, parser předpokládá gregoriánský kalendář a vytvoří nesprávný rok.

### Krok 2: Vytvořte locale‑citlivý formatter

Java **java.time API** vám umožní svázat `DateTimeFormatter` s konkrétní chronologií (kalendářním systémem) a `Locale`. Pro japonskou éru používáme `JapaneseChronology`.

```java
import java.time.chrono.JapaneseChronology;
import java.time.format.DateTimeFormatter;
import java.time.format.ResolverStyle;
import java.util.Locale;

// Step 2: Create a formatter that understands the Japanese era pattern
DateTimeFormatter japaneseFormatter = new DateTimeFormatterBuilder()
        .parseCaseInsensitive()
        .appendPattern("Gyy/MM/dd")          // G = era symbol, yy = year-of-era
        .toFormatter(Locale.JAPAN)           // Locale for Japanese symbols
        .withChronology(JapaneseChronology.INSTANCE)
        .withResolverStyle(ResolverStyle.STRICT);
```

**Klíčové body**  
- `G` parsuje text éry (`R` pro Reiwa, `H` pro Heisei, atd.).  
- `ResolverStyle.STRICT` nutí parser odmítnout nemožná data jako `R0/13/32`.  
- Nastavení `Locale` na `Locale.JAPAN` zajišťuje, že symboly éry odpovídají japonským konvencím.

> **Pro tip:** Pokud potřebujete podporovat *multiple* formáty éry (např. `HEISEI` vypsané), přidejte `.parseCaseInsensitive()` podle ukázky a rozšiřte vzor na `Guuuu` pro úplná jména.

### Krok 3: Parsujte a převeďte na gregoriánský `LocalDate`

Nyní skutečně parsujeme řetězec a transformujeme výsledek do klasického `LocalDate`, který může použít libovolná Java knihovna.

```java
import java.time.LocalDate;
import java.time.chrono.JapaneseDate;

// Step 3: Parse the era string and convert to Gregorian LocalDate
JapaneseDate japaneseDate = JapaneseDate.from(japaneseFormatter.parse(eraDateString));
LocalDate gregorianDate = LocalDate.from(japaneseDate);

// Verify the conversion
System.out.println(gregorianDate);   // Expected output: 2023-04-01
```

**Vysvětlení**  
`JapaneseDate.from(...)` vytvoří datum ukotvené v japonském kalendáři. Voláním `LocalDate.from(...)` odstraníme informaci o éře a získáme ekvivalentní ISO‑8601 datum — ideální pro ukládání, porovnávání nebo API volání.

> **Why convert?** Většina databází, REST služeb a knihoven třetích stran očekává gregoriánské datum. Udržení konverze uvnitř vašeho parsovacího postupu zabraňuje pozdějším skrytým chybám.

---

## Kompletní funkční příklad

Spojením všech částí získáte jedinou, připravenou ke spuštění Java třídu. Klidně ji zkopírujte do `ParseDateWithLocale.java` a spusťte.

```java
import java.time.LocalDate;
import java.time.chrono.JapaneseChronology;
import java.time.chrono.JapaneseDate;
import java.time.format.DateTimeFormatter;
import java.time.format.DateTimeFormatterBuilder;
import java.time.format.ResolverStyle;
import java.util.Locale;

public class ParseDateWithLocale {

    public static void main(String[] args) {
        // --- Step 1: Input ---
        String eraDateString = "R5/04/01";

        // --- Step 2: Formatter ---
        DateTimeFormatter japaneseFormatter = new DateTimeFormatterBuilder()
                .parseCaseInsensitive()
                .appendPattern("Gyy/MM/dd")
                .toFormatter(Locale.JAPAN)
                .withChronology(JapaneseChronology.INSTANCE)
                .withResolverStyle(ResolverStyle.STRICT);

        // --- Step 3: Parse & Convert ---
        JapaneseDate japaneseDate = JapaneseDate.from(japaneseFormatter.parse(eraDateString));
        LocalDate gregorianDate = LocalDate.from(japaneseDate);

        // Output
        System.out.println("Original era string: " + eraDateString);
        System.out.println("Converted Gregorian date: " + gregorianDate);
    }
}
```

**Očekávaný výstup v konzoli**

```
Original era string: R5/04/01
Converted Gregorian date: 2023-04-01
```

Spusťte program pomocí `javac ParseDateWithLocale.java && java ParseDateWithLocale`. Pokud uvidíte výše uvedené dva řádky, úspěšně jste **parsovali datum s locale**.

---

## Zpracování okrajových případů a časté otázky

### Co když vstup používá jiný symbol éry?

Japonské éry se mění přibližně každých několik desetiletí. Formatter automaticky rozpozná `M` (Meiji), `T` (Taisho), `S` (Showa), `H` (Heisei) a `R` (Reiwa). Pokud obdržíte starší éru, která není zahrnuta v defaultní `JapaneseChronology`, získáte `DateTimeParseException`. V takovém případě ověřte zdrojová data nebo poskytněte vlastní mapování.

### Jak podpořit jiné ne‑gregoriánské kalendáře?

Vzor je stejný; stačí vyměnit chronologii a locale. Například thajská buddhistická data (`BuddhistChronology`) vypadají takto:

```java
DateTimeFormatter thaiFormatter = new DateTimeFormatterBuilder()
        .appendPattern("Gyy/MM/dd")
        .toFormatter(new Locale("th", "TH"))
        .withChronology(java.time.chrono.ThaiBuddhistChronology.INSTANCE);
```

### Můžu parsovat bez symbolu éry (čistý rok‑měsíc‑den)?

Ano — jednoduše vynechejte `G` ze vzoru a použijte výchozí formatter `ISO_LOCAL_DATE`. To je klasická cesta *java date parsing* pro gregoriánské řetězce.

### Co s lenient parsováním (např. chybějící úvodní nuly)?

Přepněte `ResolverStyle.STRICT` na `ResolverStyle.LENIENT`. Buďte si vědomi, že lenient režim může tiše převést neplatná data (např. `R5/13/40` se stane `2024‑02‑09`). Pro produkční kód je obvykle bezpečnější přísný režim.

---

## Pro tipy pro robustní konverzi datumů podle locale

1. **Cache the formatter** – Vytvoření `DateTimeFormatter` je relativně levné, ale pokud parsujete tisíce datumů za sekundu, uložte jej do statického final pole.  
2. **Validate input length** – Rychlá kontrola `if (eraDateString.length() != 8)` může zabránit zbytečným výjimkám při parsování.  
3. **Log the original string** – Při ladění problémů s locale často surový vstup odhalí neviditelné znaky (mezery nulové šířky), které parser rozbijí.  
4. **Unit‑test each era** – Napište JUnit testy pro `R`, `H`, `S` atd., abyste zajistili, že budoucí aktualizace Javy nezmění mapování.

---

## Závěr

Právě jsme ukázali, jak **parsovat datum s locale** v Javě pomocí moderního *java time API*, locale‑citlivého `DateTimeFormatter` a `JapaneseChronology`. Kompletní příklad ukazuje celý tok — od surového japonského řetězce éry po čistý gregoriánský `LocalDate` — a poskytuje vám znalosti potřebné k přizpůsobení vzoru pro jiné kalendáře, jako jsou thajský buddhistický nebo islámský systém.

Další kroky? Zkuste vyměnit `JapaneseChronology` za `ThaiBuddhistChronology` nebo `HijrahChronology` a podívejte se, jak stejná struktura kódu zvládne zcela odlišné kulturní kalendáře. Můžete také prozkoumat formátování výsledného `LocalDate` zpět do locale‑specifického řetězce pomocí `DateTimeFormatter.ofLocalizedDate(FormatStyle.FULL)`.

Máte složitý locale nebo neočekávanou chybu při parsování? Zanechte komentář níže a pojďme to společně vyřešit. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Mistrovství prezentace dat v Excelu: číselné a vlastní formátování data s Aspose.Cells pro Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Efektivní převod Excelu do PDF s vlastními formáty data pomocí Aspose.Cells pro Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Ovládněte systém data 1904 v Excelu pomocí Aspose.Cells Java pro efektivní operace s buňkami](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}