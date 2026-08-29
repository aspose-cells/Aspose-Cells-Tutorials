---
category: general
date: 2026-08-11
description: Jak usunąć filtr automatyczny w Excelu przy użyciu Aspose.Cells dla Javy
  – dowiedz się, jak usunąć filtr automatyczny z Excela, wyłączyć filtr automatyczny
  w Excelu oraz programowo usunąć filtr w Excelu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to clear autofilter
- remove autofilter from excel
- remove excel filter
- how to remove autofilter
- disable autofilter in excel
language: pl
lastmod: 2026-08-11
og_description: Jak usunąć autofiltr w Excelu przy użyciu Aspose.Cells dla Javy. Przejdź
  ten kompletny poradnik, aby usunąć autofiltr z Excela, wyłączyć autofiltr w Excelu
  i uporządkować swoje arkusze.
og_image_alt: Screenshot showing Java code that clears an autofilter in an Excel file
  with Aspose.Cells
og_title: Jak wyczyścić autofilter w Excelu przy użyciu Aspose.Cells (Java) – przewodnik
  krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: How to clear autofilter in Excel with Aspose.Cells for Java – learn
    to remove autofilter from Excel, disable autofilter in Excel, and remove Excel
    filter programmatically.
  headline: How to clear autofilter in Excel with Aspose.Cells (Java)
  type: TechArticle
- description: How to clear autofilter in Excel with Aspose.Cells for Java – learn
    to remove autofilter from Excel, disable autofilter in Excel, and remove Excel
    filter programmatically.
  name: How to clear autofilter in Excel with Aspose.Cells (Java)
  steps:
  - name: '`TableWithFilter.xlsx` remains unchanged.'
    text: '`TableWithFilter.xlsx` remains unchanged.'
  - name: '`NoAutoFilter.xlsx` contains the same data, but the AutoFilter drop‑down
      arrows are no longer visible.'
    text: '`NoAutoFilter.xlsx` contains the same data, but the AutoFilter drop‑down
      arrows are no longer visible.'
  - name: If you open the file, the **remove autofilter from excel** operation will
      be evident in the UI (no filter icons on column headers).
    text: If you open the file, the **remove autofilter from excel** operation will
      be evident in the UI (no filter icons on column headers).
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Jak wyczyścić autofiltr w Excelu przy użyciu Aspose.Cells (Java)
url: /pl/java/worksheet-management/how-to-clear-autofilter-in-excel-with-aspose-cells-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak usunąć autofilter w Excelu przy użyciu Aspose.Cells (Java)

Jak usunąć autofilter w Excelu przy użyciu Aspose.Cells dla Java jest częstą potrzebą przy generowaniu raportów programowo. Ten przewodnik pokazuje, jak szybko i bezpiecznie usunąć autofilter z arkuszy Excel, aby ostateczny plik wyglądał czysto dla użytkowników końcowych.

Zobaczysz pełny, gotowy do uruchomienia przykład, który ładuje skoroszyt, uzyskuje dostęp do pierwszej tabeli, usuwa AutoFilter i zapisuje wynik. Tutorial obejmuje także warianty, takie jak obsługa wielu tabel, praca ze starszymi wersjami Aspose.Cells oraz unikanie typowych pułapek. Nie potrzebna jest zewnętrzna dokumentacja – po prostu skopiuj kod, dostosuj ścieżki plików i uruchom.

## Wymagania wstępne

Przed rozpoczęciem upewnij się, że masz:

* Zainstalowany Java 8 lub nowsza.
* Aspose.Cells for Java 25.11 lub nowszy (metoda `clear()` została dodana w wersji 25.11).
* Plik Excel (`TableWithFilter.xlsx`) zawierający tabelę z zastosowanym AutoFilter.
* Środowisko programistyczne (IDE, Maven/Gradle lub zwykłe `javac`).

Jeśli używasz Maven, dodaj zależność:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.11</version>
    <classifier>jdk17</classifier> <!-- adjust for your JDK version -->
