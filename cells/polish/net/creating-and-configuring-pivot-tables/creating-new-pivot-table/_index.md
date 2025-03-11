---
title: Utwórz nową tabelę przestawną programowo w .NET
linktitle: Utwórz nową tabelę przestawną programowo w .NET
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Naucz się programowo tworzyć tabelę przestawną w .NET przy użyciu Aspose.Cells dzięki naszemu przewodnikowi krok po kroku. Efektywnie analizuj swoje dane.
weight: 13
url: /pl/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz nową tabelę przestawną programowo w .NET

## Wstęp
Tworzenie tabeli przestawnej może wydawać się przerażającym zadaniem, zwłaszcza gdy robisz to programowo. Ale nie obawiaj się! Dzięki Aspose.Cells dla .NET tworzenie tabeli przestawnej jest nie tylko proste, ale także bardzo skuteczne w analizie danych. W tym samouczku krok po kroku przeprowadzimy Cię przez proces tworzenia nowej tabeli przestawnej w aplikacji .NET. Niezależnie od tego, czy dodajesz dane dotyczące sprzedaży, sportu czy innych wskaźników biznesowych, ten przewodnik pomoże Ci uruchomić tabele przestawne w mgnieniu oka.

## Wymagania wstępne
Zanim się za to zabierzemy, upewnijmy się, że wszystko jest gotowe. Oto, co musisz zrobić:

