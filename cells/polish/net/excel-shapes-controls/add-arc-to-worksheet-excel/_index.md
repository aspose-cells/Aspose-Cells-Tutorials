---
title: Dodaj łuk do arkusza kalkulacyjnego w programie Excel
linktitle: Dodaj łuk do arkusza kalkulacyjnego w programie Excel
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Naucz się dodawać łuki do arkuszy kalkulacyjnych programu Excel za pomocą Aspose.Cells dla .NET. Postępuj zgodnie z naszym przewodnikiem krok po kroku, aby ulepszyć projekty arkuszy kalkulacyjnych.
weight: 16
url: /pl/net/excel-shapes-controls/add-arc-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj łuk do arkusza kalkulacyjnego w programie Excel

## Wstęp
Tworzenie atrakcyjnych wizualnie arkuszy kalkulacyjnych programu Excel jest kluczowe dla prezentacji danych, a biblioteka Aspose.Cells zapewnia programistom solidne narzędzia do realizacji tego zadania. Jedną z interesujących funkcji, którą możesz chcieć włączyć do swoich dokumentów programu Excel, jest możliwość dodawania kształtów, takich jak łuki. W tym samouczku przeprowadzimy krok po kroku, jak dodawać łuki do arkusza kalkulacyjnego programu Excel przy użyciu Aspose.Cells dla .NET. Do końca tego artykułu nie tylko nauczysz się, jak dodawać łuki, ale także uzyskasz wgląd w zarządzanie kształtami w ogóle.
## Wymagania wstępne
Zanim zagłębimy się w zawiłości dodawania łuków do arkusza kalkulacyjnego, ważne jest, aby upewnić się, że masz kilka rzeczy na miejscu. Oto wymagania wstępne, których będziesz potrzebować, aby zacząć:
1. Visual Studio: Musisz mieć zainstalowany na swoim komputerze program Visual Studio, ponieważ w naszym programie będziemy używać języka C#.
2. .NET Framework: Upewnij się, że masz zainstalowany .NET Framework lub .NET Core. Aspose.Cells obsługuje oba.
3. Aspose.Cells dla .NET: Musisz mieć bibliotekę Aspose.Cells. Możesz ją pobrać ze strony[Pobieranie Aspose.Cells](https://releases.aspose.com/cells/net/) strona.
4. Podstawowa znajomość języka C#: Znajomość języka C# pomoże Ci bez problemu śledzić fragmenty kodu.
## Importuj pakiety
Aby rozpocząć pracę z Aspose.Cells w swoim projekcie, musisz zaimportować niezbędne pakiety. Oto jak to zrobić:
### Utwórz nowy projekt
- Otwórz program Visual Studio.
- Wybierz „Utwórz nowy projekt”.
- Wybierz szablon, który współpracuje z platformą .NET (np. Aplikacja konsolowa).
  
### Dodaj odwołania Aspose.Cells
- Kliknij prawym przyciskiem myszy swój projekt w Eksploratorze rozwiązań.
- Wybierz „Zarządzaj pakietami NuGet”.
- Wyszukaj „Aspose.Cells” i zainstaluj.
Teraz możesz rozpocząć kodowanie dodawania łuków.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Poniżej przedstawiono kod krok po kroku, który pokazuje, jak dodać łuki do arkusza kalkulacyjnego w programie Excel.
## Krok 1: Konfigurowanie katalogu
Pierwszym krokiem jest utworzenie katalogu, w którym zapiszesz plik Excel. Ułatwia to zarządzanie plikami wyjściowymi.
```csharp
string dataDir = "Your Document Directory";
// Utwórz katalog, jeśli jeszcze go nie ma.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
W tym fragmencie kodu określamy ścieżkę do katalogu dokumentu. Sprawdzamy również, czy katalog istnieje; jeśli nie, tworzymy go. To stanowi podstawę dla naszego wyjścia.
## Krok 2: Utwórz skoroszyt
Następnie utwórzmy nową instancję skoroszytu.
```csharp
// Utwórz nowy skoroszyt.
Workbook excelbook = new Workbook();
```
Ten wiersz tworzy nowy skoroszyt programu Excel. Pomyśl o tym jak o pustym płótnie, na którym możemy dodawać kształty, dane i inne rzeczy.
## Krok 3: Dodaj pierwszy kształt łuku
Teraz dodajmy pierwszy kształt łuku do arkusza kalkulacyjnego.
```csharp
// Dodaj kształt łuku.
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
 Tutaj dodajemy łuk do pierwszego arkusza kalkulacyjnego. Parametry definiują pozycję i rozmiar łuku:`(left, top, width, height, startAngle, endAngle)`To jak kreślenie odcinka koła!
## Krok 4: Dostosuj pierwszy łuk
Po dodaniu łuku możesz chcieć dostosować jego wygląd.
```csharp
// Ustaw kolor wypełnienia kształtu
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
// Ustaw położenie łuku.
arc1.Placement = PlacementType.FreeFloating;           
// Ustaw grubość linii.
arc1.Line.Weight = 1;      
// Ustaw styl kreskowania łuku.
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
W tej sekcji dostosowujemy łuk. Ustawiamy typ wypełnienia na jednolity kolor (w tym przypadku niebieski), definiujemy sposób jego umieszczenia, ustalamy grubość linii i wybieramy styl kreski. Zasadniczo ozdabiamy nasz łuk, aby był wizualnie atrakcyjny!
## Krok 5: Dodaj drugi kształt łuku
Dodajmy kolejny kształt łuku, aby zapewnić więcej kontekstu.
```csharp
// Dodaj kolejny kształt łuku.
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Podobnie jak w przypadku pierwszego łuku, dodajemy drugi łuk na tym samym arkuszu kalkulacyjnym. Współrzędne tutaj są nieco przesunięte, aby umieścić go inaczej.
## Krok 6: Dostosuj drugi łuk
Podobnie jak zrobiliśmy to z pierwszym łukiem, dostosujemy także drugi.
```csharp
// Ustaw kolor linii
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
// Ustaw położenie łuku.
arc2.Placement = PlacementType.FreeFloating;          
// Ustaw grubość linii.
arc2.Line.Weight = 1;           
// Ustaw styl kreskowania łuku.
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Tutaj nadajemy drugiemu łukowi ten sam styl, co pierwszemu. Możesz zmienić kolor lub styl według uznania, aby uzyskać unikalność lub cele tematyczne.
## Krok 7: Zapisz skoroszyt
Na koniec pora zapisać nowo utworzony skoroszyt z łukami.
```csharp
// Zapisz plik Excela.
excelbook.Save(dataDir + "book1.out.xls");
```
Ta linia działa jak naciśnięcie przycisku zapisz. Zapisujemy naszą pracę w określonej lokalizacji z określoną nazwą pliku. Upewnij się, że sprawdziłeś swój katalog, aby zobaczyć swoje arcydzieło w formacie Excel!
## Wniosek
tym samouczku zbadaliśmy proces dodawania kształtów łuków do arkusza kalkulacyjnego programu Excel przy użyciu Aspose.Cells dla .NET. Dzięki prostemu przewodnikowi krok po kroku nauczyłeś się, jak utworzyć nowy skoroszyt, dodać łuki, dostosować ich wygląd i zapisać dokument. Ta możliwość nie tylko poprawia atrakcyjność wizualną arkuszy kalkulacyjnych, ale także sprawia, że prezentacje danych są bardziej pouczające. Niezależnie od tego, czy tworzysz wykresy, raporty, czy po prostu eksperymentujesz, używanie kształtów, takich jak łuki, może dodać kreatywny akcent do Twoich projektów.
## Najczęściej zadawane pytania
### Czym jest Aspose.Cells?
Aspose.Cells to zaawansowana biblioteka umożliwiająca programistom tworzenie, edytowanie i konwertowanie plików Excela programowo, bez konieczności używania programu Microsoft Excel.
### Czy muszę zainstalować program Microsoft Excel, aby korzystać z Aspose.Cells?
Nie, Aspose.Cells jest całkowicie niezależny i nie wymaga instalacji programu Microsoft Excel.
### Czy mogę wypróbować Aspose.Cells za darmo?
 Tak, możesz wypróbować Aspose.Cells, używając ich[Bezpłatna wersja próbna](https://releases.aspose.com/).
### Jakie języki programowania obsługuje Aspose.Cells?
Aspose.Cells obsługuje wiele języków, w tym C#, VB.NET i inne.
### Gdzie mogę uzyskać pomoc dotyczącą Aspose.Cells?
 Możesz uzyskać wsparcie poprzez[Forum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
