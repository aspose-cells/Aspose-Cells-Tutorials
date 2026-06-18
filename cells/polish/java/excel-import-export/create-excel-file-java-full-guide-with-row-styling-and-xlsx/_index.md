---
category: general
date: 2026-06-18
description: Utwórz samouczek Java dotyczący tworzenia pliku Excel, pokazujący, jak
  ustawić kolor tła wiersza, wygenerować Excel z DataTable i zapisać skoroszyt jako
  XLSX z naprzemiennym cieniowaniem wierszy.
draft: false
keywords:
- create excel file java
- set row background color
- save workbook as xlsx
- alternating row shading excel
- generate excel from datatable
language: pl
og_description: Tworzenie pliku Excel w Javie krok po kroku. Naucz się ustawiać kolor
  tła wiersza, stosować naprzemienne cieniowanie wierszy, generować Excel z DataTable
  i zapisywać skoroszyt jako XLSX.
og_title: Tworzenie pliku Excel w Javie – Kompletny przewodnik po stylizacji i eksporcie
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Create Excel file Java tutorial showing how to set row background color,
    generate Excel from DataTable, and save workbook as XLSX with alternating row
    shading.
  headline: Create Excel File Java – Full Guide with Row Styling and XLSX Export
  type: TechArticle
- description: Create Excel file Java tutorial showing how to set row background color,
    generate Excel from DataTable, and save workbook as XLSX with alternating row
    shading.
  name: Create Excel File Java – Full Guide with Row Styling and XLSX Export
  steps:
  - name: Exporting a Large DataTable
    text: 'When dealing with 100k+ rows, you may hit memory limits. Aspose.Cells supports
      **streaming** mode:'
  - name: Using Apache POI Instead of Aspose.Cells
    text: 'If licensing is a concern, you can replace the import logic with POI’s
      `CellStyle` objects. The concept stays the same: create two `CellStyle`s, loop
      over rows, and apply `setFillForegroundColor` with `IndexedColors`. The only
      downside is the code becomes a bit more verbose.'
  - name: Adding Conditional Formatting
    text: 'Suppose you want to highlight any score above 90 in green. Add this after
      the import:'
  type: HowTo
tags:
- java
- excel
- aspose-cells
- data-export
title: Tworzenie pliku Excel w Javie – Kompletny przewodnik z formatowaniem wierszy
  i eksportem XLSX
url: /pl/java/excel-import-export/create-excel-file-java-full-guide-with-row-styling-and-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz plik Excel w Javie – Pełny przewodnik ze stylizacją wierszy i eksportem XLSX

Zastanawiałeś się kiedyś, jak **create excel file java** wyglądać będzie elegancko od razu po utworzeniu? Nie jesteś sam — programiści często potrzebują szybkiego sposobu na przekształcenie danych tabelarycznych w ładnie sformatowany arkusz kalkulacyjny bez ręcznego otwierania Excela. W tym samouczku przeprowadzimy Cię przez kompletną rozwiązanie: pobranie danych z `DataTable`, zastosowanie **alternating row shading excel**, a na koniec **save workbook as xlsx**. Po zakończeniu będziesz mieć wielokrotnego użytku fragment kodu, który możesz wkleić do dowolnego projektu Java.

Omówimy wszystko, czego potrzebujesz: wymaganą bibliotekę (Aspose.Cells for Java), dokładny kod ustawiający **row background color**, jak **generate excel from datatable**, oraz kilka praktycznych wskazówek, aby uniknąć typowych pułapek. Bez zbędnych dodatków, po prostu solidny, gotowy do uruchomienia przykład, który możesz dostosować już dziś.

## Wymagania wstępne

- Java 17 lub nowszy (kod działa z dowolnym aktualnym JDK)
- Maven lub Gradle do zarządzania zależnościami
- Podstawowa znajomość kolekcji w Javie
- Dostęp do biblioteki Aspose.Cells for Java (bezpłatna wersja próbna lub licencjonowana)

Jeśli wolisz otwarto‑źródłową alternatywę, logika łatwo przechodzi na Apache POI — wystarczy zamienić wywołania API. Dla zwięzłości pozostaniemy przy Aspose.Cells, ponieważ metoda `importDataTable` sprawia, że krok **generate excel from datatable** jest jedną linią kodu.

## Krok 1: Skonfiguruj projekt i dodaj Aspose.Cells

