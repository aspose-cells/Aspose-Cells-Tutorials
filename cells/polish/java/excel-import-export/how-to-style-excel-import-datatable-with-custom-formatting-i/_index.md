---
category: general
date: 2026-07-03
description: Jak stylizować pliki Excel przy użyciu Javy. Dowiedz się, jak formatować
  kolumnę z datą w Excelu, zastosować format liczbowy w Excelu, eksportować DataTable
  do XLSX oraz importować DataTable do Excela przy użyciu Aspose Cells.
draft: false
keywords:
- how to style excel
- format column date excel
- apply number format excel
- export datatable to xlsx
- import datatable into excel
language: pl
og_description: Jak stylizować pliki Excel w Javie. Ten tutorial pokazuje, jak formatować
  daty w kolumnie w Excelu, zastosować format liczbowy w Excelu, eksportować DataTable
  do XLSX oraz importować DataTable do Excela.
og_title: Jak stylizować Excel – Przewodnik Java poświęcony niestandardowemu formatowaniu
  kolumn
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to style Excel files using Java. Learn to format column date Excel,
    apply number format Excel, export DataTable to XLSX and import DataTable into
    Excel with Aspose Cells.
  headline: How to Style Excel – Import DataTable with Custom Formatting in Java
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: Jak stylizować Excel – importowanie DataTable z niestandardowym formatowaniem
  w Javie
url: /pl/java/excel-import-export/how-to-style-excel-import-datatable-with-custom-formatting-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak stylować Excel – Importowanie DataTable z niestandardowym formatowaniem w Javie

Zastanawiałeś się kiedyś, **jak stylować Excel** arkusze programowo, bez ręcznego otwierania pliku? Nie jesteś sam. Wielu programistów musi generować raporty, w których pierwsza kolumna jest pogrubiona, druga wyświetla daty, a pozostałe mają przejrzysty układ. W tym przewodniku przeprowadzimy Cię przez kompletny, działający przykład, który **importuje DataTable do Excela**, stosuje pogrubiony nagłówek, formatuje kolumnę z datą i w końcu **eksportuje DataTable do XLSX**.  

Użyjemy Aspose.Cells for Java, ale koncepcje można zastosować w dowolnej bibliotece umożliwiającej pracę ze stylami. Po zakończeniu będziesz mieć wielokrotnego użytku wzorzec dla **apply number format Excel** komórek, **format column date Excel**, i dostarczysz dopracowany skoroszyt swoim użytkownikom.

## Wymagania wstępne

- Java 17 (lub dowolny nowoczesny JDK)  
- Aspose.Cells for Java 23.9 lub nowszy (bezpłatna wersja próbna działa)  
- Struktura podobna do `DataTable` (przykład używa prostego mocka)  
- Twoje ulubione IDE (IntelliJ IDEA, Eclipse, VS Code…)

Nie są wymagane dodatkowe wtyczki Maven; wystarczy dodać plik JAR Aspose.Cells do classpath.

---

## Krok 1: Uzyskaj źródłowy DataTable – przygotowanie „Export DataTable to XLSX”

Zanim będziemy mogli **importować datatable do excela**, potrzebujemy obiektu `DataTable`, który reprezentuje dane, które chcesz wyeksportować. W rzeczywistych projektach możesz pobrać je z bazy danych, pliku CSV lub API. W tym tutorialu zamockujemy małą tabelę:

```java
import java.util.*;
import com.aspose.cells.*;

public class DemoData {
    public static DataTable getDataTable() {
        // Create a simple table with three columns: ID, Date, Amount
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("OrderDate", DataType.DATE_TIME);
        dt.getColumns().add("Total", DataType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[]{1, new Date(), 125.50});
        dt.getRows().add(new Object[]{2, new Date(System.currentTimeMillis() - 86400000L), 99.99});
        dt.getRows().add(new Object[]{3, new Date(System.currentTimeMillis() - 2*86400000L), 250.00});
        return dt;
    }
}
```

