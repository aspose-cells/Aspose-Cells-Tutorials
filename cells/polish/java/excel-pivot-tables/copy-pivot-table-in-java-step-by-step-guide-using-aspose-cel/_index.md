---
category: general
date: 2026-08-04
description: Kopiuj tabelę przestawną za pomocą Aspose.Cells dla Javy. Dowiedz się,
  jak skopiować zakres Excela, zduplikować tabelę przestawną i skopiować arkusz z
  tabelą przestawną w kilku linijkach.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- copy excel range
- copy range java
- duplicate pivot table
- copy worksheet with pivot
language: pl
lastmod: 2026-08-04
og_description: Skopiuj tabelę przestawną przy użyciu Aspose.Cells dla Javy. Ten samouczek
  przeprowadzi Cię przez kopiowanie zakresu Excel, duplikowanie tabeli przestawnej
  i zachowanie wszystkich danych w nowym arkuszu.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new worksheet
og_title: Kopiowanie tabeli przestawnej w Javie – pełny poradnik Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  headline: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  type: TechArticle
- description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  name: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  steps:
  - name: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
    text: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
  - name: Opening the file in Excel shows a new sheet named **CopySheet**.
    text: Opening the file in Excel shows a new sheet named **CopySheet**.
  - name: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
    text: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
  - name: All formatting, filters, and calculated fields are preserved.
    text: All formatting, filters, and calculated fields are preserved.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PivotTable
- Data copying
title: Kopiowanie tabeli przestawnej w Javie – przewodnik krok po kroku z użyciem
  Aspose.Cells
url: /pl/java/excel-pivot-tables/copy-pivot-table-in-java-step-by-step-guide-using-aspose-cel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopiowanie tabeli przestawnej w Javie – przewodnik krok po kroku z użyciem Aspose.Cells

Jeśli potrzebujesz **skopiować tabelę przestawną** z jednego arkusza do drugiego w Javie, ten przewodnik pokaże Ci dokładnie, jak to zrobić przy użyciu Aspose.Cells. Niezależnie od tego, czy generujesz raporty programowo, czy budujesz narzędzie do migracji danych, zobaczysz kompletny, gotowy do uruchomienia przykład, który zachowuje definicję i dane tabeli przestawnej.

Kopiowanie tabeli przestawnej to nie tylko kopiowanie zakresu komórek; ukryta pamięć podręczna i źródło danych muszą pozostać nienaruszone. W tym samouczku omówimy również, jak **skopiować zakres Excel**, jak **zduplikować tabelę przestawną** pomiędzy arkuszami oraz jak **skopiować arkusz z tabelą przestawną** przy użyciu tego samego API.

## Wymagania wstępne

* Java Development Kit (JDK) 8 lub nowszy.
* Maven lub Gradle do zarządzania zależnościami.
* Aspose.Cells for Java (najświeższa wersja, np. 23.12). Dodaj następującą współrzędną Maven do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* Skoroszyt źródłowy (`Source.xlsx`) zawierający tabelę przestawną w pierwszym arkuszu.

## Jak skopiować tabelę przestawną w Javie z użyciem Aspose.Cells

Główną ideą jest skopiowanie *zakresu źródłowego*, który obejmuje tabelę przestawną, a następnie wklejenie go do nowego arkusza. Aspose.Cells automatycznie kopiuje pamięć podręczną tabeli przestawnej, więc powstały arkusz zawiera w pełni funkcjonalną **zduplikowaną tabelę przestawną**.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the PivotTable
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

        // Step 2: Define the source range (including the PivotTable) to be copied
        // The range must cover the entire pivot table area, e.g., A1:G20
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)                 // first worksheet
                                    .getCells()
                                    .createRange("A1:G20");

        // Step 3: Add a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("CopySheet");

        // Step 4: Copy the source range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Step 5: Save the workbook with the copied PivotTable intact
        workbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

### Dlaczego to działa

* **Kopiowanie zakresu obejmuje pamięć podręczną tabeli przestawnej** – Aspose.Cells traktuje tabelę przestawną jako specjalny obiekt osadzony w zakresie komórek. Gdy wywołujesz `Range.copy`, biblioteka kopiuje zarówno widoczne komórki, jak i ukrytą pamięć podręczną napędzającą tabelę.
* **Nie wymaga ręcznego odtwarzania** – Nie musisz odtwarzać pól tabeli przestawnej ani źródła danych; duplikat jest gotowy do natychmiastowego odświeżenia.
* **Działa z każdą wersją Excela** – Wygenerowany plik spełnia standard Office Open XML (XLSX), więc Excel 2007+ otworzy go bez ostrzeżeń.

## Kopiowanie zakresu Excel – ponowne użycie tego samego kodu dla danych nie‑przestawnych

Jeśli potrzebujesz jedynie **skopiować zakres Excel** bez tabeli przestawnej, stosuje się ten sam wzorzec. Wystarczy dostosować adres zakresu do regionu, który chcesz zduplikować.

```java
// Example: copy A1:D10 from Sheet1 to Sheet2
Range dataRange = workbook.getWorksheets()
                          .get(0)
                          .getCells()
                          .createRange("A1:D10");
Worksheet sheet2 = workbook.getWorksheets().add("DataCopy");
dataRange.copy(sheet2.getCells().createRange("A1"));
```

