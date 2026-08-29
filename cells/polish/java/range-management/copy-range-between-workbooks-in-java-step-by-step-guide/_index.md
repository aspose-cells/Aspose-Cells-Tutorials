---
category: general
date: 2026-08-14
description: Kopiowanie zakresu między skoroszytami w Javie przy użyciu Aspose.Cells.
  Dowiedz się, jak skopiować skoroszyt z tabelą przestawną, wyeksportować obraz do
  PowerPointa oraz usunąć AutoFilter z tabeli Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: pl
lastmod: 2026-08-14
og_description: Kopiowanie zakresu między skoroszytami w Javie. Ten przewodnik pokazuje,
  jak skopiować skoroszyt z tabelą przestawną, wyeksportować obraz do PowerPointa
  oraz usunąć AutoFilter z tabeli Excel.
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: Kopiowanie zakresu między skoroszytami w Javie – kompletny samouczek Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Kopiowanie zakresu między skoroszytami w Javie – przewodnik krok po kroku
url: /pl/java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopiowanie zakresu między skoroszytami w Javie – przewodnik krok po kroku

Jeśli potrzebujesz **skopiować zakres między skoroszytami** w Javie, Aspose.Cells udostępnia przejrzyste API, które obsługuje złożone obiekty, takie jak tabele przestawne i obrazy. Ten tutorial pokazuje, jak **skopiować skoroszyt z tabelą przestawną**, **wyeksportować obraz do PowerPoint**, oraz **usunąć AutoFilter z tabeli Excel**, zachowując kod czytelny i łatwy w utrzymaniu.

Nauczysz się, jak:

* Załadować źródłowy skoroszyt i określić zakres źródłowy.  
* Utworzyć docelowy skoroszyt i skopiować zakres, tak aby tabela przestawna pozostała nienaruszona.  
* Wyeksportować pierwszy obraz na arkuszu jako edytowalny obiekt PowerPoint.  
* Usunąć AutoFilter z pierwszej tabeli Excel.  
* Załadować skoroszyt z `SmartMarkerOptions`, aby traktować tablice JSON jako pojedynczą wartość komórki.

Przykład wykorzystuje Aspose.Cells 23.10 dla Javy, ale koncepcje mają zastosowanie także do wcześniejszych wersji.

---

## Wymagania wstępne

| Wymaganie | Dlaczego jest ważne |
|-----------|---------------------|
| Java 17 lub nowsza | Wymagana przez najnowszy runtime Aspose.Cells. |
| Aspose.Cells for Java (artefakt Maven `com.aspose:aspose-cells`) | Dostarcza klasy `Workbook`, `Worksheet`, `Range` i powiązane, używane w kodzie. |
| Plik Excel źródłowy (`src.xlsx`) zawierający tabelę przestawną, obraz oraz tabelę z AutoFilter | Tutorial manipuluje tymi obiektami, aby zademonstrować każdą funkcję. |

Dodaj zależność Maven do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Kopiowanie zakresu między skoroszytami – ładowanie źródła i docelowego skoroszytu

Pierwszym krokiem jest otwarcie źródłowego skoroszytu, wybranie zakresu zawierającego dane do skopiowania oraz utworzenie pustego docelowego skoroszytu.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **Dlaczego to ważne:** Korzystając z `Range.copy`, Aspose.Cells kopiuje nie tylko surowe wartości komórek, ale także podlegający im cache tabeli przestawnej, utrzymując tabelę przestawną funkcjonalną w docelowym skoroszycie.

---

## Kopiowanie skoroszytu z tabelą przestawną podczas kopiowania zakresu

Teraz skopiuj zdefiniowany zakres ze źródłowego skoroszytu do docelowego. Tabela przestawna zostaje zachowana automatycznie, ponieważ zakres obejmuje cache tabeli przestawnej.

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **Rezultat:** Otwierając `destination.xlsx` zobaczysz taką samą strukturę tabeli przestawnej jak w `src.xlsx`. Nie jest potrzebny dodatkowy kod do odtworzenia cache tabeli przestawnej.

