---
title: Określanie zgodności pliku Excel programowo w środowisku .NET
linktitle: Określanie zgodności pliku Excel programowo w środowisku .NET
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Naucz się manipulować tabelami przestawnymi programu Excel za pomocą Aspose.Cells dla platformy .NET, obejmującymi aktualizacje danych, ustawienia zgodności i formatowanie komórek.
weight: 23
url: /pl/net/creating-and-configuring-pivot-tables/specifying-compatibility/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Określanie zgodności pliku Excel programowo w środowisku .NET

## Wstęp

dzisiejszym świecie zorientowanym na dane, zarządzanie i manipulowanie plikami Excela programowo stało się niezbędne dla wielu programistów. Jeśli pracujesz z Excelem w .NET, Aspose.Cells to potężna biblioteka, która ułatwia tworzenie, odczytywanie, modyfikowanie i zapisywanie plików Excela. Jedna z ważnych funkcji tej biblioteki pozwala programowo określić zgodność plików Excela. W tym samouczku zbadamy, jak manipulować plikami Excela, skupiając się szczególnie na zarządzaniu zgodnością za pomocą Aspose.Cells dla .NET. Na koniec zrozumiesz, jak ustawić zgodność plików Excela, zwłaszcza tabel przestawnych, podczas odświeżania i zarządzania danymi.

## Wymagania wstępne

Zanim przejdziesz do fazy kodowania, upewnij się, że masz następujące rzeczy:

1. Podstawowa znajomość języka C#: Ponieważ będziemy pisać kod w języku C#, znajomość tego języka pomoże Ci lepiej zrozumieć ten samouczek.
2.  Biblioteka Aspose.Cells dla .NET: Można ją pobrać ze strony[Strona wydań Aspose Cells](https://releases.aspose.com/cells/net/)Jeśli jeszcze tego nie zrobiłeś, rozważ skorzystanie z bezpłatnego okresu próbnego, aby najpierw poznać jego funkcje.
3. Visual Studio: środowisko IDE, w którym można efektywnie pisać i testować kod C#.
4.  Przykładowy plik Excela: Upewnij się, że masz przykładowy plik Excela, najlepiej taki, który zawiera tabelę przestawną dla demonstracji. W naszym przykładzie użyjemy`sample-pivot-table.xlsx`.

Mając te wymagania wstępne za sobą, możemy rozpocząć proces kodowania.

## Importuj pakiety

Zanim zaczniesz pisać swoją aplikację, musisz uwzględnić w kodzie niezbędne przestrzenie nazw, aby efektywnie wykorzystać bibliotekę Aspose.Cells. Oto, jak to zrobić.

### Importuj przestrzeń nazw Aspose.Cells

```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Pivot;
using System.Drawing;
```

Ten wiersz kodu zapewnia dostęp do wszystkich klas i metod w bibliotece Aspose.Cells.

Teraz przeanalizujmy ten proces szczegółowo, aby wszystko było jasne i zrozumiałe.

## Krok 1: Skonfiguruj swój katalog

Po pierwsze, skonfiguruj katalog, w którym znajdują się pliki Excela. Ważne jest, aby podać właściwą ścieżkę do pliku.

```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";
```

 Tutaj zamień`"Your Document Directory"` rzeczywistą ścieżką do plików Excel. To tutaj powinien znajdować się przykładowy plik tabeli przestawnej.

## Krok 2: Załaduj plik źródłowy Excel

Następnie musimy załadować plik Excela zawierający przykładową tabelę przestawną. 

```csharp
// Załaduj plik źródłowy programu Excel zawierający przykładową tabelę przestawną
Workbook wb = new Workbook(dataDir + "sample-pivot-table.xlsx");
```

 W tym kroku tworzymy instancję`Workbook` Klasa, która ładuje określony plik Excel. 

## Krok 3: Uzyskaj dostęp do arkuszy kalkulacyjnych

Po załadowaniu skoroszytu należy uzyskać dostęp do arkusza zawierającego dane tabeli przestawnej.

```csharp
// Uzyskaj dostęp do pierwszego arkusza kalkulacyjnego zawierającego dane tabeli przestawnej
Worksheet dataSheet = wb.Worksheets[0];
```

Tutaj uzyskujemy dostęp do pierwszego arkusza kalkulacyjnego, w którym znajduje się tabela przestawna. Możesz również przejść przez pętlę lub określić inne arkusze kalkulacyjne na podstawie struktury programu Excel.

## Krok 4: Manipulowanie danymi komórkowymi

Następnie zmodyfikujesz niektóre wartości komórek w arkuszu kalkulacyjnym. 

### Krok 4.1: Modyfikuj komórkę A3

Zacznijmy od uzyskania dostępu do komórki A3 i ustawienia jej wartości.

```csharp
// Uzyskaj dostęp do komórki A3 i ustaw jej dane
Cells cells = dataSheet.Cells;
Cell cell = cells["A3"];
cell.PutValue("FooBar");
```

Ten fragment kodu aktualizuje komórkę A3 wartością „FooBar”.

### Krok 4.2: Modyfikuj komórkę B3 za pomocą długiego ciągu

Teraz wpiszmy do komórki B3 długi ciąg znaków, przekraczający standardowe limity znaków programu Excel.

```csharp
// Uzyskaj dostęp do komórki B3 i ustaw jej dane
string longStr = "Very long text 1. very long text 2.... [continue your long string]";
cell = cells["B3"];
cell.PutValue(longStr);
```

Kod ten jest istotny, ponieważ określa oczekiwania dotyczące limitów danych, zwłaszcza podczas pracy z ustawieniami zgodności w programie Excel.

## Krok 5: Sprawdź długość komórki B3

Ważne jest również potwierdzenie długości wprowadzonego ciągu znaków.

```csharp
// Wydrukuj długość ciągu komórki B3
Console.WriteLine("Length of original data string: " + cell.StringValue.Length);
```

Służy to jedynie do weryfikacji, ile znaków mieści się w Twojej komórce.

## Krok 6: Ustaw inne wartości komórek

Teraz uzyskamy dostęp do większej liczby komórek i ustawimy pewne wartości.

```csharp
// Uzyskaj dostęp do komórki C3 i ustaw jej dane
cell = cells["C3"];
cell.PutValue("closed");

// Uzyskaj dostęp do komórki D3 i ustaw jej dane
cell = cells["D3"];
cell.PutValue("2016/07/21");
```

Każdy z tych fragmentów kodu aktualizuje kilka dodatkowych komórek w arkuszu kalkulacyjnym.

## Krok 7: Uzyskaj dostęp do tabeli przestawnej

Następnie uzyskasz dostęp do drugiego arkusza, który zawiera dane tabeli przestawnej.

```csharp
//Uzyskaj dostęp do drugiego arkusza zawierającego tabelę przestawną
Worksheet pivotSheet = wb.Worksheets[1];

// Uzyskaj dostęp do tabeli przestawnej
PivotTable pivotTable = pivotSheet.PivotTables[0];
```

Ten fragment kodu umożliwia manipulowanie tabelą przestawną w celu uzyskania ustawień zgodności.

## Krok 8: Ustaw zgodność dla programu Excel 2003

Istotne jest określenie, czy tabela przestawna jest zgodna z programem Excel 2003, czy nie. 

```csharp
// Właściwość IsExcel2003Compatible informuje, czy tabela przestawna jest zgodna z programem Excel 2003 podczas odświeżania tabeli przestawnej
pivotTable.IsExcel2003Compatible = true;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

 To tutaj zaczyna się prawdziwa transformacja. Poprzez ustawienie`IsExcel2003Compatible` Do`true`, podczas odświeżania ograniczasz długość znaków do 255.

## Krok 9: Sprawdź długość po ustawieniu zgodności

Po ustawieniu zgodności sprawdźmy, jak wpłynie to na dane.

```csharp
// Sprawdź wartość komórki B5 arkusza przestawnego.
Cell b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to True: " + b5.StringValue.Length);
```

Prawdopodobnie zobaczysz wynik potwierdzający efekt obcięcia, jeśli początkowe dane przekroczą 255 znaków.

## Krok 10: Zmień ustawienia zgodności

Teraz zmieńmy ustawienia zgodności i sprawdźmy ponownie.

```csharp
//Teraz ustaw właściwość IsExcel2003Compatible na false i ponownie odśwież
pivotTable.IsExcel2003Compatible = false;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

Dzięki temu Twoje dane będą miały oryginalną długość, bez wcześniejszych ograniczeń.

## Krok 11: Ponownie sprawdź długość 

Sprawdźmy, czy dane teraz dokładnie odzwierciedlają jego rzeczywistą długość.

```csharp
// Teraz wydrukuje oryginalną długość danych komórki. Dane nie zostały już obcięte.
b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to False: " + b5.StringValue.Length);
```

Powinieneś zobaczyć, że wynik potwierdza usunięcie obcięcia.

## Krok 12: Formatowanie komórek

Aby poprawić wrażenia wizualne, możesz sformatować komórki. 

```csharp
// Ustaw wysokość wiersza i szerokość kolumny komórki B5, a także zawiń jej tekst
pivotSheet.Cells.SetRowHeight(b5.Row, 100);
pivotSheet.Cells.SetColumnWidth(b5.Column, 65);
Style st = b5.GetStyle();
st.IsTextWrapped = true;
b5.SetStyle(st);
```

Te wiersze kodu ułatwiają odczytywanie danych, dostosowując wymiary komórek i włączając zawijanie tekstu.

## Krok 13: Zapisz skoroszyt

Na koniec zapisz skoroszyt ze zmianami, które wprowadziłeś.

```csharp
// Zapisz skoroszyt w formacie xlsx
wb.Save(dataDir + "SpecifyCompatibility_out.xlsx", SaveFormat.Xlsx);
```

 Wybór odpowiedniego formatu pliku jest kluczowy przy zapisywaniu plików Excel.`Xlsx`Format ten jest powszechnie używany i kompatybilny z wieloma wersjami programu Excel.

## Wniosek

Gratulacje! Zaprogramowałeś ustawienia zgodności plików Excela za pomocą Aspose.Cells dla .NET. W tym samouczku opisano każdy krok, od konfiguracji środowiska po zmianę ustawień zgodności dla tabel przestawnych. Jeśli kiedykolwiek pracowałeś z danymi, które wymagały określonych ograniczeń lub zgodności, jest to umiejętność, której nie powinieneś przegapić.

## Najczęściej zadawane pytania

### Czym jest Aspose.Cells?  
Aspose.Cells to biblioteka .NET zaprojektowana, aby ułatwić programistom bezproblemowe tworzenie, edytowanie i konwertowanie plików Excel.

### Dlaczego zgodność z programem Excel jest ważna?  
Zgodność z programem Excel jest kluczowa, ponieważ pozwala mieć pewność, że pliki będzie można otwierać i używać w zamierzonych wersjach programu Excel, zwłaszcza jeśli zawierają funkcje lub formaty nieobsługiwane we wcześniejszych wersjach.

### Czy mogę programowo tworzyć tabele przestawne za pomocą Aspose.Cells?  
Tak, możesz tworzyć i manipulować tabelami przestawnymi programowo, używając Aspose.Cells. Biblioteka udostępnia różne metody dodawania źródeł danych, pól i funkcji powiązanych z tabelami przestawnymi.

### Jak sprawdzić długość ciągu znaków w komórce programu Excel?  
Możesz użyć`StringValue` własność`Cell` obiekt, aby pobrać zawartość komórki, a następnie wywołać`.Length` właściwość pozwalająca na ustalenie długości ciągu.

### Czy mogę dostosować formatowanie komórek poza wysokością i szerokością wiersza?  
 Oczywiście! Aspose.Cells umożliwia rozbudowane formatowanie komórek. Możesz zmieniać style czcionek, kolory, obramowania, formaty liczb i wiele więcej za pomocą`Style` klasa.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
