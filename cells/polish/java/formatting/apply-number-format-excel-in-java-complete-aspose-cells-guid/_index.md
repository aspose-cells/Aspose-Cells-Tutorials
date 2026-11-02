---
category: general
date: 2026-07-20
description: Zastosuj formatowanie liczb w Excelu przy użyciu Javy i Aspose.Cells.
  Dowiedz się, jak zastosować styl walutowy w Excelu, utworzyć skoroszyt Excel w Javie
  oraz efektywnie importować DataTable do Excela.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- apply currency style excel
- create excel workbook java
- import datatable to excel
language: pl
lastmod: 2026-07-20
og_description: Zastosuj formatowanie liczb w Excelu przy użyciu Javy. Ten przewodnik
  pokazuje, jak zastosować styl walutowy w Excelu, utworzyć skoroszyt Excel w Javie
  oraz importować tabelę danych do Excela krok po kroku.
og_image_alt: Screenshot of an Excel workbook where apply number format excel has
  been applied to a currency column
og_title: Zastosuj formatowanie liczb w Excelu w Javie – Pełny poradnik Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Apply number format excel using Java and Aspose.Cells. Learn how to
    apply currency style excel, create excel workbook java, and import datatable to
    excel efficiently.
  headline: Apply Number Format Excel in Java – Complete Aspose.Cells Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Open the workbook with `new Workbook("Existing.xlsx")`, fetch
      the target worksheet, and follow steps 3‑5 to apply the style array to new data.
    question: Can I apply the number format to an existing workbook?
  - answer: Use a different built‑in number index (`14` for short date, `22` for long
      date) or a custom format like `yyyy‑mm‑dd`. The workflow stays the same.
    question: What if I need to format dates instead of currency?
  - answer: 'Yes. Just change the file extension in `workbook.save("MyFile.xls")`.
      Aspose will automatically switch to the binary format. ## Wrap‑Up – What We
      Achieved We have **applied number format excel** to a column of monetary values,
      demonstrated how to **apply currency style excel**, shown the simplest wa'
    question: Does this work with older Excel versions (.xls)?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Zastosowanie formatu liczbowego w Excelu w Javie – Kompletny przewodnik Aspose.Cells
url: /pl/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zastosowanie formatu liczbowego w Excelu w Javie – Kompletny przewodnik Aspose.Cells

Zastanawiałeś się kiedyś, jak **apply number format excel** bezpośrednio z kodu Java? Być może tworzysz raporty finansowe lub potrzebujesz szybkiego sposobu na sformatowanie kolumny kwot bez ręcznego otwierania Excela. Dobra wiadomość? Dzięki Aspose.Cells możesz to zrobić w kilku linijkach kodu, a przy okazji nauczysz się **apply currency style excel**, **create excel workbook java** oraz **import datatable to excel** w jednej, schludnej procedurze.

W tym tutorialu przejdziemy przez praktyczny przykład: lista kwot przechowywana w `List<Map<String,Object>>` zostaje zaimportowana do nowego skoroszytu, pierwsza kolumna otrzymuje wbudowany format walutowy, a plik zostaje zapisany gotowy do dystrybucji. Gotowy, by zobaczyć, jak to proste? Zanurzmy się.

## Prerequisites – What You’ll Need

Zanim zaczniemy, upewnij się, że masz:

- **Java Development Kit (JDK) 8+** – kod działa na dowolnym współczesnym JDK.
- Bibliotekę **Aspose.Cells for Java** (artefakt Maven `com.aspose:aspose-cells`) – to silnik, który pozwala manipulować plikami Excel bez zainstalowanego Office.
- **Ulubione IDE** (IntelliJ IDEA, Eclipse, VS Code…) – dowolny edytor się sprawdzi, ale IDE przyspiesza debugowanie.
- Podstawową znajomość **Java collections** – użyjemy `List` z `Map`, aby zasymulować DataTable.

To wszystko. Bez zewnętrznych serwisów, bez instalacji Excela, czysta Java.

## Step 1: Create Excel Workbook Java – Instantiating the Workbook

