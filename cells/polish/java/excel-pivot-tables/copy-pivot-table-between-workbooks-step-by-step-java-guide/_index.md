---
category: general
date: 2026-07-14
description: Skopiuj tabelę przestawną między skoroszytami przy użyciu Javy. Dowiedz
  się, jak skopiować tabelę przestawną, skopiować zakres w Excelu i wyeksportować
  tabelę przestawną w kilka minut.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- copy range between workbooks
- export pivot table
language: pl
lastmod: 2026-07-14
og_description: Szybko kopiuj tabelę przestawną w Javie. Ten przewodnik pokazuje,
  jak kopiować tabelę przestawną, kopiować zakres Excel oraz eksportować tabelę przestawną
  przy użyciu Aspose.Cells.
og_image_alt: Diagram illustrating copy pivot table process between two Excel workbooks
og_title: Kopiowanie tabeli przestawnej między skoroszytami – samouczek automatyzacji
  w Javie
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Copy pivot table between workbooks using Java. Learn how to copy pivot,
    copy Excel range, and export pivot table in minutes.
  headline: Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Kopiowanie tabeli przestawnej między skoroszytami – Przewodnik Java krok po
  kroku
url: /pl/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopiowanie tabeli przestawnej między skoroszytami – kompletny samouczek Java

Czy kiedykolwiek potrzebowałeś **skopiować tabelę przestawną** z jednego skoroszytu do drugiego i zastanawiałeś się, dlaczego zwykłe triki kopiuj‑wklej psują układ? Nie jesteś sam. W wielu przepływach raportowania tabela przestawna znajduje się w pliku głównym, ale procesy downstream wymagają lekkiej kopii.

W tym przewodniku przeprowadzimy Cię przez czysty, programowy sposób duplikacji tabeli przestawnej — bez ręcznego majsterkowania. Po zakończeniu będziesz wiedział, **jak skopiować tabelę przestawną**, jak **bezpiecznie skopiować zakres Excel**, a nawet jak **wyeksportować tabelę przestawną** do nowego pliku, wszystko przy użyciu Aspose.Cells for Java.

## Co zbudujesz

- Wczytaj skoroszyt źródłowy, który już zawiera tabelę przestawną.  
- Utwórz (lub otwórz) skoroszyt docelowy.  
- Zdefiniuj dokładny zakres, w którym znajduje się tabela przestawna.  
- Skopiuj ten zakres — łącznie z definicją tabeli przestawnej — do nowego skoroszytu.  
- Zapisz wynik, aby inne aplikacje mogły go otworzyć bez utraty obliczeń.

Bez zewnętrznych narzędzi, bez VBA, tylko czysty kod Java, który możesz wkleić do dowolnego projektu Maven lub Gradle.

## Wymagania wstępne

- Java 17 lub nowsza (kod działa na Java 8+, ale nowsze JDK zapewniają lepszą wydajność).  
- Aspose.Cells for Java 23.9 lub nowsza – dodaj zależność z Maven Central.  
- Dwa pliki Excel: `SourceWithPivot.xlsx` (zawiera tabelę przestawną) oraz pusty plik zastępczy dla kopii.  

Jeśli jesteś nowy w Aspose.Cells, biblioteka abstrahuje szczegóły niskopoziomowego OOXML, pozwalając traktować arkusze jak zwykłe obiekty Java.

## Krok 1: Skonfiguruj swój projekt

Najpierw dodaj artefakt Aspose.Cells Maven do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust if you use a different JDK -->
</dependency>
```

Lub dla Gradle:

```gradle
implementation 'com.aspose:aspose-cells:23.9:jdk17'
```

> **Wskazówka:** Jeśli używasz IDE takiego jak IntelliJ, pozwól mu automatycznie importować bibliotekę; oszczędza to wiele pisania.

## Krok 2: Wczytaj skoroszyt źródłowy

Potrzebujemy instancji `Workbook`, która wskazuje na plik zawierający tabelę przestawną. Konstruktor wczytuje cały plik do pamięci, więc możesz pracować z nim offline.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {

        // Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

Dlaczego najpierw go wczytać? Ponieważ pamięć podręczna tabeli przestawnej, lista pól i układ są przechowywane wewnątrz arkusza. Wczytanie skoroszytu do pamięci gwarantuje, że kopiujemy *definicję*, a nie tylko wyświetlane wartości.

## Krok 3: Utwórz lub otwórz skoroszyt docelowy

Masz dwie opcje: rozpocząć od zupełnie nowego skoroszytu lub otworzyć istniejący szablon. Tutaj utworzymy pusty, co jest najczęstszym scenariuszem, gdy potrzebna jest czysta kopia.

```java
        // Create an empty destination workbook (or open an existing one)
        Workbook destinationWorkbook = new Workbook(); // blank workbook with a default sheet
```

Jeśli później zdecydujesz się kopiować do konkretnego arkusza, po prostu zamień `getWorksheets().get(0)` na odpowiedni indeks lub nazwę.

## Krok 4: Zdefiniuj dokładny zakres, w którym znajduje się tabela przestawna

Tabela przestawna zazwyczaj zajmuje prostokątny blok. Najbezpieczniejszym podejściem jest wyraźne określenie komórek w lewym górnym i prawym dolnym rogu. W naszym przykładzie tabela przestawna znajduje się od **A1** do **H30**.

```java
        // Define the range in the source sheet that includes the pivot table
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)                     // first worksheet
                                          .getCells()
                                          .createRange("A1:H30");
