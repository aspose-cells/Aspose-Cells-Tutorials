---
category: general
date: 2026-11-19
description: Dowiedz się, jak skopiować tabelę przestawną w Javie, zachowując jej
  dane i układ. Ten przewodnik krok po kroku pokazuje również, jak efektywnie kopiować
  tabele przestawne w Excelu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- how to preserve pivot
- preserve pivot table
- copy excel pivot
language: pl
lastmod: 2026-11-19
og_description: Kopiowanie tabeli przestawnej w Javie z Aspose.Cells. Skorzystaj z
  tego przewodnika, aby dowiedzieć się, jak zachować tabele przestawne i dokładnie
  kopiować dane przestawne z Excela.
og_image_alt: Illustration of the copy pivot table workflow in Java
og_title: Kopiowanie tabeli przestawnej w Javie – kompletny przewodnik Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy pivot table in Java while preserving its data and
    layout. This step‑by‑step guide also shows how to copy excel pivot tables efficiently.
  headline: How to copy pivot table in Java with Aspose.Cells
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Pivot tables
title: Jak skopiować tabelę przestawną w Javie przy użyciu Aspose.Cells
url: /pl/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak skopiować tabelę przestawną w Javie przy użyciu Aspose.Cells

Jeśli potrzebujesz **skopiować tabelę przestawną** z jednego skoroszytu do drugiego, ten przewodnik pokaże Ci dokładnie, jak to zrobić w Javie. Niezależnie od tego, czy budujesz silnik raportowania, czy migrujesz dane, zobaczysz niezawodny sposób zachowania pamięci podręcznej przestawnej, pól i formatowania.

Kopiowanie tabeli przestawnej może być trudne, ponieważ proste skopiowanie zakresu często traci podstawowe źródło danych. W tym tutorialu użyjemy Aspose.Cells, aby **jak skopiować przestawną** zachowując wszystkie obliczenia, a także omówimy **jak zachować przestawne** tabele, gdy docelowy skoroszyt jest pusty.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

* Java 17 lub nowszą zainstalowaną.
* Aspose.Cells for Java (wersja 23.9 lub późniejsza) dodaną do classpath projektu.
* Dwa pliki Excel: skoroszyt źródłowy zawierający tabelę przestawną oraz pusty skoroszyt docelowy (lub skoroszyt, do którego chcesz scalić dane).

Nie potrzebujesz specjalnej licencji do przykładu kodu, ale ważna licencja Aspose.Cells usuwa znaki wodne wersji ewaluacyjnej.

## Krok 1: Załaduj skoroszyt źródłowy zawierający tabelę przestawną

Pierwszym krokiem jest otwarcie skoroszytu, w którym znajduje się oryginalna przestawna. Załadowanie pliku daje dostęp do arkusza, komórek i pamięci podręcznej przestawnej.

```java
// Step 1: Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Dlaczego to ważne*: Aspose.Cells odczytuje cały skoroszyt, w tym ukryte dane pamięci podręcznej, które napędzają przestawną. Bez pełnego załadowania pliku operacja kopiowania utraciłaby definicję przestawnej.

## Krok 2: Przygotuj skoroszyt docelowy

Utwórz nowy skoroszyt (lub otwórz istniejący) i pobierz jego pierwszy arkusz. To miejsce, w którym zostanie umieszczona przestawna.

```java
// Step 2: Create a new destination workbook and get its first worksheet
Workbook destWb = new Workbook();                     // empty workbook
Worksheet destWs = destWb.getWorksheets().get(0);    // first sheet
```

*Wskazówka*: Jeśli już masz docelowy skoroszyt, zamień wywołanie `new Workbook()` na `new Workbook("target.xlsx")`. Dzięki temu możesz **skopiować excel pivot** do wstępnie wypełnionego skoroszytu.

## Krok 3: Zdefiniuj obszar komórek obejmujący tabelę przestawną

Musisz określić dokładny zakres, który obejmuje przestawną. Zakres zawiera tabelę przestawną, listę pól oraz wszelkie otaczające dane, które chcesz zachować.

```java
// Step 3: Define the cell area that covers the pivot table in the source sheet
CellArea area = CellArea.createCellArea("A1", "H30"); // adjust as needed
```

*Dlaczego to ważne*: `CellArea` informuje Aspose.Cells, co ma zostać skopiowane. Jeśli obszar jest zbyt mały, przestawna zostanie obcięta; jeśli jest zbyt duży, skopiujesz niepotrzebne dane. Dostosuj współrzędne do rzeczywistego rozmiaru przestawnej.

## Krok 4: Wykonaj operację kopiowania przy użyciu CopyOptions

Użyj metody `copy` na kolekcji komórek arkusza źródłowego. Przekazanie nowego obiektu `CopyOptions()` zapewnia przeniesienie całego formatowania, formuł i pamięci podręcznej przestawnej.

```java
// Step 4: Copy the defined range (including the pivot table) to the destination worksheet
srcWb.getWorksheets().get(0).getCells().copy(area, destWs.getCells(), new CopyOptions());
```

### Dlaczego `CopyOptions` zachowuje przestawną

`CopyOptions` instruuje Aspose.Cells, aby traktował zakres jako *cały* obiekt, a nie płaską listę wartości. To klucz do **jak zachować przestawną**: pamięć podręczna przestawnej jest duplikowana, więc skoroszyt docelowy może przeliczyć przestawną bez ręcznej interwencji.

## Krok 5: Zapisz skoroszyt docelowy

Na koniec zapisz plik docelowy na dysku. Zapisany plik będzie zawierał w pełni funkcjonalną kopię oryginalnej przestawnej.

```java
// Step 5: Save the destination workbook – the pivot table is preserved
destWb.save("YOUR_DIRECTORY/copied_with_pivot.xlsx");
```

*Oczekiwany rezultat*: Otwarcie `copied_with_pivot.xlsx` w Excelu pokazuje identyczną tabelę przestawną, wraz z segmentatorami, filtrami i polami obliczeniowymi. Możesz ją odświeżyć, a źródło danych będzie wskazywać na skopiowany zakres w tym samym skoroszycie.

---

![Diagram przedstawiający proces kopiowania tabeli przestawnej](/images/copy-pivot-table-workflow.png){.align-center width=600 alt="Diagram przedstawiający przepływ kopiowania tabeli przestawnej z skoroszytu źródłowego do docelowego"}

## Jak kopiować tabele przestawne między wieloma arkuszami

Jeśli musisz **skopiować excel pivot** z kilku arkuszy, powtórz kroki 3‑4 dla każdego arkusza źródłowego. Możesz także przeiterować `srcWb.getWorksheets()` i skopiować każdą przestawną do odpowiadającego arkusza w `destWb`. Oto zwięzły przykład pętli:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet srcWs = srcWb.getWorksheets().get(i);
    Worksheet newDestWs = destWb.getWorksheets().add();
    // Assume each pivot occupies A1:H30 – adjust per sheet if needed
    CellArea area = CellArea.createCellArea("A1", "H30");
    srcWs.getCells().copy(area, newDestWs.getCells(), new CopyOptions());
}
destWb.save("YOUR_DIRECTORY/multi_sheet_copy.xlsx");
```

