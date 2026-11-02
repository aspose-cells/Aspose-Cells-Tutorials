---
category: general
date: 2026-06-18
description: Szybko utwórz PNG z tabeli przestawnej w Javie. Dowiedz się, jak wyeksportować
  obraz danych z Excela, wyeksportować obraz tabeli przestawnej oraz zapisać zakres
  jako plik PNG.
draft: false
keywords:
- create png from pivot
- export excel data image
- export pivot table image
- export excel range image
- export pivot table file
language: pl
og_description: Utwórz PNG z tabeli przestawnej w Javie. Ten przewodnik pokazuje,
  jak wyeksportować obraz danych z Excela, wyeksportować obraz tabeli przestawnej
  oraz wygenerować plik PNG z zakresu tabeli przestawnej.
og_title: Tworzenie PNG z Pivot w Javie – Kompletny poradnik eksportu
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Create PNG from pivot quickly with Java. Learn how to export Excel
    data image, export pivot table image, and save the range as a PNG file.
  headline: Create PNG from Pivot in Java – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create PNG from pivot quickly with Java. Learn how to export Excel
    data image, export pivot table image, and save the range as a PNG file.
  name: Create PNG from Pivot in Java – Full Step‑by‑Step Guide
  steps:
  - name: '**File exists** – `new File(outputPath).exists()` should return `true`.'
    text: '**File exists** – `new File(outputPath).exists()` should return `true`.'
  - name: '**Image dimensions** – Open the PNG; the width/height should match the
      range’s visual size.'
    text: '**Image dimensions** – Open the PNG; the width/height should match the
      range’s visual size.'
  - name: '**Data fidelity** – Compare a screenshot of the Excel sheet with the PNG;
      they should be identical pixel‑for‑pixel.'
    text: '**Data fidelity** – Compare a screenshot of the Excel sheet with the PNG;
      they should be identical pixel‑for‑pixel.'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Tworzenie PNG z Pivot w Javie – Kompletny przewodnik krok po kroku
url: /pl/java/excel-pivot-tables/create-png-from-pivot-in-java-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz PNG z tabeli przestawnej w Javie – Pełny przewodnik krok po kroku

Zastanawiałeś się kiedyś, jak **create PNG from pivot** bez ręcznego otwierania Excela? Może musisz osadzić wykres przestawny w raporcie lub budujesz pulpit nawigacyjny, który pobiera dane na żywo z pliku .xlsx. Dobra wiadomość jest taka, że nie musisz walczyć z obiektami COM ani z przechwytywaniem ekranu — Java może to zrobić czysto.

W tym samouczku przejdziemy przez kompletną rozwiązanie, które **exports an Excel range image**, konkretnie tabelę przestawną, do pliku PNG. Zobaczysz dokładnie, jak **export excel data image**, dlaczego `ImageOrPrintOptions` ma znaczenie i na co zwrócić uwagę przy **export pivot table file**. Po zakończeniu będziesz mieć gotowy do uruchomienia program w Javie, który zapisuje `pivot.png` obok Twojego skoroszytu.

## Wymagania wstępne

- Java 17 (lub dowolny nowszy JDK) – kod używa standardowych funkcji języka, nie wymaga lambd.
- Biblioteka Aspose.Cells for Java (bezpłatna wersja próbna lub płatna licencja). Dodaj zależność Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version>
</dependency>
```

- Plik Excel (`pivots.xlsx`) zawierający przynajmniej jedną tabelę przestawną.
- Podstawowa znajomość metod `main` w Javie; nie są potrzebne dodatkowe frameworki.

> **Wskazówka:** Jeśli używasz Gradle, zamień fragment XML na `implementation "com.aspose:aspose-cells:24.9"`.

## Krok 1: Załaduj skoroszyt zawierający tabelę przestawną

Pierwszą rzeczą, którą robimy, jest otwarcie skoroszytu. Aspose.Cells ukrywa niskopoziomową obsługę plików, więc pojedyncza linia dostarcza w pełni funkcjonalny obiekt `Workbook`.

```java
import com.aspose.cells.*;