Pierwszą rzeczą, której potrzebujemy, jest obiekt skoroszytu. Pomyśl o nim jak o pustym płótnie, na którym umieścimy wszystko.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook(); // creates an in‑memory Excel file
```

Dlaczego najpierw tworzymy skoroszyt? Aspose.Cells działa w całości w pamięci, więc możesz dodawać arkusze, style i dane, zanim dotkniesz dysku. Takie podejście jest szybkie i ułatwia testowanie kodu.

## Step 2: Prepare Data – Import Datatable to Excel Using a List of Maps

W wielu aplikacjach korporacyjnych dane pochodzą z baz jako tabele. Tutaj symulujemy to przy pomocy `List<Map<String,Object>>`. Każda mapa reprezentuje wiersz, a klucz `"Amount"` mapuje na wartość liczbową.

```java
// Step 2: Build a DataTable‑like structure (list of maps)
List<Map<String, Object>> dataRows = new ArrayList<>();

// Row 1
dataRows.add(new HashMap<>() {{
    put("Amount", 1234.56);
}});
// Row 2
dataRows.add(new HashMap<>() {{
    put("Amount", 7890.12);
}});
```

Możesz zapytać: „Dlaczego nie użyć `ResultSet` lub POJO?” Metoda `importDataTable` przyjmuje dowolną kolekcję zachowującą się jak DataTable, a lista map jest najprostszym sposobem na pokazanie koncepcji bez dodatkowych zależności.

## Step 3: Define the Number Format – Apply Currency Style Excel

Teraz serce tutorialu: **apply number format excel**. Aspose.Cells dostarcza wbudowane formaty liczb; format walutowy ma indeks 5. Pobieramy domyślny styl z pierwszego arkusza, modyfikujemy jego format liczbowy i przechowujemy go do późniejszego użycia.

```java
// Step 3: Get the default style and set a currency number format
Style currencyStyle = workbook.getWorksheets().get(0).getCells().getDefaultStyle();
currencyStyle.setNumber(5); // 5 = built‑in currency format ($#,##0.00)
```

Dlaczego używamy domyślnego stylu jako bazy? Zawiera już domyślną czcionkę, wyrównanie i inne ustawienia skoroszytu, więc musisz zmienić tylko to, co istotne – w tym wypadku format liczbowy. Jeśli potrzebny byłby niestandardowy format (np. “€#,##0.00”), można wywołać `currencyStyle.setCustom("#,##0.00 €")`.

## Step 4: Set Up Import Options – Linking the Style Array

Aspose.Cells pozwala przekazać tablicę obiektów `Style`, które odpowiadają importowanym kolumnom. Ponieważ nasze dane mają tylko jedną kolumnę, podajemy jednowymiarową tablicę zawierającą styl walutowy.

```java
// Step 4: Configure import options with the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(new Style[] { currencyStyle });
```

Jeśli kiedykolwiek będziesz musiał stylizować wiele kolumn różnie, po prostu rozbuduj tablicę: `new Style[] { styleForCol1, styleForCol2, … }`. Kolejność stylów musi odpowiadać kolejności kolumn w źródłowych danych.

## Step 5: Import Data – Bringing the Datatable Into the Worksheet

Mając gotowy skoroszyt, przygotowane dane i zdefiniowane style, w końcu **import datatable to excel**. Zaczynamy od komórki `A1`, włączamy nagłówki kolumn (`true`) i przekazujemy `ImportTableOptions`.

```java
// Step 5: Perform the import
Worksheet worksheet = workbook.getWorksheets().get(0);
worksheet.getCells().importDataTable(dataRows, true, "A1", importOptions);
```

Zwróć uwagę na flagę `true` – Aspose.Cells automatycznie wygeneruje wiersz nagłówka na podstawie kluczy map (`"Amount"`). Jeśli ustawisz `false`, nagłówek zostanie pominięty, co daje większą kontrolę nad ostatecznym układem.

## Step 6: Save the File – Create Excel Workbook Java on Disk

Ostatni element układanki to zapisanie skoroszytu z pamięci do fizycznego pliku. Możesz wybrać dowolny format obsługiwany przez Aspose (`.xlsx`, `.xls`, `.csv`, …). Tutaj zapisujemy jako plik XLSX.

```java
// Step 6: Save the workbook to disk
String outputPath = "DataTableWithCurrencyStyle.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Po uruchomieniu programu otwórz wygenerowany plik. Zobaczysz kolumnę `"Amount"` sformatowaną z symbolem dolara, dwoma miejscami po przecinku i odpowiednimi separatorami tysięcy – dokładnie to, czego oczekujesz, **apply number format excel** dla wartości walutowych.