```

> **Dlaczego nie używać `copyRows`?**  
> `copyRows` kopiuje surowe wartości komórek, ale pomija podstawową pamięć podręczną tabeli przestawnej. Kopiując cały zakres, Aspose.Cells zachowuje metadane tabeli przestawnej, umożliwiając docelowi zachowanie pełnej interaktywności.

## Krok 5: Skopiuj zakres (łącznie z tabelą przestawną) do docelowego skoroszytu

Teraz dzieje się magia. Metoda `copy` klonuje wszystko — wartości, formuły, formaty i sam obiekt tabeli przestawnej — do docelowego miejsca.

```java
        // Copy the defined range (with the pivot table) to the destination sheet
        sourceRange.copy(destinationWorkbook.getWorksheets()
                                            .get(0)               // destination sheet
                                            .getCells()
                                            .createRange("A1"));
```

Jeśli potrzebujesz wkleić do innej komórki, po prostu zmień `"A1"` na `"C5"` lub dowolny inny adres. Metoda automatycznie dostosowuje wewnętrzne odwołania, aby tabela przestawna nadal działała.

## Krok 6: Zapisz skoroszyt docelowy

Na koniec zapisz nowy skoroszyt na dysku. Powstały plik może być otwarty w Excelu, LibreOffice lub innym przeglądarce arkuszy kalkulacyjnych, a tabela przestawna zachowa się dokładnie tak, jak w źródle.

```java
        // Save the destination workbook with the copied pivot table
        destinationWorkbook.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

### Oczekiwany wynik

- `CopyPivotResult.xlsx` otwiera się z w pełni funkcjonalną tabelą przestawną identyczną z oryginałem.  
- Wszystkie segmentatory, filtry i pola obliczeniowe pozostają nienaruszone.  
- Brak utraty danych — wartości są obliczane w locie po odświeżeniu tabeli przestawnej.

## Typowe warianty i przypadki brzegowe

| Sytuacja | Co należy dostosować |
|-----------|----------------|
| **Kopiowanie do istniejącego skoroszytu** | Wczytaj docelowy skoroszyt zamiast tworzyć nowy: `new Workbook("ExistingFile.xlsx")`. |
| **Tabela przestawna ma nieznany rozmiar** | Użyj `Worksheet.getPivotTables().get(0).getPivotTableRange()`, aby programowo pobrać dokładny adres. |
| **Zachowanie połączeń danych** | Po skopiowaniu wywołaj `destinationWorkbook.getWorksheets().get(0).getPivotTables().get(0).setRefreshOnLoad(true);`, aby utrzymać aktywne zewnętrzne połączenia danych. |
| **Eksport tabeli przestawnej jako CSV** | Po skopiowaniu możesz wywołać `destinationWorkbook.save("PivotExport.csv", SaveFormat.CSV);` — to spłaszcza jedynie wartości tabeli przestawnej. |

> **Uwaga:** Gdy skoroszyty źródłowy i docelowy używają różnych ustawień regionalnych, formaty liczb mogą się zmienić. Jawnie ustaw `setLocale` skoroszytu, jeśli potrzebna jest spójność.

## Pełny działający przykład (wszystkie importy włączone)

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load source workbook containing the pivot
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

        // 2️⃣ Create (or open) destination workbook
        Workbook destinationWorkbook = new Workbook(); // blank workbook

        // 3️⃣ Identify the range that encloses the pivot table
        //    If you don't know the range, you can retrieve it via:
        //    PivotTable pt = sourceWorkbook.getWorksheets().get(0).getPivotTables().get(0);
        //    String address = pt.getPivotTableRange().getRefersTo();
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:H30");

        // 4️⃣ Copy the range (pivot included) to the destination sheet
        sourceRange.copy(destinationWorkbook.getWorksheets()
                                            .get(0)
                                            .getCells()
                                            .createRange("A1"));

        // 5️⃣ Persist the result
        destinationWorkbook.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");

        System.out.println("Pivot table copied successfully!");
    }
}
```

Uruchom program, otwórz `CopyPivotResult.xlsx`, a zobaczysz dokładnie tę samą tabelę przestawną, od której zacząłeś — gotową do dalszej analizy lub dystrybucji.

## Podsumowanie

Właśnie pokazaliśmy **jak skopiować tabelę przestawną** z jednego skoroszytu do drugiego przy użyciu Aspose.Cells for Java. Kroki obejmowały wczytanie źródła, zdefiniowanie dokładnego **zakresu Excel do skopiowania**, wykonanie kopiowania oraz ostatecznie **eksport tabeli przestawnej** do nowego pliku. Obsługując zakres zamiast pojedynczych komórek, zapewniamy, że wewnętrzna pamięć podręczna tabeli przestawnej podąża za nią, utrzymując raport dynamiczny.

## Co warto zbadać dalej

- **Automatyzacja odświeżania**: Zaplanuj operację kopiowania przy użyciu zadania Quartz, aby Twoje pliki downstream były zawsze aktualne.  
- **Kopiowanie wielu tabel przestawnych**: Przejdź pętlą przez `sourceWorkbook.getWorksheets().get(0).getPivotTables()` i skopiuj każdą do osobnych arkuszy.  
- **Zastosowanie stylizacji**: Użyj obiektów `Style`, aby ujednolicić czcionki i kolory w całym skoroszycie docelowym.  

Jeśli masz pytania dotyczące obsługi dużych skoroszytów lub zachowania zewnętrznych źródeł danych, zostaw komentarz poniżej. Szczęśliwego kodowania i ciesz się swobodą programowej automatyzacji Excela!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Manipulacja tabelą przestawną Excel przy użyciu Aspose.Cells Java: Kompletny przewodnik](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Jak zaktualizować źródło tabeli przestawnej Excel przy użyciu Aspose.Cells for Java: Kompletny przewodnik](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Automatyzacja stylizacji i zapisywania tabeli przestawnej Excel przy użyciu Aspose.Cells for Java: Kompletny przewodnik](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}