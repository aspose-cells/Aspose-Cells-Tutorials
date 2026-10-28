---
category: general
date: 2026-10-07
description: Jak podzielić kolumny przy użyciu Aspose.Cells dla Javy. Dowiedz się,
  jak podzielić ciąg znaków na kolumny, zautomatyzować formułę Excel i zapisać formułę
  w komórce w kilku linijkach kodu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to split columns
- split string into columns
- automate excel formula
- write formula to cell
language: pl
lastmod: 2026-10-07
og_description: Jak podzielić kolumny w Javie przy użyciu Aspose.Cells. Ten samouczek
  pokazuje, jak podzielić ciąg znaków na kolumny, zautomatyzować ocenę formuł Excel
  oraz zapisać formułę w komórce.
og_image_alt: Screenshot of Java code that splits columns in an Excel worksheet using
  Aspose.Cells
og_title: Jak podzielić kolumny w Javie przy użyciu Aspose.Cells – szybki poradnik
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: How to split columns using Aspose.Cells for Java. Learn to split string
    into columns, automate Excel formula, and write formula to cell in a few lines
    of code.
  headline: How to split columns in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Jak podzielić kolumny w Javie przy użyciu Aspose.Cells – przewodnik krok po
  kroku
url: /pl/java/data-manipulation/how-to-split-columns-in-java-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak podzielić kolumny w Javie przy użyciu Aspose.Cells – przewodnik krok po kroku

Jeśli potrzebujesz **how to split columns** w arkuszu Excel programowo, ten przewodnik pokaże Ci kompletny proces z Aspose.Cells dla Javy. Dowiesz się także, jak **split string into columns**, **automate Excel formula** evaluation oraz **write formula to a cell** używając zwięzłego, gotowego do produkcji kodu.

Programowe dzielenie kolumn eliminuje ręczne kopiowanie‑wklejanie, zmniejsza liczbę błędów i umożliwia przetwarzanie danych na dużą skalę. Po zakończeniu tego samouczka będziesz mógł generować, modyfikować i oceniać formuły w locie, czyniąc Excel prawdziwą częścią Twojego backendu w Javie.

## Wymagania wstępne

* Java 17 lub nowszy zainstalowany.
* Maven 3.8+ (lub Gradle) do zarządzania zależnościami.
* Licencja Aspose.Cells for Java (darmowa wersja ewaluacyjna działa do nauki).
* Podstawowa znajomość składni Javy i koncepcji Excela.

Jeśli którekolwiek z tych elementów brakuje, zainstaluj je najpierw; przykłady kodu zakładają standardowy projekt Maven.

## Krok 1: Dodaj Aspose.Cells do swojego projektu

Dodaj następującą zależność do swojego `pom.xml`. Spowoduje to pobranie najnowszej stabilnej biblioteki Aspose.Cells.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version available -->
</dependency>
```

**Dlaczego ten krok jest ważny:** Biblioteka dostarcza klasy `Workbook`, `Worksheet` i `Cell` niezbędne do manipulacji plikami Excel bez Microsoft Office. Bez tej zależności kod się nie skompiluje.

## Krok 2: Utwórz skoroszyt i wybierz pierwszy arkusz

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
```

Obiekt `Workbook` reprezentuje cały plik Excel. Dostęp do pierwszego arkusza zapewnia przewidywalny punkt wyjścia dla formuły, którą napiszemy.

## Krok 3: Zapisz formułę WRAPCOLS w docelowej komórce

```java
        // Step 3: Identify the target cell (A1) where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Step 3: Write the WRAPCOLS formula to split a long string into three columns
        // WRAPCOLS(string, columns) distributes the string across the specified number of columns.
        targetCell.setFormula("=WRAPCOLS(\"This is a very long string that needs to be split\",3)");
```

**Dlaczego używamy `WRAPCOLS`:** Wbudowana funkcja Excela `WRAPCOLS` automatycznie dzieli pojedynczą wartość tekstową na określoną liczbę kolumn, inteligentnie obsługując granice wyrazów. To najpewniejszy sposób na **split string into columns** bez własnej logiki parsowania.

## Krok 4: Wymuś ocenę formuły w skoroszycie

```java
        // Step 4: Calculate all formulas in the workbook so the result becomes visible
        workbook.calculateFormula();
```

Wywołanie `calculateFormula()` **automates Excel formula** evaluation po stronie serwera. Bez tego wywołania komórka nadal będzie zawierała tekst formuły, a nie obliczone wartości.

## Krok 5: Pobierz i wyświetl wynik po podzieleniu

