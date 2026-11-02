---
category: general
date: 2026-07-06
description: Jak skopiować tabelę przestawną w Javie przy użyciu Aspose.Cells – krok
  po kroku przewodnik po programowym duplikowaniu tabel przestawnych w Excelu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- duplicate excel pivot
language: pl
lastmod: 2026-07-06
og_description: Jak skopiować tabelę przestawną w Javie przy użyciu Aspose.Cells umożliwia
  szybkie i niezawodne duplikowanie tabel przestawnych w Excelu.
og_image_alt: Screenshot of Java code copying an Excel pivot table with Aspose.Cells
og_title: Jak skopiować tabelę przestawną w Javie – Kompletny przewodnik Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
    to duplicate Excel pivot tables programmatically.
  headline: How to copy pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
title: Jak skopiować tabelę przestawną w Javie przy użyciu Aspose.Cells
url: /pl/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak skopiować tabelę przestawną w Javie przy użyciu Aspose.Cells

Zastanawiałeś się kiedyś **jak skopiować pivot** tabele w pliku Excel bez ręcznego otwierania skoroszytu? Nie jesteś jedyny. W wielu pipeline'ach raportowych musisz **zduplikować tabele przestawne Excel** w locie — być może, aby utworzyć migawkę, przenieść ją na nowy arkusz lub wygenerować szablon dla użytkowników końcowych.

W tym tutorialu przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który dokładnie to pokazuje. Korzystając z biblioteki Aspose.Cells for Java załadujemy skoroszyt, znajdziemy zakres źródłowy tabeli przestawnej, skopiujemy go do nowej lokalizacji i zapiszemy wynik. Bez niejasnych odniesień, tylko konkretne rozwiązanie, które możesz od razu wstawić do swojego projektu.

---

## Wymagania wstępne

* **Java Development Kit (JDK) 8+** – kod kompiluje się na dowolnym aktualnym JDK.
* **Aspose.Cells for Java** wersja 25.11 lub nowsza – metoda `Range.copy` obsługująca tabele przestawne została wprowadzona w tej wersji.
* Plik **input.xlsx**, który już zawiera tabelę przestawną (możesz ją utworzyć w Excelu w celu testów).
* Narzędzie do budowania według własnego wyboru (Maven, Gradle lub zwykły `javac`). Pokażemy zależność Maven dla szybkiego startu.

```xml
<!-- Add this to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.12</version> <!-- Use the latest stable -->
</dependency>
```

---

## Krok 1: Załaduj źródłowy skoroszyt

Pierwszą rzeczą, którą robimy, jest otwarcie pliku Excel, który zawiera oryginalną tabelę przestawną. Aspose.Cells traktuje skoroszyt jako obiekt w pamięci, więc możesz nim manipulować bez uruchamiania Excela.

```java
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

> **Dlaczego to ważne:** Załadowanie skoroszytu daje dostęp do arkuszy, komórek i, co najważniejsze, pamięci podręcznej pivot, która obsługuje tabelę przestawną. Bez tego kroku biblioteka nie ma czego kopiować.

---

## Krok 2: Pobierz arkusz zawierający tabelę przestawną

Jeśli Twój skoroszyt ma wiele arkuszy, musisz wskazać właściwy. Tutaj po prostu pobieramy pierwszy arkusz, ale możesz także użyć `get("SheetName")` dla wyszukiwania po nazwie.

```java
// Obtain the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Pro tip:** Przy pracy z wieloma arkuszami, zapamiętaj indeks lub nazwę w pliku konfiguracyjnym, aby uniknąć twardego kodowania liczb.

---

## Krok 3: Zdefiniuj zakres źródłowy obejmujący tabelę przestawną

Od wersji 25.11 Aspose.Cells pozwala traktować tabelę przestawną jako zwykły zakres komórek. Określ komórki w lewym‑górnym i prawym‑dolnym rogu, które obejmują całą tabelę przestawną.

```java
// The range A1:D20 covers the whole pivot table in this example
Range sourceRange = worksheet.getCells().createRange("A1:D20");
```

> **Edge case:** Jeśli Twoja tabela przestawna rozszerza się dynamicznie (np. później dodawane są wiersze), rozważ użycie `worksheet.getPivotTables().get(0).getDataRange()` aby programowo pobrać dokładny zakres.

---

## Krok 4: Zdefiniuj zakres docelowy, w którym tabela przestawna zostanie skopiowana

Wybierz dowolną pustą komórkę, w której ma pojawić się zduplikowana tabela przestawna. W tym demo zaczynamy od **F1**, pozostawiając przerwę między oryginałem a kopią.

```java
// Destination starts at cell F1 – adjust as needed
Range destinationRange = worksheet.getCells().createRange("F1");
```

> **Dlaczego nie nowy arkusz?** Możesz także utworzyć nowy arkusz (`workbook.getWorksheets().add("Copy")`) i użyć jego komórek jako docelowych. Ta sama metoda `copy` działa pomiędzy arkuszami.

---

## Krok 5: Skopiuj tabelę przestawną do nowej lokalizacji

Teraz dzieje się magia. Metoda `copy` klonuje tabelę przestawną, jej pamięć podręczną, formatowanie i nawet powiązane segmentatory (od najnowszej wersji).

