---
category: general
date: 2026-07-03
description: Parsuj datę z uwzględnieniem lokalizacji przy użyciu API java.time w
  Javie. Poznaj obsługę formatu japońskiej ery, konwersję daty według lokalizacji
  oraz solidne techniki parsowania dat w Javie.
draft: false
keywords:
- parse date with locale
- java date parsing
- japanese era format
- locale date conversion
- java time API
language: pl
og_description: Parsowanie daty z uwzględnieniem lokalizacji w Javie przy użyciu API
  java.time. Ten przewodnik pokazuje obsługę formatu japońskiej ery, konwersję daty
  według lokalizacji oraz najlepsze praktyki zapewniające niezawodne parsowanie dat.
og_title: Parsowanie daty z lokalizacją w Javie – Pełny samouczek programistyczny
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
title: Parsowanie daty z lokalizacją w Javie – Kompletny przewodnik krok po kroku
url: /pl/java/advanced-features/parse-date-with-locale-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Parsowanie daty z uwzględnieniem lokalizacji w Javie – Kompletny przewodnik krok po kroku

Kiedykolwiek potrzebowałeś **parse date with locale** w Javie, ale nie byłeś pewien, których klas użyć? Nie jesteś sam — radzenie sobie z kalendarzami innymi niż gregoriański czy formatami regionalnymi może przypominać dekodowanie tajnego języka. W tym samouczku przeprowadzimy Cię przez rzeczywisty przykład: przekształcenie japońskiego ciągu epoki, takiego jak `R5/04/01`, w standardowy gregoriański obiekt `Date` `2023‑04‑01`. Po zakończeniu będziesz mieć wielokrotnego użytku wzorzec dla dowolnego formatu daty zależnego od lokalizacji.

Omówimy wszystko, od wymaganych importów po obsługę przypadków brzegowych, i wtrącimy kilka powiązanych koncepcji — *java date parsing*, *japanese era format*, *locale date conversion* oraz nowoczesnego *java time API* — abyś mógł dostosować rozwiązanie do własnych projektów. Bez zewnętrznych bibliotek, tylko czysta Java 8+.

---

## Co obejmuje ten samouczek

- Ustawienie ciągu formatu **Japanese era** (`Reiwa`).
- Użycie `DateTimeFormatter` z `JapaneseChronology` i `Locale`.
- Konwersja otrzymanego `JapaneseDate` na `LocalDate` (Gregorian).
- Wypisanie końcowej daty w formacie ISO‑8601.
- Typowe pułapki, takie jak nieobsługiwane ery lub niepasujące wzorce.
- Szybkie wariacje dla innych lokalizacji (Thai Buddhist, Islamic itp.).

**Wymagania wstępne**  
JDK 8 lub nowszy, podstawowa znajomość `java.time` oraz IDE lub CLI do uruchamiania kodu Java. To wszystko — bez dodatkowych zależności Maven.

---

## Parsowanie daty z lokalizacją – krok po kroku

Poniżej dzielimy rozwiązanie na trzy naturalne kroki. Każdy krok zawiera dokładny kod, którego potrzebujesz, krótkie wyjaśnienie *dlaczego* jest to ważne oraz wskazówkę, której możesz nie znaleźć w oficjalnej dokumentacji.

### Krok 1: Zdefiniuj ciąg daty z erą

Najpierw przechowaj japoński ciąg epoki dokładnie tak, jak go otrzymujesz (np. z pliku CSV lub interfejsu użytkownika).

```java
// Step 1: Define a date string using the Japanese era format (Reiwa 5)
String eraDateString = "R5/04/01";
```

> **Dlaczego to ważne:**  
> Początkowe `R` oznacza *Reiwa*, aktualną erę Japonii. Jeśli pominiesz znacznik ery, parser założy kalendarz gregoriański i wygeneruje nieprawidłowy rok.

### Krok 2: Zbuduj formatator uwzględniający lokalizację

API **java.time** w Javie pozwala powiązać `DateTimeFormatter` z określoną chronologią (systemem kalendarzowym) oraz `Locale`. Dla japońskiej ery używamy `JapaneseChronology`.

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

**Kluczowe punkty**  
- `G` analizuje tekst ery (`R` dla Reiwa, `H` dla Heisei, itp.).  
- `ResolverStyle.STRICT` wymusza odrzucenie niemożliwych dat, takich jak `R0/13/32`.  
- Ustawienie `Locale` na `Locale.JAPAN` zapewnia, że symbole ery odpowiadają japońskim konwencjom.

> **Pro tip:** Jeśli musisz obsługiwać *wiele* formatów ery (np. pełna nazwa `HEISEI`), dodaj `.parseCaseInsensitive()` jak pokazano i rozszerz wzorzec do `Guuuu` dla pełnych nazw.

### Krok 3: Parsuj i konwertuj na gregoriański `LocalDate`

Teraz faktycznie parsujemy ciąg i przekształcamy wynik w klasyczny `LocalDate`, który może wykorzystać dowolna biblioteka Java.

```java
import java.time.LocalDate;
import java.time.chrono.JapaneseDate;

// Step 3: Parse the era string and convert to Gregorian LocalDate
JapaneseDate japaneseDate = JapaneseDate.from(japaneseFormatter.parse(eraDateString));
LocalDate gregorianDate = LocalDate.from(japaneseDate);

// Verify the conversion
System.out.println(gregorianDate);   // Expected output: 2023-04-01
```

