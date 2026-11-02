---
category: general
date: 2026-06-27
description: Eksportuj tabelę przestawną jako obraz tabeli przestawnej Excel w Javie.
  Dowiedz się, jak ustawić format PNG, skonfigurować opcje i zapisać plik w kilku
  prostych krokach.
draft: false
keywords:
- export pivot table
- excel pivot image
- set png format
language: pl
og_description: Eksportuj tabelę przestawną jako obraz tabeli przestawnej w Excelu
  przy użyciu Javy. Ten przewodnik pokazuje, jak ustawić format PNG i zapisać obraz
  z pewnością.
og_title: Eksport tabeli przestawnej do PNG w Javie – Przewodnik krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Export pivot table as an Excel pivot image in Java. Learn how to set
    PNG format, configure options, and save the file in just a few steps.
  headline: Export pivot table to PNG in Java – Complete Programming Guide
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Eksport tabeli przestawnej do PNG w Javie – Kompletny przewodnik programistyczny
url: /pl/java/excel-pivot-tables/export-pivot-table-to-png-in-java-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eksport tabeli przestawnej do PNG w Javie – Kompletny przewodnik programistyczny

Kiedykolwiek potrzebowałeś **export pivot table** z skoroszytu Excel, ale nie wiedziałeś, jak uzyskać czysty plik obrazu? Nie jesteś jedyny — wielu programistów napotyka ten problem przy tworzeniu pulpitów raportowych. Dobra wiadomość jest taka, że kilkoma liniami kodu Java możesz zamienić dowolną tabelę przestawną w wyraźny **Excel pivot image** zapisany jako PNG.  

W tym samouczku przeprowadzimy Cię przez cały proces: odczytanie skoroszytu, odnalezienie pierwszej tabeli przestawnej, skonfigurowanie eksportu, aby **set PNG format**, oraz zapisanie obrazu na dysku. Po zakończeniu będziesz mieć wielokrotnego użytku fragment kodu, który możesz wkleić do dowolnego projektu.

## Czego się nauczysz

- Jak załadować plik Excel przy użyciu Aspose.Cells (lub Apache POI, jeśli wolisz).
- Dokładne wywołania API potrzebne do **export pivot table** jako PNG.
- Dlaczego ustawienie formatu obrazu ma znaczenie i jak poprawnie **set PNG format**.
- Typowe pułapki — takie jak obsługa wielu tabel przestawnych lub brakujące arkusze — oraz jak ich uniknąć.
- Pełny, gotowy do uruchomienia przykład Java, który możesz skopiować i wkleić.

> **Prerequisites**  
> • Java 17 lub nowszy (kod działa również w starszych wersjach, ale zalecany jest 17).  
> • Biblioteka Aspose.Cells for Java (darmowa wersja próbna działa bez problemu).  
> • Podstawowa znajomość plików Excel i Java I/O.

---

## Krok 1: Dodaj zależność Aspose.Cells

Jeśli używasz Maven, wstaw następującą zależność do swojego `pom.xml`. W przeciwnym razie pobierz plik JAR ze strony Aspose i dodaj go do classpath.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest as of June 2026 -->
</dependency>
```

*Pro tip:* Utrzymuj wersje bibliotek zgodnie z oficjalnymi notatkami wydania, aby uniknąć nieoczekiwanych błędów.

## Krok 2: Załaduj skoroszyt i znajdź tabelę przestawną

Najpierw otwieramy plik Excel, następnie pobieramy pierwszą tabelę przestawną z pierwszego arkusza. Jeśli skoroszyt nie zawiera tabel przestawnych, zakończymy działanie w sposób elegancki.

```java
import com.aspose.cells.*;

public class PivotTableExporter {

