---
category: general
date: 2026-09-27
description: Konwertuj JSON do Excela przy użyciu Aspose.Cells – dowiedz się, jak
  wypełnić Excel danymi z JSON i jak efektywnie przetwarzać JSON w Excelu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert json to excel
- populate excel from json
- how to process json in excel
- Aspose.Cells Java
- smart marker JSON
- excel automation Java
language: pl
lastmod: 2026-09-27
og_description: Konwertuj JSON do Excela przy użyciu Aspose.Cells. Ten samouczek pokazuje,
  jak wypełnić Excel danymi z JSON oraz wyjaśnia, jak przetwarzać JSON w Excelu za
  pomocą inteligentnych znaczników.
og_image_alt: Excel sheet after JSON data is merged into a single cell using Aspose.Cells
  Smart Marker
og_title: Konwertuj JSON do Excela przy użyciu Aspose.Cells – pełny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Convert JSON to Excel with Aspose.Cells – learn how to populate Excel
    from JSON and how to process JSON in Excel efficiently.
  headline: How to convert JSON to Excel and populate Excel from JSON using Aspose.Cells
  type: TechArticle
- description: Convert JSON to Excel with Aspose.Cells – learn how to populate Excel
    from JSON and how to process JSON in Excel efficiently.
  name: How to convert JSON to Excel and populate Excel from JSON using Aspose.Cells
  steps:
  - name: Why each step matters
    text: '* **Step 1** – The JSON string is the source data. Because we set `ArrayAsSingle`,
      the processor will not try to create rows for each object; instead it will write
      the raw JSON text into the cell. * **Step 2** – Loading the template separates
      presentation (the Excel layout) from data (the JSON). Thi'
  - name: 4.1 Converting a large JSON payload
    text: 'If the JSON text exceeds the default cell length limit, increase the column
      width or set the cell’s `Style` to wrap text:'
  - name: 4.2 Using a named range instead of a fixed cell
    text: You can place the smart‑marker inside a named range (e.g., `JsonCell`) and
      refer to it by name in the template. The processing code remains unchanged;
      Aspose.Cells resolves the marker wherever it appears.
  - name: 4.3 Merging multiple JSON objects into separate cells
    text: If you later decide to expand the array into rows, simply remove `options.setArrayAsSingle(true)`.
      The processor will generate a table where each object occupies a row, and you
      can customize column headings with additional markers.
  - name: 4.4 Handling nested JSON structures
    text: For nested objects, use dot notation in the marker, e.g., `${person.name}`.
      The processor will traverse the hierarchy automatically, allowing you to **populate
      Excel from JSON** with complex data models.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Jak przekonwertować JSON na Excel i wypełnić Excel z JSON przy użyciu Aspose.Cells
url: /pl/java/excel-import-export/how-to-convert-json-to-excel-and-populate-excel-from-json-us/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak przekonwertować JSON do Excela i wypełnić Excel z JSON przy użyciu Aspose.Cells

Jeśli potrzebujesz **konwertować JSON do Excela**, ten przewodnik pokazuje kompletną, gotową do uruchomienia rozwiązanie. Po przeczytaniu pierwszych dwóch zdań zrozumiesz, jak **wypełnić Excel z JSON** przy użyciu pojedynczego wyrażenia smart‑marker oraz dlaczego wywołanie `SmartMarkerOptions.setArrayAsSingle(true)` jest niezbędne dla pożądanego układu.

Przejdziemy przez każdy krok niezbędny do **przetwarzania JSON w Excelu**: ładowanie szablonu, konfigurowanie silnika smart‑marker, łączenie danych i zapisywanie wyniku. Tutorial zakłada, że masz podstawową wiedzę o Javie oraz działającą licencję Aspose.Cells. Nie są wymagane żadne zewnętrzne narzędzia, a kod kompiluje się i działa na Java 8+.

## Wymagania wstępne

* Java Development Kit (JDK) 8 lub nowszy zainstalowany.
* Aspose.Cells for Java (najnowsza wersja w momencie pisania, 23.9) dodana do classpathu projektu.
* Szablon Excel o nazwie `SmartMarkerTemplate.xlsx`, który zawiera smart‑marker `${jsonArray:ArrayAsSingle}` w komórce, w której ma się pojawić dane JSON.
* Katalog, do którego możesz zapisywać plik wyjściowy `JsonSingleCell.xlsx`.

