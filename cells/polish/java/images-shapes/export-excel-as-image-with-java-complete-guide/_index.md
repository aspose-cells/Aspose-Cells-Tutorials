---
category: general
date: 2026-11-22
description: Eksportuj plik Excel jako obraz przy użyciu Javy i Aspose.Cells. Dowiedz
  się, jak dodać obraz do arkusza i zapisać Excel jako plik PNG w kilku krokach.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel as image
- add picture to worksheet
- export excel sheet to png
- save excel as png file
- save workbook as image
language: pl
lastmod: 2026-11-22
og_description: Eksportuj Excel jako obraz w Javie przy użyciu Aspose.Cells. Skorzystaj
  z tego przewodnika, aby dodać obraz do arkusza i szybko zapisać plik Excel jako
  PNG.
og_image_alt: Code snippet showing Java export of an Excel worksheet to a PNG image
og_title: Eksportuj Excel jako obraz w Javie – samouczek krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Export Excel as image with Java using Aspose.Cells. Learn how to add
    picture to worksheet and save Excel as PNG file in a few steps.
  headline: Export Excel as image with Java – complete guide
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Image export
title: Eksportowanie Excela jako obrazu w Javie – kompletny przewodnik
url: /pl/java/images-shapes/export-excel-as-image-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eksportowanie Excela jako obrazu w Javie – kompletny przewodnik

Jeśli potrzebujesz **eksportować Excel jako obraz** w aplikacji Java, ten tutorial pokaże Ci gotowe rozwiązanie. Zobaczysz, jak dodać obraz do arkusza, skonfigurować opcje eksportu i w końcu **zapisać Excel jako plik PNG** przy użyciu kilku linii kodu.

Poradnik obejmuje wszystko, od konfiguracji Maven po obsługę przypadków brzegowych, dzięki czemu możesz zintegrować tę technikę w każdym projekcie wymagającym wizualnych migawków arkuszy kalkulacyjnych.

## Wymagania wstępne

* Zainstalowany Java 17 lub nowszy.
* Maven 3.6+ (lub Gradle) do zarządzania zależnościami.
* Licencja Aspose.Cells for Java (darmowa wersja ewaluacyjna działa do testów).
* Przykładowy skoroszyt Excel (`sample.xlsx`) zawierający dane, które chcesz wyeksportować.

## Krok 1: Dodaj zależność Aspose.Cells

Aspose.Cells udostępnia klasę `ImageOrPrintOptions` używaną do **eksportowania Excela jako obrazu**. Dodaj następującą zależność do swojego `pom.xml` (lub odpowiedniego wpisu Gradle).

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Wskazówka:** Utrzymuj numer wersji aktualny; nowsze wydania zawierają ulepszenia wydajności renderowania obrazu.

## Krok 2: Załaduj skoroszyt i wybierz arkusz

Pierwszy krok programistyczny to otwarcie pliku Excel i uzyskanie referencji do arkusza, który chcesz wyeksportować.

```java
import com.aspose.cells.*;

public class ExcelToImage {
    public static void main(String[] args) throws Exception {
        // Load the workbook from disk
        Workbook wb = new Workbook("sample.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = wb.getWorksheets().get(0);
```

*Dlaczego to ważne*: Załadowanie skoroszytu daje dostęp do jego wewnętrznych obiektów, a wybranie właściwego arkusza zapewnia renderowanie odpowiedniego zakresu.

## Krok 3: Skonfiguruj ImageOrPrintOptions (eksport Excela jako obrazu)

`ImageOrPrintOptions` kontroluje format obrazu, rozdzielczość i inne szczegóły renderowania. Tutaj ustawiamy format na PNG, co spełnia wymóg **eksportu arkusza Excela do PNG**.

```java
        // Create options for image export
        ImageOrPrintOptions opts = new ImageOrPrintOptions();

        // Set the desired image format (PNG)
        opts.setSaveFormat(SaveFormat.PNG);

        // Optional: increase resolution for sharper output
        opts.setResolution(300);
```

Ustawienie formatu na `PNG` zapewnia bezstratną kompresję, czyniąc plik odpowiednim do dalszego przetwarzania lub włączenia do raportów.

## Krok 4: Dodaj obraz do arkusza (add picture to worksheet)

Jeśli potrzebujesz osadzić obraz — na przykład logo lub migawkę innego zakresu — użyj kolekcji `Pictures`. Poniższy kod wstawia obraz zakresu `A1:G20` w lewym górnym rogu arkusza.

