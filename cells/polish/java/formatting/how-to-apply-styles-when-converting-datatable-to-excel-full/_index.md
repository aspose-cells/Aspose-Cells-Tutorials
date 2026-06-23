---
category: general
date: 2026-06-21
description: Jak zastosować style podczas konwertowania DataTable do Excela w Javie.
  Dowiedz się, jak zaimportować DataTable do Excela, dodać własne style w Excelu i
  zapisać skoroszyt do pliku w kilka minut.
draft: false
keywords:
- how to apply styles
- convert datatable to excel
- save workbook to file
- add custom styles excel
- import datatable to excel
language: pl
og_description: Jak zastosować style podczas konwertowania DataTable do Excela w Javie.
  Ten przewodnik pokazuje, jak zaimportować DataTable do Excela, dodać niestandardowe
  style w Excelu oraz zapisać skoroszyt do pliku.
og_title: Jak zastosować style przy konwertowaniu DataTable do Excela – Poradnik Java
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to apply styles while converting DataTable to Excel in Java. Learn
    to import datatable to excel, add custom styles excel, and save workbook to file
    in minutes.
  headline: How to Apply Styles When Converting DataTable to Excel – Full Java Guide
  type: TechArticle
- description: How to apply styles while converting DataTable to Excel in Java. Learn
    to import datatable to excel, add custom styles excel, and save workbook to file
    in minutes.
  name: How to Apply Styles When Converting DataTable to Excel – Full Java Guide
  steps:
  - name: 5.1 Conditional Formatting Instead of Fixed Styles
    text: If you need to highlight rows where `Score > 90`, you can add a `ConditionalFormattingCollection`
      after the import. This gives you dynamic coloring without hard‑coding extra
      styles.
  - name: 5.2 Merging Cells for Titles
    text: Sometimes a report needs a big title spanning multiple columns. Use `worksheet.getCells().merge(0,
      0, 1, 3)` and then apply a distinct style to that merged region.
  - name: 5.3 Large DataSets – Performance Considerations
    text: When dealing with >100k rows, set `ImportDataTableOptions` to `ImportDataTableOptions.NO_FORMATTING`
      first, then apply styles in a second pass. This avoids the overhead of styling
      each cell during import.
  - name: 5.4 Multi‑Sheet Export
    text: If you have several `DataTable`s, just create additional worksheets via
      `workbook.getWorksheets().add("Sheet2")` and repeat the **import datatable to
      excel** step for each sheet.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- DataTable
title: Jak zastosować style przy konwertowaniu DataTable do Excela – pełny przewodnik
  Java
url: /pl/java/formatting/how-to-apply-styles-when-converting-datatable-to-excel-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zastosować style przy konwertowaniu DataTable do Excela – Pełny przewodnik Java

Zastanawiałeś się kiedyś **jak zastosować style**, gdy musisz **przekonwertować DataTable do Excela**? Nie jesteś jedyny. W wielu wewnętrznych narzędziach pobieramy dane z baz danych, wkładamy je do `DataTable`, a potem oczekujemy ładnie wyglądającego arkusza kalkulacyjnego bez dodatkowej pracy. Spoiler: musisz dokładnie powiedzieć bibliotece, co oznacza „ładny”.

W tym tutorialu przejdziemy przez kompletny, gotowy do uruchomienia przykład, który pokazuje **jak zastosować style** przy użyciu Aspose.Cells for Java, importuje `DataTable` do Excela, **dodaje własne style w stylu Excel**, i w końcu **zapisuje skoroszyt do pliku**. Po zakończeniu będziesz mieć wielokrotnego użytku fragment kodu, który możesz wstawić do dowolnego projektu.

---

## Czego będziesz potrzebować

- **Java 17** (lub dowolny nowszy JDK) – kod działa również na Java 8+.  
- **Aspose.Cells for Java** JAR (bezpłatna wersja próbna wystarczy do testów).  
- Źródło `DataTable` – stworzymy prosty mock, ale możesz podmienić dowolny rzeczywisty wynik zapytania.  
- Ulubione IDE (IntelliJ, Eclipse, VS Code… wybór należy do Ciebie).

Nie są wymagane dodatkowe narzędzia budujące; wystarczy zwykły plik Maven `pom.xml`, ale możesz też dodać JAR ręcznie.

---

## Krok 1: Konfiguracja projektu i zależności

Najpierw – dodajmy bibliotekę do classpath.

