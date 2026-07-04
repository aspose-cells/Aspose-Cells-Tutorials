---
category: general
date: 2026-07-03
description: Eksportuj obraz tabeli przestawnej Excel przy użyciu Javy. Dowiedz się,
  jak krok po kroku ustawić format obrazu PNG w Aspose.Cells.
draft: false
keywords:
- excel pivot table image
- set image format png
- Aspose.Cells export
- Java Excel automation
- pivot table to image
language: pl
og_description: Eksport obrazu tabeli przestawnej Excel w Javie wyjaśniony. Skorzystaj
  z tego samouczka, aby szybko i niezawodnie ustawić format obrazu PNG.
og_title: obraz tabeli przestawnej Excel – przewodnik Java po eksporcie do PNG
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Export an excel pivot table image using Java. Learn how to set image
    format png with Aspose.Cells step‑by‑step.
  headline: 'excel pivot table image: Export to PNG with Java'
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel
- ImageExport
title: 'obraz tabeli przestawnej Excel: eksport do PNG w Javie'
url: /pl/java/excel-pivot-tables/excel-pivot-table-image-export-to-png-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excel pivot table image – Eksport tabeli przestawnej jako PNG w Javie

Czy kiedykolwiek potrzebowałeś przekształcić **excel pivot table image** w gotowy do udostępnienia PNG, ale nie wiedziałeś od czego zacząć? Nie jesteś sam. W wielu pipeline'ach raportowych tabela przestawna jest gwiazdą, jednak reszta zespołu chce tylko statyczny obraz. Dobra wiadomość? Kilka linijek Java i Aspose.Cells pozwala **set image format png** i uzyskać dokładnie to, czego potrzebujesz.

W tym przewodniku przeprowadzimy Cię przez cały proces: załadowanie skoroszytu, pobranie pierwszej tabeli przestawnej, skonfigurowanie opcji eksportu i w końcu zapisanie wyraźnego pliku PNG na dysku. Po zakończeniu będziesz mieć wielokrotnego użytku fragment kodu, który możesz wstawić do dowolnego projektu Java.

## Czego się nauczysz

- Jak załadować skoroszyt Excel z systemu plików.
- Jak znaleźć konkretną tabelę przestawną na arkuszu.
- Dokładne kroki, aby **set image format png** dla eksportowanego obrazu.
- Typowe pułapki (wiele tabel przestawnych, duże zestawy danych) i jak ich uniknąć.
- Gotowa do uruchomienia klasa Java, którą możesz skopiować i wkleić.

### Wymagania wstępne

- Zainstalowany Java 8 lub nowszy.
- Biblioteka Aspose.Cells for Java (najnowsza wersja z dnia 2026‑07‑03).
- Plik Excel (`input.xlsx`) zawierający przynajmniej jedną tabelę przestawną.
- Podstawowa znajomość Maven lub Gradle do zarządzania zależnościami.

---

## Krok 1: Dodaj Aspose.Cells do swojego projektu

Najpierw upewnij się, że plik JAR Aspose.Cells znajduje się na classpathie. Jeśli używasz Maven, wstaw to do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest at time of writing -->
</dependency>
```

Dla Gradle jest to równie proste:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **Pro tip:** Aspose oferuje darmowy 30‑dniowy klucz ewaluacyjny. Zarejestruj się na ich stronie, a następnie dodaj `License.setLicense("Aspose.Cells.lic");` na początku programu, aby odblokować pełne funkcje.

## Krok 2: Załaduj skoroszyt i uzyskaj dostęp do tabeli przestawnej

Teraz otworzymy plik Excel i pobierzemy pierwszą tabelę przestawną. Poniższy kod robi dokładnie to i jest celowo defensywny — jeśli skoroszyt nie ma arkuszy lub arkusz nie zawiera tabeli przestawnej, wyrzucimy wyraźny wyjątek.

```java
import com.aspose.cells.*;

import java.io.File;

