---
category: general
date: 2026-06-30
description: Jak skopiować zakres w Javie przy użyciu Aspose.Cells – duplikować zakres
  Excela, kopiować tabelę przestawną i efektywnie ładować skoroszyt Excel.
draft: false
keywords:
- how to copy range
- copy pivot table
- pivot table to sheet
- duplicate excel range
- load excel workbook
language: pl
og_description: Jak skopiować zakres w Javie przy użyciu Aspose.Cells. Dowiedz się,
  jak duplikować zakres w Excelu, kopiować tabelę przestawną i wczytywać skoroszyt
  Excel w kilka minut.
og_title: Jak skopiować zakres w Javie – Przewodnik krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  headline: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  name: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  steps:
  - name: Expected Output
    text: 'When you execute `CopyPivotDemo`, the console prints:'
  - name: What if the source workbook has multiple worksheets?
    text: You can loop through `sourceWorkbook.getWorksheets()` and copy each relevant
      range. Just be careful to maintain the same sheet names in the destination if
      you need to preserve references.
  - name: Does the copied pivot retain its data source?
    text: Yes. Aspose.Cells copies the pivot cache along with the range, so the destination
      workbook still points to the original data source within the same file. If you
      later move the data to a different sheet, you may need to refresh the pivot
      manually.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot’s data source is an external file, you’ll have to embed that
      data into the destination workbook first (e.g., copy the source data range)
      before copying the pivot. Otherwise the pivot will show “#REF!” errors.
  - name: Can I copy the pivot without the surrounding data?
    text: Absolutely. Just adjust `pivotRange` to cover only the pivot’s cells (usually
      the top‑left corner plus the data area). You can also use `sourceSheet.getPivotTables().get(0).getPivotTableArea()`
      to retrieve the exact range programmatically.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Jak skopiować zakres w Javie – kopiowanie tabeli przestawnej przy użyciu Aspose.Cells
url: /pl/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak skopiować zakres w Javie – kopiowanie tabeli przestawnej przy użyciu Aspose.Cells

Zastanawiałeś się kiedyś **jak skopiować zakres** z jednego skoroszytu Excel do drugiego, nie tracąc integralności tabeli przestawnej? Nie jesteś sam. W wielu przepływach raportowania potrzeba *zduplikowania zakresu Excel* przy zachowaniu logiki przestawnej jest codziennym problemem. Na szczęście Aspose.Cells dla Javy robi to prostym ruchem, a w tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który pokaże także, jak **załadować skoroszyt Excel**, skopiować tabelę przestawną i zapisać wynik.

Pod koniec tego przewodnika będziesz mieć samodzielny program w Javie, który:

* Ładuje istniejący skoroszyt (`load excel workbook`);
* Definiuje dokładne komórki zawierające tabelę przestawną;
* Kopiuje tę **tabelę przestawną do arkusza** w zupełnie nowym skoroszycie;
* Zapisuje nowy plik, gotowy do dalszego przetwarzania.

Bez zewnętrznych skryptów, bez ręcznych kroków — tylko czysty kod.

## Co będzie potrzebne

Zanim zaczniemy, upewnij się, że masz:

* Java 8 lub nowszą (kod działa również z Java 11+);
* bibliotekę Aspose.Cells dla Javy (można ją pobrać z Maven Central);
* dwa przykładowe pliki Excel — jeden źródłowy z tabelą przestawną (`source.xlsx`) oraz folder docelowy, w którym zapiszesz `copy-pivot.xlsx`.

To wszystko. Nie są potrzebne żadne zaawansowane triki IDE; wystarczy dowolny edytor tekstu i `javac`.

## Krok 1: Konfiguracja projektu i import Aspose.Cells

Na początek — dodajmy bibliotekę. Jeśli używasz Maven, dodaj następującą zależność do pliku `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Jeśli nie korzystasz z Maven, pobierz plik JAR ze strony Aspose i umieść go w classpath. Gdy to będzie gotowe, utwórz nową klasę Javy o nazwie `CopyPivotDemo`.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // The implementation will go here.
    }
}
```

