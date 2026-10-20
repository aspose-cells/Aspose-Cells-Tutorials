---
category: general
date: 2026-10-20
description: Dowiedz się, jak skopiować tabelę przestawną przy użyciu Aspose.Cells
  w Javie. Ten samouczek pokazuje, jak skopiować zakres do nowego arkusza i bezpiecznie
  zduplikować arkusz z tabelą przestawną.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new sheet
- duplicate pivot table sheet
language: pl
lastmod: 2026-10-20
og_description: Jak skopiować tabelę przestawną przy użyciu Aspose.Cells w Javie.
  Postępuj zgodnie z tym przewodnikiem, aby skopiować zakres do nowego arkusza i zduplikować
  arkusz z tabelą przestawną bez utraty danych.
og_image_alt: Screenshot showing how to copy pivot table from one worksheet to another
  in a Java program
og_title: Jak skopiować tabelę przestawną w Javie – kompletny samouczek Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  headline: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  name: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Load the workbook that holds the original pivot table.
    text: Load the workbook that holds the original pivot table.
  - name: Identify the exact range that includes the pivot table.
    text: Identify the exact range that includes the pivot table.
  - name: Create a new worksheet that will receive the copied data.
    text: Create a new worksheet that will receive the copied data.
  - name: Use the `Range.copy` method to transfer the range to the new sheet.
    text: Use the `Range.copy` method to transfer the range to the new sheet.
  - name: Save the workbook to a new file.
    text: Save the workbook to a new file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Jak skopiować tabelę przestawną w Javie przy użyciu Aspose.Cells – przewodnik
  krok po kroku
url: /pl/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells-step-by-st/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak skopiować tabelę przestawną w Javie przy użyciu Aspose.Cells – przewodnik krok po kroku

Jeśli potrzebujesz **jak skopiować tabelę przestawną** w aplikacji Java, ten przewodnik przeprowadzi Cię przez dokładne kroki. Niezależnie od tego, czy tworzysz silnik raportowania, czy automatyzujesz migrację danych, zobaczysz, jak skopiować zakres do nowego arkusza, zachowując definicję i dane tabeli przestawnej.

Kopiowanie tabeli przestawnej może wydawać się ryzykowne, ponieważ ukryta pamięć podręczna i ustawienia pól często zostają utracone. Ten tutorial demonstruje niezawodne podejście przy użyciu Aspose.Cells, prezentuje kompletny działający kod i wyjaśnia, dlaczego każda linia ma znaczenie. Po zakończeniu będziesz w stanie zduplikować arkusz z tabelą przestawną w kilka sekund.

## Wymagania wstępne

* Java 8 lub nowsza zainstalowana.
* Aspose.Cells for Java (wersja 23.10 lub późniejsza) dodana do classpathu projektu.
* Plik źródłowy workbook (`source.xlsx`) zawierający tabelę przestawną w zakresie `A1:G20`.
* Podstawowa znajomość Javy i koncepcji Excela.

Nie są wymagane dodatkowe biblioteki; Aspose.Cells obsługuje wszystkie operacje Excel wewnętrznie.

## Jak skopiować tabelę przestawną – ogólna strategia

Podstawowa idea jest prosta:

1. Załaduj workbook, który zawiera oryginalną tabelę przestawną.
2. Zidentyfikuj dokładny zakres, który zawiera tabelę przestawną.
3. Utwórz nowy arkusz, który otrzyma skopiowane dane.
4. Użyj metody `Range.copy`, aby przenieść zakres do nowego arkusza.  
   Metoda ta automatycznie kopiuje pamięć podręczną tabeli przestawnej, więc tabela pozostaje funkcjonalna.
5. Zapisz workbook do nowego pliku.

Ponieważ operacja kopiowania działa na poziomie zakresu, **zduplikowany arkusz z tabelą przestawną** zachowuje wszystkie konfiguracje pól, filtry i elementy obliczeniowe.