Dodaj następującą zależność do swojego `pom.xml` (Maven) lub `build.gradle` (Gradle). To pobierze główną bibliotekę, która pozwala nam manipulować skoroszytami, stylami i kolorami.

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-cells:24.9'
```

Po odświeżeniu projektu jesteś gotowy, aby napisać kod w Javie w stylu **create excel file java**.

## Krok 2: Utwórz skoroszyt i załaduj dane

Najpierw tworzymy nowy `Workbook`. Następnie uzyskujemy `DataTable` — może to być wynik zapytania JDBC, parsera CSV lub dowolna tabela w pamięci, którą już posiadasz.

```java
import com.aspose.cells.*;

public class ExcelExporter {

    // Simulated method that returns a DataTable with dummy data
    private static DataTable getData() {
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("Name", DataType.STRING);
        dt.getColumns().add("Score", DataType.DOUBLE);

        // Add some rows
        dt.getRows().add(new Object[]{1, "Alice", 92.5});
        dt.getRows().add(new Object[]{2, "Bob", 85.0});
        dt.getRows().add(new Object[]{3, "Charlie", 78.3});
        dt.getRows().add(new Object[]{4, "Diana", 88.9});
        return dt;
    }

    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook (or load an existing one)
        Workbook workbook = new Workbook();