1. Zainstaluj .NET Framework: Upewnij się, że masz zainstalowany .NET Framework na swoim komputerze. Aspose.Cells obsługuje różne wersje, ale najlepiej jest trzymać się najnowszej.
2.  Biblioteka Aspose.Cells: Musisz mieć bibliotekę Aspose.Cells. Możesz[pobierz tutaj](https://releases.aspose.com/cells/net/)lub zdobądź[licencja tymczasowa](https://purchase.aspose.com/temporary-license/) do oceny.
3. Konfiguracja środowiska IDE: Przygotuj środowisko IDE zgodne z językiem C#, np. Visual Studio, w którym możesz rozpocząć nowy projekt.
4. Podstawowa znajomość języka C#: Znajomość programowania w języku C# pomoże Ci nadążać za nauką, bez popadania w rutynę.

Wszystko gotowe? Świetnie! Przejdźmy do importowania niezbędnych pakietów.

## Importuj pakiety
Po pierwsze, musisz zaimportować wymagane przestrzenie nazw do swojego projektu C#. Otwórz plik C# i dodaj następujące dyrektywy using:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Te przestrzenie nazw zapewniają dostęp do funkcji skoroszytu, arkusza kalkulacyjnego i tabeli przestawnej, z których będziemy korzystać w tym samouczku.

## Krok 1: Utwórz obiekt skoroszytu
Utworzenie skoroszytu to początek Twojej podróży. Zacznijmy od utworzenia nowego skoroszytu i uzyskania dostępu do pierwszego arkusza.

```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";
// Tworzenie instancji obiektu skoroszytu
Workbook workbook = new Workbook();

// Uzyskanie odniesienia do nowo dodanego arkusza kalkulacyjnego
Worksheet sheet = workbook.Worksheets[0];
```

 W tym kroku tworzymy`Workbook`wystąpienie reprezentujące nasz plik Excel i pobrać pierwszy arkusz kalkulacyjny, który będzie naszym placem zabaw dla tabeli przestawnej.

## Krok 2: Wprowadź dane do komórek
Następnie wypełnijmy nasz arkusz przykładowymi danymi. Wprowadzimy wiersze dla różnych sportów, kwartałów i danych sprzedaży, aby dać naszej tabeli przestawnej coś do podsumowania.

```csharp
Cells cells = sheet.Cells;

// Ustawianie wartości komórek
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

// Wypełnianie komórki danych = cells["A2"];
cell.PutValue("Golf");
// ... Więcej wpisów danych
```

Tutaj definiujemy nasze nagłówki kolumn i wstawiamy wartości pod każdym nagłówkiem. Te dane będą stanowić źródło dla naszej tabeli przestawnej, więc upewnij się, że jest uporządkowana! Przejdź przez ten blok, a utworzysz kompleksowy zestaw danych.

## Krok 3: Dodawanie tabeli przestawnej
Mając gotowe dane, czas utworzyć tabelę przestawną. Użyjemy kolekcji tabel przestawnych z arkusza kalkulacyjnego, aby dodać naszą nową tabelę przestawną.

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// Dodawanie tabeli przestawnej do arkusza kalkulacyjnego
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

tym fragmencie kodu dodajemy tabelę przestawną do arkusza kalkulacyjnego, która odwołuje się do naszego zakresu danych (w tym przypadku komórki A1 do C8). Umieszczamy tabelę przestawną zaczynając od komórki E3 i nazywamy ją „PivotTable2”. Całkiem proste, prawda?

## Krok 4: Dostosuj tabelę przestawną
Teraz, gdy mamy naszą tabelę przestawną, dostosujmy ją, aby pokazywała znaczące podsumowania. Możemy kontrolować, co pojawia się w wierszach, kolumnach i obszarach danych tabeli przestawnej.

```csharp
// Uzyskiwanie dostępu do wystąpienia nowo dodanej tabeli przestawnej
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

// Niewyświetlanie sum całkowitych dla wierszy.
pivotTable.RowGrand = false;

// Przeciąganie pierwszego pola do obszaru wiersza.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

// Przeciągnij drugie pole do obszaru kolumny.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

// Przeciąganie trzeciego pola do obszaru danych.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

W tym kroku informujemy tabelę przestawną, aby ukryła sumy całkowite dla wierszy, a następnie określamy, które pola mają znaleźć się w obszarach wierszy, kolumn i danych. Nazwy sportów wypełnią wiersze, kwartały wypełnią kolumny, a dane sprzedaży zapewnią podsumowania.

## Krok 5: Zapisz skoroszyt
Na koniec chcemy zapisać nowo utworzony skoroszyt, aby zobaczyć owoce naszej pracy.

```csharp
// Zapisywanie pliku Excel
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

Wystarczy, że podasz właściwą ścieżkę, a dane wyjściowe tabeli przestawnej zostaną zapisane w pliku Excel, który możesz otworzyć i przejrzeć.

## Wniosek
Tworzenie tabel przestawnych programowo przy użyciu Aspose.Cells dla .NET może znacznie zaoszczędzić czas, zwłaszcza w przypadku dużych zestawów danych. Nauczyłeś się, jak skonfigurować projekt, zaimportować niezbędne pakiety, wypełnić dane i utworzyć od podstaw konfigurowalną tabelę przestawną. Więc następnym razem, gdy będziesz tonąć w liczbach, zapamiętaj ten samouczek i pozwól Aspose.Cells wykonać ciężką pracę za Ciebie.

## Najczęściej zadawane pytania
### Czym jest Aspose.Cells?
Aspose.Cells to zaawansowana biblioteka .NET umożliwiająca programowe tworzenie i zarządzanie arkuszami kalkulacyjnymi programu Excel.

### Czy istnieje bezpłatna wersja próbna Aspose.Cells?
 Tak, możesz otrzymać bezpłatną wersję próbną[Tutaj](https://releases.aspose.com/).

### Czy mogę dostosować wygląd tabeli przestawnej?
Oczywiście! Możesz dostosować formatowanie, układ, a nawet style tabeli przestawnej według swoich potrzeb.

### Gdzie mogę znaleźć więcej przykładów i dokumentacji dotyczącej Aspose.Cells?
 Możesz sprawdzić[dokumentacja](https://reference.aspose.com/cells/net/) aby uzyskać kompleksowe przewodniki i przykłady.

### Jak uzyskać pomoc techniczną dotyczącą Aspose.Cells?
 Możesz uzyskać wsparcie poprzez[Forum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