public class ExportPivotToPng {
    public static void main(String[] args) throws Exception {
        // Adjust the path to point at your actual file location
        String workbookPath = "YOUR_DIRECTORY/pivots.xlsx";
        Workbook workbook = new Workbook(workbookPath);
```

> **Dlaczego to ważne:** Załadowanie skoroszytu weryfikuje format pliku i przygotowuje wewnętrzny model, co jest niezbędne przed zapytaniem o jakiekolwiek tabele przestawne.

## Krok 2: Uzyskaj dostęp do pierwszego arkusza

Większość arkuszy kalkulacyjnych przechowuje tabele przestawne na pierwszym arkuszu, ale w razie potrzeby możesz zmienić indeks. Tutaj po prostu pobieramy pierwszy arkusz.

```java
        // Grab the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

> **Przypadek brzegowy:** Jeśli Twój skoroszyt zawiera ukryte arkusze, Aspose nadal je zwraca; przed kontynuacją możesz potrzebować sprawdzić `sheet.isVisible()`.

## Krok 3: Pobierz zakres zajmowany przez pierwszą tabelę przestawną

Teraz dochodzi do sedna operacji: zlokalizowanie zakresu tabeli przestawnej. Kolekcja `getPivotTables()` pozwala wybrać potrzebną tabelę przestawną, a `getRange()` zwraca obiekt `Range`, który reprezentuje dokładne komórki.

```java
        // Assume the workbook has at least one pivot table
        PivotTable pivot = sheet.getPivotTables().get(0);
        Range pivotRange = pivot.getRange();
```

> **Dlaczego ten krok jest kluczowy:** Obiekt `Range` zna wymiary, formatowanie i dane tabeli przestawnej. Gdy później wywołamy `toImage`, użyje tych metadanych do renderowania obrazu PNG o idealnej jakości pikselowej.

## Krok 4: Skonfiguruj opcje eksportu obrazu – format PNG

Aspose daje precyzyjną kontrolę nad wyjściowym obrazem: DPI, skalowanie, obramowania i oczywiście format pliku. Ponieważ chcemy PNG, ustawiamy `ImageFormat.PNG`. Możesz także dostosować `setTransparent(true)`, jeśli potrzebny jest kanał alfa.

```java
        // Set up export options for a high‑quality PNG
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setImageFormat(ImageFormat.PNG);
        // Optional: increase resolution for sharper output
        options.setResolution(300);
```

> **Częste pytanie:** *Czy mogę wyeksportować do JPEG lub BMP zamiast?* Tak — po prostu zamień `ImageFormat.PNG` na `ImageFormat.JPEG` lub `ImageFormat.BMP`.

## Krok 5: Wyeksportuj zakres tabeli przestawnej do pliku obrazu

Na koniec wywołujemy `toImage` na obiekcie `Range`. Metoda przyjmuje ścieżkę docelową oraz opcje, które właśnie skonfigurowaliśmy. Operacja zapisuje plik na dysku w jednej linii.

```java
        // Define the output file path
        String outputPath = "YOUR_DIRECTORY/pivot.png";

        // Export the pivot range as a PNG image
        pivotRange.toImage(outputPath, options);

        System.out.println("Pivot table exported successfully to " + outputPath);
    }
}
```

> **Oczekiwany wynik:** Po uruchomieniu programu zobaczysz `pivot.png` w określonym katalogu. Otwórz go dowolnym przeglądarką obrazów i powinieneś zobaczyć dokładny układ oryginalnej tabeli przestawnej z Excela, w tym nagłówki kolumn, wiersze sum częściowych i wszystkie zastosowane style.

## Weryfikacja wyniku – szybka lista kontrolna

1. **Plik istnieje** – `new File(outputPath).exists()` powinno zwrócić `true`.
2. **Wymiary obrazu** – Otwórz PNG; szerokość/wysokość powinny odpowiadać wizualnemu rozmiarowi zakresu.
3. **Wierność danych** – Porównaj zrzut ekranu arkusza Excel z PNG; powinny być identyczne piksel po pikselu.

Jeśli którykolwiek z tych testów nie powiedzie się, sprawdź ponownie, czy ścieżka do skoroszytu jest poprawna oraz czy tabela przestawna nie jest ukryta lub odfiltrowana.

## Eksport obrazu zakresu Excel vs. eksport obrazu tabeli przestawnej

Możesz się zastanawiać, czy istnieje różnica między **export excel range image** a **export pivot table image**. W praktyce:

| Cel | Metoda | Typowe zastosowanie |
|------|--------|----------------------|
| Eksport dowolnego zakresu (np. A1:D20) | `sheet.getCells().createRange("A1:D20").toImage(...)` | Uchwycenie statycznej tabeli lub regionu wykresu |
| Eksport konkretnej tabeli przestawnej | `pivot.getRange().toImage(...)` | Zachowanie dynamicznego układu, sum częściowych i filtrów |

Oba podejścia używają tego samego API `toImage`; kluczem jest wybranie odpowiedniego obiektu `Range`. Kiedy **export pivot table file** zapisujesz zasadniczo wizualną reprezentację, a nie same dane.

## Obsługa wielu tabel przestawnych

Jeśli Twój skoroszyt zawiera kilka tabel przestawnych, po prostu przeiteruj kolekcję:

```java
        for (int i = 0; i < sheet.getPivotTables().getCount(); i++) {
            PivotTable pt = sheet.getPivotTables().get(i);
            String out = "YOUR_DIRECTORY/pivot_" + i + ".png";
            pt.getRange().toImage(out, options);
            System.out.println("Exported pivot #" + i + " to " + out);
        }
```

> **Dlaczego pętla?** Zautomatyzowane potoki raportowania często muszą opublikować każdą tabelę przestawną w skoroszycie. Pętla sprawia, że rozwiązanie jest skalowalne bez dodatkowego kodu.

## Typowe pułapki i jak ich unikać

- **Brak licencji** – Bez ważnej licencji Aspose.Cells biblioteka doda znak wodny do PNG. Zarejestruj licencję wcześnie: `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`.
- **Duże tabele przestawne powodują obciążenie pamięci** – Jeśli tabela przestawna obejmuje tysiące wierszy, rozważ zwiększenie pamięci heap JVM (`-Xmx2g`) lub eksport w sekcjach.
- **Nieprawidłowy format obrazu** – Przekazanie `ImageFormat.JPEG` przy oczekiwaniu przezroczystości spowoduje jednolite tło. Trzymaj się PNG, gdy potrzebny jest kanał alfa.

## Bonus: Eksport do tablicy bajtów dla API webowych

Czasami nie chcesz mieć pliku na dysku; potrzebujesz bajtów obrazu do wysłania przez HTTP. Zamień wywołanie oparte na pliku na `MemoryStream` (Aspose `ByteArrayOutputStream`):

```java
        java.io.ByteArrayOutputStream stream = new java.io.ByteArrayOutputStream();
        pivotRange.toImage(stream, options);
        byte[] pngBytes = stream.toByteArray();
        // Now you can return pngBytes from a REST endpoint
```

> **Scenariusz rzeczywisty:** Kontroler Spring Boot może zwrócić `ResponseEntity<byte[]>` z `Content-Type: image/png`, umożliwiając przeglądarkom wyświetlenie tabeli przestawnej w locie.

## Zakończenie

Teraz dokładnie wiesz, jak **create PNG from pivot** przy użyciu Javy i Aspose.Cells. Poradnik obejmował wszystko od ładowania skoroszytu, lokalizacji zakresu tabeli przestawnej, konfiguracji opcji eksportu PNG, po zapisanie pliku obrazu. Zbadaliśmy również powiązane zadania, takie jak **export excel data image**, **export pivot table image**, a nawet **export excel range image** dla sekcji nie‑przestawnych.

Kolejne kroki? Spróbuj dodać własne style do PNG (np. ustawić kolor tła) lub zintegrować procedurę eksportu w większym zadaniu wsadowym, które przetwarza dziesiątki skoroszytów nocą. Możesz także eksperymentować z innymi formatami wyjściowymi — PDF, SVG lub nawet wielostronicowym TIFF — zamieniając enum `ImageFormat`.

Masz pytania dotyczące przypadków brzegowych, licencjonowania lub optymalizacji wydajności? Dodaj komentarz poniżej i powodzenia w kodowaniu!

## Co warto nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Export Excel Workbook as Image Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Customize Pivot Table Globalization & PDF Export in Java with Aspose.Cells](/cells/english/java/data-analysis/customize-pivot-table-globalization-pdf-export-java/)
- [How to Manage Excel Pivot Table Compatibility with Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}