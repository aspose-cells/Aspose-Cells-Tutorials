---
category: general
date: 2026-08-20
description: Dowiedz się, jak wyeksportować wykres do pliku docx i przekonwertować
  skoroszyt Excel na docx przy użyciu Aspose.Cells w Javie. Przewodnik krok po kroku
  z pełnym kodem.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export chart to docx
- convert excel workbook to docx
- Aspose.Cells Java
- editable chart DOCX
- Excel to Word conversion
language: pl
lastmod: 2026-08-20
og_description: Eksportuj wykres do formatu docx i konwertuj skoroszyt Excel na docx
  przy użyciu Aspose.Cells for Java. Zapoznaj się z tym kompletnym, działającym samouczkiem.
og_image_alt: Screenshot showing a Java code editor exporting an Excel chart to a
  DOCX file
og_title: Eksportuj wykres do docx przy użyciu Aspose.Cells – przewodnik Java
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to export chart to docx and convert Excel workbook to docx
    with Aspose.Cells in Java. Step‑by‑step guide with complete code.
  headline: How to export chart to docx from Excel using Aspose.Cells for Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- DOCX
- Excel
title: Jak wyeksportować wykres do pliku docx z Excela przy użyciu Aspose.Cells for
  Java
url: /pl/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eksport wykresu do docx z skoroszytu Excel przy użyciu Javy

Jeśli potrzebujesz **export chart to docx** bezpośrednio z pliku Excel, ten tutorial pokazuje gotowe rozwiązanie. Po zakończeniu przewodnika będziesz także wiedział, jak **convert Excel workbook to docx** zachowując edytowalny wykres, tak aby powstały dokument Word mógł być modyfikowany bez utraty jakości.

Eksportowanie wykresów jest powszechne, gdy tworzysz raporty łączące obliczenia w arkuszach kalkulacyjnych z bogatymi układami Worda. Aspose.Cells for Java upraszcza konwersję, a API pozwala zachować wykres jako edytowalny — nie jest wymagana statyczna grafika.

## Co obejmuje ten tutorial

* Ładowanie istniejącego skoroszytu, który zawiera wykres.  
* Konfigurowanie `ImageOrPrintOptions`, aby skierować wyjście do formatu DOCX.  
* Włączenie flagi `ExportEditableCharts` (dostępnej od wersji 25.10).  
* Zapisanie skoroszytu jako pliku DOCX, który zachowuje edytowalny wykres.  

Nie są potrzebne żadne zewnętrzne narzędzia poza plikiem JAR Aspose.Cells. Kod działa z Java 8+ oraz dowolną aktualną wersją Aspose.Cells.

## Wymagania wstępne

| Wymaganie | Dlaczego jest ważne |
|-------------|----------------|
| **Aspose.Cells for Java** (v25.10 lub nowsza) | Funkcja `setExportEditableCharts` została wprowadzona w tej wersji. |
| **Java Development Kit (JDK) 8 lub nowszy** | Zapewnia środowisko uruchomieniowe do kompilacji i wykonania przykładu. |
| **Skoroszyt Excel (`.xlsx`) zawierający przynajmniej jeden wykres** | Wykres jest obiektem, który zostanie wyeksportowany do DOCX. |
| **IDE Java lub narzędzie budujące (np. Maven, Gradle)** | Ułatwia zarządzanie zależnościami i uruchamianie. |

