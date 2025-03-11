---
title: Przesuń pierwszy wiersz w dół podczas wstawiania wierszy tabeli danych w programie Excel
linktitle: Przesuń pierwszy wiersz w dół podczas wstawiania wierszy tabeli danych w programie Excel
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Naucz się wstawiać wiersze DataTable w programie Excel bez przesuwania pierwszego wiersza w dół za pomocą Aspose.Cells dla .NET. Przewodnik krok po kroku dla bezproblemowej automatyzacji.
weight: 11
url: /pl/net/excel-data-import-export/shift-first-row-down-when-inserting-cells-datatable-rows-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Przesuń pierwszy wiersz w dół podczas wstawiania wierszy tabeli danych w programie Excel

## Wstęp

Czy jesteś zmęczony ręcznym przesuwaniem wierszy podczas wstawiania nowych danych do arkuszy kalkulacyjnych programu Excel? Cóż, masz szczęście! W tym artykule zagłębimy się w to, jak zautomatyzować ten proces za pomocą Aspose.Cells dla .NET. Do końca tego samouczka nie tylko nauczysz się, jak pracować z tabelami danych w programie Excel, ale także jak dostosować opcje importu, aby lepiej odpowiadały Twoim potrzebom. Zaufaj mi; może to zaoszczędzić Ci mnóstwo czasu i kłopotów! Więc weź filiżankę kawy i zaczynajmy!

## Wymagania wstępne

Zanim przejdziemy do kodowania, upewnijmy się, że wszystko jest skonfigurowane:

1. Visual Studio: Upewnij się, że masz zainstalowany program Visual Studio (wersja 2017 lub nowsza powinna działać bez problemu).
2.  Aspose.Cells dla .NET: Musisz mieć bibliotekę Aspose.Cells. Jeśli jeszcze tego nie zrobiłeś, możesz ją pobrać[Tutaj](https://releases.aspose.com/cells/net/).
3. Podstawowa znajomość języka C# i programu Excel: Podstawowa znajomość programowania w języku C# i działania programu Excel z pewnością pomoże Ci efektywniej nadążać za nauką.

 Będziesz także chciał mieć pod ręką przykładowy plik Excela. W tym przewodniku użyjemy przykładu o nazwie`sampleImportTableOptionsShiftFirstRowDown.xlsx`. Możesz utworzyć ten plik lub znaleźć szablon, który odpowiada Twoim potrzebom.

## Importuj pakiety

Zanim zagłębimy się w kodowanie, musimy upewnić się, że zaimportowaliśmy niezbędne pakiety. W swoim projekcie C# uwzględnij następujące przestrzenie nazw:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Pakiety te są niezbędne do pracy ze skoroszytem, arkuszem kalkulacyjnym i tabelami.

## Krok 1: Skonfiguruj swój projekt

### Utwórz nowy projekt C#

Zacznij od utworzenia nowej aplikacji konsoli C# w Visual Studio. Nadaj swojemu projektowi odpowiednią nazwę, np. „ExcelDataImport”.

### Dodaj pakiet NuGet Aspose.Cells

Aby dodać pakiet Aspose.Cells, kliknij prawym przyciskiem myszy swój projekt w Solution Explorer, wybierz Manage NuGet Packages i wyszukaj „Aspose.Cells”. Zainstaluj pakiet, aby upewnić się, że masz dostęp do wszystkich potrzebnych nam funkcji.

## Krok 2: Zdefiniuj tabelę danych

 Następnie wdrożymy`ICellsDataTable` interfejs do tworzenia klasy, która dostarcza dane do zaimportowania. Oto jak możesz ustrukturyzować`CellsDataTable` klasa:

```csharp
class CellsDataTable : ICellsDataTable
{
    int m_index = -1;
    static String[] colsNames = new String[] { "Pet", "Fruit", "Country", "Color" };
    static String[] col0data = new String[] { "Dog", "Cat", "Duck" };
    static String[] col1data = new String[] { "Apple", "Pear", "Banana" };
    static String[] col2data = new String[] { "UK", "USA", "China" };
    static String[] col3data = new String[] { "Red", "Green", "Blue" };
    static String[][] colsData = new String[][] { col0data, col1data, col2data, col3data };
    
    // ... Wdrażanie innych członków ...
}
```

Tutaj definiujemy nazwy kolumn i dane dla każdej kolumny, co ułatwi utworzenie struktury zaimportowanej tabeli.

## Krok 3: Implementacja elementów interfejsu ICellsDataTable

 W ramach`CellsDataTable` klasa, musisz zaimplementować członków`ICellsDataTable` interfejs. Oto wymagana implementacja:

```csharp
public object this[string columnName]
{
    get
    {
        throw new NotImplementedException();
    }
}

object ICellsDataTable.this[int columnIndex]
{
    get
    {
        return colsData[columnIndex][m_index];
    }
}

string[] ICellsDataTable.Columns
{
    get { return colsNames; }
}

int ICellsDataTable.Count
{
    get { return col0data.Length; }
}

void ICellsDataTable.BeforeFirst()
{
    m_index = -1;
}

bool ICellsDataTable.Next()
{
    m_index++;
    return (m_index < Count);
}
```

Ta część klasy odpowiada za pobieranie danych, definiowanie liczby wierszy i kolumn oraz zarządzanie bieżącym stanem indeksu.

## Krok 4: Napisz funkcję główną

 Teraz utwórzmy`Run`metoda orkiestracji całego procesu importowania tabeli:

```csharp
public static void Run()
{
    string sourceDir = "Your Document Directory\\";
    string outputDir = "Your Document Directory\\";
    
    CellsDataTable cellsDataTable = new CellsDataTable();
    Workbook wb = new Workbook(sourceDir + "sampleImportTableOptionsShiftFirstRowDown.xlsx");
    Worksheet ws = wb.Worksheets[0];
```

## Krok 5: Ustaw opcje importu

 Aby kontrolować zachowanie importu, należy utworzyć wystąpienie`ImportTableOptions` i odpowiednio ustawić właściwości. Konkretnie chcemy ustawić`ShiftFirstRowDown` Do`false`.

```csharp
    ImportTableOptions opts = new ImportTableOptions();
    opts.ShiftFirstRowDown = false; // Nie chcemy przesuwać pierwszego rzędu w dół
```

## Krok 6: Importowanie tabeli danych

 Teraz możemy zaimportować dane z naszego`CellsDataTable` do arkusza kalkulacyjnego.

```csharp
    ws.Cells.ImportData(cellsDataTable, 2, 2, opts);
}
```

To polecenie spowoduje bezpośrednie wstawienie tabeli danych, zaczynając od określonego wiersza i kolumny.

## Krok 7: Zapisz skoroszyt

Na koniec zapiszemy zmodyfikowany skoroszyt z powrotem do pliku:

```csharp
    wb.Save(outputDir + "outputImportTableOptionsShiftFirstRowDown-False.xlsx");
}
```

## Wniosek

I masz to! Nauczyłeś się, jak wstawiać wiersze DataTable do arkusza Excela bez przenoszenia pierwszego wiersza za pomocą Aspose.Cells dla .NET. Ten proces nie tylko usprawnia manipulację danymi w programie Excel, ale także zwiększa wydajność aplikacji, automatyzując zazwyczaj uciążliwe zadanie. Mając tę wiedzę w swoim zestawie narzędzi, jesteś lepiej przygotowany do obsługi zadań automatyzacji programu Excel, oszczędzając czas i wysiłek.

## Najczęściej zadawane pytania

### Czym jest Aspose.Cells dla .NET?
Aspose.Cells for .NET to biblioteka programistyczna umożliwiająca programistom tworzenie, edytowanie i konwertowanie plików Excel w aplikacjach .NET.

### Czy potrzebuję licencji, aby korzystać z Aspose.Cells?
Tak, będziesz potrzebować ważnej licencji, aby korzystać z pełnych funkcji. Jednak bezpłatna wersja próbna jest dostępna do wstępnego testowania.

### Czy mogę używać Aspose.Cells w aplikacjach internetowych?
Oczywiście! Aspose.Cells jest idealny dla aplikacji desktopowych, internetowych i chmurowych opracowanych w .NET.

### Jakie typy plików Excel mogę utworzyć za pomocą Aspose.Cells?
Możesz tworzyć różnorodne formaty plików Excel, w tym XLSX, XLS, CSV i inne.

### Gdzie mogę uzyskać pomoc dotyczącą Aspose.Cells?
 Możesz zadać pytania lub znaleźć pomoc w[Fora Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