**Wyjaśnienie**  
`JapaneseDate.from(...)` tworzy obiekt daty osadzony w japońskim kalendarzu. Wywołując `LocalDate.from(...)` usuwamy informacje o erze i uzyskujemy równoważną datę ISO‑8601 — idealną do przechowywania, porównań lub wywołań API.

> **Dlaczego konwertować?** Większość baz danych, usług REST i bibliotek firm trzecich oczekuje daty gregoriańskiej. Utrzymanie konwersji wewnątrz procedury parsowania zapobiega późniejszym subtelnym błędom.

---

## Pełny działający przykład

Łącząc wszystko razem, oto pojedyncza, gotowa do uruchomienia klasa Java. Śmiało skopiuj i wklej do `ParseDateWithLocale.java` i uruchom.

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

**Oczekiwany wynik w konsoli**

```
Original era string: R5/04/01
Converted Gregorian date: 2023-04-01
```

Uruchom program poleceniem `javac ParseDateWithLocale.java && java ParseDateWithLocale`. Jeśli zobaczysz powyższe dwie linie, udało Ci się **parse date with locale**.

---

## Obsługa przypadków brzegowych i typowe pytania

### Co jeśli wejście używa innego symbolu ery?

Japońskie ery zmieniają się mniej więcej co kilka dekad. Formatator automatycznie rozpoznaje `M` (Meiji), `T` (Taisho), `S` (Showa), `H` (Heisei) i `R` (Reiwa). Jeśli otrzymasz starszą erę, której nie obejmuje domyślna `JapaneseChronology`, zostanie rzucony `DateTimeParseException`. W takim przypadku zweryfikuj dane źródłowe lub dostarcz własne mapowanie.

### Jak obsługiwać inne kalendarze nie‑gregoriańskie?

Wzorzec jest identyczny; wystarczy zamienić chronologię i lokalizację. Na przykład, tajskie daty buddyjskie (`BuddhistChronology`) wyglądają tak:

```java
DateTimeFormatter thaiFormatter = new DateTimeFormatterBuilder()
        .appendPattern("Gyy/MM/dd")
        .toFormatter(new Locale("th", "TH"))
        .withChronology(java.time.chrono.ThaiBuddhistChronology.INSTANCE);
```

### Czy mogę parsować bez symbolu ery (czysty rok‑miesiąc‑dzień)?

Tak — po prostu pomiń `G` w wzorcu i użyj domyślnego formatatora `ISO_LOCAL_DATE`. To klasyczna ścieżka *java date parsing* dla ciągów gregoriańskich.

### A co z luźnym parsowaniem (np. brak wiodących zer)?

Zamień `ResolverStyle.STRICT` na `ResolverStyle.LENIENT`. Pamiętaj, że tryb luźny może cicho przekształcić nieprawidłowe daty (np. `R5/13/40` staje się `2024‑02‑09`). W kodzie produkcyjnym zazwyczaj bezpieczniejszy jest tryb ścisły.

---

## Pro tipy dla solidnej konwersji dat z lokalizacją

1. **Cache the formatter** – Tworzenie `DateTimeFormatter` jest stosunkowo tanie, ale jeśli parsujesz tysiące dat na sekundę, przechowaj go w statycznym polu finalnym.
2. **Validate input length** – Szybka kontrola `if (eraDateString.length() != 8)` może zapobiec niepotrzebnym wyjątkom parsowania.
3. **Log the original string** – Podczas debugowania problemów z lokalizacją surowe dane wejściowe często ujawniają niewidzialne znaki (zero‑width spaces), które psują parser.
4. **Unit‑test each era** – Napisz testy JUnit dla `R`, `H`, `S` itp., aby zapewnić, że przyszłe aktualizacje Javy nie zmienią mapowania.

---

## Podsumowanie

Pokazaliśmy właśnie, jak **parse date with locale** w Javie, wykorzystując nowoczesne *java time API*, formatator uwzględniający lokalizację `DateTimeFormatter` oraz `JapaneseChronology`. Pełny przykład przedstawia cały przepływ — od surowego japońskiego ciągu ery do czystego gregoriańskiego `LocalDate` — i wyposaża Cię w wiedzę potrzebną do dostosowania wzorca do innych kalendarzy, takich jak tajski buddyjski czy islamski.

Następne kroki? Spróbuj zamienić `JapaneseChronology` na `ThaiBuddhistChronology` lub `HijrahChronology` i zobacz, jak ta sama struktura kodu radzi sobie z całkowicie innymi kalendarzami kulturowymi. Możesz także zbadać formatowanie otrzymanego `LocalDate` z powrotem do ciągu specyficznego dla lokalizacji, używając `DateTimeFormatter.ofLocalizedDate(FormatStyle.FULL)`.

Masz trudną lokalizację lub nieoczekiwany błąd parsowania? Dodaj komentarz poniżej, a wspólnie rozwiążemy problem. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Opanowanie prezentacji danych w Excelu: formatowanie liczb i niestandardowych dat przy użyciu Aspose.Cells dla Javy](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Efektywne konwertowanie Excela do PDF z niestandardowymi formatami dat przy użyciu Aspose.Cells dla Javy](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Opanuj system dat 1904 w Excelu używając Aspose.Cells Java dla efektywnych operacji na komórkach](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}