```xml
<!-- pom.xml snippet -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-cells</artifactId>
        <version>24.9</version> <!-- check the latest version -->
    </dependency>
</dependencies>
```

Jeśli nie używasz Maven, po prostu wrzuć `aspose-cells-24.9.jar` do folderu `libs` i dodaj go do ścieżki kompilacji.

> **Pro tip:** Aspose dostarcza klasę `License`. Zarejestruj licencję od razu, inaczej w wygenerowanym pliku pojawią się znaki wodne.

```java
import com.aspose.cells.*;

public class ExcelExporter {
    static {
        try {
            License license = new License();
            license.setLicense("Aspose.Cells.lic"); // place your license file in resources
        } catch (Exception e) {
            System.out.println("License not found – running in evaluation mode.");
        }
    }
    // …rest of the class
}
```

Teraz możemy przejść do omówienia **jak zastosować style**.

---

## Krok 2: Tworzenie własnych stylów dla Excela

Magia dopracowanego arkusza tkwi w stylach komórek. Aspose pozwala zdefiniować obiekt `Style`, dostosować czcionki, kolory, obramowania i potem używać go wszędzie, gdzie potrzebujesz. Poniżej kompaktowy sposób na **dodanie własnych stylów w całym Excelu**.

```java
/**
 * Builds an array of two custom styles:
 * 1. Header style – bold, gray background, centered.
 * 2. Data style   – thin borders, left‑aligned.
 */
private static Style[] buildImportStyles(Workbook workbook) {
    // Header style
    Style headerStyle = workbook.createStyle();
    Font headerFont = headerStyle.getFont();
    headerFont.setBold(true);
    headerFont.setColor(Color.getWhite());
    headerStyle.setPattern(BackgroundType.SOLID);
    headerStyle.setBackgroundColor(Color.getGray25());
    headerStyle.setHorizontalAlignment(TextAlignmentType.CENTER);
    headerStyle.setVerticalAlignment(TextAlignmentType.CENTER);

    // Data style
    Style dataStyle = workbook.createStyle();
    dataStyle.setBorder(BorderType.LEFT_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setBorder(BorderType.RIGHT_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setBorder(BorderType.TOP_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setBorder(BorderType.BOTTOM_BORDER, CellBorderType.THIN, Color.getBlack());
    dataStyle.setHorizontalAlignment(TextAlignmentType.LEFT);
    dataStyle.setVerticalAlignment(TextAlignmentType.CENTER);

    return new Style[] { headerStyle, dataStyle };
}
```

Zauważ, że stworzyliśmy **dwa odrębne style** – jeden dla nagłówków kolumn, a drugi dla wierszy danych. Możesz rozszerzyć tę tablicę o dowolną liczbę stylów; Aspose zastosuje je kolejno, gdy wywołasz `importDataTable`.

---

## Krok 3: Importowanie DataTable do arkusza

Teraz przyszedł czas na część, która naprawdę **importuje DataTable do Excela**. Metoda `importDataTable` przyjmuje źródłowy `DataTable`, flagę określającą, czy mają być nagłówki kolumn, początkowy wiersz/kolumnę oraz tablicę stylów, którą właśnie zbudowaliśmy.

```java
public static void exportDataTableToExcel(DataTable dataTable, String outputPath) throws Exception {
    // 1️⃣ Create a new workbook and grab the first worksheet
    Workbook workbook = new Workbook();
    Worksheet worksheet = workbook.getWorksheets().get(0);

    // 2️⃣ Build the custom styles (header + data)
    Style[] importStyles = buildImportStyles(workbook);

    // 3️⃣ Import the DataTable – start at A1 (0,0), keep column names, apply styles
    worksheet.getCells().importDataTable(dataTable, true, 0, 0, importStyles);

    // 4️⃣ Auto‑fit columns for a tidy look
    worksheet.autoFitColumns();

    // 5️⃣ Finally, **save workbook to file**
    workbook.save(outputPath);
}
```

Krótka uwaga: argument `true` mówi Aspose, aby **zachować nagłówki kolumn** – to typowy przypadek, gdy chcesz czytelny raport. Jeśli ustawisz `false`, pierwszy wiersz danych stanie się nagłówkiem.

---

## Krok 4: Połączenie wszystkiego – minimalny działający przykład

