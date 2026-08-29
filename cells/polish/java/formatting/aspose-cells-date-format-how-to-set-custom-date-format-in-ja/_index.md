---
category: general
date: 2026-06-21
description: Przewodnik po formacie dat w Aspose Cells – dowiedz się, jak ustawić
  własny format daty, zmienić ustawienia regionalne skoroszytu i zastosować globalny
  format daty w Javie.
draft: false
keywords:
- aspose cells date format
- set custom date format
- how to set date format
- change workbook locale
- set global date format
language: pl
og_description: 'Samouczek formatowania dat w Aspose Cells: dowiedz się, jak ustawić
  własny format daty, zmienić lokalizację skoroszytu i ustawić globalny format daty
  dla projektów Java.'
og_title: Format daty w Aspose Cells – Ustaw niestandardowy format daty w Javie
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
title: 'Format daty w Aspose Cells: jak ustawić własny format daty w Javie'
url: /pl/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Cells Date Format – Kompletny przewodnik Java

Zastanawiałeś się kiedyś, jak ustawić własny format daty w Aspose Cells dla Javy? Nie jesteś jedyny. Niezależnie od tego, czy generujesz raporty dla japońskiego klienta, czy po prostu potrzebujesz spójnego stylu dat w całym skoroszycie, opanowanie **aspose cells date format** jest niezbędne.

W tym samouczku przeprowadzimy praktyczny, kompleksowy przykład, który pokaże Ci **jak ustawić format daty** globalnie, zmienić lokalizację skoroszytu i zastosować własny wzorzec, taki jak japoński rok ery. Po zakończeniu będziesz mieć gotowy fragment kodu, który możesz wkleić do dowolnego projektu — bez zgadywania.

## Co obejmuje ten przewodnik

- Utworzenie nowej instancji `Workbook`.
- Zmiana lokalizacji skoroszytu, aby wbudowane formaty respektowały regionalne zasady.
- Definiowanie **set custom date format** przy użyciu `DateTimeFormatter`.
- Zastosowanie tego formatu globalnie przy pomocy `WorkbookSettings`.
- Typowe pułapki (np. nadpisywanie formatów na poziomie komórek) i jak ich unikać.
- Szybkie warianty dla innych lokalizacji lub ciągów formatów.

Wystarczy środowisko programistyczne Java, Maven lub Gradle do pobrania Aspose Cells oraz podstawowa znajomość składni Javy. Gotowy? Zanurzmy się.

## Krok 1: Skonfiguruj projekt i zaimportuj Aspose Cells

Na początek — upewnij się, że Aspose Cells for Java znajduje się na classpath. Jeśli używasz Maven, dodaj następującą zależność do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

Użytkownicy Gradle mogą dodać:

```gradle
implementation 'com.aspose:aspose-cells:24.9'
```

> **Wskazówka:** Aspose oferuje darmową 30‑dniową wersję próbną licencji. Umieść plik `Aspose.Cells.lic` w katalogu głównym projektu i wywołaj `License license = new License(); license.setLicense("Aspose.Cells.lic");` przed utworzeniem jakiegokolwiek skoroszytu.

Teraz zaimportuj klasy, których będziemy potrzebować:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import com.aspose.cells.DateTimeFormatter;
import com.aspose.cells.CultureInfo;
```

Te importy dają dostęp do kontenera skoroszytu, jego ustawień oraz formatatora uwzględniającego lokalizację.

## Krok 2: Utwórz nowy skoroszyt i uzyskaj dostęp do jego ustawień

Nowy `Workbook` rozpoczyna się z domyślną (zazwyczaj US) lokalizacją. Aby globalnie kontrolować obsługę dat, musimy pobrać jego obiekt `WorkbookSettings`:

```java
// Step 2: Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the settings object – this is where we’ll apply the date format
WorkbookSettings settings = workbook.getSettings();
```

Obiekt `settings` jest centralnym węzłem. Wszystko, co tutaj zmienisz — np. format daty — wpływa na każdą komórkę, która **nie** ma już wyraźnie nadpisanego stylu.

## Krok 3: Zdefiniuj własny format daty/czasu (przykład japońska era)

Załóżmy, że potrzebujesz dat w formacie japońskiej ery, np. „令和04.10.01”. Wzorzec `"ggyy.MM.dd"` działa, gdy jest użyty z japońską kulturą:

```java
// Step 3: Build a formatter for the Japanese era year
DateTimeFormatter formatter = new DateTimeFormatter(
        "ggyy.MM.dd",                // Pattern: era (gg), year (yy), month, day
        new CultureInfo("ja-JP")    // Locale: Japanese (Japan)
);
```

Jeśli wolisz prostszy styl ISO (`"yyyy-MM-dd"`), po prostu zamień ciąg wzorca — nie są potrzebne żadne inne zmiany.

## Krok 4: Zastosuj własny format jako globalny format daty

Teraz łączymy formatator z globalnymi ustawieniami skoroszytu. To krok **set global date format**, który zapewnia, że każda komórka wyświetlająca datę automatycznie używa naszego wzorca:

```java
// Step 4: Apply the custom formatter globally
settings.setDateTimeFormat(formatter);
```

W tym momencie każda data wpisana do arkusza — niezależnie czy przez `Cell.putValue(new Date())`, czy odczytana ze źródła danych — będzie wyświetlana przy użyciu japońskiego wzorca ery.

## Krok 5: Wypełnij skoroszyt przykładowymi datami (opcjonalnie)

Dodajmy kilka wierszy, aby zobaczyć format w działaniu. Ta część nie jest ściśle wymagana dla logiki formatowania dat, ale pomaga zweryfikować, że wszystko działa:

```java
// Step 5: Insert sample dates into the first sheet
var sheet = workbook.getWorksheets().get(0);
var cells = sheet.getCells();