</dependency>
```

## Jak usunąć autofilter w Excelu przy użyciu Aspose.Cells

Poniżej znajduje się kompletny program w języku Java. Każdy krok zawiera krótkie wyjaśnienie „dlaczego”, abyś zrozumiał przepływ API, a nie tylko składnię.

```java
import com.aspose.cells.*;

public class RemoveAutoFilter {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains a table with an AutoFilter
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableWithFilter.xlsx");

        // Step 2: Access the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Retrieve the first ListObject (table) on the worksheet
        // ListObject represents an Excel table; it holds the AutoFilter object.
        ListObject table = worksheet.getListObjects().get(0);

        // Step 4: Clear the AutoFilter applied to the table (new API in 25.11)
        // The clear() method removes the filter criteria and disables the drop‑down arrows.
        table.getAutoFilter().clear();

        // Step 5: Save the modified workbook without the AutoFilter
        workbook.save("YOUR_DIRECTORY/NoAutoFilter.xlsx");
    }
}
```

### Dlaczego każdy wiersz ma znaczenie

| Krok | Cel |
|------|-----|
| **Załaduj skoroszyt** | Otwiera plik Excel w pamięci, aby Aspose.Cells mógł manipulować jego zawartością. |
| **Uzyskaj dostęp do arkusza** | Pliki Excel mogą zawierać wiele arkuszy; potrzebujesz właściwego, aby pracować z tabelą. |
| **Pobierz ListObject** | ListObject jest programistyczną reprezentacją tabeli Excel. Tabela zawiera obiekt AutoFilter. |
| **Wyczyść AutoFilter** | `clear()` usuwa kryteria filtru i ukrywa strzałki filtru. To podstawowa operacja dla *remove autofilter from excel*. |
| **Zapisz skoroszyt** | Zapisuje zmiany na dysk, tworząc plik, w którym filtr jest wyłączony. |

## Usuń filtr Excel z wielu tabel (opcjonalnie)

Jeśli Twój skoroszyt zawiera więcej niż jedną tabelę, iteruj po kolekcji `ListObjects`:

```java
Worksheet ws = workbook.getWorksheets().get(0);
for (int i = 0; i < ws.getListObjects().getCount(); i++) {
    ListObject tbl = ws.getListObjects().get(i);
    tbl.getAutoFilter().clear();   // disables filter for each table
}
```

Ten fragment kodu demonstruje **jak usunąć autofilter** z każdej tabeli w arkuszu, co jest przydatne przy przetwarzaniu raportów wsadowych.

## Obsługa skoroszytów bez AutoFilter

Wywołanie `clear()` na tabeli, która nie ma filtru, nie generuje wyjątku – jest operacją bez efektu. Jednak jeśli spróbujesz uzyskać dostęp do nieistniejącej tabeli (`get(0)` gdy kolekcja jest pusta), Aspose.Cells zgłosi `IndexOutOfRangeException`. Zabezpiecz się przed tym prostym sprawdzeniem:

```java
if (worksheet.getListObjects().getCount() > 0) {
    ListObject firstTable = worksheet.getListObjects().get(0);
    firstTable.getAutoFilter().clear();
}
```

Ten defensywny wzorzec pomaga **wyłączyć autofilter w excel** bezpiecznie w różnych plikach wejściowych.

## Zgodność ze starszymi wersjami Aspose.Cells

Metoda `clear()` została wprowadzona w wersji 25.11. Dla wcześniejszych wydań musisz ręcznie zresetować zakres filtru:

```java
AutoFilter filter = table.getAutoFilter();
filter.setRange("");               // removes the filter range
filter.setShowFilter(false);       // hides filter arrows
```

Choć to działa, nowsze API `clear()` jest bardziej czytelne i mniej podatne na błędy. Jeśli możesz zaktualizować, zrób to, aby uprościć kod.

## Częste pułapki i wskazówki profesjonalne

* **Separatory ścieżek plików** – Używaj `File.separator` lub ukośników (`/`), aby uniknąć problemów specyficznych dla platformy.
* **Blokowanie skoroszytu** – Upewnij się, że plik źródłowy nie jest otwarty w Excelu, gdy Twój proces Java zapisuje go; w przeciwnym razie `save()` zgłosi `IOException`.
* **Duże skoroszyty** – Dla plików >100 MB rozważ użycie parametru `loadOptions`, aby załadować tylko wymagane arkusze, zmniejszając zużycie pamięci.
* **Testowanie wyniku** – Otwórz zapisany `NoAutoFilter.xlsx` w Excelu i sprawdź, czy strzałki filtru zniknęły. Możesz także programowo sprawdzić `table.getAutoFilter().isShowFilter()`; powinno zwrócić `false`.

## Oczekiwany wynik

Po uruchomieniu programu:

1. `TableWithFilter.xlsx` pozostaje niezmieniony.
2. `NoAutoFilter.xlsx` zawiera te same dane, ale strzałki rozwijane AutoFilter nie są już widoczne.
3. Jeśli otworzysz plik, operacja **remove autofilter from excel** będzie widoczna w interfejsie (brak ikon filtru w nagłówkach kolumn).

## Pełny plik źródłowy do kopiowania i wklejania

Zapisz poniższy kod jako `RemoveAutoFilter.java`. Dostosuj placeholder `YOUR_DIRECTORY` do ścieżki bezwzględnej lub względnej na swoim komputerze.

```java
import com.aspose.cells.*;