Poniżej znajduje się samodzielna metoda `main`, która tworzy przykładowy `DataTable`, wywołuje procedurę eksportu i zapisuje `output.xlsx` w folderze `./results`.

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExporter {

    // (License block omitted for brevity – see Step 1)

    public static void main(String[] args) throws Exception {
        // Mock a DataTable – replace this with your real DB call
        DataTable dataTable = createSampleDataTable();

        // Define where the Excel file should land
        String outputPath = "results/output.xlsx";

        // Perform the conversion and styling
        exportDataTableToExcel(dataTable, outputPath);

        System.out.println("Excel file generated at: " + outputPath);
    }

    /** Helper that builds a simple DataTable with three columns */
    private static DataTable createSampleDataTable() {
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", CellValueType.INTEGER);
        dt.getColumns().add("Name", CellValueType.STRING);
        dt.getColumns().add("Score", CellValueType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[] {1, "Alice", 85.5});
        dt.getRows().add(new Object[] {2, "Bob", 92.0});
        dt.getRows().add(new Object[] {3, "Charlie", 78.3});
        return dt;
    }

    // (Style builder and export method from Steps 2‑3 go here)
}
```

**Oczekiwany wynik:** Otwórz `output.xlsx`, a zobaczysz pogrubiony, szary wiersz nagłówka, komórki danych z cienkimi obramowaniami oraz kolumny automatycznie dopasowane do zawartości. To właśnie **jak zastosować style**, aby arkusz wyglądał profesjonalnie.

![Jak zastosować style w skoroszycie Excel](/images/excel-styles.png){alt="jak zastosować style w skoroszycie Excel"}

*(Zrzut ekranu pokazuje nagłówek w pogrubionej szarości oraz wiersze danych z cienkimi obramowaniami.)*

---

## Krok 5: Zaawansowane wskazówki i przypadki brzegowe

### 5.1 Formatowanie warunkowe zamiast stałych stylów  
Jeśli musisz podświetlić wiersze, w których `Score > 90`, możesz dodać `ConditionalFormattingCollection` po imporcie. Dzięki temu uzyskasz dynamiczne kolorowanie bez konieczności twardego kodowania dodatkowych stylów.

```java
FormatConditionCollection fcc = worksheet.getConditionalFormattings().add();
FormatCondition fc = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90");
fc.getStyle().setBackgroundColor(Color.getLightGreen());
```

### 5.2 Scalanie komórek dla tytułów  
Czasami raport wymaga dużego tytułu rozciągniętego na kilka kolumn. Użyj `worksheet.getCells().merge(0, 0, 1, 3)`, a następnie zastosuj odrębny styl dla tego połączonego obszaru.

### 5.3 Duże zestawy danych – kwestie wydajności  
Przy pracy z ponad 100 tys. wierszy najpierw ustaw `ImportDataTableOptions` na `ImportDataTableOptions.NO_FORMATTING`, a potem zastosuj style w drugim przebiegu. To eliminuje narzut stylizacji każdej komórki podczas importu.

### 5.4 Eksport wielo‑arkuszowy  
Jeśli masz kilka `DataTable`, po prostu utwórz dodatkowe arkusze za pomocą `workbook.getWorksheets().add("Sheet2")` i powtórz krok **importu DataTable do Excela** dla każdego arkusza.

---

## Podsumowanie

Omówiliśmy **jak zastosować style** od początku do końca: konfigurację Aspose.Cells, budowanie **własnych stylów w Excelu**, **importowanie DataTable do Excela** oraz w końcu **zapis skoroszytu do pliku**. Pełny przykład kodu jest gotowy do skopiowania, a dodatkowe wskazówki dają plan działania dla bardziej zaawansowanych raportów.

Następnie możesz zbadać **dodawanie własnych stylów w Excelu** dla wykresów lub poeksperymentować z **konwersją DataTable do Excela** w endpointzie Spring Boot REST. Tak czy inaczej, masz teraz solidne podstawy do przekształcania surowych tabel w dopracowane arkusze – bez ręcznego formatowania.

Masz pytania

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z krok‑po‑kroku wyjaśnieniami, pomagając Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak zastosować style do komórek Excel przy użyciu Aspose.Cells for Java – Kompletny przewodnik](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)
- [Scalanie komórek i stosowanie stylów w Excelu przy użyciu Aspose.Cells for Java – Kompletny przewodnik](/cells/english/java/formatting/merge-cells-apply-styles-aspose-cells-java/)
- [Jak zaimportować DataTable do Excela przy użyciu Aspose.Cells dla .NET (przewodnik krok po kroku)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}