> **Pro tip:** Utrzymuj folder `src/main/java` w porządku i nadaj klasie znaczącą nazwę; ułatwi to późniejszą konserwację.

## Krok 2: Załaduj źródłowy skoroszyt (`load excel workbook`)

Teraz faktycznie **load excel workbook**, który zawiera tabelę przestawną, którą chcemy skopiować. Konstruktor `Workbook` przyjmuje ścieżkę do pliku, więc upewnij się, że jest ona poprawna.

```java
// Step 2: Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Dlaczego wybieramy pierwszy arkusz? W większości prostych przypadków tabela przestawna znajduje się na pierwszym arkuszu, ale możesz zmienić indeks lub użyć nazwy arkusza, jeśli zajdzie taka potrzeba. Ta elastyczność jest jedną z zalet Aspose.Cells.

## Krok 3: Zdefiniuj zakres zawierający tabelę przestawną

Tabela przestawna zazwyczaj obejmuje blok komórek. Załóżmy, że zajmuje `A1:G20`. Możesz dostosować adres do własnych danych.

```java
// Step 3: Define the range that includes the pivot table
Range pivotRange = sourceSheet.getCells().createRange("A1:G20");
```

Jeśli nie jesteś pewien dokładnego adresu, otwórz skoroszyt w Excelu, zaznacz całą tabelę przestawną i spójrz na pole nazwy. Pamiętaj, że **duplicate excel range** działa najlepiej, gdy celujesz w dokładny obszar — bez dodatkowych wierszy, bez brakujących kolumn.

## Krok 4: Utwórz nowy skoroszyt docelowy

Potrzebujemy świeżego skoroszytu, który przyjmie skopiowany zakres. To tutaj **copy pivot table** zostanie przeniesione do nowego arkusza.

```java
// Step 4: Create a new workbook to receive the copied range
Workbook destinationWorkbook = new Workbook(); // starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

W tym momencie skoroszyt docelowy jest pusty, ale Aspose.Cells automatycznie dodaje domyślny arkusz, którego użyjemy jako docelowego.

## Krok 5: Skopiuj zakres — tabela przestawna pozostaje nienaruszona

Oto magiczna linia, która **copy pivot table** zachowując wszystkie wewnętrzne połączenia.

```java
// Step 5: Copy the range (pivot table stays intact) to the destination sheet
destinationSheet.getCells().copy(pivotRange,
        destinationSheet.getCells().createRange("A1"));
```

Metoda `copy` przyjmuje dwa argumenty: źródłowy `Range` oraz docelowy `Range`. Rozpoczynając docelowy zakres od `A1`, umieszczamy tabelę przestawną dokładnie tam, gdzie była w źródle. Aspose.Cells kopiuje podkład pamięci tabeli przestawnej, więc nowy skoroszyt nadal wie, jak odświeżyć przestawną.

## Krok 6: Zapisz wynikowy skoroszyt

Na koniec zapisz nowy plik na dysku. Możesz wybrać dowolny format obsługiwany przez Aspose (`.xlsx`, `.xls`, `.csv` itp.). Pozostaniemy przy `.xlsx`.

```java
// Step 6: Save the resulting workbook
destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");
System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
```

Uruchom program, a powinieneś zobaczyć świeży skoroszyt z taką samą strukturą tabeli przestawnej. Otwórz go w Excelu — jeśli wszystko poszło dobrze, będziesz mógł odświeżyć przestawną bez błędów.

### Oczekiwany wynik

Po uruchomieniu `CopyPivotDemo` w konsoli pojawi się:

```
Pivot table successfully copied to copy-pivot.xlsx
```

Otwarcie `copy-pivot.xlsx` pokazuje arkusz identyczny z obszarem tabeli przestawnej w źródle, a **pivot table to sheet** działa tak samo jak oryginał.

## Pełny działający przykład