Jeśli którekolwiek z tych elementów brakuje, zainstaluj JDK, pobierz plik JAR Aspose.Cells i utwórz szablon zgodnie z opisem w następnym rozdziale.

## Krok 1: Utwórz szablon Excel ze smart‑markerem

Smart‑marker informuje Aspose.Cells, gdzie wstawić dane. W tym przypadku chcemy, aby cała tablica JSON była traktowana jako pojedyncza wartość, więc umieszczamy następujący marker w docelowej komórce (np. **A1**):

```
${jsonArray:ArrayAsSingle}
```

> **Wskazówka:** Modyfikator `ArrayAsSingle` instruuje procesor, aby renderował całą tablicę w jednej komórce zamiast rozwijać ją do tabeli. Jest to kluczowa opcja dla scenariusza **konwertowanie JSON do Excela** demonstrowanego później.

Zapisz skoroszyt jako `SmartMarkerTemplate.xlsx` w folderze, do którego będziesz odwoływać się w kodzie Java.

## Krok 2: Napisz program Java, który **konwertuje JSON do Excela**

Poniżej znajduje się pełny plik źródłowy `JsonSmartMarker.java`. Każda linia jest skomentowana, abyś mógł zobaczyć, jak program **wypełnia Excel z JSON** i **przetwarza JSON w Excelu**.

```java
import com.aspose.cells.*;

public class JsonSmartMarker {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Define the JSON data that will be merged into the workbook.
        // The array contains two simple objects – you can replace it with any valid JSON.
        String json = "[{\"name\":\"John\",\"age\":30},{\"name\":\"Anna\",\"age\":25}]";

        // 2️⃣ Load the Excel template that already contains the smart‑marker.
        // Adjust the path to match your environment.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/SmartMarkerTemplate.xlsx");

        // 3️⃣ Configure SmartMarker to treat the JSON array as a single value.
        // This option is what makes the **convert JSON to Excel** operation produce one cell.
        SmartMarkerOptions options = new SmartMarkerOptions();
        options.setArrayAsSingle(true);   // key option for single‑cell output

        // 4️⃣ Process the JSON data using the configured options.
        // The SmartMarkerProcessor reads the JSON string, matches the marker,
        // and writes the resulting representation into the workbook.
        workbook.getSmartMarkerProcessor().process(json, options);

        // 5️⃣ Save the resulting workbook. The file now contains the JSON text in the target cell.
        workbook.save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
    }
}
```

### Dlaczego każdy krok ma znaczenie

* **Krok 1** – Ciąg JSON jest danymi źródłowymi. Ponieważ ustawiliśmy `ArrayAsSingle`, procesor nie będzie próbował tworzyć wierszy dla każdego obiektu; zamiast tego zapisze surowy tekst JSON w komórce.
* **Krok 2** – Ładowanie szablonu oddziela prezentację (układ Excela) od danych (JSON). Ta praktyka utrzymuje logikę **wypełniania Excela z JSON** w czystości i umożliwia ponowne użycie.
* **Krok 3** – `SmartMarkerOptions.setArrayAsSingle(true)` jest jedynym przełącznikiem potrzebnym do zmiany domyślnego zachowania rozwijania tablic. Bez niego procesor wygenerowałby tabelę, co nie jest pożądane przy **konwertowaniu JSON do Excela** w jedną komórkę.
* **Krok 4** – Metoda `process` wykonuje ciężką pracę **przetwarzania JSON w Excelu**. Parsuje JSON, dopasowuje marker i zapisuje wynik zgodnie z opcjami.
* **Krok 5** – Zapisanie skoroszytu finalizuje konwersję. Plik wyjściowy `JsonSingleCell.xlsx` może być otwarty w dowolnej aplikacji arkusza kalkulacyjnego.

## Krok 3: Zweryfikuj wynik

Otwórz `JsonSingleCell.xlsx`. Komórka **A1** (lub komórka, w której umieściłeś `${jsonArray:ArrayAsSingle}`) powinna zawierać dokładny ciąg JSON:

```
[{"name":"John","age":30},{"name":"Anna","age":25}]
```

Skoroszyt teraz przechowuje dane JSON w jednej komórce, co dowodzi, że program pomyślnie **konwertuje JSON do Excela** i **wypełnia Excel z JSON**.

