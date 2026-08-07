---
category: general
date: 2026-07-23
description: Utwórz nowy skoroszyt w Javie i dowiedz się, jak kopiować tabelę przestawną,
  kopiować zakres Excel oraz eksportować tabelę przestawną przy użyciu Aspose.Cells
  w kilka minut.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- how to copy pivot
- copy excel range
- export pivot table
language: pl
lastmod: 2026-07-23
og_description: Utwórz nowy skoroszyt w Javie i natychmiast skopiuj tabelę przestawną,
  skopiuj zakres Excela, a następnie wyeksportuj tabelę przestawną przy użyciu Aspose.Cells.
  Przejdź do tego pełnego poradnika.
og_image_alt: Screenshot of Java code copying a pivot table from one workbook to another
og_title: Utwórz nowy skoroszyt w Javie – kopiowanie tabeli przestawnej krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Create new workbook in Java and learn how to copy pivot table, copy
    excel range, and export pivot table with Aspose.Cells in minutes.
  headline: Create New Workbook in Java – Full Guide to Copy Pivot Table
  type: TechArticle
- questions:
  - answer: You’ll need to copy each relevant range separately, then recreate the
      pivot on the destination sheet using `PivotTable` APIs.
    question: What if the source pivot spans more than one worksheet?
  - answer: Set `sourceRange.setCopyDataOnly(false)` before the copy. This tells Aspose
      to keep the cache but not the underlying source data.
    question: Can I copy only the pivot layout without the data?
  - answer: CSV doesn’t support pivots, but you can export the pivot’s *result* by
      calling `pivotTable.calculate()` and then saving the sheet as CSV.
    question: Is there a way to copy the pivot to a CSV file?
  - answer: Formatting lives in the style collection. After copying, you can call
      `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())`
      to transfer styles.
    question: Why does the copied pivot lose its formatting?
  type: FAQPage
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Utwórz nowy skoroszyt w Javie – Pełny przewodnik po kopiowaniu tabeli przestawnej
url: /pl/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie nowego skoroszytu w Javie – Kompletny przewodnik po kopiowaniu tabel przestawnych

Zastanawiałeś się kiedyś, jak **utworzyć nowy skoroszyt** w Javie, zachowując przy tym złożoną tabelę przestawną? Nie jesteś jedynym, który drapie się po głowie nad tym problemem. W wielu aplikacjach raportowych trzeba przenieść tabelę przestawną z pliku źródłowego do nowego skoroszytu, być może aby wysłać go klientowi lub wykonać dalsze obliczenia. Dobra wiadomość? Kilka linijek kodu wystarczy, aby zrobić to automatycznie – bez ręcznego kopiowania i wklejania.

W tym samouczku przejdziemy przez cały proces: wczytanie pliku źródłowego, określenie zakresu zawierającego tabelę przestawną, **skopiowanie zakresu Excel**, utworzenie **nowego skoroszytu** oraz w końcu **eksport tabeli przestawnej** do nowego pliku. Po zakończeniu będziesz mieć samodzielny, gotowy do uruchomienia program w Javie, który odpowie na pytanie „**jak skopiować tabelę przestawną**” bez domysłów.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz:

- Java 17 lub nowszą (kod działa z dowolnym aktualnym JDK)
- Bibliotekę Aspose.Cells for Java (wersja trial lub licencjonowana)
- Przykładowy plik `source.xlsx` zawierający tabelę przestawną w zakresie `A1:G20`
- IDE lub narzędzie budujące (Maven/Gradle) do zarządzania plikiem JAR Aspose.Cells

Masz wszystko? Świetnie – zaczynamy.

## Krok 1: Konfiguracja projektu i import Aspose.Cells

Na początek musisz dodać Aspose.Cells do swojego projektu. Jeśli używasz Maven, wstaw tę zależność do pliku `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.8</version> <!-- check for the latest version -->
</dependency>
```

Jeśli wolisz Gradle, odpowiednik wygląda tak:

```groovy
implementation 'com.aspose:aspose-cells:24.8'
```