Metoda `copy` zachowuje formuły, formatowanie i komentarze, co czyni ją uniwersalnym rozwiązaniem dla dowolnego bloku danych Excel.

## Duplikowanie tabeli przestawnej w wielu arkuszach

Czasami trzeba **zduplikować tabelę przestawną** kilka razy — np. po jednej na dział. Pętla po docelowych arkuszach i ponowne użycie wywołania `sourceRange.copy` wygląda następująco:

```java
String[] departments = {"Sales", "Marketing", "Finance"};
for (String dept : departments) {
    Worksheet ws = workbook.getWorksheets().add(dept + "Pivot");
    sourceRange.copy(ws.getCells().createRange("A1"));
}
```

Każdy nowy arkusz zawiera niezależną tabelę przestawną, którą można odświeżać osobno. Pamięć podręczna jest duplikowana, więc zmiany w jednym arkuszu nie wpływają na pozostałe.

## Kopiowanie arkusza z tabelą przestawną – zachowanie ustawień na poziomie arkusza

Jeśli chcesz **skopiować arkusz z tabelą przestawną**, jednocześnie zachowując ustawienia strony, szerokości kolumn i nazwy zakresów, użyj `Worksheet.copy` zamiast ręcznego kopiowania zakresu. Ta metoda klonuje cały arkusz, włącznie z tabelą przestawną.

```java
Worksheet original = workbook.getWorksheets().get(0);
Worksheet clone = workbook.getWorksheets().addCopy(original);
clone.setName("FullCopy");
workbook.save("YOUR_DIRECTORY/FullCopy.xlsx");
```

`addCopy` jest przydatny, gdy arkusz zawiera wykresy, obrazy lub niestandardowe style, które muszą przemieścić się razem z tabelą przestawną.

## Typowe pułapki i jak ich uniknąć

| Problem | Dlaczego się pojawia | Rozwiązanie |
|-------|----------------|-----|
| **Utrata pamięci podręcznej tabeli przestawnej po kopiowaniu** | Użycie `Cell.copy` na pojedynczych komórkach (zamiast zakresu) pomija ukrytą pamięć podręczną. | Zawsze kopiuj *cały* zakres obejmujący tabelę przestawną, jak pokazano w Kroku 2. |
| **Zakres źródłowy za mały** | Zakres nie obejmuje obszaru danych tabeli przestawnej, więc nowy arkusz pokazuje tylko wartości statyczne. | Rozszerz adres (np. `A1:G20`), aby objąć całą tabelę przestawną oraz ewentualne segmentatory czy filtry. |
| **Niezgodność wersji skoroszytu docelowego** | Zapis jako XLS (starszy format) usuwa nowoczesne funkcje tabel przestawnych. | Zapisz jako XLSX (domyślnie) lub jawnie ustaw `SaveFormat.XLSX`. |
| **Uszkodzone zewnętrzne źródło danych** | Tabela przestawna odwołuje się do źródła danych poza skoroszytem; kopiowanie nie osadza go. | Użyj `PivotTable.refreshData()` po kopiowaniu lub osadź dane źródłowe w tym samym skoroszycie. |

## Oczekiwany wynik

Po uruchomieniu programu:

1. `CopyWithPivot.xlsx` pojawia się w `YOUR_DIRECTORY`.
2. Otwierając plik w Excelu, widzisz nowy arkusz o nazwie **CopySheet**.
3. **CopySheet** zawiera w pełni funkcjonalną tabelę przestawną identyczną z oryginałem, gotową do odświeżenia.
4. Wszystkie formatowania, filtry i pola obliczeniowe są zachowane.

Jeśli otworzysz `FullCopy.xlsx`, zobaczysz pełną replikę oryginalnego arkusza, włącznie z wykresami i obrazami, które znajdowały się na arkuszu źródłowym.

## Podsumowanie

* Nauczyłeś się, jak **skopiować tabelę przestawną** w Javie przy użyciu Aspose.Cells.
* To samo podejście działa dla zwykłego **skopiowania zakresu Excel** lub scenariuszy **copy range java**.
* W operacjach masowych możesz **zduplikować tabelę przestawną** w wielu arkuszach.
* Gdy potrzebny jest cały arkusz, **skopiuj arkusz z tabelą przestawną** używając `addCopy`.

## Kolejne kroki

* Zbadaj **PivotTable.refreshData()**, aby programowo zaktualizować pamięć podręczną po kopiowaniu.
* Połącz logikę kopiowania z **strumieniowaniem plików Excel**, aby obsługiwać duże skoroszyty bez ładowania wszystkiego do pamięci.
* Sprawdź wsparcie Aspose.Cells dla **segmentatorów tabel przestawnych**, jeśli Twoje raporty opierają się na interaktywnych filtrach.

Śmiało dostosuj kod do własnej struktury projektu, eksperymentuj z różnymi rozmiarami zakresów lub zintegrować go z większym potokiem przetwarzania danych. Szczęśliwego kodowania!

## Co powinieneś się nauczyć dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak zaktualizować źródło tabeli przestawnej Excel przy użyciu Aspose.Cells dla Java: Kompletny przewodnik](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Manipulacja tabelą przestawną Excel Aspose Cells Java](/cells/hongkong/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Utwórz nowy skoroszyt Excel – kopiowanie i duplikowanie tabeli przestawnej](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}