---
category: general
date: 2026-11-22
description: Dowiedz się, jak ustawić lokalizację w skoroszycie Java, zmienić język
  skoroszytu i ustawić kalendarz na japoński, podając przejrzyste przykłady kodu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set locale
- change workbook language
- set locale to japanese
- how to set calendar
language: pl
lastmod: 2026-11-22
og_description: Jak szybko ustawić locale w skoroszycie Java. Skorzystaj z tego samouczka,
  aby zmienić język skoroszytu, ustawić locale na japoński i skonfigurować japoński
  kalendarz.
og_image_alt: Screenshot showing how to set locale in a Java workbook
og_title: Jak ustawić locale w skoroszycie Java – przewodnik krok po kroku
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
title: Jak ustawić ustawienia regionalne w skoroszycie Java przy użyciu Aspose.Cells
url: /pl/java/workbook-operations/how-to-set-locale-in-a-java-workbook-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak ustawić lokalizację w skoroszycie Java przy użyciu Aspose.Cells

Ustawienie lokalizacji w skoroszycie Java jest powszechnym wymaganiem, gdy trzeba dostosować arkusz kalkulacyjny do różnych regionów. W tym przewodniku dowiesz się, jak ustawić lokalizację, zmienić język skoroszytu oraz ustawić kalendarz na japoński przy użyciu API Aspose.Cells.

Internacjonalizacja skoroszytu wykracza poza tłumaczenie tekstu; wpływa także na formaty liczb, parsowanie dat oraz domyślny system kalendarzowy. Po zakończeniu tego samouczka będziesz w stanie:

* Skonfigurować lokalizację skoroszytu na japoński (Japonia) – **set locale to japanese**.  
* Zmienić język skoroszytu, aby formuły i ciągi interfejsu uwzględniały docelową kulturę – **change workbook language**.  
* Przełączyć kalendarz na japoński kalendarz cesarski – **how to set calendar**.  

Kroki działają z dowolną aktualną wersją Aspose.Cells for Java (v23.9 lub nowszą) i wymagają jedynie standardowego środowiska programistycznego Java.

## Wymagania wstępne

| Requirement | Reason |
|-------------|--------|
| Java 8 lub wyższy | Biblioteka jest przeznaczona dla Java 8+. |
| Aspose.Cells for Java (v23.9+) | Udostępnia `Workbook`, `WorkbookSettings` oraz narzędzia do obsługi lokalizacji. |
| IDE (IntelliJ IDEA, Eclipse, or VS Code) | Do kompilacji i uruchamiania przykładu. |
| Basic knowledge of Java | Wymagana do zrozumienia fragmentów kodu. |

Dodaj zależność Aspose.Cells Maven do swojego `pom.xml` (lub pobierz plik JAR ręcznie):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust for your JDK version -->
</dependency>
```

## Jak ustawić lokalizację i kalendarz w skoroszycie

Pierwszym krokiem jest utworzenie instancji skoroszytu i pobranie jego obiektu ustawień. Obiekt ustawień udostępnia API lokalizacji i kalendarza.

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

### Dlaczego każdy wiersz ma znaczenie

* **`new Workbook()`** – Tworzy pusty skoroszyt, który możesz modyfikować przed zapisaniem.  
* **`getSettings()`** – Zwraca obiekt `WorkbookSettings`; wszystkie opcje regionalne znajdują się tutaj.  
* **`setCalendar(...)`** – Zastępuje domyślny kalendarz gregoriański japońskim kalendarzem cesarskim, wpływając na sposób wyświetlania i parsowania dat.  
* **`setLocale(new Locale("ja","JP"))`** – Zmienia język i konwencje regionalne (np. nazwy miesięcy, separatory dziesiętne). To jest sedno **how to set locale** dla skoroszytu.  

Uruchomienie programu tworzy plik `LocaleDemo.xlsx`. Otwórz go w Excelu lub LibreOffice, a zobaczysz japońskie nazwy miesięcy, symbole waluty japońskiego jena oraz daty sformatowane zgodnie z japońskim kalendarzem.

## Zmiana języka skoroszytu (ustawienie lokalizacji na japoński)

Jeśli Twoim głównym celem jest **change workbook language**, możesz skupić się wyłącznie na wywołaniu `setLocale`. Poniższy fragment izoluje ten krok:

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Change only the language to Japanese (Japan)
settings.setLocale(new Locale("ja", "JP"));
workbook.save("JapaneseLanguage.xlsx");
```