Gdy biblioteka znajdzie się na classpath, zaimportuj potrzebne klasy:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **Pro tip:** Aspose.Cells to biblioteka komercyjna, ale oferuje w pełni funkcjonalną 30‑dniową wersję ewaluacyjną, która dodaje znak wodny do wyników – idealna do wypróbowania tego rozwiązania.

## Krok 2: Wczytanie skoroszytu źródłowego

Teraz **utworzymy nowy skoroszyt**, ale najpierw potrzebujemy źródła, które zawiera tabelę przestawną. Ten krok jest fundamentem każdej operacji **copy excel range**, ponieważ obiekt zakresu dokładnie wie, które komórki (wraz z pamięcią podręczną tabeli przestawnej) należy przenieść.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0) – adjust if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Dlaczego nie odczytać od razu samego zakresu? Ponieważ metadane tabeli przestawnej znajdują się w pamięci podręcznej arkusza, a Aspose.Cells automatycznie dołącza je przy kopiowaniu zakresu.

## Krok 3: Zdefiniowanie zakresu zawierającego tabelę przestawną

W wielu rzeczywistych plikach tabela przestawna zajmuje prostokątny blok. W tym przykładzie przyjmujemy, że znajduje się w `A1:G20`. Oczywiście możesz dostosować adres do własnego układu.

```java
// Define the exact area that includes the pivot table
Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

Jeśli nie jesteś pewien dokładnego adresu, możesz użyć `sourceSheet.getCells().getMaxDataRow()` oraz `getMaxDataColumn()`, aby dynamicznie obliczyć granice. To przydatny trik, gdy rozmiar tabeli zmienia się w czasie.

## Krok 4: **Utworzenie nowego skoroszytu** i arkusza docelowego

Oto moment, w którym faktycznie **tworzymy nowy skoroszyt**, który przyjmie skopiowaną zawartość. Pomyśl o tym jak o czystym płótnie, na które wkleisz tabelę przestawną.

```java
// Create an empty workbook – this is our destination
Workbook destinationWorkbook = new Workbook();

// By default a new workbook comes with one worksheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Dlaczego zaczynamy od pustego skoroszytu? Gwarantuje to, że żadne ukryte style ani poprzednie tabele nie zakłócą kopiowania, dając czysty rezultat gotowy do **export pivot table**.

## Krok 5: Kopiowanie tabeli przestawnej (i jej podstawowego zakresu)

Teraz serce samouczka: **copy pivot table**. Aspose.Cells traktuje kopiowanie zakresu jako głęboką kopię, co oznacza, że pamięć podręczna tabeli przestawnej podróżuje razem z komórkami. Dlatego ta jedna linijka wykonuje całą ciężką pracę.

```java
// Copy the defined range (including the pivot) to the destination sheet at A1
sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

Jeśli kiedykolwiek zastanawiałeś się **jak skopiować tabelę przestawną** bez utraty jej funkcjonalności, oto odpowiedź. Arkusz docelowy zawiera teraz w pełni działającą tabelę, którą możesz odświeżać, modyfikować lub po prostu wyeksportować.

### Przypadek brzegowy: Zachowanie ustawień odświeżania

Czasami tabela przestawna w źródle jest ustawiona na odświeżanie przy otwarciu. Aby zachować to zachowanie, możesz skopiować opcje tabeli explicite:

```java
// Optional: retain the original pivot's refresh settings
PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
PivotTable destPivot = destinationSheet.getPivotTables().get(0);
destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
```

Ten fragment zapewnia, że skopiowana tabela zachowuje się dokładnie tak samo jak oryginał.

## Krok 6: Zapisanie skoroszytu docelowego – **Export Pivot Table**

Na koniec **eksportujemy tabelę przestawną**, zapisując nowy skoroszyt na dysku. Możesz wybrać dowolny format obsługiwany przez Aspose: XLSX, XLS, CSV, PDF itp. W tym przewodniku pozostaniemy przy XLSX.

```java
// Save the workbook that now contains the copied pivot
destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);
```

Jeśli potrzebujesz przesłać plik przez usługę webową, możesz zapisać go do `ByteArrayOutputStream` zamiast do ścieżki pliku – Aspose ułatwia to zadanie.

## Pełny działający przykład

Łącząc wszystkie elementy, oto kompletny, gotowy do uruchomienia program. Śmiało skopiuj, wklej i uruchom go w swoim IDE.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 3️⃣ Copy the range (pivot table included) to the destination sheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Optional: Preserve refresh settings if needed
        if (!sourceSheet.getPivotTables().isEmpty()) {
            PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
            PivotTable destPivot = destinationSheet.getPivotTables().get(0);
            destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
        }

        // 4️⃣ Save the result – this effectively **export pivot table**
        destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);

        System.out.println("Pivot table copied successfully!");
    }
}
```

