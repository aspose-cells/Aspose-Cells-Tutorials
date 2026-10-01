---
category: general
date: 2026-10-01
description: Dowiedz się, jak kopiować tabele przestawne między skoroszytami Excela
  przy użyciu Javy. Ten przewodnik krok po kroku pokazuje również, jak kopiować zakresy
  między skoroszytami i bezpiecznie duplikować zakresy w Excelu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range between workbooks
- how to copy excel
- duplicate excel range
- copy range to workbook
language: pl
lastmod: 2026-10-01
og_description: Jak kopiować tabele przestawne między skoroszytami Excela przy użyciu
  Javy. Skorzystaj z tego przewodnika, aby skopiować zakres do skoroszytu, zduplikować
  zakresy Excela i zachować dane tabel przestawnych.
og_image_alt: Screenshot of Java code that copies a pivot table from one Excel workbook
  to another
og_title: Jak kopiować tabele przestawne między skoroszytami Excel w Javie – kompletny
  przewodnik
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  headline: How to copy pivot tables between Excel workbooks in Java
  type: TechArticle
- description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  name: How to copy pivot tables between Excel workbooks in Java
  steps:
  - name: Expected output
    text: '* Console: `Pivot table copied successfully.` * `destination.xlsx` opens
      in Excel with a pivot table identical to the one in `source.xlsx`. Refreshing
      the pivot shows the same data source, proving that **how to copy pivot** works
      as intended.'
  - name: Copying multiple worksheets
    text: If your project requires copying several sheets, loop through the workbook’s
      worksheets and repeat steps 2‑4 for each sheet. The pivot in each sheet will
      be preserved independently.
  - name: Preserving external data connections
    text: Pivot tables that rely on external data sources keep the connection string
      after copying. However, the destination file must have access to the same data
      source. Verify the connection by opening the pivot and checking the **Data**
      tab.
  - name: Dealing with merged cells
    text: If the source range contains merged cells, Aspose.Cells copies the merge
      layout automatically. Still, validate the result if the destination workbook
      uses a different default column width.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- Pivot table
- Data manipulation
title: Jak kopiować tabele przestawne między skoroszytami Excela w Javie
url: /pl/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak kopiować tabele przestawne między skoroszytami Excel w Javie

Jeśli potrzebujesz **how to copy pivot** tabele z jednego pliku Excel do drugiego, ten przewodnik dostarcza gotowe rozwiązanie. Po przeczytaniu pierwszych dwóch zdań dokładnie będziesz wiedział, które wywołania API zachowują definicję tabeli przestawnej podczas kopiowania zakresu danych.

Dowiesz się również, jak **copy range between workbooks**, **duplicate Excel range** obiekty, oraz bezpiecznie **copy range to workbook** bez utraty formuł czy formatowania. Nie są wymagane żadne zewnętrzne skrypty — wystarczy pojedynczy projekt Java wykorzystujący Aspose.Cells for Java.

## Wymagania wstępne

* Java Development Kit 17 lub nowszy.
* Maven lub Gradle do zarządzania zależnościami.
* Ważna licencja Aspose.Cells for Java (darmowa wersja ewaluacyjna działa do testów).
* Dwa pliki Excel: `source.xlsx` (zawiera tabelę przestawną) oraz pusty `destination.xlsx` (lub pozwól, aby kod go utworzył).

## Krok 1: Skonfiguruj projekt Maven

Utwórz plik `pom.xml`, który zawiera Aspose.Cells. Ta zależność udostępnia klasy `Workbook`, `Worksheet` i `Range` używane w przykładzie.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>excel-pivot-copy</artifactId>
    <version>1.0.0</version>
    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>24.10</version> <!-- latest at time of writing -->
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** Utrzymuj wersję Aspose.Cells aktualną; nowsze wydania zapewniają lepsze wsparcie dla złożonych struktur pamięci podręcznej tabel przestawnych.

## Krok 2: Załaduj źródłowy skoroszyt zawierający tabelę przestawną

Pierwszy blok kodu demonstruje **how to copy excel** dane poprzez załadowanie pliku źródłowego. Konstruktor `Workbook` odczytuje cały plik do pamięci, zachowując wszystkie obiekty arkuszy, w tym tabele przestawne.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Access the first worksheet (index 0) where the pivot resides
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Dlaczego to ważne:* Aspose.Cells przechowuje tabele przestawne jako część wewnętrznego modelu arkusza. Załadowanie skoroszytu zapewnia dostępność pamięci podręcznej tabeli przestawnej do późniejszego kopiowania.

## Krok 3: Zdefiniuj zakres obejmujący tabelę przestawną

Tabela przestawna może obejmować wiele wierszy i kolumn. W większości przypadków możesz skopiować cały używany zakres arkusza. Metoda `createRange` tworzy obiekt `Range`, którym będzie obsługiwana operacja kopiowania.

```java
        // Define the range to copy – includes the pivot table and its source data
        // Adjust the address if your pivot occupies a different block
        Range srcRange = srcWs.getCells().createRange("A1:H20");
```

Jeśli tabela przestawna rozciąga się poza `H20`, po prostu zmień ciąg adresu. Ten krok jest rdzeniem obsługi **duplicate excel range**; obiekt zakresu zna formuły, style i ukryte wiersze.

## Krok 4: Utwórz nowy skoroszyt, który otrzyma skopiowany zakres

Możesz rozpocząć od pustego skoroszytu lub załadować istniejący plik docelowy. Tutaj tworzymy nowy skoroszyt, co jest najczystszym sposobem na **copy range to workbook**.