![Arkusz Excel po połączeniu danych JSON w jedną komórkę przy użyciu Aspose.Cells](excel-output.png){: .center-image alt="Arkusz Excel po połączeniu danych JSON w jedną komórkę przy użyciu Aspose.Cells Smart Marker"}

## Krok 4: Typowe warianty i przypadki brzegowe

### 4.1 Konwertowanie dużego ładunku JSON

Jeśli tekst JSON przekracza domyślny limit długości komórki, zwiększ szerokość kolumny lub ustaw `Style` komórki na zawijanie tekstu:

```java
Cell target = workbook.getWorksheets().get(0).getCells().get("A1");
target.getStyle().setWrapText(true);
workbook.getWorksheets().get(0).autoFitColumns();
```

### 4.2 Użycie nazwanego zakresu zamiast stałej komórki

Możesz umieścić smart‑marker wewnątrz nazwanego zakresu (np. `JsonCell`) i odwoływać się do niego po nazwie w szablonie. Kod przetwarzający pozostaje niezmieniony; Aspose.Cells rozwiązuje marker, gdziekolwiek się pojawi.

### 4.3 Łączenie wielu obiektów JSON w oddzielne komórki

Jeśli później zdecydujesz się rozwinąć tablicę w wiersze, po prostu usuń `options.setArrayAsSingle(true)`. Procesor wygeneruje tabelę, w której każdy obiekt zajmuje wiersz, a nagłówki kolumn możesz dostosować przy użyciu dodatkowych markerów.

### 4.4 Obsługa zagnieżdżonych struktur JSON

Dla zagnieżdżonych obiektów użyj notacji kropkowej w markerze, np. `${person.name}`. Procesor automatycznie przejdzie hierarchię, umożliwiając **wypełnianie Excela z JSON** przy użyciu złożonych modeli danych.

## Krok 5: Wskazówki do użycia w produkcji

* **Wymuszanie licencji:** Aspose.Cells działa w trybie ewaluacyjnym z znakiem wodnym. Zastosuj swoją licencję przed wywołaniem `new Workbook(...)`, aby uniknąć znaku wodnego w produkcji.
* **Wydajność:** W przypadku ogromnych plików JSON strumieniuj dane zamiast ładować cały ciąg do pamięci. Aspose.Cells obsługuje przeciążenia `process` przyjmujące `InputStream`.
* **Obsługa błędów:** Owiń wywołanie `process` w blok try‑catch dla `Exception`. Zaloguj komunikat wyjątku, aby pomóc w diagnozowaniu niepoprawnego JSON lub niepasujących markerów.
* **Testowanie:** Dołącz testy jednostkowe, które porównują wygenerowaną wartość komórki z oczekiwanym ciągiem JSON. To zapewnia, że logika **konwertowania JSON do Excela** pozostaje niezawodna po zmianach w kodzie.

## Podsumowanie

Masz teraz kompletny, działający przykład, który **konwertuje JSON do Excela**, demonstruje jak **wypełnić Excel z JSON** i wyjaśnia **jak przetwarzać JSON w Excelu** przy użyciu smart‑markerów Aspose.Cells. Poprzez dostosowanie szablonu i `SmartMarkerOptions` możesz przełączać się między wyjściem w jednej komórce a rozwiniętymi tabelami, obsługiwać zagnieżdżone struktury i integrować rozwiązanie w większych pipeline'ach przetwarzania danych.

**Kolejne kroki**

* Zbadaj inne modyfikatory smart‑markerów, takie jak `:Repeat` i `:If`, aby tworzyć bardziej dynamiczne raporty.
* Połącz to podejście ze źródłami CSV lub baz danych, aby tworzyć hybrydowe źródła danych.
* Przejrzyj dokumentację Aspose.Cells dotyczącą [składni Smart Marker](https://docs.aspose.com/cells/java/smart-markers/) w celu głębszej personalizacji.

Miłego kodowania i ciesz się automatyzacją swoich przepływów pracy w Excelu przy użyciu Javy!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Efektywne importowanie JSON do Excela przy użyciu Aspose.Cells dla Java: Kompletny przewodnik](/cells/english/java/import-export/import-json-to-excel-aspose-cells-java/)
- [Importowanie danych JSON do Excela przy użyciu Aspose.Cells Java: Kompletny przewodnik](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Import JSON do Excela Aspose Cells Java](/cells/spanish/java/import-export/import-json-to-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}