    public static void main(String[] args) {
        try {
            // Load the workbook (replace with your actual path)
            Workbook workbook = new Workbook("C:/data/report.xlsx");

            // Access the first worksheet – you can also loop through all sheets
            Worksheet ws = workbook.getWorksheets().get(0);

            // Verify that the sheet actually contains pivot tables
            if (ws.getPivotTables().getCount() == 0) {
                System.out.println("No pivot tables found on the first sheet.");
                return;
            }

            // Retrieve the first pivot table (this is the target for export)
            PivotTable pivotTable = ws.getPivotTables().get(0);
```

> **Dlaczego ten krok ma znaczenie** – Obiekt `PivotTable` jest punktem wejścia dla każdego eksportu obrazu. Próba wywołania `toImage` na nieistniejącej tabeli przestawnej spowoduje `NullPointerException`, dlatego najpierw sprawdzamy liczbę.

## Krok 3: Skonfiguruj opcje eksportu obrazu (Set PNG Format)

Teraz tworzymy instancję `ImageOrPrintOptions` i wyraźnie **set PNG format**. PNG jest bezstratny, co zachowuje ostrość linii siatki i czcionek.

```java
            // Step 3: Configure image export options – we want PNG
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
            imgOptions.setImageFormat(ImageFormat.PNG);   // <-- set png format
            imgOptions.setOnePagePerSheet(true);          // optional: force single‑page output
            imgOptions.setTransparent(true);              // optional: keep background transparent
```

*Uwaga:* Jeśli potrzebujesz JPEG, po prostu zamień `ImageFormat.PNG` na `ImageFormat.JPEG`. Ten sam obiekt opcji działa dla obu formatów.

## Krok 4: Eksportuj tabelę przestawną jako plik obrazu

Gdy opcje są gotowe, wywołujemy `toImage`. Metoda zapisuje plik bezpośrednio, więc nie są potrzebne dodatkowe strumienie.

```java
            // Step 4: Export the pivot table as an image file
            String outputPath = "C:/exports/pivot.png";
            pivotTable.toImage(outputPath, imgOptions);

            System.out.println("Pivot table exported successfully to: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

Uruchomienie programu tworzy plik o nazwie `pivot.png`, który wygląda dokładnie tak jak tabela przestawna w Excelu. Otwórz go w dowolnym przeglądarce obrazów, aby to zweryfikować.

### Oczekiwany wynik

```
Pivot table exported successfully to: C:/exports/pivot.png
```

Powstały obraz będzie odpowiadał układowi na ekranie, w tym szerokościom kolumn, wysokościom wierszy oraz wszelkiemu zastosowanemu formatowaniu warunkowemu.

## Obsługa wielu tabel przestawnych (Zaawansowane)

Co zrobić, jeśli Twój arkusz zawiera kilka tabel przestawnych i chcesz wybrać tylko jedną konkretną? Możesz przeiterować `ws.getPivotTables()` i wybrać według nazwy:

```java
PivotTable target = null;
for (int i = 0; i < ws.getPivotTables().getCount(); i++) {
    PivotTable pt = ws.getPivotTables().get(i);
    if ("SalesByRegion".equals(pt.getName())) {
        target = pt;
        break;
    }
}
if (target == null) {
    System.out.println("Desired pivot table not found.");
    return;
}
target.toImage("C:/exports/sales_by_region.png", imgOptions);
```

*Dlaczego jest to przydatne*: W rzeczywistych raportach często masz podsumowującą tabelę przestawną oraz szczegółową. Wybór według nazwy zapobiega przypadkowym nadpisaniom.

## Typowe problemy i jak ich uniknąć

| Issue | Symptom | Fix |
|------|----------|-----|
| **Brak arkusza** | `IndexOutOfBoundsException` when accessing `ws` | Sprawdź, czy `workbook.getWorksheets().getCount() > 0` przed indeksowaniem. |
| **Brak tabel przestawnych** | Silent failure or empty image | Użyj sprawdzenia `ws.getPivotTables().getCount()` (zobacz Krok 2). |
| **Nieprawidłowy format obrazu** | Output looks blurry or has artifacts | Zawsze używaj `setImageFormat(ImageFormat.PNG)` dla bezstratnego wyjścia; unikaj JPEG w tabelach z dużą ilością tekstu. |
| **Ścieżka pliku nie do zapisu** | `IOException` at `toImage` | Upewnij się, że katalog istnieje (`new File(outputPath).getParentFile().mkdirs()`). |

## Pro Tip: Eksportuj do tablicy bajtów dla aplikacji webowych

Jeśli tworzysz usługę webową, która zwraca PNG bezpośrednio do przeglądarki, możesz zapisać do `ByteArrayOutputStream` zamiast pliku:

```java
ByteArrayOutputStream baos = new ByteArrayOutputStream();
pivotTable.toImage(baos, imgOptions);
byte[] pngBytes = baos.toByteArray();
// Send pngBytes as HTTP response with Content-Type: image/png
```

Eliminuje to potrzebę plików tymczasowych i przyspiesza odpowiedź.

---

## Pełny działający przykład (wszystkie kroki połączone)

Poniżej znajduje się kompletny program gotowy do skopiowania i wklejenia, zawierający wszystkie omówione najlepsze praktyki.

```java
import com.aspose.cells.*;
import java.io.*;

public class PivotTableExporter {

    public static void main(String[] args) {
        // 1️⃣ Load workbook
        Workbook workbook;
        try {
            workbook = new Workbook("C:/data/report.xlsx");
        } catch (Exception e) {
            System.err.println("Failed to load workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Get first worksheet and ensure a pivot exists
        if (workbook.getWorksheets().getCount() == 0) {
            System.out.println("Workbook contains no worksheets.");
            return;
        }
        Worksheet ws = workbook.getWorksheets().get(0);
        if (ws.getPivotTables().getCount() == 0) {
            System.out.println("No pivot tables on the first sheet.");
            return;
        }
        PivotTable pivotTable = ws.getPivotTables().get(0); // export pivot table

        // 3️⃣ Configure export options – set png format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.PNG); // <-- set png format
        imgOptions.setOnePagePerSheet(true);
        imgOptions.setTransparent(true);

        // 4️⃣ Prepare output directory
        String outDir = "C:/exports";
        new File(outDir).mkdirs(); // create if missing

        // 5️⃣ Export the image
        String outPath = outDir + "/pivot.png";
        try {
            pivotTable.toImage(outPath, imgOptions);
            System.out.println("Pivot table exported successfully to: " + outPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

Uruchomienie tej klasy wygeneruje `pivot.png` w katalogu `C:/exports`. Otwórz plik, a zobaczysz dokładną wizualną replikę oryginalnej tabeli przestawnej — idealną do osadzania w raportach, e‑mailach lub stronach internetowych.

![Wyeksportowana tabela przestawna zapisana jako PNG – przykład obrazu tabeli przestawnej Excel](https://example.com/images/pivot-export.png "przykład eksportu tabeli przestawnej")

*Image alt text:* **przykład eksportu tabeli przestawnej pokazujący PNG obrazu tabeli przestawnej Excel**

## Zakończenie

Właśnie pokazaliśmy, jak **export pivot table** dane z Excela do wysokiej jakości PNG przy użyciu Javy. Kluczowe kroki to załadowanie skoroszytu, odnalezienie tabeli przestawnej, skonfigurowanie `ImageOrPrintOptions` aby **set PNG format**, oraz ostateczne wywołanie `toImage`.  

Mając tę wiedzę, możesz teraz automatyzować generowanie raportów, osadzać migawki tabel przestawnych w pulpitach, lub udostępniać je bezpośrednio z API webowego. Następnie możesz zbadać opcje skalowania **excel pivot image**, dodać znaki wodne, lub nawet przekonwertować PNG do PDF dla raportów do druku.  

Masz pytania dotyczące obsługi większych skoroszytów lub integracji ze Spring Boot? zostaw komentarz poniżej i powodzenia w kodowaniu!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak zaktualizować źródło tabeli przestawnej Excel przy użyciu Aspose.Cells dla Java: Kompletny przewodnik](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Automatyzacja stylizacji i zapisywania tabeli przestawnej Excel przy użyciu Aspose.Cells dla Java: Kompletny przewodnik](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)
- [Manipulacja tabelą przestawną Excel przy użyciu Aspose.Cells Java: Kompletny przewodnik](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}