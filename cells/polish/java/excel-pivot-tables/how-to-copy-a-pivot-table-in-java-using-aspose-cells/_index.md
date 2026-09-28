---
category: general
date: 2026-09-27
description: Kopiowanie tabeli przestawnej w Javie przy użyciu Aspose.Cells – przewodnik
  krok po kroku, który pokazuje, jak skopiować zakres i zachować definicje tabeli
  przestawnej.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot table
- copy range aspose cells
language: pl
lastmod: 2026-09-27
og_description: Skopiuj tabelę przestawną w Javie przy użyciu Aspose.Cells. Zapoznaj
  się z tym kompletnym samouczkiem, aby skopiować zakres w Aspose.Cells i zachować
  definicje tabeli przestawnej w niezmienionej formie.
og_image_alt: Screenshot of copy pivot table operation in Aspose.Cells Java
og_title: Kopiowanie tabeli przestawnej w Javie – szybki przewodnik Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Copy pivot table in Java with Aspose.Cells – a step‑by‑step guide that
    shows how to copy range and preserve pivot definitions.
  headline: How to copy a pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Jak skopiować tabelę przestawną w Javie przy użyciu Aspose.Cells
url: /pl/java/excel-pivot-tables/how-to-copy-a-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak skopiować tabelę przestawną w Javie przy użyciu Aspose.Cells

Jeśli potrzebujesz **copy pivot table** z jednego skoroszytu do drugiego, ten przewodnik pokaże Ci dokładnie, jak to zrobić przy użyciu Aspose.Cells dla Javy. Rozwiązanie działa dla dowolnej tabeli przestawnej, którą utworzyłeś, i zachowuje definicję tabeli przestawnej bez ręcznego odtwarzania.

Nauczysz się, jak załadować plik źródłowy, określić zakres zawierający tabelę przestawną, skopiować ten zakres do nowego skoroszytu i w końcu zapisać wynik. Poradnik obejmuje także typowe pułapki, takie jak zachowanie źródeł danych i obsługa dużych skoroszytów.

## Czego będziesz potrzebować

* Java 17 lub nowsza (kod kompiluje się również z JDK 8+)
* Aspose.Cells for Java 23.9 lub nowsza – najnowsza wersja oferuje najbardziej niezawodne wsparcie **copy range aspose cells**
* Plik Excel źródłowy zawierający tabelę przestawną (np. `SourceWithPivot.xlsx`)
* IDE lub narzędzie budujące (Maven/Gradle), które może odwoływać się do pliku JAR Aspose.Cells

## Krok 1: Załaduj skoroszyt źródłowy zawierający tabelę przestawną

Pierwszym działaniem jest otwarcie skoroszytu, który zawiera tabelę przestawną, którą chcesz zduplikować. Ładowanie pliku tworzy w‑pamięci reprezentację wszystkich arkuszy, komórek i pamięci podręcznych tabel przestawnych.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Access the first worksheet (adjust the index if needed)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Dlaczego to ma znaczenie:**  
Aspose.Cells odczytuje cały skoroszyt, w tym ukryte arkusze pamięci podręcznej tabel przestawnych. Jeśli pominiesz ten krok, późniejsza operacja **copy pivot table** straci podstawowe źródło danych.

## Krok 2: Utwórz pusty skoroszyt docelowy

Następnie utwórz nowy skoroszyt, który przyjmie skopiowaną tabelę przestawną. Rozpoczęcie od czystego skoroszytu zapobiega przypadkowym nadpisaniom.

```java
        // Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Wskazówka:** Domyślny skoroszyt zawiera jeden pusty arkusz, co jest idealne dla prostej kopii. Jeśli potrzebujesz skopiować do konkretnej nazwy arkusza, zmień nazwę `destWs` przy pomocy `destWs.setName("TargetSheet")`.

## Krok 3: Określ zakres źródłowy obejmujący tabelę przestawną

Tabela przestawna zajmuje prostokątny blok komórek. Musisz podać dokładny zakres; w przeciwnym razie zostaną skopiowane tylko surowe dane. W tym przykładzie zakładamy, że tabela przestawna zajmuje **A1:G20**, ale możesz dostosować adres do swojego pliku.

```java
        // Define the range that includes the pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Dlaczego to działa:**  
Gdy wywołujesz `createRange` na kolekcji `Cells` arkusza, Aspose.Cells dołącza definicję tabeli przestawnej, jej pamięć podręczną oraz wszelkie formatowanie. To jest sedno poprawnego **how to copy pivot table**.

## Krok 4: Skopiuj określony zakres do arkusza docelowego

