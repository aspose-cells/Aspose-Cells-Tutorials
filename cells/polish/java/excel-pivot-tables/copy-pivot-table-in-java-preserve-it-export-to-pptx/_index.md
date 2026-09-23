---
category: general
date: 2026-03-01
description: Skopiuj tabelę przestawną w Javie, zachowując jej strukturę, następnie
  wyeksportuj Excel do PPTX, wyłącz AutoFilter w Excelu i użyj Smart Marker dla tablic
  JSON – pełny przewodnik krok po kroku.
draft: false
keywords:
- copy pivot table
- preserve pivot table
- use smart marker
- disable excel autofilter
- export excel to pptx
language: pl
og_description: Kopiowanie tabeli przestawnej w Javie, zachowanie definicji tabeli
  przestawnej, eksport do PPTX, wyłączenie AutoFilter i użycie Smart Marker – kompletny
  przewodnik dla programistów.
og_title: Kopiowanie tabeli przestawnej w Javie – zachowaj ją, wyeksportuj do PPTX
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Kopiowanie tabeli przestawnej w Javie – zachowaj ją, wyeksportuj do PPTX
url: /pl/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skopiuj tabelę przestawną w Javie – zachowaj ją, wyeksportuj do PPTX

Kiedykolwiek potrzebowałeś **skopiować tabelę przestawną** z jednego skoroszytu do drugiego, nie tracąc przy tym definicji tabeli przestawnej? Nie jesteś jedynym, który się nad tym zastanawia. W wielu rzeczywistych projektach będziesz przenosić dane, a ostatnią rzeczą, jaką chcesz, jest zepsuta tabela przestawna, która generuje błędy w czasie wykonywania.  

W tym samouczku przeprowadzimy Cię przez kompletną rozwiązanie, które nie tylko **kopiuje tabelę przestawną**, ale także pokazuje, jak **zachować tabelę przestawną** przy kopiowaniu, **wyeksportować Excel do PPTX**, **wyłączyć AutoFilter w Excelu** oraz **użyć smart marker**, aby wstawić tablicę JSON jako pojedynczą komórkę. Po zakończeniu będziesz mieć pojedynczy, uruchamialny program w Javie, obejmujący wszystkie cztery scenariusze.

## Wymagania wstępne

- Java 8 lub nowsza (kod działa również z Java 11)  
- Biblioteka Aspose.Cells for Java (wersja 23.9 lub nowsza) – możesz ją pobrać z Maven Central  
- Podstawowa znajomość pojęć Excela, takich jak tabele przestawne, tabele i pola tekstowe  

Jeśli brakuje Ci pliku JAR Aspose.Cells, dodaj to do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

Teraz zanurzmy się w temat.

## Krok 1: Skopiuj tabelę przestawną – zachowując definicję tabeli przestawnej