### Oczekiwany wynik

Po uruchomieniu programu w konsoli pojawi się:

```
Pivot table copied successfully!
```

A plik `copied_with_pivot.xlsx` pojawi się w katalogu `YOUR_DIRECTORY`. Otwórz go w Excelu, a zobaczysz tabelę przestawną w całości, gotową do odświeżenia lub edycji.

## Często zadawane pytania i rozwiązywanie problemów

- **Co zrobić, gdy źródłowa tabela przestawna rozciąga się na więcej niż jeden arkusz?**  
  Należy skopiować każdy odpowiedni zakres osobno, a następnie odtworzyć tabelę przestawną w arkuszu docelowym przy użyciu API `PivotTable`.

- **Czy mogę skopiować tylko układ tabeli, bez danych?**  
  Ustaw `sourceRange.setCopyDataOnly(false)` przed kopiowaniem. To polecenie mówi Aspose, aby zachował pamięć podręczną, ale nie przenosił danych źródłowych.

- **Czy istnieje sposób na skopiowanie tabeli przestawnej do pliku CSV?**  
  CSV nie obsługuje tabel przestawnych, ale możesz wyeksportować *wynik* tabeli, wywołując `pivotTable.calculate()`, a następnie zapisując arkusz jako CSV.

- **Dlaczego skopiowana tabela traci formatowanie?**  
  Formatowanie znajduje się w kolekcji stylów. Po kopiowaniu możesz wywołać `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())`, aby przenieść style.

## Podsumowanie

Pokazaliśmy, jak **utworzyć nowy skoroszyt** w Javie, **skopiować tabelę przestawną** oraz **wyeksportować tabelę przestawną** – wszystko przy użyciu przejrzystego, powtarzalnego przykładu kodu. Definiując dokładny **copy excel range**, wykorzystując semantykę głębokiego kopiowania Aspose.Cells i zachowując opcjonalne ustawienia, możesz zautomatyzować praktycznie każde zadanie migracji tabel przestawnych.

Gotowy na kolejny krok? Spróbuj zmienić format wyjściowy na PDF lub przeiteruj wiele plików źródłowych, aby przetworzyć dziesiątki tabel przestawnych jednocześnie. Ten sam wzorzec się sprawdzi – wystarczy dostosować ścieżki plików i adresy zakresów.

Jeśli napotkasz problem, zostaw komentarz poniżej lub zajrzyj do dokumentacji Aspose.Cells, aby poznać zaawansowane techniki manipulacji tabelami przestawnymi. Miłego kodowania i ciesz się czasem zaoszczędzonym dzięki automatyzacji tych uciążliwych operacji kopiuj‑wklej!

## Co warto nauczyć się dalej?

Poniższe samouczki dotyczą ściśle powiązanych tematów, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz szczegółowe wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Jak tworzyć tabele przestawne w Excelu przy użyciu Aspose.Cells for Java: Kompletny przewodnik](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Jak aktualizować źródło tabeli przestawnej w Excelu przy użyciu Aspose.Cells for Java: Kompletny przewodnik](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Jak tworzyć i eksportować Excel do HTML przy użyciu Aspose.Cells Java | Przewodnik po operacjach na skoroszycie](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}