Możesz pobrać najnowszy Aspose.Cells JAR ze strony [Aspose website](https://products.aspose.com/cells/java/).

## Krok 1: Skonfiguruj projekt i dodaj zależność Aspose.Cells

Jeśli używasz Maven, dodaj następującą zależność do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version> <!-- use the latest version -->
</dependency>
```

Dla Gradle, dodaj:

```gradle
implementation 'com.aspose:aspose-cells:25.10'
```

> **Pro tip:** Użyj dokładnie tej wersji, która wprowadziła `ExportEditableCharts` (25.10) lub nowszej. Starsze wersje zignorują flagę i wygenerują statyczny obraz zamiast tego.

## Krok 2: Załaduj skoroszyt zawierający wykres

Klasa `Workbook` reprezentuje cały plik Excel. Załadowanie go to jednowierszowa operacja:

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Load the workbook with the chart you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");
```

> **Why this matters:** Skoroszyt musi być w pełni załadowany, zanim zastosujesz jakiekolwiek opcje eksportu. Jeśli ścieżka do pliku jest nieprawidłowa, Aspose.Cells zgłosi `FileNotFoundException`.

## Krok 3: Skonfiguruj opcje obrazu/drukowania dla wyjścia DOCX

`ImageOrPrintOptions` kontroluje, jak skoroszyt jest renderowany. Ustawienie formatu zapisu na `DOCX` informuje Aspose.Cells, aby wygenerował dokument Word zamiast obrazu.

```java
        // Create options and specify DOCX as the target format
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);
```

Możesz również dostosować rozmiar strony, DPI lub jakość obrazu, ale nie są one wymagane przy eksporcie wykresu.

## Krok 4: Włącz eksport edytowalnych wykresów

Od wersji 25.10 Aspose.Cells może osadzać wykresy jako natywne obiekty wykresów Worda. Dzięki temu są w pełni edytowalne w Microsoft Word.

```java
        // Turn on the editable chart export flag
        options.setExportEditableCharts(true);
```

> **Edge case:** Jeśli ustawisz tę flagę na `false` (lub ją pominiesz), wykres zostanie wyrenderowany jako statyczny obraz. Użyj `true` tylko wtedy, gdy docelowi odbiorcy muszą edytować wykres po konwersji.

## Krok 5: Zapisz skoroszyt jako plik DOCX

Na koniec wywołaj `Workbook.save` z skonfigurowanymi opcjami:

```java
        // Save the workbook as a DOCX document that contains an editable chart
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

Gdy program zakończy działanie, otwórz `ChartEditable.docx` w Microsoft Word. Powinieneś zobaczyć oryginalny wykres, a po kliknięciu prawym przyciskiem pojawi się opcja **Edit Data** — co potwierdza, że wykres jest naprawdę edytowalny.

## Pełny, gotowy do uruchomienia przykład

Poniżej znajduje się kompletny plik źródłowy. Skopiuj go do swojego IDE, zamień `YOUR_DIRECTORY` na ścieżkę absolutną lub względną i uruchom.

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");

        // Step 2: Create image/print options and set the target format to DOCX
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);

        // Step 3: Enable exporting of editable charts (available from version 25.10)
        options.setExportEditableCharts(true);

        // Step 4: Save the workbook as a DOCX document with the configured options
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

**Expected output**

* Plik o nazwie `ChartEditable.docx` w określonym katalogu.  
* Otwierając plik w Wordzie, wykres wygląda dokładnie tak, jak w Excelu, a podwójne kliknięcie wykresu umożliwia edycję jego serii danych.

## Typowe problemy i jak ich uniknąć

| Objaw | Przyczyna | Rozwiązanie |
|---------|-------|-----|
| Word wyświetla **statyczny obraz** zamiast edytowalnego wykresu | `setExportEditableCharts` nie wywołane lub używana wersja < 25.10 | Upewnij się, że flaga jest ustawiona na `true` i używasz Aspose.Cells 25.10 lub nowszej. |
| Wygenerowany DOCX jest **pusty** | Nieprawidłowa ścieżka do źródłowego skoroszytu lub niewystarczające uprawnienia | Zweryfikuj ścieżkę do skoroszytu oraz dostęp aplikacji do odczytu/zapisu. |
| Układ wykresu wygląda **zniekształcony** | Ustawienia strony w Excelu (np. ukryte wiersze/kolumny) różnią się od domyślnych w Wordzie | Dostosuj `ImageOrPrintOptions` (np. `setOnePagePerSheet(true)`) aby kontrolować skalowanie. |
| **Wydajność** spada przy dużych skoroszytach | Eksportowanie wielu wykresów lub dużych zestawów danych | Eksportuj tylko potrzebne arkusze lub użyj `setSheetIndex`, aby ograniczyć przetwarzanie. |

## Rozszerzanie rozwiązania

* **Wiele wykresów:** Iteruj po wszystkich arkuszach i wywołuj `worksheet.getCharts()`, aby wyeksportować każdy wykres osobno.  
* **Niestandardowe stylowanie DOCX:** Po zapisaniu użyj Aspose.Words, aby dodać nagłówki, stopki lub style do wygenerowanego dokumentu.  
* **Konwersja wsadowa:** Umieść kod w pętli przetwarzającej katalog plików `.xlsx`, generując DOCX dla każdego z nich.

## Podsumowanie

Masz teraz niezawodną metodę do **export chart to docx** i **convert Excel workbook to docx**, zachowując pełną edytowalność wykresu. Kluczowe kroki to załadowanie skoroszytu, skonfigurowanie `ImageOrPrintOptions` dla DOCX, włączenie `ExportEditableCharts` i zapis wyniku.

Eksperymentuj z dodatkowymi opcjami — takimi jak ustawianie marginesów strony czy osadzanie formuł skoroszytu — aby dopasować wyjście do swojego procesu raportowania. Gdy potrzebujesz programowo generować raporty Worda z danych Excel, to podejście zapewnia czyste i utrzymywalne rozwiązanie.

--- 

*Gotowy, aby wypróbować? Sklonuj przykład, zaktualizuj ścieżki do plików i uruchom program. Jeśli napotkasz problemy, zajrzyj do dokumentacji Aspose.Cells for Java lub przejrzyj powiązane tematy poniżej.*  

### Powiązane tematy, które możesz dalej eksplorować

* **convert excel workbook to pdf** – generowanie raportów PDF z tego samego skoroszytu.  
* **Aspose.Cells chart formatting** – dostosowywanie kolorów, znaczników i osi przed eksportem.  
* **Embedding images in DOCX with Aspose.Words** – łączenie wykresów z inną zawartością Worda.  

Miłego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Automate Excel Chart Access Using Aspose.Cells Java: A Step-by-Step Guide](/cells/english/java/charts-graphs/excel-charts-access-aspose-cells-java/)
- [Customize Excel Chart Data Labels Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}