Gdy po prostu kopiujesz zakres komórek zawierający tabelę przestawną, metadane tabeli przestawnej często pozostają w tyle. Aspose.Cells oferuje wygodny sposób na zachowanie definicji, używając `copyRange` wraz z instancją `CopyOptions`.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot (A1:G20 is just an example)
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Prepare the destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot definition travels with it
        destSheet.getCells().copyRange(pivotRange,
                new CellArea(0, 0, 19, 6), // destination area (rows 0‑19, cols 0‑6)
                new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Dlaczego to działa:** `CopyOptions` mówi Aspose.Cells, aby przeniosło wszystko, w tym pamięć podręczną tabeli przestawnej i ustawienia pól. Bez tego otrzymasz jedynie wartości i utracisz możliwość odświeżania tabeli przestawnej.

**Przypadek brzegowy:** Jeśli Twoja źródłowa tabela przestawna obejmuje więcej niż sztywno zakodowany zakres `A1:G20`, dostosuj zakres odpowiednio lub użyj `sourceSheet.getPivotTables().get(0).getDataRange()`, aby pobrać go dynamicznie.

![Przykład kopiowania tabeli przestawnej](image.png "Kopiowanie tabeli przestawnej w Javie")

*Tekst alternatywny obrazu: diagram kopiowania tabeli przestawnej w Javie*

## Krok 2: Wyeksportuj arkusz z edytowalnym polem tekstowym do PPTX

Często potrzebujesz przekształcić arkusz Excela w slajd PowerPoint — myśl o cotygodniowych pulpitach nawigacyjnych, które muszą być prezentowane. Aspose.Cells może bezpośrednio zapisać arkusz jako plik PPTX, zachowując kształty takie jak pola tekstowe.

```java
import com.aspose.cells.*;

public class ExportToPptxDemo {

    public static void main(String[] args) throws Exception {
        // Load workbook that contains a TextBox shape
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Export the first worksheet to PPTX
        wb.save("YOUR_DIRECTORY/output.pptx", SaveFormat.PPTX);

        System.out.println("Worksheet exported to PPTX successfully.");
    }
}
```

**Co się dzieje:** Metoda `save` z parametrem `SaveFormat.PPTX` konwertuje cały arkusz, w tym dowolne edytowalne pole tekstowe, na slajd PowerPoint. Tekst wewnątrz pola pozostaje edytowalny po otwarciu pliku PPTX w PowerPoint.

**Wskazówka:** Jeśli masz wiele arkuszy i chcesz zachować tylko konkretny, wywołaj `wb.getWorksheets().removeAt(index)` dla pozostałych przed zapisem.

## Krok 3: Wyłącz AutoFilter w Excelu w tabeli

AutoFilter jest przydatny dla użytkowników końcowych, ale czasami trzeba go wyłączyć programowo — być może przed eksportem danych lub przy generowaniu czystego raportu. Oto jak **wyłączyć AutoFilter w Excelu** w tabeli Excel.

```java
import com.aspose.cells.*;

public class DisableAutoFilterDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");
        Worksheet sheet = wb.getWorksheets().get(0);

        // Assume the first table in the sheet is the target
        Table table = sheet.getTables().get(0);

        // Turn off the AutoFilter arrows
        table.setShowAutoFilter(false);

        // Save the modified workbook
        wb.save("YOUR_DIRECTORY/noFilter.xlsx");
        System.out.println("AutoFilter disabled and workbook saved.");
    }
}
```

**Dlaczego możesz tego potrzebować:** Eksport do formatów, które nie obsługują AutoFilter (np. CSV lub PDF), może spowodować pojawienie się niechcianych ikon filtrów. Wyłączenie go zapewnia czysty wynik.

**Częsty problem:** Jeśli arkusz nie zawiera tabel, `getTables().get(0)` spowoduje `IndexOutOfBoundsException`. Zawsze najpierw sprawdzaj `sheet.getTables().size()` w kodzie produkcyjnym.

## Krok 4: Użyj Smart Marker — wstaw tablicę JSON jako pojedynczą wartość komórki

Smart Marker to silnik szablonów Aspose. Jeden przydatny trik polega na traktowaniu całej tablicy JSON jako pojedynczej wartości komórki, co jest idealne do logowania lub przekazywania danych strukturalnych dalej. Użyjmy **smart marker**, aby to osiągnąć.

```java
import com.aspose.cells.*;

public class SmartMarkerDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Initialise the SmartMarker processor with the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

        // JSON array we want to embed
        String jsonArray = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Configure the processor to treat arrays as a single cell
        processor.setOptions(SmartMarkerOptions.ArrayAsSingle);

        // Apply the marker – assume cell A1 contains the marker ${json}
        processor.apply(jsonArray);

        // Save the result
        wb.save("YOUR_DIRECTORY/smartMarkerResult.xlsx");
        System.out.println("JSON array inserted via Smart Marker.");
    }
}
```

**Jak to działa:** Znacznik `${json}` w skoroszycie zostaje zastąpiony całym ciągiem JSON, ponieważ ustawiliśmy `ArrayAsSingle`. Bez tej opcji Aspose próbowałby rozwinąć każdy element tablicy do osobnych wierszy.

**Wariant:** Jeśli potrzebujesz podzielić tablicę na wiersze, po prostu pomiń `ArrayAsSingle`, a Smart Marker automatycznie rozwinie ją.

## Pełny działający przykład — wszystkie kroki połączone

Poniżej znajduje się pojedyncza klasa Java, która łączy wszystkie opisane operacje. Uruchom ją jako zwykłą metodę `main`; wystarczy dostosować ścieżki plików do swojego środowiska.

```java
import com.aspose.cells.*;

public class CompleteExcelAutomation {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Copy Pivot Table -----------
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet srcSheet = srcWb.getWorksheets

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}