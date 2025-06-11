---
"description": "Dowiedz się, jak tworzyć tabele przestawne w programie Excel za pomocą Aspose.Cells dla języka Java. Zautomatyzuj grupowanie i analizę danych za pomocą przykładów kodu źródłowego."
"linktitle": "Grupowanie danych w tabelach przestawnych"
"second_title": "Aspose.Cells Java Excel Processing API"
"title": "Grupowanie danych w tabelach przestawnych"
"url": "/pl/java/excel-pivot-tables/grouping-data-in-pivot-tables/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Grupowanie danych w tabelach przestawnych


Tabele przestawne to potężne narzędzie do analizowania i podsumowywania danych w arkuszach kalkulacyjnych. Umożliwiają grupowanie i kategoryzowanie danych w celu uzyskania cennych spostrzeżeń. W tym artykule przyjrzymy się, jak skutecznie grupować dane w tabelach przestawnych przy użyciu Aspose.Cells for Java, wraz z przykładami kodu źródłowego.

## Wstęp

Tabele przestawne zapewniają elastyczny sposób organizowania i podsumowywania danych z dużych zestawów danych. Umożliwiają tworzenie niestandardowych widoków danych poprzez grupowanie ich w kategorie lub hierarchie. Może to pomóc w łatwiejszym identyfikowaniu trendów, wzorców i wartości odstających w danych.

## Krok 1: Utwórz tabelę przestawną

Zacznijmy od utworzenia tabeli przestawnej przy użyciu Aspose.Cells dla Java. Poniżej znajduje się przykład, jak utworzyć tabelę przestawną z przykładowego pliku Excel.

```java
// Załaduj plik Excel
Workbook workbook = new Workbook("sample.xlsx");

// Uzyskaj dostęp do arkusza kalkulacyjnego zawierającego dane
Worksheet worksheet = workbook.getWorksheets().get(0);

// Określ zakres danych
CellArea sourceData = new CellArea();
sourceData.startRow = 0;
sourceData.endRow = 19; // Zakładając 20 wierszy danych
sourceData.startColumn = 0;
sourceData.endColumn = 3; // Zakładając 4 kolumny danych

// Utwórz tabelę przestawną na podstawie zakresu danych
int index = worksheet.getPivotTables().add(sourceData, "A1", "PivotTable1");

// Pobierz tabelę przestawną według indeksu
PivotTable pivotTable = worksheet.getPivotTables().get(index);

// Dodaj pola do wierszy i kolumn
pivotTable.addFieldToArea("Product", PivotFieldType.ROW);
pivotTable.addFieldToArea("Region", PivotFieldType.COLUMN);

// Dodaj wartości i zastosuj agregację
pivotTable.addFieldToArea("Sales", PivotFieldType.DATA);
pivotTable.getDataFields().get(0).setFunction(PivotFieldFunction.SUM);

// Zapisz zmodyfikowany plik Excela
workbook.save("output.xlsx");
```

## Krok 2: Dane grupowe

W Aspose.Cells for Java możesz grupować dane w tabeli przestawnej za pomocą `PivotField` klasa. Oto przykład, jak grupować pole w tabeli przestawnej:

```java
// Uzyskaj dostęp do pola „Produkt” w tabeli przestawnej
PivotField productField = pivotTable.getPivotFields().get("Product");

// Grupuj pole „Produkt” według określonego kryterium, np. według litery początkowej
productField.setIsAutoSubtotals(false);
productField.setBaseField("Product");
productField.setAutoSort(true);
productField.setAutoShow(true);

// Zapisz zmodyfikowany plik Excela ze zgrupowanymi danymi
workbook.save("output_grouped.xlsx");
```

## Krok 3: Dostosuj grupowanie

Możesz dalej dostosowywać ustawienia grupowania, takie jak określanie przedziałów grupowania opartych na dacie lub niestandardowych reguł grupowania. Oto przykład dostosowywania grupowania opartego na dacie:

```java
// Uzyskaj dostęp do pola „Data” w tabeli przestawnej (zakładając, że jest to pole daty)
PivotField dateField = pivotTable.getPivotFields().get("Date");

// Grupuj daty według miesięcy
dateField.setIsAutoSubtotals(false);
dateField.setIsDateGroup(true);
dateField.setDateGroupingType(PivotFieldDateGroupingType.MONTHS);

// Zapisz zmodyfikowany plik Excela z niestandardowym grupowaniem dat
workbook.save("output_custom_grouping.xlsx");
```

## Wniosek

Grupowanie danych w tabelach przestawnych to cenna technika analizy i podsumowywania danych w programie Excel, a Aspose.Cells for Java ułatwia automatyzację tego procesu. Dzięki podanym przykładom kodu źródłowego możesz tworzyć tabele przestawne, dostosowywać grupowanie i efektywnie uzyskiwać wgląd w swoje dane.

## Często zadawane pytania

### 1. Jaki jest cel tabel przestawnych w programie Excel?

Tabele przestawne w programie Excel służą do podsumowywania i analizowania dużych zestawów danych. Umożliwiają tworzenie niestandardowych widoków danych, ułatwiając identyfikację wzorców i trendów.

### 2. Jak mogę dostosować grupowanie danych w tabeli przestawnej?

Możesz dostosować grupowanie danych w tabeli przestawnej za pomocą `PivotField` Klasa w Aspose.Cells dla Java. Pozwala to określić kryteria grupowania, takie jak przedziały oparte na dacie lub reguły niestandardowe.

### 3. Czy mogę zautomatyzować tworzenie tabel przestawnych za pomocą Aspose.Cells dla Java?

Tak, można zautomatyzować tworzenie tabel przestawnych w programie Excel za pomocą pakietu Aspose.Cells dla języka Java, jak pokazano w podanych przykładach kodu źródłowego.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}