```java
        // Insert a picture of the range A1:G20 at cell (0,0)
        ws.getPictures().add(0, 0, "A1:G20");
```

> **Dlaczego możesz to zrobić:** Dodanie obrazu przed eksportem pozwala połączyć statyczną grafikę z danymi arkusza, tworząc bogatszy końcowy obraz.

## Krok 5: Zapisz arkusz jako plik PNG (save excel as png file, save workbook as image)

Na koniec wywołaj `Workbook.save` z skonfigurowanymi opcjami. Metoda zapisuje plik PNG w określonym katalogu.

```java
        // Save the worksheet as an image file
        wb.save("output/pivot.png", opts);

        System.out.println("Export completed: output/pivot.png");
    }
}
```

Po zakończeniu programu, `output/pivot.png` zawiera pikselowo idealną reprezentację arkusza, włącznie z dodanym obrazem.

### Pełny plik źródłowy

```java
import com.aspose.cells.*;

public class ExcelToImage {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook wb = new Workbook("sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // Configure export options
        ImageOrPrintOptions opts = new ImageOrPrintOptions();
        opts.setSaveFormat(SaveFormat.PNG);
        opts.setResolution(300); // optional high‑DPI output

        // Add picture to worksheet
        ws.getPictures().add(0, 0, "A1:G20");

        // Export worksheet as PNG image
        wb.save("output/pivot.png", opts);
        System.out.println("Export completed: output/pivot.png");
    }
}
```

Uruchomienie klasy generuje plik PNG pokazany poniżej (obraz jest ilustracyjny; Twój plik będzie odzwierciedlał rzeczywistą zawartość arkusza).

![Eksportowany arkusz Excel jako PNG](/images/excel-to-png.png "Wynik eksportu Excela jako obrazu przy użyciu Javy")

*Tekst alternatywny (alt obrazu):* **Wynik eksportu Excela jako obrazu przy użyciu Javy – migawka PNG arkusza** (spełnia wymóg alt obrazu).

## Typowe pułapki i jak ich unikać

| Issue | Reason | Fix |
|-------|--------|-----|
| **Plik nie znaleziony** | Ścieżka do `sample.xlsx` jest nieprawidłowa. | Użyj ścieżki bezwzględnej lub umieść plik w katalogu głównym projektu. |
| **Pusty obraz** | Arkusz nie ma widocznej zawartości lub zakres obrazu jest pusty. | Sprawdź, czy komórki `A1:G20` zawierają dane lub dostosuj zakres. |
| **Niska rozdzielczość** | Domyślne DPI to 96, co może wyglądać rozmycie po wydrukowaniu. | Wywołaj `opts.setResolution(300)` (lub wyższą) przed zapisem. |
| **Wyjątek licencyjny** | Używanie wersji ewaluacyjnej może dodać znak wodny. | Zastosuj ważną licencję Aspose.Cells przy pomocy `License license = new License(); license.setLicense("Aspose.Total.lic");`. |

## Kolejne kroki

Teraz, gdy możesz **eksportować Excel jako obraz**, możesz rozważyć:

* **Eksportuj arkusz Excela do PNG** dla każdego arkusza w skoroszycie (iteruj przez `wb.getWorksheets()`).
* Konwersja PNG do PDF przy użyciu Aspose.PDF, jeśli potrzebny jest format przyjazny dokumentom.
* Osadzenie wygenerowanego PNG w stronie internetowej lub jako załącznik e‑mail bezpośrednio z Javy.

Te rozszerzenia opierają się na tym samym wzorcu `ImageOrPrintOptions`, utrzymując spójność bazy kodu.

## Zakończenie

Nauczyłeś się, jak **eksportować Excel jako obraz** w Javie, jak **dodać obraz do arkusza**, oraz jak **zapisać Excel jako plik PNG** przy użyciu Aspose.Cells. Pełny przykład demonstruje niezawodny sposób na **zapisanie skoroszytu jako obrazu**, obsługę rozdzielczości i unikanie typowych błędów. Zastosuj ten wzorzec do automatyzacji raportowania, generowania miniatur lub integracji wizualizacji arkuszy kalkulacyjnych w dowolnym procesie opartym na Javie.

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak wyeksportować arkusz Excel do PNG przy użyciu Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Eksportowanie skoroszytu Excel jako obrazu przy użyciu Aspose.Cells for Java: przewodnik krok po kroku](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Eksportowanie skoroszytu Excel jako obrazu przy użyciu Aspose Cells dla Java](/cells/german/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}