public class PivotTableToPng {

    public static void main(String[] args) {
        // Adjust these paths to match your environment
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/pivot.png";

        try {
            // Load the workbook from disk
            Workbook wb = new Workbook(inputPath);

            // Ensure there is at least one worksheet
            if (wb.getWorksheets().getCount() == 0) {
                throw new IllegalStateException("The workbook contains no worksheets.");
            }

            // Grab the first worksheet (index 0)
            Worksheet ws = wb.getWorksheets().get(0);

            // Verify that the worksheet actually has a pivot table
            if (ws.getPivotTables().getCount() == 0) {
                throw new IllegalStateException("No pivot tables found on the first worksheet.");
            }

            // Retrieve the first pivot table
            PivotTable pt = ws.getPivotTables().get(0);

            // -------------------------------------------------
            // Step 3: Configure image export options (PNG)
            // -------------------------------------------------
            ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
            // This is where we **set image format png**
            imgOpt.setImageFormat(ImageFormat.PNG);
            // Optional: increase the DPI for sharper output (default is 96)
            imgOpt.setResolution(300);

            // -------------------------------------------------
            // Step 4: Export the pivot table as an image file
            // -------------------------------------------------
            pt.toImage(outputPath, imgOpt);

            System.out.println("Successfully exported the excel pivot table image to: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### Dlaczego te kroki są ważne

- **Loading the workbook** daje nam dostęp do podstawowych struktur danych; Aspose.Cells ukrywa niskopoziomowe parsowanie OpenXML.
- **Accessing the worksheet** jest konieczne, ponieważ tabele przestawne są powiązane z konkretnym arkuszem. Jeśli masz wiele arkuszy, możesz przeiterować `wb.getWorksheets()` i wybrać ten, który zawiera pożądaną tabelę przestawną.
- **Retrieving the pivot table** jest sercem operacji. `ws.getPivotTables().get(0)` pobiera pierwszą, ale możesz też wyszukać po nazwie używając `ws.getPivotTables().get("MyPivot")`.
- **Setting image format png** (drugie słowo kluczowe) instruuje Aspose.Cells, aby renderował wynik jako bezstratny PNG. Ten format zachowuje ostre linie i tekst, idealny do raportów.
- **Exporting with `toImage`** zapisuje plik w jednym wywołaniu, automatycznie obsługując paginację i skalowanie.

## Krok 3: Zweryfikuj wynik

Po uruchomieniu programu przejdź do `YOUR_DIRECTORY` i powinieneś zobaczyć `pivot.png`. Otwórz go w dowolnym przeglądarce obrazów — zauważ wyraźne linie siatki i dokładny układ, jaki widzisz w Excelu. Jeśli obraz jest rozmyty, zwiększ DPI w `imgOpt.setResolution()`; 300‑600 działa dobrze dla zasobów drukowanych.

![excel pivot table image exported as PNG](excel-pivot-table-image.png "excel pivot table image exported as PNG")

*Tekst alternatywny obrazu:* **excel pivot table image exported as PNG**

## Obsługa wielu tabel przestawnych

Co zrobić, jeśli arkusz zawiera więcej niż jedną tabelę przestawną? Powyższy fragment pobiera pierwszą, ale możesz iterować:

```java
for (int i = 0; i < ws.getPivotTables().getCount(); i++) {
    PivotTable pt = ws.getPivotTables().get(i);
    String outFile = "YOUR_DIRECTORY/pivot_" + i + ".png";
    pt.toImage(outFile, imgOpt);
}
```

Ta pętla wygeneruje `pivot_0.png`, `pivot_1.png` itd., każdy reprezentujący inną tabelę przestawną. Pamiętaj, aby **set image format png** raz przed pętlą; tę samą instancję `ImageOrPrintOptions` można ponownie używać.

## Przypadki brzegowe i wskazówki

| Sytuacja | Na co zwrócić uwagę | Sugerowane rozwiązanie |
|-----------|-------------------|---------------|
| **Duża tabela przestawna (wiele wierszy/kolumn)** | PNG może stać się bardzo duży, powodując obciążenie pamięci. | Użyj `imgOpt.setOnePagePerSheet(false)`, aby podzielić na wiele stron, lub zmniejsz DPI. |
| **Ukryte wiersze/kolumny** | Aspose respektuje widoczność; ukryte dane nie będą wyświetlane. | Odkryj programowo za pomocą `ws.showRows(start, count, true)`. |
| **Niestandardowe style (czcionki, kolory)** | Niektóre firmowe czcionki mogą nie być renderowane, jeśli nie są zainstalowane na serwerze. | Osadź czcionkę w JVM lub użyj czcionek systemowych poprzez `imgOpt.setFontEmbeddingMode(FontEmbeddingMode.EMBED_ALL)`. |
| **Inny format wyjściowy potrzebny później** | Możesz potrzebować JPEG lub BMP. | Zmień `imgOpt.setImageFormat(ImageFormat.JPEG)` — ten sam kod działa, tylko inna wartość wyliczenia. |

## Pełny działający przykład (Kopiuj‑Wklej)

Poniżej znajduje się cała klasa, gotowa do kompilacji. Wklej ją do `PivotTableToPng.java`, dostosuj ścieżki i uruchom `javac PivotTableToPng.java && java PivotTableToPng`.

```java
import com.aspose.cells.*;

public class PivotTableToPng {

    public static void main(String[] args) {
        // ----- Configuration -----
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/pivot.png";

        try {
            // Load workbook
            Workbook wb = new Workbook(inputPath);

            // Guard clauses
            if (wb.getWorksheets().getCount() == 0) {
                throw new IllegalStateException("Workbook has no worksheets.");
            }

            Worksheet ws = wb.getWorksheets().get(0);
            if (ws.getPivotTables().getCount() == 0) {
                throw new IllegalStateException("No pivot tables on the first worksheet.");
            }

            // Retrieve the first pivot table
            PivotTable pt = ws.getPivotTables().get(0);

            // ----- Set image format png -----
            ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
            imgOpt.setImageFormat(ImageFormat.PNG);   // <-- key line
            imgOpt.setResolution(300);                // optional, for sharper output

            // Export to PNG
            pt.toImage(outputPath, imgOpt);

            System.out.println("excel pivot table image exported successfully: " + outputPath);
        } catch (Exception ex) {
            System.err.println("Error during export:");
            ex.printStackTrace();
        }
    }
}
```

Uruchom ją, a otrzymasz **excel pivot table image** zapisaną jako plik PNG — dokładnie to, co obiecywał tutorial.

---

## Zakończenie

Właśnie omówiliśmy wszystko, co potrzebne, aby **export an excel pivot table image** przy użyciu Java, i pokazaliśmy dokładnie, jak **set image format png** z Aspose.Cells. Od ładowania skoroszytu po obsługę przypadków brzegowych, rozwiązanie jest zwarte, niezawodne i gotowe do produkcji.

Co dalej? Spróbuj wyeksportować wiele tabel przestawnych w partii, eksperymentuj z różnymi ustawieniami DPI dla zasobów gotowych do druku lub zmień format na JPEG dla obrazów zoptymalizowanych pod sieć. Możesz także zbadać osadzanie PNG w raporcie PDF — Aspose.PDF robi to z łatwością.

Masz własny twist w workflow lub napotykasz problem? zostaw komentarz, a wspólnie znajdziemy rozwiązanie. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Eksport skoroszytu Excel jako obrazu przy użyciu Aspose.Cells dla Java: Przewodnik krok po kroku](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Jak zaktualizować źródło tabeli przestawnej Excel przy użyciu Aspose.Cells dla Java: Kompletny przewodnik](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Jak stworzyć wykres Excel z linią trendu i wyeksportować go jako obraz przy użyciu Aspose.Cells dla Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}