Poniżej kompletny, gotowy do uruchomienia kod klasy Java, który łączy wszystkie kroki. Skopiuj‑wklej go do swojego IDE, dostosuj ścieżki do plików i uruchom.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook (load excel workbook)
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot table
        // Adjust the address if your pivot occupies a different area
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Create a fresh workbook for the destination
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot table stays intact
        destinationSheet.getCells().copy(pivotRange,
                destinationSheet.getCells().createRange("A1"));

        // 5️⃣ Save the new workbook
        destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");

        System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
    }
}
```

> **Uwaga:** Jeśli Twoja tabela przestawna rozciąga się na więcej niż jeden arkusz, powtórz krok kopiowania dla każdego odpowiedniego arkusza lub użyj `Workbook.copy`, aby sklonować całe arkusze.

## Często zadawane pytania i przypadki brzegowe

### Co zrobić, gdy źródłowy skoroszyt ma wiele arkuszy?

Możesz iterować po `sourceWorkbook.getWorksheets()` i kopiować każdy interesujący Cię zakres. Pamiętaj tylko, aby zachować te same nazwy arkuszy w docelowym skoroszycie, jeśli musisz utrzymać odwołania.

### Czy skopiowana tabela przestawna zachowuje źródło danych?

Tak. Aspose.Cells kopiuje pamięć tabeli przestawnej razem z zakresem, więc skoroszyt docelowy wciąż wskazuje na oryginalne źródło danych w tym samym pliku. Jeśli później przeniesiesz dane do innego arkusza, może być konieczne ręczne odświeżenie tabeli przestawnej.

### Jak skopiować tabelę przestawną korzystającą z zewnętrznego źródła danych?

Gdy źródło danych tabeli przestawnej jest zewnętrznym plikiem, najpierw musisz wstawić te dane do skoroszytu docelowego (np. skopiować zakres źródłowy), zanim skopiujesz samą tabelę przestawną. W przeciwnym razie pojawią się błędy „#REF!”.

### Czy mogę skopiować tabelę przestawną bez otaczających danych?

Oczywiście. Po prostu dopasuj `pivotRange`, aby obejmował tylko komórki tabeli przestawnej (zwykle lewy‑górny róg plus obszar danych). Możesz także użyć `sourceSheet.getPivotTables().get(0).getPivotTableArea()`, aby programowo pobrać dokładny zakres.

## Wskazówki dla projektów produkcyjnych

* **Przetwarzanie wsadowe:** Jeśli musisz zduplikować dziesiątki skoroszytów, opakuj powyższy kod w metodę i wywołuj ją w pętli iterującej po katalogu.
* **Wydajność:** Dla dużych plików, używaj jednej instancji `Workbook` i wywołuj `Workbook.calculateFormula()` dopiero po zakończeniu wszystkich kopiowań.
* **Obsługa błędów:** Otocz logikę kopiowania blokiem try‑catch i loguj `Exception.getMessage()`; Aspose rzuca `CellsException` przy nieprawidłowych zakresach.

## Podsumowanie

Właśnie omówiliśmy **jak skopiować zakres** w Javie przy użyciu Aspose.Cells, pokazując jak **duplicate excel range**, **copy pivot table** oraz **load excel workbook** w jednym schludnym programie. Kroki są proste, kod w pełni uruchamialny, a podejście skaluje się od jednego arkusza do zadań wsadowych na poziomie przedsiębiorstwa.

Gotowy na kolejny wyzwanie? Spróbuj wyeksportować skopiowaną tabelę przestawną do PDF lub programowo odświeżyć ją po dodaniu nowych danych. Oba zadania opierają się na tej samej bazie, więc będziesz dobrze przygotowany, by je zrealizować.

Masz pytania lub chcesz podzielić się własnymi modyfikacjami? zostaw komentarz poniżej — miłego kodowania! 

![Diagram illustrating how a range with a pivot table is copied from one workbook to another](https://example.com/images/how-to-copy-range-diagram.png "how to copy range diagram")


## Co warto nauczyć się dalej?


Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne przykłady kodu oraz szczegółowe wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [How to Implement a Named Range with Workbook Scope in Aspose.Cells Java for Enhanced Excel Data Management](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java: A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}