*Pro tip*: Użyj `srcWs.getPivotTables().getCount()`, aby sprawdzić, czy arkusz faktycznie zawiera przestawną przed kopiowaniem. Dzięki temu unikniesz kopiowania nieistotnych danych.

## Typowe pułapki i jak ich unikać

| Problem | Dlaczego się pojawia | Rozwiązanie |
|-------|----------------|-----|
| **Przestawna traci pamięć podręczną** | Użycie `Worksheet.copy()` bez `CopyOptions` kopiuje tylko wartości komórek. | Zawsze używaj `srcWs.getCells().copy(..., new CopyOptions())`. |
| **Docelowy skoroszyt pokazuje błędy #REF!** | Skopiowana przestawna nadal odwołuje się do zewnętrznego źródła danych w oryginalnym skoroszycie. | Po kopiowaniu wywołaj `destWs.getPivotTables().get(0).refresh();`, aby ponownie powiązać pamięć z nowym zakresem. |
| **Znikają segmentatory** | Segmentatory są przechowywane poza głównym obszarem komórek. | Rozszerz `CellArea`, aby objąć zakresy segmentatorów, lub skopiuj cały arkusz (`srcWs.copy(destWs, new CopyOptions())`). |
| **Spowolnienie wydajności przy dużych przestawnych** | Kopiowanie ogromnych zakresów z formatowaniem może być wolne. | Użyj `CopyOptions.setOnlyData(true)`, jeśli nie potrzebujesz formatowania, a następnie zastosuj style ręcznie. |

## Jak zachować formatowanie tabeli przestawnej przy aktualizacji danych

Czasami trzeba **jak zachować przestawną** po zmianie danych źródłowych. Po skopiowaniu możesz zablokować styl przestawnej:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.setPreserveFormatting(true);   // keeps colors, fonts, and layout
pt.refresh();                     // recalculates with new data
```

Ustawienie `PreserveFormatting` zapewnia, że wszelkie niestandardowe style zastosowane w źródle przetrwają kopiowanie.

## Weryfikacja kopii

Szybki sposób, aby potwierdzić, że kopiowanie się powiodło, to porównanie definicji przestawnych:

```java
PivotTable srcPt = srcWb.getWorksheets().get(0).getPivotTables().get(0);
PivotTable destPt = destWs.getPivotTables().get(0);

System.out.println("Source fields: " + srcPt.getFields().size());
System.out.println("Destination fields: " + destPt.getFields().size());
// Both numbers should match
```

Jeśli liczby się zgadzają i docelowy skoroszyt otwiera się bez błędów, udało Ci się **skopiować tabelę przestawną**.

## Podsumowanie

Teraz wiesz, jak **skopiować tabelę przestawną** z jednego skoroszytu Excel do drugiego przy użyciu Aspose.Cells dla Javy oraz zobaczyłeś dokładne kroki, aby **jak skopiować przestawną** przy zachowaniu pamięci podręcznej, formatowania i segmentatorów. Ten sam schemat działa w scenariuszach **skopiować excel pivot** na wielu arkuszach, a kod można dostosować do przypadków brzegowych, takich jak zachowanie formatowania przestawnej czy obsługa dużych zestawów danych.

### Kolejne kroki

* Zbadaj opcje **preserve pivot table**, takie jak `setPreserveFormatting` i `refresh` dla dynamicznych źródeł danych.  
* Spróbuj kopiować tabele przestawne między skoroszytami o różnych kolejnościach kolumn — dostosuj `CellArea` odpowiednio.  
* Połącz tę technikę z Aspose.Slides, aby osadzić migawki przestawnych w prezentacjach PowerPoint.

Miłego kodowania i zachęcamy do eksperymentowania z wariantami, które pasują do Twojego konkretnego pipeline’u automatyzacji!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz wyjaśnienia krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [How to copy a pivot table between worksheets in Java](/cells/english/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/)
- [How to copy pivot table to a new workbook in Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}