        // Step 2: Obtain the data to be written as a DataTable
        DataTable dataTable = getData(); // assume this returns the source data
```

W tym momencie mamy czysty skoroszyt i wypełniony `DataTable`. Następny krok to miejsce, gdzie dzieje się wizualna magia.

## Krok 3: Zdefiniuj style wierszy – ustawianie koloru tła wiersza

Chcemy, aby każdy wiersz miał odrębne tło, naprzemiennie w jasnym niebieskim i jasnym szarym kolorze. To zwiększa czytelność, szczególnie w dużych raportach. Poniższy kod tworzy tablicę `Style` — po jednym elemencie na każdy wiersz danych — i przypisuje **set row background color** w zależności od indeksu wiersza.

```java
        // Step 3: Prepare an array of row styles – one style per data row
        Style[] rowStyles = new Style[dataTable.getRows().size()];
        for (int i = 0; i < rowStyles.length; i++) {
            rowStyles[i] = workbook.createStyle();

            // Step 4: Alternate background colors for better readability
            if (i % 2 == 0) {
                // Even rows – light blue
                rowStyles[i].setForegroundColor(Color.getLightBlue());
            } else {
                // Odd rows – light gray
                rowStyles[i].setForegroundColor(Color.getLightGray());
            }
            // Apply solid fill pattern
            rowStyles[i].setPattern(BackgroundType.SOLID);
        }
```

Zauważ, że używamy `Color.getLightBlue()` i `Color.getLightGray()`. Aspose.Cells oferuje bogatą paletę, ale możesz zamienić te wywołania na dowolny `Color`, który Ci odpowiada — być może kolory Twojej marki korporacyjnej.

## Krok 4: Importuj DataTable ze stylizacją

Teraz łączymy dane i tablicę stylów. Metoda `importDataTable` zajmuje się kopiowaniem wierszy, zastosowaniem odpowiedniego stylu, a nawet dodaje nagłówki kolumn, jeśli przekażesz `true` dla flagi `importColumnNames`.

```java
        // Step 5: Import the DataTable into the first worksheet using the styles
        Worksheet sheet = workbook.getWorksheets().get(0);
        sheet.getCells().importDataTable(dataTable, true, "A1", rowStyles);
```

Anchor `"A1"` informuje Aspose, gdzie rozpocząć zapisywanie — w lewym górnym rogu arkusza. Ponieważ dostarczyliśmy tablicę `rowStyles`, każdy wiersz dziedziczy ustawiony wcześniej kolor tła, osiągając **alternating row shading excel** bez pętli po imporcie.

## Krok 5: Zapisz stylizowany skoroszyt jako XLSX

Na koniec zapisujemy skoroszyt na dysku. Metoda `save` automatycznie określa format na podstawie rozszerzenia pliku, więc użycie `.xlsx` daje nam nowoczesny skoroszyt Office Open XML, który można otworzyć w Excelu, Google Sheets lub LibreOffice.

```java
        // Step 6: Save the styled workbook to a file
        workbook.save("styledTable.xlsx"); // save workbook as xlsx
        System.out.println("Excel file created successfully!");
    }
}
```

Uruchomienie metody `main` tworzy plik o nazwie `styledTable.xlsx` w katalogu głównym Twojego projektu. Otwórz go, a zobaczysz starannie sformatowaną tabelę z naprzemiennymi kolorami wierszy — dokładnie to, czego oczekuje interesariusz biznesowy od raportu.

![Screenshot of styled Excel file created with Java](images/styled_excel_java.png "create excel file java example")

*Tekst alternatywny obrazu:* **create excel file java** zrzut ekranu pokazujący naprzemienną cieniowanie wierszy

## Dlaczego to podejście działa lepiej niż ręczne stylizowanie komórka po komórce

Możesz się zastanawiać, dlaczego używamy tablicy stylów zamiast pętli po każdym wierszu po imporcie. Odpowiedź jest dwuetapowa:

1. **Performance** – Zastosowanie stylu podczas importu eliminuje dodatkowe przejście po arkuszu, co może być kosztowne przy tysiącach wierszy.
2. **Maintainability** – Logika stylu znajduje się w jednym miejscu (`rowStyles`), co ułatwia zamianę kolorów, dodawanie obramowań lub zmianę wzoru bez modyfikacji kodu importu.

Jeśli później będziesz musiał dodać więcej wskazówek wizualnych (np. podświetlić wiersze z wynikiem poniżej progu), po prostu rozbuduj blok `if` wewnątrz pętli — nie są potrzebne żadne inne zmiany.

## Typowe warianty i przypadki brzegowe

### Eksport dużego DataTable

Przy obsłudze ponad 100 tys. wierszy możesz napotkać ograniczenia pamięci. Aspose.Cells obsługuje tryb **streaming**:

```java
Workbook wb = new Workbook(FileFormatType.XLSX);
wb.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
```

Ustaw preferencję pamięci przed tworzeniem stylów, a biblioteka zapisze dane w plikach tymczasowych zamiast trzymać wszystko w RAM.

### Użycie Apache POI zamiast Aspose.Cells

Jeśli licencjonowanie jest problemem, możesz zamienić logikę importu na obiekty `CellStyle` z POI. Koncepcja pozostaje ta sama: utwórz dwa `CellStyle`, przeiteruj wiersze i zastosuj `setFillForegroundColor` z `IndexedColors`. Jedyną wadą jest nieco bardziej rozbudowany kod.

### Dodawanie formatowania warunkowego

Załóżmy, że chcesz podświetlić każdy wynik powyżej 90 na zielono. Dodaj to po imporcie:

```java
FormatConditionCollection fcc = sheet.getConditionalFormattings().add();
FormatCondition fc = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90");
Style conditionStyle = workbook.createStyle();
conditionStyle.setForegroundColor(Color.getLightGreen());
conditionStyle.setPattern(BackgroundType.SOLID);
fc.setStyle(conditionStyle);
```

Teraz arkusz nie tylko ma naprzemienne cieniowanie, ale także dynamiczne podświetlenia.

## Podsumowanie: Co osiągnęliśmy

- **Create excel file java** z `DataTable` przy użyciu Aspose.Cells.
- **Set row background color** programowo, osiągając **alternating row shading excel**.
- **Save workbook as xlsx**, zapewniając kompatybilność z nowoczesnymi narzędziami arkuszy kalkulacyjnych.
- Pokażemy, jak **generate excel from datatable** efektywnie i rozbudowanie.

To wszystko mieści się w zwartej, łatwej do odczytania klasie Java, którą możesz skopiować i wkleić do własnej bazy kodu.

## Kolejne kroki i powiązane tematy

Jeśli podobał Ci się ten przewodnik, możesz również przyjrzeć się:

- **Exporting charts** z Javy do Excela (API wykresów Aspose.Cells).
- **Password‑protecting** wygenerowany skoroszyt (`workbook.protect(...)`).
- **Writing large datasets** przy użyciu streaming, aby utrzymać niskie zużycie pamięci.
- **Integrating with Spring Boot** w celu udostępnienia wygenerowanego pliku jako odpowiedź do pobrania.

Każdy z tych tematów opiera się na tej samej podstawie, którą tutaj przedstawiliśmy — więc śmiało eksperymentuj i rozwijaj.

---

*Szczęśliwego kodowania! Jeśli napotkasz problemy lub masz pomysły na dalsze ulepszenia, zostaw komentarz poniżej. Kontynuujmy dyskusję.*

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Utwórz skoroszyt Excel przy użyciu Aspose.Cells w Javie: przewodnik krok po kroku](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Jak ustawić wysokość wierszy w Excelu przy użyciu Aspose.Cells dla Java — kompletny przewodnik](/cells/english/java/formatting/mastering-excel-row-heights-aspose-cells-java/)
- [Jak utworzyć plik Excel w Javie i stylizować go przy użyciu Aspose.Cells](/cells/english/java/advanced-features/excel-master-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}