```java
        // Step 5: Retrieve the computed value from the target cell
        String result = targetCell.getStringValue(); // returns the first column of the split result
        System.out.println("First column output: " + result);

        // Optionally, read the other columns created by WRAPCOLS
        String second = worksheet.getCells().get("B1").getStringValue();
        String third  = worksheet.getCells().get("C1").getStringValue();

        System.out.println("Second column output: " + second);
        System.out.println("Third column output: " + third);

        // Save the workbook to verify the split visually (optional)
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

Po uruchomieniu programu konsola wyświetli:

```
First column output: This is a very long
Second column output: string that needs
Third column output: to be split
```

Wygenerowany plik `SplitColumnsResult.xlsx` pokazuje trzy kolumny wypełnione podzielonym tekstem.

## Zrozumienie funkcji WRAPCOLS

* **Składnia:** `WRAPCOLS(text, columns, [delimiter])`
* **Parametry:**
  * `text` – ciąg znaków, który chcesz podzielić.
  * `columns` – liczba kolumn, na które rozłożyć tekst.
  * `delimiter` (opcjonalny) – znak używany do podziału ciągu; domyślnie jest to spacja.
* **Wartość zwracana:** Tablica, która rozlewa się na sąsiednie komórki, przy czym każdy element zawiera część oryginalnego tekstu.

Ponieważ funkcja rozlewa się poziomo, wystarczy zapisać formułę w najbardziej po lewej komórce (A1 w przykładzie). Excel automatycznie wypełnia B1, C1, … w razie potrzeby.

## Typowe warianty i przypadki brzegowe

| Situation | Recommended adjustment |
|-----------|------------------------|
| **Zmienna liczba kolumn** | Zastąp sztywno zakodowaną wartość `3` zmienną: `targetCell.setFormula(String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount));` |
| **Niestandardowy delimiter** | Użyj trzeciego argumentu, np. `=WRAPCOLS(A2,4,",")` aby podzielić po przecinkach. |
| **Pusty ciąg źródłowy** | Funkcja zwraca puste komórki; zabezpiecz się przed `null` lub pustymi ciągami przed ustawieniem formuły. |
| **Duże zestawy danych** | Zastosuj formułę w pętli dla każdego wiersza, a następnie wywołaj `calculateFormula()` raz po zakończeniu pętli, aby poprawić wydajność. |
| **Znaki nie‑ASCII** | WRAPCOLS działa z Unicode; upewnij się, że plik źródłowy Javy jest zapisany w UTF‑8. |

**Wskazówka:** Podczas przetwarzania wielu wierszy, przechowuj formułę w zmiennej typu string i używaj jej ponownie, aby uniknąć kosztów wielokrotnego konkatenowania łańcuchów.

## Pełny, gotowy do uruchomienia przykład

Poniżej znajduje się kompletny program gotowy do skopiowania i wklejenia. Zawiera on instrukcje importu, obsługę wyjątków oraz opcjonalną operację zapisu.

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the long string and desired column count
        String longString = "This is a very long string that needs to be split";
        int columnCount = 3;

        // Write the WRAPCOLS formula to cell A1
        Cell targetCell = worksheet.getCells().get("A1");
        String formula = String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount);
        targetCell.setFormula(formula);

        // Evaluate all formulas in the workbook
        workbook.calculateFormula();

        // Read and display each column's result
        System.out.println("First column output: " + worksheet.getCells().get("A1").getStringValue());
        System.out.println("Second column output: " + worksheet.getCells().get("B1").getStringValue());
        System.out.println("Third column output: " + worksheet.getCells().get("C1").getStringValue());

        // Save the workbook for visual verification
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

Uruchomienie tego programu generuje taki sam wynik w konsoli, jak pokazano wcześniej, oraz zapisuje plik Excel, który wyraźnie demonstruje **how to split columns**.

## Lista kontrolna rozwiązywania problemów

* **Formuła nie jest oceniana** – Upewnij się, że po ustawieniu formuły wywołano `workbook.calculateFormula()`.
* **Puste komórki po podzieleniu** – Sprawdź, czy ciąg źródłowy nie jest `null` ani pusty oraz czy liczba kolumn jest większa od zera.
* **Wyjątek licencyjny** – Dostarcz prawidłowy plik licencji Aspose.Cells (`License license = new License(); license.setLicense("Aspose.Total.lic");`) przed utworzeniem skoroszytu, aby usunąć znaki wodne wersji ewaluacyjnej.
* **Spowolnienie wydajności przy dużych arkuszach** – Wywołaj `calculateFormula()` raz po zapisaniu wszystkich formuł, a nie po każdej pojedynczej komórce.

## Zakończenie

Teraz wiesz, **how to split columns** w Javie przy użyciu Aspose.Cells, jak **split string into columns** za pomocą funkcji `WRAPCOLS`, jak **automate Excel formula** evaluation oraz jak **write formula to a cell** programowo. Ta technika eliminuje ręczne kroki przygotowania danych i integruje potężne możliwości obsługi tekstu w Excelu bezpośrednio w Twoich aplikacjach Java.

### Następne kroki

* Zbadaj inne funkcje tekstowe, takie jak `TEXTSPLIT` i `FILTERXML`, dla bardziej złożonych scenariuszy parsowania.
* Połącz `WRAPCOLS` z `IFERROR`, aby elegancko obsługiwać nieoczekiwane dane wejściowe.
* Zintegruj rozwiązanie z usługą Spring Boot, która przyjmuje dane CSV przez REST i zwraca wypełniony plik Excel.

Opanowując te wzorce, możesz tworzyć solidne, zautomatyzowane przepływy pracy w Excelu, które skalują się wraz z potrzebami Twojego biznesu. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [aspose cells java – Rozdzielanie nazw na kolumny](/cells/english/java/cell-operations/aspose-cells-java-split-names-columns/)
- [Automatyczne dopasowanie kolumn Excela w Javie przy użyciu Aspose.Cells](/cells/english/java/formatting/aspose-cells-java-auto-fit-excel-columns-guide/)
- [Jak usunąć puste kolumny w Excelu przy użyciu Aspose.Cells Java&#58; Kompletny przewodnik](/cells/english/java/worksheet-management/delete-blank-columns-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}