Teraz użyj metody `copy`, aby zduplikować zakres. Metoda kopiuje wszystko wewnątrz zakresu, w tym definicję tabeli przestawnej, formuły i style.

```java
        // Copy the range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));
```

**Ważna uwaga:**  
Jeśli potrzebujesz tylko danych bez tabeli przestawnej, możesz użyć `srcRange.copyData`. Jednak aby wykonać prawdziwe **copy pivot table**, musisz skopiować cały zakres, jak pokazano powyżej.

## Krok 5: Zapisz skoroszyt docelowy

Na koniec zapisz nowy skoroszyt na dysku. Powstały plik będzie zawierał w pełni funkcjonalną tabelę przestawną identyczną ze źródłową.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Uruchomienie programu generuje `CopyPivotResult.xlsx` z takim samym układem tabeli przestawnej, filtrami i obliczeniami jak w oryginalnym pliku.

## Oczekiwany wynik

Po otwarciu `CopyPivotResult.xlsx` w Excelu:

* Tabela przestawna pojawia się w **A1:G20** na pierwszym arkuszu.
* Wszystkie pola wierszy/kolumn, filtry i pola wartości są nienaruszone.
* Odświeżenie tabeli przestawnej aktualizuje to samo źródło danych co skoroszyt źródłowy (jeśli dane źródłowe są osadzone).

## Przypadki brzegowe i praktyczne wskazówki

| Sytuacja | Jak sobie poradzić |
|-----------|------------------|
| **Pivot obejmuje więcej kolumn niż przewidziano** | Użyj `srcWs.getPivotTables().get(0).getPivotTableArea()`, aby programowo uzyskać dokładny adres. |
| **Skoroszyt źródłowy zawiera wiele tabel przestawnych** | Przejdź pętlą po `srcWs.getPivotTables()` i skopiuj każdy zakres osobno, dostosowując adresy docelowe. |
| **Duże skoroszyty powodują obciążenie pamięci** | Włącz `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` przed załadowaniem źródła. |
| **Potrzebujesz skopiować tylko definicję tabeli przestawnej, nie dane** | Po skopiowaniu usuń w docelowym skoroszycie wiersze danych źródłowych przy pomocy `destWs.getCells().deleteRows(startRow, count)`. |
| **Plik docelowy musi zachować oryginalne formatowanie** | Ustaw `CopyOptions` z `options.setPasteType(PasteType.ALL)` dla pełnej wierności kopiowania. |

**Pro tip:** Zawsze weryfikuj skopiowaną tabelę przestawną, wywołując programowo `destWs.getPivotTables().get(0).refresh()`. Zapewnia to aktualność pamięci podręcznej, szczególnie gdy dane źródłowe znajdują się w zewnętrznym połączeniu.

## Pełny, uruchamialny przykład

Poniżej znajduje się cały program, który możesz skopiować‑wkleić do swojego IDE. Zamień `YOUR_DIRECTORY` na rzeczywistą ścieżkę na swoim komputerze.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 3: Define the range that includes the pivot table in the source sheet
        // Adjust the address if your pivot occupies a different area
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 4: Copy the defined range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Uruchomienie tego kodu **copy pivot table** dokładnie tak, jak opisano, i demonstruje najprostszy sposób użycia **copy range aspose cells** przy zachowaniu funkcjonalności tabeli przestawnej.

## Zakończenie

Teraz wiesz, jak **copy pivot table** w Javie przy użyciu Aspose.Cells, od załadowania skoroszytu źródłowego po zapisanie pliku docelowego. Poradnik przedstawił niezbędne kroki, wyjaśnił, dlaczego każdy z nich jest ważny, oraz omówił typowe przypadki brzegowe.  

Następnie możesz zbadać:

* **jak skopiować tabelę przestawną** pomiędzy różnymi arkuszami w tym samym skoroszycie
* Używanie **copy range aspose cells** do duplikowania wykresów lub formatowania warunkowego
* Automatyzacja odświeżania tabeli przestawnej po skopiowaniu, aby utrzymać aktualność danych

Śmiało eksperymentuj z większymi zakresami, wieloma tabelami przestawnymi lub integruj tę logikę w większym potoku przetwarzania Excel. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki dotyczą ściśle powiązanych tematów, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z krok‑po‑kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Kopiowanie tabeli przestawnej w Javie – zachowanie, eksport do PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [Jak zaktualizować źródło tabeli przestawnej Excel przy użyciu Aspose.Cells dla Javy&#58; kompleksowy przewodnik](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Manipulacja tabelą przestawną Excel przy użyciu Aspose.Cells Java&#58; kompleksowy przewodnik](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}