## Expected Result

| Kwota |
|-------|
| $1,234.56 |
| $7,890.12 |

Nagłówek „Kwota” pojawia się pogrubioną czcionką (domyślny styl), a każda komórka pod nim wyświetla ustawiony format walutowy. Nie ma potrzeby ręcznego formatowania w Excelu.

## Pro Tips and Common Pitfalls

- **Reuse Styles Wisely** – Style są lekkie, ale tworzenie nowego `Style` dla każdej komórki może obniżyć wydajność. Zawsze używaj tego samego obiektu stylu, gdy stosujesz ten sam format do wielu komórek, tak jak zrobiliśmy to z `currencyStyle`.
- **Custom Formats** – Jeśli Twoja lokalizacja używa innego symbolu waluty, zamień `currencyStyle.setNumber(5)` na `currencyStyle.setCustom("€#,##0.00")`. Przetestuj format w Excelu, aby upewnić się, że działa zgodnie z oczekiwaniami.
- **Large Datasets** – Przy tysiącach wierszy rozważ użycie `importDataTable` z flagą `ImportTableOptions.setImportDataOnly(true)`, aby pominąć generowanie nagłówka i przyspieszyć import.
- **Thread Safety** – Obiekty Aspose.Cells **nie** są bezpieczne wątkowo. Twórz osobny `Workbook` dla każdego wątku, jeśli generujesz raporty równolegle.

## Frequently Asked Questions

**Q: Czy mogę zastosować format liczbowy do istniejącego skoroszytu?**  
A: Oczywiście. Otwórz skoroszyt za pomocą `new Workbook("Existing.xlsx")`, pobierz docelowy arkusz i wykonaj kroki 3‑5, aby zastosować tablicę stylów do nowych danych.

**Q: Co zrobić, jeśli potrzebuję formatować daty zamiast waluty?**  
A: Użyj innego wbudowanego indeksu liczbowego (`14` dla krótkiej daty, `22` dla długiej daty) lub niestandardowego formatu, np. `yyyy‑mm‑dd`. Przebieg pracy pozostaje taki sam.

**Q: Czy to działa ze starszymi wersjami Excela (.xls)?**  
A: Tak. Wystarczy zmienić rozszerzenie pliku w `workbook.save("MyFile.xls")`. Aspose automatycznie przełączy się na format binarny.

## Wrap‑Up – What We Achieved

Zastosowaliśmy **apply number format excel** do kolumny z wartościami pieniężnymi, pokazaliśmy, jak **apply currency style excel**, przedstawiliśmy najprostszy sposób na **create excel workbook java**, oraz użyliśmy Aspose.Cells do **import datatable to excel** bez interakcji z UI. Wszystko to w krótkim, samodzielnym programie, który możesz skopiować, wkleić i uruchomić.

Co dalej? Rozbuduj przykład:

- Dodaj kolejne kolumny (np. „Date”, „Description”) i przypisz różne style do każdej z nich.
- Wyeksportuj te same dane do CSV i zobacz, jak formaty liczb zostają utracone.
- Zintegruj kod z usługą Spring Boot, która zwraca skoroszyt jako pobieralny plik HTTP.

Eksperymentuj, a jeśli napotkasz problemy, zostaw komentarz poniżej. Szczęśliwego kodowania!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Apply Styles to Excel Cells Using Aspose.Cells for Java - Complete Guide](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)
- [Merge Cells & Apply Styles in Excel using Aspose.Cells for Java - A Complete Guide](/cells/english/java/formatting/merge-cells-apply-styles-aspose-cells-java/)
- [Aspose.Cells for Java&#58; How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}