```java
// Perform the copy – the pivot is now duplicated at the destination
sourceRange.copy(destinationRange);
```

> **Important:** Operacja kopiowania jest *głęboka*; **nie** tworzy odwołania do oryginalnej tabeli przestawnej. Możesz modyfikować nową tabelę niezależnie, nie wpływając na źródło.

---

## Krok 6: Zapisz skoroszyt z zduplikowaną tabelą przestawną

Na koniec zapisz zmodyfikowany skoroszyt na dysku. Możesz nadpisać oryginał lub utworzyć nowy plik; tutaj wybieramy to drugie, aby pozostawić źródło nietknięte.

```java
// Save the workbook – the duplicated pivot lives in output.xlsx
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

Gdy otworzysz **output.xlsx** w Excelu, zobaczysz oryginalną tabelę przestawną w kolumnach A‑D oraz idealną kopię zaczynającą się od kolumny F. Obie tabele można odświeżać osobno.

## Pełny działający przykład

Łącząc wszystko razem, oto kompletna klasa Java, którą możesz skompilować i uruchomić od razu:

```java
import com.aspose.cells.*;

public class ExportPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Define the source range that includes the pivot table (supported from version 25.11)
        // Adjust the range to match your actual pivot dimensions
        Range sourceRange = worksheet.getCells().createRange("A1:D20");

        // Step 4: Define the destination range where the pivot table will be copied
        // Change "F1" to any starting cell you prefer
        Range destinationRange = worksheet.getCells().createRange("F1");

        // Step 5: Copy the pivot table to the new location
        sourceRange.copy(destinationRange);

        // Step 6: Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Expected result:** Otwierając `output.xlsx` zobaczysz oryginalną tabelę przestawną (A1:D20) oraz identyczną tabelę zaczynającą się od F1. Obie tabele zachowują filtry, style i pola obliczeniowe.

## Obsługa typowych wariantów

| Sytuacja | Co należy dostosować |
|-----------|----------------------|
| **Wiele tabel przestawnych** na tym samym arkuszu | Iteruj przez `worksheet.getPivotTables()` i skopiuj każdą, używając własnego zakresu docelowego. |
| **Dynamiczny zakres danych** | Użyj `worksheet.getPivotTables().get(0).getDataRange()` aby automatycznie wykryć obszar źródłowy. |
| **Kopiowanie do innego skoroszytu** | Załaduj drugi obiekt `Workbook`, utwórz arkusz docelowy, a następnie wywołaj `sourceRange.copy(destWorksheet.getCells().createRange("A1"))`. |
| **Zachowanie segmentatorów** | Od wersji 25.12 segmentatory są kopiowane automatycznie, gdy zakres je obejmuje. Zweryfikuj w Excelu po zapisaniu. |

## Porady i pułapki

* **Version check:** Metoda `copy` obsługująca tabele przestawne została dodana w **Aspose.Cells 25.11**. Jeśli używasz starszej wersji, otrzymasz wyjątek. Zawsze sprawdzaj wersję `aspose-cells` w swoim `pom.xml`.
* **Performance:** Kopiowanie dużych tabel przestawnych może być intensywne pod względem pamięci. Jeśli potrzebujesz tylko danych, rozważ wyeksportowanie pivotu do płaskiej tabeli zamiast klonowania całego obiektu.
* **Refresh behavior:** Zduplikowana tabela przestawna zachowuje własną pamięć podręczną. Jeśli zmodyfikujesz dane źródłowe, wywołaj `pivotTable.refresh()` na nowej tabeli, aby przeliczyć wyniki.
* **Formatting quirks:** Niektóre niestandardowe formaty liczb mogą nie przetrwać kopiowania w bardzo starych wersjach Excela (<2007). Przetestuj na wersji Excela używanej przez docelowych odbiorców.

## Zakończenie

Masz teraz solidną, kompleksową odpowiedź na **jak skopiować pivot** tabele przy użyciu Aspose.Cells for Java oraz widziałeś, jak **zduplikować tabele przestawne Excel** w kilku linijkach kodu. Podejście działa dla jednej lub wielu tabel, na różnych arkuszach, a nawet pomiędzy skoroszytami.

Kolejne kroki mogą obejmować:

* Automatyzację kopiowania każdej tabeli przestawnej w zadaniu wsadowym.
* Dodanie kodu zmieniającego nazwę zduplikowanej tabeli (np. `pivotTable.setName("Copy_of_Sales")`).
* Integrację tej procedury w większej usłudze raportowej, która generuje PDF‑y lub eksporty CSV.

Wypróbuj, dopasuj zakresy do swoich rzeczywistych danych i pozwól bibliotece wykonać ciężką pracę. Szczęśliwego kodowania!

## Co warto się nauczyć dalej?

Poniższe tutoriale dotyczą ściśle powiązanych tematów, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne przykłady kodu oraz szczegółowe wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Jak tworzyć tabele przestawne w Excelu przy użyciu Aspose.Cells dla Javy: Kompletny przewodnik](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Manipulacja tabelami przestawnymi Excel przy użyciu Aspose.Cells Java: Kompletny przewodnik](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Jak zaktualizować źródło tabeli przestawnej Excel przy użyciu Aspose.Cells dla Javy: Kompletny przewodnik](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}