public class RemoveAutoFilter {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains a table with an AutoFilter
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableWithFilter.xlsx");

        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Retrieve the first ListObject (table) on the worksheet
        ListObject table = worksheet.getListObjects().get(0);

        // Clear the AutoFilter applied to the table (new API in 25.11)
        table.getAutoFilter().clear();

        // Save the modified workbook without the AutoFilter
        workbook.save("YOUR_DIRECTORY/NoAutoFilter.xlsx");
    }
}
```

Kompiluj i uruchom:

```bash
javac -cp "path/to/aspose-cells-25.11.jar" RemoveAutoFilter.java
java -cp ".:path/to/aspose-cells-25.11.jar" RemoveAutoFilter
```

Powinieneś nie zobaczyć żadnego wyjścia w konsoli, jeśli wszystko się powiodło; wynikowy plik znajdzie się w tym samym katalogu.

## Podsumowanie

Teraz wiesz **jak usunąć autofilter** w Excelu przy użyciu Aspose.Cells dla Java. Tutorial obejmował podstawowe kroki, jak **remove autofilter from excel** dla wielu tabel, jak obsługiwać skoroszyty bez filtrów oraz co zrobić przy użyciu starszych wersji biblioteki. Postępując zgodnie z kompletnym przykładem, możesz zintegrować usuwanie filtrów w dowolnym zautomatyzowanym procesie raportowania.

**Kolejne kroki**

* Zbadaj inne funkcje Aspose.Cells, takie jak **disable autofilter in excel**, zachowując formatowanie tabeli.
* Połącz tę technikę z usuwaniem walidacji danych (`ListObject.getValidation().clear()`), aby uzyskać w pełni czysty eksport.
* Przejrzyj dokumentację API Aspose.Cells pod kątem dodatkowych manipulacji tabelą, takich jak dodawanie wierszy czy stylowanie komórek.

Śmiało eksperymentuj z różnymi strukturami plików i podziel się swoimi odkryciami. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Automatyzacja filtrowania Excel przy użyciu Aspose.Cells w Java: Kompleksowy przewodnik po implementacji AutoFilter](/cells/english/java/data-analysis/aspose-cells-java-apply-autofilter-excel/)
- [Implementacja AutoFilter 'Zaczyna się od' w Excelu przy użyciu Aspose.Cells Java](/cells/english/java/data-analysis/implement-autofilter-begins-with-aspose-cells-java/)
- [Implementacja AutoFilter 'Kończy się na' w Excelu przy użyciu Aspose.Cells dla Java: Kompleksowy przewodnik](/cells/english/java/data-analysis/aspose-cells-java-autofilter-ends-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}