**Co się zmienia?**  
* Ciągi formatowania komórek przełączają się na japoński (np. `#,##0.00` staje się `#,##0.00` z symbolem jena).  
* Wbudowane nazwy funkcji (takie jak `SUM`) pozostają po angielsku, ponieważ lokalizacja funkcji w Excelu jest niezależna, ale ciągi dat i komunikaty o błędach podążają za japońskimi konwencjami.  

**Kiedy tego używać?**  
* Gdy potrzebujesz arkusza wyświetlającego liczby i daty dla japońskiej publiczności, ale podstawowy kalendarz może pozostać gregoriański.  
* Dla raportów eksportowanych do PDF lub drukowanych, zapewniając, że język wizualny odpowiada docelowemu rynkowi.

## Jak ustawić kalendarz na japoński kalendarz

Czasami wymaganie **how to set calendar** jest oddzielne od lokalizacji. Dla starszych systemów, które przechowują daty w japońskiej erze cesarskiej, musisz wyraźnie ustawić kalendarz, zachowując opcjonalnie domyślną lokalizację.

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

**Kluczowe punkty:**

* `Calendar.getInstance(Locale.JAPAN)` zwraca `java.util.Calendar` skonfigurowany dla japońskiej ery.  
* Skoroszyt będzie teraz wyświetlał daty przy użyciu symboli ery (R dla Reiwa, H dla Heisei itp.).  
* To ustawienie **nie** wpływa na formatowanie liczb ani język interfejsu; połącz je z `setLocale`, jeśli potrzebujesz obu.

## Pełny przykład end‑to‑end

Poniżej znajduje się kompletny, gotowy do uruchomienia program, który demonstruje **how to set locale**, **change workbook language** oraz **set the calendar** w jednej spójnej sekwencji. Dodaje także przykładową komórkę, aby zobrazować efekt.

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

**Oczekiwany wynik:**  
Otwierając `FullJapaneseLocale.xlsx` zobaczysz pierwszą komórkę z datą w formacie `R3/04/01` (Reiwa 3) oraz drugą komórkę sformatowaną jako `¥1,234,567.89`. Potwierdza to, że **how to set locale**, **change workbook language** i **how to set calendar** działają razem.

## Typowe pułapki i jak ich unikać

| Pitfall | Why it happens | Fix |
|---------|----------------|-----|
| Using `Locale.CHINA` instead of `new Locale("ja","JP")` | `Locale.CHINA` ustawia język chiński, a nie japoński. | Zawsze twórz `Locale` jako `"ja", "JP"` dla japońskiego. |
| Forgetting to call `settings.setCalendar(...)` after `setLocale` | Kalendarz domyślnie pozostaje gregoriański, więc daty pojawiają się w niewłaściwej erze. | Wywołaj `setCalendar` **po** ustawieniu lokalizacji lub ustaw oba razem, jak pokazano. |
| Saving the workbook before applying settings | Ustawienia są stosowane do obiektu w pamięci; wczesny zapis zapisuje domyślną lokalizację. | Zastosuj wszystkie zmiany lokalizacji/kalendarza **przed** wywołaniem `workbook.save()`. |
| Using an outdated Aspose.Cells version | Starsze wersje nie posiadają przeciążeń `setCalendar`. | Zaktualizuj do v23.9+ lub sprawdź notatki wydania pod kątem wsparcia lokalizacji. |

## Testowanie konfiguracji

1. Uruchom klasę **FullLocaleExample**.  
2. Otwórz wygenerowany plik `FullJapaneseLocale.xlsx` w Excelu.  
3. Zweryfikuj, że:  
   * Kolumna dat wyświetla japońskie symbole ery (`R`, `H` itp.).  
   * Kolumna liczb używa symbolu jena i separatorów przecinkowych.  
   * Wszystkie wbudowane komunikaty o błędach (np. `#DIV/0!`) pojawiają się po japońsku, jeśli skoroszyt zawiera błędy.  

Jeśli którykolwiek z tych testów nie powiedzie się, sprawdź ponownie, czy obiekt `WorkbookSettings`, który modyfikowałeś, jest tym samym, który jest używany przy zapisie.

## Kolejne kroki

* **Localize formulas** – Choć lokalizacja kontroluje formatowanie, możesz także przetłumaczyć własne nazwy funkcji przy użyciu `FormulaParser`.  
* **Apply locale to existing workbooks** – Załaduj skoroszyt przy pomocy `new Workbook`...

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne, działające przykłady kodu wraz z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Format dat w Aspose Cells: Jak ustawić niestandardowy format daty w Javie](/cells/english/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/)
- [Jak ustawić język w plikach Excel przy użyciu Aspose.Cells .NET dla wsparcia wielojęzycznego](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [Jak ustawić format liczbowy komórki i konwertować japońskie daty w C# przy użyciu Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}