## Krok 1: Załaduj źródłowy workbook

```java
// Import Aspose.Cells classes
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Dlaczego to ważne*: Załadowanie workbooka daje dostęp do jego arkuszy, komórek i pamięci podręcznej tabeli przestawnej. Aspose.Cells wczytuje cały plik do pamięci, więc kolejne operacje są szybkie i bezpieczne wątkowo.

## Krok 2: Zdefiniuj zakres źródłowy zawierający tabelę przestawną

```java
        // Locate the first worksheet (index 0) and create a range covering the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)               // first sheet
                                    .getCells()
                                    .createRange("A1:G20"); // adjust if your pivot table is larger
```

*Dlaczego to ważne*: Wywołanie `createRange` informuje Aspose.Cells dokładnie, które komórki skopiować. Uwzględnienie całego obszaru tabeli przestawnej zapewnia, że ukryte wiersze pamięci podręcznej również zostaną przeniesione. Jeśli pominiesz jakąkolwiek część pamięci podręcznej, skopiowana tabela przestawna będzie pusta.

## Krok 3: Dodaj docelowy arkusz dla skopiowanych danych

```java
        // Add a new worksheet that will hold the duplicated pivot table
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");
```

*Dlaczego to ważne*: Dodanie dedykowanego arkusza izoluje skopiowaną tabelę przestawną od oryginału, ułatwiając porównywanie wyników lub użycie arkusza jako szablonu do dalszego przetwarzania.

## Krok 4: Skopiuj zakres do docelowego arkusza (tabela przestawna jest zachowana)

```java
        // Copy the defined range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

*Dlaczego to ważne*: Metoda `copy` nie tylko kopiuje wartości komórek i formatowanie, ale także replikuję pamięć podręczną tabeli przestawnej. To kluczowy krok, który umożliwia **zduplikowanie arkusza z tabelą przestawną** bez utraty funkcjonalności.

## Krok 5: Zapisz workbook z skopiowanym zakresem

