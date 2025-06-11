---
"description": "Dowiedz się, jak przekonwertować arkusz kalkulacyjny programu Excel do formatu SVG za pomocą Aspose.Cells dla platformy .NET, korzystając z tego przewodnika krok po kroku. Idealne dla programistów .NET, którzy chcą renderować arkusz programu Excel do formatu SVG."
"linktitle": "Konwersja arkusza kalkulacyjnego do formatu SVG w .NET"
"second_title": "Aspose.Cells .NET API przetwarzania programu Excel"
"title": "Konwersja arkusza kalkulacyjnego do formatu SVG w .NET"
"url": "/pl/net/conversion-and-rendering/converting-worksheet-to-svg/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Konwersja arkusza kalkulacyjnego do formatu SVG w .NET

## Wstęp

Jeśli chcesz przekonwertować arkusz kalkulacyjny programu Excel na format SVG, trafiłeś we właściwe miejsce! Aspose.Cells for .NET to potężne narzędzie, które umożliwia programistom manipulowanie plikami programu Excel i konwertowanie ich do różnych formatów, w tym szeroko obsługiwanego SVG (Scalable Vector Graphics). Ten samouczek przeprowadzi Cię przez proces konwersji arkusza kalkulacyjnego na SVG w .NET, rozkładając go krok po kroku, dzięki czemu nawet początkujący mogą z łatwością go śledzić.

## Wymagania wstępne

Zanim zagłębisz się w kod, upewnijmy się, że masz wszystko, czego potrzebujesz:

1. Aspose.Cells dla .NET: Pobierz i zainstaluj najnowszą wersję Aspose.Cells dla .NET ze strony [Aspose.Cells dla .NET](https://releases.aspose.com/cells/net/).
2. Środowisko programistyczne .NET: Będziesz potrzebować zainstalowanego programu Visual Studio lub innego środowiska IDE .NET.
3. Podstawowa znajomość języka C#: Znajomość języka C# jest wymagana, ale nie martw się, wszystko jasno wyjaśnimy.
4. Plik Excela: Przygotuj plik Excela, który chcesz przekonwertować do formatu SVG.

## Importowanie niezbędnych pakietów

Zanim zaczniesz kodować, upewnij się, że na początku pliku C# uwzględniłeś wymagane przestrzenie nazw.

```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```

Pakiety te są niezbędne do pracy z Aspose.Cells i obsługi opcji renderowania, takich jak eksport do formatu SVG.

Teraz, gdy omówiliśmy podstawy, możemy przejść do konkretnych kroków konwersji arkusza kalkulacyjnego programu Excel na obraz SVG.

## Krok 1: Ustaw ścieżkę do katalogu dokumentów

Pierwszą rzeczą, której potrzebujemy, jest zdefiniowanie ścieżki do folderu, w którym znajduje się plik Excel. Jest to kluczowe, ponieważ kod będzie odwoływał się do katalogu, aby ładować i zapisywać pliki.

```csharp
// Ścieżka do katalogu dokumentów
string dataDir = "Your Document Directory";
```

Pamiętaj o wymianie `"Your Document Directory"` z rzeczywistą ścieżką, w której znajduje się plik Excel.

## Krok 2: Załaduj plik Excela za pomocą `Workbook`

Następnie musimy załadować plik Excela do instancji `Workbook` Klasa. `Workbook` Klasa reprezentuje cały plik Excela, łącznie ze wszystkimi arkuszami kalkulacyjnymi w nim zawartymi.

```csharp
string filePath = dataDir + "Template.xlsx";
Workbook book = new Workbook(filePath);
```

Tutaj, `"Template.xlsx"` jest nazwą pliku Excel, z którym pracujesz. Upewnij się, że ten plik istnieje w określonym katalogu, w przeciwnym razie wystąpią błędy.

## Krok 3: Ustaw opcje obrazu lub wydruku dla konwersji SVG

Zanim będziemy mogli przekonwertować arkusz kalkulacyjny do formatu SVG, musimy określić opcje obrazu. `ImageOrPrintOptions` Klasa pozwala kontrolować sposób konwersji arkusza kalkulacyjnego. Konkretnie, musimy ustawić `SaveFormat` Do `SVG` i upewnij się, że każdy arkusz kalkulacyjny zostanie przekonwertowany na pojedynczą stronę.

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.SaveFormat = SaveFormat.Svg;
imgOptions.OnePagePerSheet = true;
```

Ten `SaveFormat.Svg` opcja zapewnia, że formatem wyjściowym będzie SVG, podczas gdy `OnePagePerSheet` zapewnia, że każdy arkusz kalkulacyjny będzie renderowany na pojedynczej stronie.

## Krok 4: Przejrzyj każdy arkusz w skoroszycie

Teraz musimy przejść przez wszystkie arkusze w pliku Excel. Każdy arkusz zostanie przekonwertowany indywidualnie.

```csharp
foreach (Worksheet sheet in book.Worksheets)
{
    // Przetworzymy każdy arkusz kalkulacyjny osobno
}
```

Pętla ta zapewnia, że niezależnie od liczby arkuszy w skoroszycie, każdy z nich zostanie obsłużony.

## Krok 5: Utwórz `SheetRender` Obiekt do renderowania

Dla każdego arkusza roboczego utworzymy `SheetRender` obiekt. Ten obiekt jest odpowiedzialny za konwersję arkusza kalkulacyjnego do pożądanego formatu obrazu, którym w tym przypadku jest SVG.

```csharp
SheetRender sr = new SheetRender(sheet, imgOptions);
```

Ten `SheetRender` Obiekt przyjmuje dwa argumenty: arkusz kalkulacyjny, który konwertujesz i opcje obrazu, które zdefiniowałeś wcześniej.

## Krok 6: Konwertuj arkusz kalkulacyjny do formatu SVG

Na koniec, w pętli, przekonwertujemy każdy arkusz roboczy do formatu SVG. Używamy zagnieżdżonej pętli, aby przejść przez strony (chociaż w tym przypadku jest tylko jedna strona na arkusz roboczy, dzięki `OnePagePerSheet` opcja).

```csharp
for (int i = 0; i < sr.PageCount; i++)
{
    // Wyeksportuj arkusz do formatu obrazu SVG
    sr.ToImage(i, filePath + sheet.Name + i + ".out.svg");
}
```

Ten kod zapisze arkusz jako plik SVG w tym samym katalogu co plik Excel. Każdy plik SVG zostanie nazwany zgodnie z nazwą arkusza i numerem indeksu, aby uniknąć konfliktów nazw.

## Wniosek

to wszystko! Udało Ci się przekonwertować arkusz kalkulacyjny programu Excel do formatu SVG przy użyciu Aspose.Cells dla .NET. Ten proces pozwala Ci zachować układ i projekt arkusza kalkulacyjnego, jednocześnie umożliwiając jego wyświetlanie w dowolnej przeglądarce lub urządzeniu obsługującym SVG, czyli w zasadzie we wszystkich. Niezależnie od tego, czy pracujesz ze złożonymi plikami programu Excel, czy po prostu prostą tabelą, ta metoda zapewnia, że Twoje dane są pięknie renderowane w formacie przyjaznym dla sieci.

## Najczęściej zadawane pytania

### Czym jest SVG i dlaczego warto go używać?
SVG (Scalable Vector Graphics) to przyjazny dla sieci format, który można skalować w nieskończoność bez utraty jakości. Jest idealny do wykresów, diagramów i obrazów, które muszą być wyświetlane w różnych rozmiarach.

### Czy Aspose.Cells obsługuje konwersję dużych plików Excela?
Tak, Aspose.Cells może wydajnie obsługiwać duże pliki Excela i konwertować je do formatu SVG bez większych problemów z wydajnością.

### Czy liczba arkuszy, które mogę przekonwertować do formatu SVG, jest ograniczona?
Nie, w Aspose.Cells nie ma wrodzonego limitu konwersji wielu arkuszy kalkulacyjnych. Jedynym ograniczeniem byłaby pamięć i wydajność systemu.

### Czy potrzebuję licencji, aby korzystać z Aspose.Cells?
Tak, Aspose.Cells wymaga licencji do użytku produkcyjnego. Możesz uzyskać tymczasową licencję [Tutaj](https://purchase.aspose.com/temporary-license/) lub odkryj [bezpłatny okres próbny](https://releases.aspose.com/).

### Czy mogę dostosować plik wyjściowy SVG?
Tak, możesz to zmienić `ImageOrPrintOptions` aby dostosować różne aspekty wyjścia SVG, takie jak rozdzielczość i skalowanie.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}