> **Dlaczego to ważne:** Uzyskanie danych od razu oznacza, że reszta logiki stylizacji może koncentrować się wyłącznie na prezentacji, a nie na manipulacji danymi.

---

## Krok 2: Utwórz tablicę przechowującą definicje stylów dla każdej kolumny

Aspose.Cells pozwala przekazać tablicę **Style[]** przy importowaniu `DataTable`. Każdy element odpowiada kolumnie i określa, jak ta kolumna będzie wyglądać po imporcie. Przydzielmy tablicę na podstawie liczby kolumn:

```java
DataTable dataTable = DemoData.getDataTable();
Style[] columnStyles = new Style[dataTable.getColumns().size()];
```

> **Wskazówka:** Jeśli masz wiele kolumn, rozważ budowanie tablicy w pętli i ponowne użycie jednego obiektu `Style`, gdy formatowanie jest identyczne. To zmniejsza zużycie pamięci.

---

## Krok 3: Zdefiniuj style – pogrubiony nagłówek i formatowanie daty

Teraz odpowiemy na klasyczne pytanie **format column date excel** i pokażemy także **apply number format excel** dla innych kolumn.

```java
// --- Style for the first column (header bold) ---
columnStyles[0] = new Style();
columnStyles[0].getFont().setBold(true);          // Makes header text bold

// --- Style for the second column (date formatting) ---
columnStyles[1] = new Style();
columnStyles[1].setNumber(StyleNumberFormat.DATE); // Uses the built‑in DATE format

// --- Optional: Style for the third column (currency) ---
columnStyles[2] = new Style();
columnStyles[2].setNumber(StyleNumberFormat.CURRENCY_USD);
```

**Co się tutaj dzieje?**  
- `StyleNumberFormat.DATE` informuje Excel, aby traktował wartość komórki jako krótką datę (np. *01/31/2024*).  
- `StyleNumberFormat.CURRENCY_USD` automatycznie dodaje symbol `$` i dwie miejsca po przecinku.  
- Ustawienie czcionki na pogrubioną w pierwszej kolumnie sprawia, że nagłówek wyróżnia się, co jest częstym wymogiem, gdy **how to style excel** arkusze dla czytelności.

> **Przypadek brzegowy:** Jeśli Twoje dane źródłowe już zawierają sformatowane ciągi, może być konieczne przekształcenie ich do obiektów `java.util.Date` przed importem; w przeciwnym razie Excel potraktuje je jako zwykły tekst.

---

## Krok 4: Utwórz nowy skoroszyt i uzyskaj dostęp do pierwszego arkusza

Nowy skoroszyt zapewnia czyste płótno. Pobierzemy pierwszy arkusz, w którym zostanie umieszczony import.

```java
Workbook workbook = new Workbook();               // New empty workbook
Worksheet worksheet = workbook.getWorksheets().get(0); // First sheet (index 0)
```

> **Dlaczego nowy skoroszyt?** Rozpoczęcie od zera gwarantuje, że żadne pozostałe style ani ukryte wiersze nie zakłócą ostatecznego wyniku — co jest niezbędne, gdy **how to style excel** pliki konsekwentnie w wielu uruchomieniach.

---

## Krok 5: Importuj DataTable z stylami kolumn

Oto serce operacji: wprowadzanie `DataTable` do arkusza przy jednoczesnym zastosowaniu tablicy stylów, którą zbudowaliśmy.

```java
// The third argument (true) tells Aspose.Cells to include column headers.
worksheet.getCells().importDataTable(dataTable, true, columnStyles);
```

**Wyjaśnienie:**  
- `importDataTable` kopiuje zarówno wiersz nagłówka, jak i wiersze danych.  
- Tablica `columnStyles` odpowiada każdej kolumnie, więc nagłówek pierwszej kolumny staje się pogrubiony, druga kolumna wyświetla daty, a trzecia kolumna pojawia się jako waluta.  
- Ten pojedynczy wiersz zastępuje dziesiątki ręcznych kroków formatowania komórek, ilustrując czysty sposób **apply number format excel** programowo.

---