```java
        // Persist the workbook to a new file
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

*Dlaczego to ważne*: Zapis tworzy nowy plik Excel (`result.xlsx`), który zawiera zarówno oryginalny, jak i zduplikowany arkusz z tabelą przestawną. Teraz możesz otworzyć plik w Excelu, aby zweryfikować, że tabela przestawna działa dokładnie tak jak wcześniej.

## Pełny, działający przykład

Łącząc wszystko razem, oto kompletny program, który możesz skopiować i wkleić do swojego IDE:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1. Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // 2. Define the source range that contains the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)
                                    .getCells()
                                    .createRange("A1:G20");

        // 3. Add a destination worksheet for the copied data
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");

        // 4. Copy the range to the destination worksheet (pivot table is preserved)
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // 5. Save the workbook with the copied range
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

### Oczekiwany wynik

* Otwierając `result.xlsx` zobaczysz dwa arkusze:
  * **Sheet1** – oryginalne dane i tabela przestawna.
  * **CopyResult** – dokładna kopia tabeli przestawnej, w pełni funkcjonalna.
* Wszystkie pola tabeli przestawnej, filtry i elementy obliczeniowe zachowują się identycznie jak w źródle.

Jeśli zmodyfikujesz źródłową tabelę przestawną po skopiowaniu, zduplikowany arkusz **nie** odzwierciedli tych zmian, ponieważ pamięć podręczna została skopiowana w momencie kopiowania. Taka izolacja jest często pożądana, gdy potrzebujesz migawki raportu.

## Typowe pułapki i jak ich unikać

| Problem | Dlaczego się dzieje | Rozwiązanie |
|-------|----------------|-----|
| **Tabela przestawna jest pusta** | Zakres kopiowania pominął ukryte wiersze pamięci podręcznej. | Upewnij się, że zakres obejmuje całą pamięć podręczną (zwykle kilka wierszy poniżej widocznej tabeli). |
| **Nazwa docelowego arkusza już istnieje** | `add("CopyResult")` rzuca wyjątek, jeśli nazwa jest zajęta. | Użyj `workbook.getWorksheets().addUniqueName("CopyResult")` lub sprawdź `contains` przed dodaniem. |
| **Błędy ścieżki pliku** | Nieprawidłowy `YOUR_DIRECTORY` powoduje `FileNotFoundException`. | Użyj ścieżek bezwzględnych lub `Paths.get(...).toAbsolutePath()` w Javie, aby rozwiązać lokalizacje. |
| **Spowolnienie wydajności przy dużych workbookach** | Kopiowanie ogromnych zakresów kopiuję niepotrzebne komórki. | Ogranicz zakres do dokładnego obszaru tabeli przestawnej lub użyj `Range.copy` z `CopyOptions`, aby pominąć formatowanie, jeśli nie jest potrzebne. |

## Porada: użycie `CopyOptions` dla większej kontroli

Jeśli potrzebujesz tylko danych tabeli przestawnej i chcesz pominąć formatowanie komórek, możesz przekazać obiekt `CopyOptions`:

```java
CopyOptions options = new CopyOptions();
options.setCopyStyle(false);        // skip styles
options.setCopyMerged(true);        // keep merged cells
sourceRange.copy(destinationSheet.getCells().createRange("A1"), options);
```

## Jak skopiować zakres do nowego arkusza bez utraty formuł

Powyższy przykład już kopiuje formuły, ponieważ `Range.copy` domyślnie je zachowuje. Jeśli chcesz tylko wartości (np. aby zamrozić bieżący stan), ustaw `options.setPasteType(PasteType.VALUES)`.

```java
CopyOptions opt = new CopyOptions();
opt.setPasteType(PasteType.VALUES);
sourceRange.copy(destinationSheet.getCells().createRange("A1"), opt);
```

Teraz docelowy arkusz zawiera statyczne wartości, ale tabela przestawna nadal będzie działać, ponieważ jej pamięć podręczna jest częścią zakresu.

## Podsumowanie rozwiązania

* **Jak skopiować tabelę przestawną** – załaduj workbook, zdefiniuj dokładny zakres, dodaj nowy arkusz, skopiuj zakres i zapisz.
* Proces pokazuje także **kopiowanie zakresu do nowego arkusza** oraz jak bezpiecznie **zduplikować arkusz z tabelą przestawną**.
* Możesz dopasować kopiowanie przy użyciu `CopyOptions` pod kątem wydajności lub scenariuszy tylko z wartościami.

## Kolejne kroki i powiązane tematy

* **Odświeżanie pamięci podręcznej tabeli przestawnej programowo** – użyj `PivotTable.refreshData()` po zaktualizowaniu danych źródłowych.
* **Eksport tabeli przestawnej do PDF** – połącz tę technikę kopiowania z `PdfSaveOptions`, aby tworzyć raporty w formie migawki.
* **Automatyzacja duplikacji wielu arkuszy** – przeiteruj wszystkie arkusze i zastosuj tę samą logikę kopiowania.

Eksperymentuj z tymi wariantami, aby dostosować wzorzec do własnego potoku raportowania. Jeśli napotkasz przypadki brzegowe, takie jak zewnętrzne źródła danych lub tabele przestawne sterowane VBA, to samo podejście kopiowania zakresu działa, ale może być konieczne skopiowanie również obiektów połączeń.

---

*Szczęśliwego kodowania! Jeśli ten tutorial pomógł Ci nauczyć się **jak skopiować tabelę przestawną**, podziel się nim z zespołem lub przyczyń się do ulepszeń.*

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak skopiować zakres i zachować tabelę przestawną w Javie](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [Utwórz nowy workbook w Javie – pełny przewodnik po kopiowaniu tabeli przestawnej](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Kopiowanie tabeli przestawnej między workbookami – przewodnik krok po kroku w Javie](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}