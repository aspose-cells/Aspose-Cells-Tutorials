---
title: Dodaj kontrolkę TextBox do wykresu
linktitle: Dodaj kontrolkę TextBox do wykresu
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak dodać pole tekstowe do wykresów w programie Excel za pomocą Aspose.Cells dla platformy .NET. Ulepsz wizualizację danych bez wysiłku.
weight: 12
url: /pl/net/inserting-controls-in-charts/add-textbox-control-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj kontrolkę TextBox do wykresu

## Wstęp

Tworzenie dynamicznych i wizualnie atrakcyjnych wykresów w programie Excel to fantastyczny sposób na skuteczne przedstawienie danych. Jedną z przydatnych funkcji, z których możesz skorzystać, jest dodanie pola tekstowego do wykresu. Dzięki Aspose.Cells dla .NET to zadanie staje się łatwe i przyjemne! W tym przewodniku przeprowadzimy Cię przez proces integrowania pola tekstowego z wykresem krok po kroku. Niezależnie od tego, czy jesteś doświadczonym programistą, czy dopiero zaczynasz, ten samouczek zapewni Ci wszystkie narzędzia potrzebne do ulepszenia wykresów w programie Excel. Więc jesteś gotowy, aby się zanurzyć?

## Wymagania wstępne

Zanim przejdziemy do kodowania, jest kilka rzeczy, które powinieneś mieć na miejscu:

- Podstawowa znajomość języka C#: podstawowa znajomość programowania w języku C# będzie pomocna. Nie martw się; nie musisz być ekspertem, wystarczy, że będziesz swobodnie poruszać się po składni.
-  Zainstalowana biblioteka Aspose.Cells: Upewnij się, że masz zainstalowaną bibliotekę Aspose.Cells dla .NET. Możesz ją pobrać z[Tutaj](https://releases.aspose.com/cells/net/) jeśli jeszcze tego nie zrobiłeś.
- Visual Studio: Znajomość programu Visual Studio lub dowolnego środowiska IDE preferowanego do obsługi platformy .NET jest niezbędna.
- Istniejący plik Excela: W tym przykładzie będziemy pracować z istniejącym plikiem Excela o nazwie „sampleAddingTextBoxControlInChart.xls”. Możesz utworzyć plik lub pobrać próbkę.

Teraz, gdy wszystko mamy już gotowe, możemy zająć się kodowaniem!

## Importuj pakiety

Po pierwsze, musimy zaimportować niezbędne przestrzenie nazw Aspose.Cells do naszego projektu C#. Możesz to zrobić łatwo, umieszczając następujące wiersze na górze pliku kodu:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using System.Drawing;
```

## Krok 1: Zdefiniuj katalogi źródłowe i wyjściowe

Zanim zaczniemy pracę z plikiem Excel, ważne jest, aby określić, gdzie znajduje się plik wejściowy i gdzie chcesz zapisać plik wyjściowy. Pomaga to w utrzymaniu porządku w projekcie.

```csharp
// Katalog źródłowy
string sourceDir = "Your Document Directory";

// Katalog wyjściowy
string outputDir = "Your Output Directory";
```
 Zastępować`"Your Document Directory"` I`"Your Output Directory"` z rzeczywistymi ścieżkami w Twoim systemie.

## Krok 2: Otwórz istniejący plik Excel

Następnie musimy otworzyć plik Excel zawierający wykres, który chcemy zmodyfikować. Pozwoli nam to pobrać wykres i wprowadzić zmiany.

```csharp
// Otwórz istniejący plik.
Workbook workbook = new Workbook(sourceDir + "sampleAddingTextBoxControlInChart.xls");
```
Ten wiersz inicjuje nowy obiekt Workbook z podanym przez nas plikiem.

## Krok 3: Uzyskaj dostęp do wykresu w arkuszu kalkulacyjnym

Ponieważ wykresy w programie Excel są przechowywane w arkuszu kalkulacyjnym, musimy najpierw uzyskać dostęp do arkusza kalkulacyjnego, a następnie uzyskać pożądany wykres. W tym przykładzie uzyskamy dostęp do pierwszego wykresu w pierwszym arkuszu kalkulacyjnym.

```csharp
// W pierwszym arkuszu pobierz wykres projektanta.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```
Zmieniając wartość indeksu, możesz wybrać inne arkusze kalkulacyjne lub wykresy, jeśli plik zawiera ich więcej.

## Krok 4: Dodaj nowe pole tekstowe do wykresu

Teraz jesteśmy gotowi, aby dodać nasz TextBox. Określimy jego pozycję i rozmiar podczas tworzenia.

```csharp
// Dodaj nowe pole tekstowe do wykresu.
Aspose.Cells.Drawing.TextBox textbox0 = chart.Shapes.AddTextBoxInChart(400, 1100, 350, 2550);
```
tym poleceniu parametry definiują lokalizację (x, y) i rozmiar (szerokość, wysokość) pola tekstowego na wykresie. Dostosuj te wartości w oparciu o swoje konkretne potrzeby układu.

## Krok 5: Ustaw tekst dla pola tekstowego

Gdy TextBox jest już na swoim miejscu, czas wypełnić go treścią. Możesz dodać dowolny tekst, który uznasz za niezbędny dla swojego wykresu.

```csharp
// Wypełnij tekst.
textbox0.Text = "Sales By Region";
```
Możesz zastąpić frazę „Sprzedaż według regionu” dowolnym tekstem związanym z Twoimi danymi.

## Krok 6: Dostosuj właściwości pola tekstowego

Teraz sprawmy, aby nasz TextBox wyglądał dobrze! Możesz dostosować różne właściwości, takie jak kolor czcionki, rozmiar i styl.

```csharp
// Ustaw kolor czcionki.
textbox0.Font.Color = Color.Maroon; // Zmień na wybrany kolor

// Ustaw czcionkę na pogrubioną.
textbox0.Font.IsBold = true;

// Ustaw rozmiar czcionki.
textbox0.Font.Size = 14;

// Ustaw atrybut czcionki na kursywę.
textbox0.Font.IsItalic = true;
```

Każdy z tych wierszy modyfikuje wygląd tekstu wewnątrz pola tekstowego, zwiększając jego widoczność i atrakcyjność.

## Krok 7: Formatowanie wyglądu pola tekstowego

Ważne jest również sformatowanie tła i obramowania pola tekstowego. Dzięki temu wyróżnia się ono na wykresie.

```csharp
// Pobierz format wypełnienia pola tekstowego.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;

// Pobierz typ formatu linii pola tekstowego.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;

// Ustaw grubość linii.
lineformat.Weight = 2;

// Ustaw styl myślnika na ciągły.
lineformat.DashStyle = Aspose.Cells.Drawing.MsoLineDashStyle.Solid;
```

Opcje te umożliwiają ustawienie wypełnienia tła pola tekstowego i dostosowanie jego obramowania.

## Krok 8: Zapisz zmodyfikowany plik Excela

Ostatnim krokiem jest zapisanie zmian, które wprowadziłeś do nowego pliku Excel. Dzięki temu oryginalny plik pozostanie nietknięty.

```csharp
// Zapisz plik Excela.
workbook.Save(outputDir + "outputAddingTextBoxControlInChart.xls");
```
 Zastępować`"outputAddingTextBoxControlInChart.xls"` z dowolną nazwą pliku.

## Wniosek

Gratulacje! Udało Ci się dodać kontrolkę TextBox do wykresu przy użyciu Aspose.Cells dla .NET. Ta prosta, ale skuteczna zmiana może sprawić, że Twoje wykresy będą bardziej informacyjne i atrakcyjne wizualnie. Reprezentacja danych jest kluczem do skutecznej komunikacji, a dzięki narzędziom takim jak Aspose masz możliwość ulepszenia tej prezentacji przy minimalnym wysiłku.

## Najczęściej zadawane pytania

### Czym jest Aspose.Cells dla .NET?
Aspose.Cells for .NET to zaawansowana biblioteka umożliwiająca tworzenie, edytowanie i konwertowanie plików Excel bez konieczności korzystania z programu Microsoft Excel.

### Czy mogę dodać wiele pól tekstowych do jednego wykresu?
Tak! Możesz dodać tyle TextBoxów, ile potrzebujesz, powtarzając kroki tworzenia TextBoxów z różnymi pozycjami.

### Czy korzystanie z Aspose.Cells jest bezpłatne?
Aspose.Cells to płatna biblioteka, ale możesz pobrać bezpłatną wersję próbną ze strony[Tutaj](https://releases.aspose.com/).

### Gdzie mogę znaleźć więcej dokumentacji na temat Aspose.Cells?
 Możesz uzyskać dostęp do kompleksowej dokumentacji[Tutaj](https://reference.aspose.com/cells/net/).

### Gdzie mogę uzyskać pomoc, jeśli napotkam problemy?
 Możesz szukać pomocy na forum pomocy technicznej Aspose[Tutaj](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