## Krok 6: Zapisz stylowany skoroszyt – ukończenie „Export DataTable to XLSX”

Na koniec zapisujemy skoroszyt na dysku. Dostosuj ścieżkę do zapisu w folderze, w którym masz uprawnienia zapisu.

```java
String outputPath = "C:/temp/styledImport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Otwórz plik w Excelu i powinieneś zobaczyć:

- Nagłówek kolumny **ID** pogrubiony.  
- Kolumna **OrderDate** sformatowana jako daty (np. *04/27/2024*).  
- Kolumna **Total** wyświetlana z symbolem dolara i dwoma miejscami po przecinku.

> **Pro tip:** Jeśli musisz obsługiwać starsze wersje Excela, wywołaj `workbook.save(outputPath, SaveFormat.XLS)` zamiast domyślnego XLSX.

---

## Krok 7: Zweryfikuj wynik i opcjonalne poprawki

Dobrym zwyczajem jest podwójne sprawdzenie wygenerowanego pliku, szczególnie przy automatyzacji raportów dla interesariuszy.

```java
// Quick verification: read the first cell's style
Cell firstHeader = worksheet.getCells().get(0, 0);
boolean isBold = firstHeader.getStyle().getFont().isBold();
System.out.println("Header bold? " + isBold);
```

Jeśli `isBold` wypisze `true`, Twoja rutyna **how to style excel** działała zgodnie z zamierzeniami. Od tego momentu możesz:

- Dodać formatowanie warunkowe (np. podświetlić sumy > $200).  
- Zablokować pierwszy wiersz dla łatwiejszego przewijania.  
- Wstawić wykres odwołujący się do zaimportowanych danych.

Wszystkie te rozszerzenia stosują ten sam wzorzec: zdefiniuj `Style`, zastosuj go i zapisz.

---

## Częste pytania i przypadki brzegowe

| Question | Answer |
|----------|--------|
| **Czy mogę stylizować więcej niż jedną kolumnę w ten sam sposób?** | Tak — użyj ponownie jednego obiektu `Style` dla wszystkich kolumn, które mają takie samo formatowanie. |
| **Co się stanie, jeśli mój DataTable ma więcej kolumn niż stylów?** | Każda kolumna bez odpowiadającego wpisu w `columnStyles` użyje domyślnego stylu. |
| **Jak zmienić format daty na „dd‑MMM‑yyyy”?** | Użyj `columnStyles[1].setCustom("#dd-MMM-yyyy#");` zamiast wbudowanego `DATE`. |
| **Czy istnieje sposób na automatyczne dopasowanie szerokości kolumn po imporcie?** | Wywołaj `worksheet.autoFitColumns();` po `importDataTable`. |
| **Czy to będzie działać na Linux/macOS?** | Zdecydowanie — Aspose.Cells jest niezależny od platformy, o ile masz kompatybilny JDK. |

---

## Podsumowanie

Masz teraz solidny, kompleksowy przykład **how to style Excel** skoroszytów poprzez **importowanie datatable do excela**, **format column date excel** i **apply number format excel** przy użyciu Javy. Kod pokazuje pełny przepływ od **export datatable to xlsx** po otwarcie pliku w Excelu, obejmując zarówno *co*, jak i *dlaczego* za każdym krokiem.

Spróbuj: dostosuj tablicę stylów, dodaj więcej kolumn lub podłącz rzeczywiste zapytanie do bazy danych. Ten sam wzorzec pozwoli Ci generować profesjonalnie wyglądające raporty jednym kliknięciem, bez ręcznego formatowania.

![Arkusz Excel stylowany wygenerowany przez kod tutoriala](https://example.com/images/styled-worksheet.png "Zrzut ekranu stylowanego arkusza Excel utworzonego przy użyciu Javy i Aspose.Cells")
*Tekst alternatywny obrazu: „Arkusz Excel stylowany przy użyciu Javy i Aspose.Cells, pokazujący pogrubiony nagłówek i sformatowaną kolumnę daty.”*

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Aspose.Cells for Java: How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}