cells.get("A1").putValue(new java.util.Date()); // Today’s date
cells.get("A2").putValue(java.sql.Date.valueOf("2024-12-31")); // Specific date
cells.get("A3").putValue(java.time.LocalDateTime.now()); // Date‑time now
```

Po zapisaniu skoroszytu, te komórki wyświetlą coś w rodzaju:

```
A1: 令和05.04.21
A2: 令和06.12.31
A3: 令和05.04.21 14:37:12
```

(Dokładny rok ery zależy od bieżącego japońskiego kalendarza.)

## Krok 6: Zapisz skoroszyt i zweryfikuj wynik

Na koniec zapisz skoroszyt do pliku, aby móc otworzyć go w Excelu, LibreOffice lub dowolnym przeglądarce, która respektuje format:

```java
// Step 6: Save the workbook
workbook.save("CustomDateFormatDemo.xlsx");
System.out.println("Workbook saved with custom date format.");
```

Otwórz `CustomDateFormatDemo.xlsx` i powinieneś zobaczyć daty sformatowane zgodnie z ustalonym wzorcem. Jeśli zauważysz niezgodność, sprawdź ponownie, czy żaden styl na poziomie komórki nie nadpisuje globalnego ustawienia (zobacz sekcję „Edge Cases” poniżej).

## Przypadki brzegowe i warianty

### 1. Nadpisywanie globalnego formatu na poziomie komórki

Jeśli komórka już ma styl z określonym formatem liczbowym, globalne ustawienie jest ignorowane dla tej komórki. Aby wymusić globalny format, wyczyść styl komórki:

```java
cells.get("A1").getStyle().setNumber(0); // Reset number format to default
```

### 2. Zmiana lokalizacji skoroszytu bez własnego wzorca

Czasami po prostu chcesz **change workbook locale**, aby wbudowane formaty dat (np. `14‑03‑2024`) odpowiadały regionalnym konwencjom. Możesz to zrobić bez `DateTimeFormatter`:

```java
WorkbookSettings localeSettings = workbook.getSettings();
localeSettings.setCultureInfo(new CultureInfo("fr-FR")); // French (France)
```

Teraz każdy domyślny styl daty będzie wyświetlany jako `21/04/2025` zamiast `04/21/2025`.

### 3. Używanie wielu własnych formatów w jednym skoroszycie

Aspose Cells pozwala zdefiniować kilka własnych formatów i stosować je selektywnie:

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

### 4. Resetowanie do domyślnego formatu

Jeśli musisz przywrócić domyślną obsługę dat Aspose, po prostu przekaż `null`:

```java
settings.setDateTimeFormat(null); // Clears the custom global format
```

## Często zadawane pytania

- **Czy to wpływa na istniejące arkusze?**  
  Tak — każdy arkusz załadowany do `Workbook` po ustawieniu globalnego formatu odziedziczy go, chyba że komórka już ma wyraźny styl.

- **Czy mogę ustawić format po zapisaniu danych?**  
  Oczywiście. Globalny format jest stosowany w czasie renderowania, więc możesz najpierw wypełnić komórki, a potem ustawić format.

- **Co zrobić, jeśli potrzebuję kalendarza specyficznego dla lokalizacji (np. tajski buddyjski)?**  
  Użyj odpowiedniego kodu `CultureInfo` (`"th-TH"`), a formatator automatycznie uwzględni ten kalendarz.

- **Czy to wpływa na wydajność?**  
  Nieznaczny. Formatator jest buforowany w `WorkbookSettings`, więc narzut występuje tylko raz na skoroszyt.

## Pełny działający przykład

Poniżej znajduje się kompletny, gotowy do uruchomienia program, który zawiera wszystkie omówione kroki:

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

**Oczekiwany wynik w Excelu:**

| Komórka | Wartość wyświetlana |
|------|----------------|
| A1   | 令和05.04.21   |
| A2   | 令和06.12.31   |
| A3   | 令和05.04.21 14:45:03 (czas może się różnić) |

Otwórz plik, a zobaczysz daty sformatowane dokładnie tak, jak określono.

## Zakończenie

Właśnie nauczyłeś się, jak **aspose cells date format** skoroszyt w Javie, od zmiany lokalizacji po zastosowanie **set custom date format**, które działa globalnie. Korzystając z `WorkbookSettings` i `DateTimeFormatter`, uzyskujesz precyzyjną kontrolę nad tym, jak każda data jest wyświetlana — bez konieczności ręcznego stylowania.

Następnie możesz zbadać **how to set date format** dla konkretnych kolumn lub połączyć własne formaty liczb z formatowaniem warunkowym, aby uzyskać dopracowany raport. Te same zasady mają zastosowanie: zdefiniuj formatator, podłącz go przez styl i pozwól Aspose zająć się resztą.

Miłego kodowania i śmiało eksperymentuj z innymi lokalizacjami — Twoi użytkownicy podziękują Ci za dopracowane, kulturowo świadome arkusze kalkulacyjne!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Efektywne konwertowanie Excela do PDF z własnymi formatami dat przy użyciu Aspose.Cells dla Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Mistrzostwo prezentacji danych w Excelu: formatowanie liczb i własnych dat przy użyciu Aspose.Cells dla Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Jak tworzyć i formatować komórki Excela przy użyciu Aspose.Cells dla Java: przewodnik krok po kroku](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}