```java
        // Create a new workbook for the destination
        Workbook destWb = new Workbook(); // starts with one default sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

> **Note:** Jeśli potrzebujesz skopiować tabelę przestawną do określonej nazwy arkusza, zmień nazwę `destWs` przy pomocy `destWs.setName("Report")` przed wklejeniem.

## Krok 5: Skopiuj zakres – Aspose.Cells automatycznie zachowuje tabelę przestawną

Metoda `copy` przenosi wszystko wewnątrz źródłowego zakresu, w tym definicję tabeli przestawnej, pamięć podręczną i formatowanie. Nie jest wymagany dodatkowy kod, aby tabela przestawna pozostała funkcjonalna.

```java
        // Copy the range to the destination worksheet; pivot tables are preserved automatically
        srcRange.copy(destWs.getCells().createRange("A1"));
```

*Dlaczego to działa:* Aspose.Cells traktuje tabelę przestawną jako zbiór ukrytych komórek i metadanych dołączonych do zakresu. Gdy wywołujesz `copy`, biblioteka odtwarza te metadane w docelowym skoroszycie.

## Krok 6: Zapisz docelowy skoroszyt

Na koniec zapisz wynik na dysk. Zapisany plik zawiera identyczną tabelę przestawną, którą możesz odświeżać lub modyfikować tak jak oryginał.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");

        System.out.println("Pivot table copied successfully.");
    }
}
```

Uruchomienie programu wypisuje potwierdzenie i tworzy `destination.xlsx` z w pełni funkcjonalną tabelą przestawną.

## Pełny, uruchamialny przykład

Po połączeniu wszystkich kroków, pełna klasa Java wygląda następująco:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load source workbook with pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot and its source data
        Range srcRange = srcWs.getCells().createRange("A1:H20");

        // 3️⃣ Prepare destination workbook (blank by default)
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // 4️⃣ Copy range – pivot table is kept intact
        srcRange.copy(destWs.getCells().createRange("A1"));

        // 5️⃣ Save the new file
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

### Oczekiwany wynik

* Konsola: `Pivot table copied successfully.`
* `destination.xlsx` otwiera się w Excelu z tabelą przestawną identyczną do tej w `source.xlsx`. Odświeżenie tabeli przestawnej pokazuje ten sam źródło danych, co dowodzi, że **how to copy pivot** działa zgodnie z zamierzeniami.

## Obsługa typowych wariantów

### Kopiowanie wielu arkuszy

Jeśli Twój projekt wymaga kopiowania kilku arkuszy, przeiteruj arkusze skoroszytu i powtórz kroki 2‑4 dla każdego arkusza. Tabela przestawna w każdym arkuszu zostanie zachowana niezależnie.

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet src = srcWb.getWorksheets().get(i);
    Worksheet dest = destWb.getWorksheets().add();
    src.getCells().copy(dest.getCells());
}
```

### Zachowanie zewnętrznych połączeń danych

Tabele przestawne korzystające z zewnętrznych źródeł danych zachowują ciąg połączenia po skopiowaniu. Jednak plik docelowy musi mieć dostęp do tego samego źródła danych. Zweryfikuj połączenie, otwierając tabelę przestawną i sprawdzając kartę **Data**.

### Radzenie sobie z scalonymi komórkami

Jeśli zakres źródłowy zawiera scalone komórki, Aspose.Cells automatycznie kopiuje układ scalania. Mimo to, zweryfikuj wynik, jeśli docelowy skoroszyt używa innej domyślnej szerokości kolumny.

## Najlepsze praktyki dla niezawodnego kopiowania

| Praktyka | Powód |
|----------|--------|
| Użyj dokładnego używanego zakresu (`srcWs.getCells().getMaxDisplayRange()`) zamiast sztywno zakodowanego adresu | Gwarantuje, że cała tabela przestawna i jej dane źródłowe są uwzględnione. |
| Zastosuj licencję przed intensywnymi operacjami | Zapobiega znakowi wodnemu wersji ewaluacyjnej i poprawia wydajność. |
| Odśwież tabelę przestawną po skopiowaniu (`pivotTable.refresh()`) jeśli dane źródłowe uległy zmianie | Zapewnia, że docelowy skoroszyt odzwierciedla najnowsze wartości. |
| Napisz testy jednostkowe, które otwierają docelowy skoroszyt i sprawdzają, że `pivotTable.getPivotFields().size()` jest równy źródłowi | Wykrywa przypadkową utratę pól podczas przyszłych zmian w kodzie. |

## Zakończenie

Teraz wiesz, jak **how to copy pivot** tabele między skoroszytami Excel w Javie, a także jak **copy range between workbooks**, **duplicate excel range** i **copy range to workbook**, zachowując wszystkie formatowania i formuły. Przykład używa Aspose.Cells, które abstrahuje niskopoziomową obsługę XML wymaganą przez OpenXML SDK.

Następnie, zapoznaj się z powiązanymi tematami, takimi jak **updating pivot cache programmatically**, **exporting pivot data to CSV**, lub **creating pivot tables from scratch**. Każdy z nich opiera się na tych samych koncepcjach przedstawionych tutaj.

Miłego kodowania i zachęcamy do eksperymentowania z większymi zakresami, wieloma tabelami przestawnymi lub własnym stylowaniem — ten sam wzorzec działa we wszystkich scenariuszach.

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak tworzyć tabele przestawne w Excelu przy użyciu Aspose.Cells for Java: Kompletny przewodnik](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Jak kopiować wiele kolumn w Excelu przy użyciu Aspose.Cells Java: Kompletny przewodnik](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Kopiowanie obrazów między arkuszami w Excelu przy użyciu Aspose.Cells for Java: Kompletny przewodnik](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}