---

## Eksport obrazu do PowerPoint

Aspose.Cells może oznaczyć obraz do eksportu jako edytowalny obiekt PowerPoint. Poniższy kod wybiera pierwszy obraz na docelowym arkuszu i ustawia flagę eksportu.

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **Co widzisz:** Otwierając `destination.pptx` w PowerPoint, obraz jest wyświetlany jako natywny kształt, który możesz edytować, zmieniać rozmiar lub animować.

---

## Usuwanie AutoFilter z tabeli Excel

Jeśli źródłowy arkusz zawiera tabelę z AutoFilter, możesz chcieć usunąć go po skopiowaniu. Poniższy kod uzyskuje dostęp do pierwszej tabeli i usuwa jej filtr.

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **Efekt:** Tabela pozostaje w skoroszycie, ale strzałki filtrów znikają, dając czysty widok danych.

---

## Ładowanie skoroszytu z opcjami SmartMarker – traktowanie tablic JSON jako pojedynczej komórki

Podczas generowania raportu z JSON, Aspose.Cells może traktować całą tablicę jako jedną wartość komórki. Jest to przydatne przy wstawianiu ciągów JSON do szablonu bez rozwijania ich na wiele komórek.

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **Dlaczego możesz tego użyć:** Jeśli ładunek JSON zawiera tablicę, którą chcesz wyświetlić jako ciąg JSON w jednej komórce, `setArrayAsSingle(true)` zapobiega rozdzieleniu tablicy na oddzielne wiersze lub kolumny.

---

![Copy range between workbooks in Java – Aspose.Cells code example](copy-range-workbooks.png)

*Tekst alternatywny obrazu:* **Kopiowanie zakresu między skoroszytami w Javie – przykład kodu Aspose.Cells** (zgodny z głównym słowem kluczowym).

---

## Oczekiwany wynik

| Nazwa pliku                | Zawartość |
|----------------------------|-----------|
| `destination.xlsx`         | Skopiowany zakres z funkcjonalną tabelą przestawną. |
| `destination.pptx`         | Wyeksportowany obraz jako edytowalny kształt PowerPoint. |
| `final_output.xlsx`        | Tabela bez strzałek AutoFilter. |
| `template_filled.xlsx`     | Tablica JSON przechowywana jako pojedyncza wartość komórki. |

Otwórz każdy plik w odpowiedniej aplikacji (Excel lub PowerPoint), aby zweryfikować, że operacje zakończyły się sukcesem.

---

## Podsumowanie

Teraz wiesz, jak **skopiować zakres między skoroszytami** w Javie przy użyciu Aspose.Cells, zachowując tabelę przestawną, eksportując obraz do PowerPoint oraz usuwając AutoFilter z tabeli Excel. Ten sam schemat można rozszerzyć na kopiowanie dowolnego zakresu Excel do nowego skoroszytu, obsługę tablic JSON w SmartMarker lub łączenie dodatkowych transformacji.

Kolejne kroki, które możesz rozważyć:

* **Kopiowanie zakresu Excel do nowego skoroszytu** z wieloma arkuszami.  
* Użycie **eksportu obrazu do PowerPoint** do masowego wyodrębniania obrazów.  
* Zastosowanie **usuwania autofilter z tabeli Excel** w większych pipeline'ach raportowych.  
* Połączenie tych technik z Aspose.Slides w celu pełnej automatyzacji Excel‑do‑PowerPoint.

Śmiało eksperymentuj z różnymi adresami zakresów, wieloma tabelami przestawnymi lub własnymi formatami obrazów. API Aspose.Cells jest zaprojektowane z myślą o programistycznej elastyczności, więc możesz dostosować przedstawione wzorce do dowolnego scenariusza automatyzacji Excel w przedsiębiorstwie.

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Copy Page Setup Settings Between Worksheets in Excel Using Aspose.Cells Java](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [Excel Copy Worksheets Between Workbooks](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}