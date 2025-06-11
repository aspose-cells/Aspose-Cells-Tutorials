---
"description": "Dowiedz się, jak łatwo dodawać obrazy do wykresów Excela za pomocą Aspose.Cells dla .NET. Ulepsz swoje wykresy i prezentacje w zaledwie kilku prostych krokach."
"linktitle": "Dodaj obraz do wykresu"
"second_title": "Aspose.Cells .NET API przetwarzania programu Excel"
"title": "Dodaj obraz do wykresu"
"url": "/pl/net/inserting-controls-in-charts/add-picture-to-chart/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj obraz do wykresu

## Wstęp

Czy masz dość nudnych wykresów, którym brakuje osobistego akcentu? Chcesz dowiedzieć się, jak urozmaicić wizualizacje w programie Excel, dodając obrazy? Cóż, masz szczęście! W tym samouczku zanurzymy się w świat Aspose.Cells dla .NET i nauczymy się, jak dodawać obrazy do wykresów w programie Excel. Więc weź swoją ulubioną filiżankę kawy i zaczynajmy!

## Wymagania wstępne

Zanim przejdziemy do szczegółów kodowania, istnieje kilka warunków wstępnych, które musisz spełnić, aby wszystko poszło gładko:

- Visual Studio: Tutaj będziesz pisać i uruchamiać swój kod .NET. Upewnij się, że masz go zainstalowanego.
- Aspose.Cells dla .NET: Ta biblioteka będzie Ci potrzebna do pracy z plikami Excel. Możesz [pobierz tutaj](https://releases.aspose.com/cells/net/).
- Podstawowa znajomość języka C#: wprawdzie przeprowadzę Cię przez kod, ale znajomość podstaw języka C# sprawi, że wszystko stanie się jaśniejsze.

### Kroki instalacji

1. Zainstaluj Aspose.Cells: Możesz dodać Aspose.Cells do swojego projektu Visual Studio za pomocą Menedżera pakietów NuGet. Aby to zrobić, przejdź do Narzędzia > Menedżer pakietów NuGet > Zarządzaj pakietami NuGet dla rozwiązania i wyszukaj „Aspose.Cells”. Kliknij Zainstaluj.
2. Konfigurowanie projektu: Utwórz nowy projekt aplikacji konsolowej C# w programie Visual Studio.

## Importuj pakiety

Gdy już wszystko skonfigurujesz, następnym krokiem jest zaimportowanie niezbędnych pakietów do projektu. Oto jak to zrobić:

### Importuj wymagane przestrzenie nazw

Na górze pliku z kodem C# musisz zaimportować następujące przestrzenie nazw:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

To mówi Twojemu programowi: „Hej! Zamierzam użyć tych fajnych funkcji z Aspose.Cells.”

Teraz, gdy spełniliśmy już wszystkie wymagania wstępne, podzielmy proces na mniejsze kroki. 

## Krok 1: Zdefiniuj swoje katalogi

Po pierwsze, musimy skonfigurować ścieżki dla naszych plików wejściowych i wyjściowych. Ten krok jest kluczowy, ponieważ musimy wiedzieć, gdzie znaleźć nasz istniejący plik Excel i gdzie zapisać zmodyfikowany plik.

```csharp
//Katalog źródłowy
string sourceDir = "Your Document Directory/";

//Katalog wyjściowy
string outputDir = "Your Output Directory/";
```

Zastępować `Your Document Directory` I `Your Output Directory` z rzeczywistymi ścieżkami na Twoim komputerze. 

## Krok 2: Załaduj istniejący skoroszyt

Teraz wczytajmy istniejący plik Excela, do którego chcemy dodać nasz obrazek na wykresie.

```csharp
// Otwórz istniejący plik.
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

Ten kod otwiera skoroszyt i przygotowuje go do edycji.

## Krok 3: Przygotuj strumień obrazu

Przed dodaniem obrazka musimy odczytać obraz, który chcemy wstawić do wykresu. 

```csharp
// Pobierz plik obrazu do strumienia.
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

Upewnij się, że zdjęcie zostało zapisane w określonym katalogu.

## Krok 4: Wybierz cel wykresu

Teraz określmy, do którego wykresu dodamy nasz obraz. W tym przykładzie będziemy celować w pierwszy wykres na pierwszym arkuszu.

```csharp
// W drugim arkuszu znajdziesz wykres projektanta.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

Dostęp do dowolnego arkusza kalkulacyjnego można uzyskać poprzez odpowiednią zmianę indeksu.

## Krok 5: Dodaj obraz do wykresu

Po wybraniu wykresu czas dodać zdjęcie! 

```csharp
// Dodaj nowy obrazek do wykresu.
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

Tutaj, `50` I `50` to współrzędne X i Y, pod którymi zostanie umieszczony obraz, oraz `200` jest szerokością i wysokością obrazu.

## Krok 6: Dostosuj format linii obrazu

Chcesz dodać trochę stylu do swojego zdjęcia? Możesz dostosować jego obramowanie! Oto jak to zrobić:

```csharp
// Pobierz typ formatu linii obrazu.
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

// Ustaw styl myślnika.
lineformat.DashStyle = MsoLineDashStyle.Solid;

// Ustaw grubość linii.
lineformat.Weight = 4;    
```

Ten fragment kodu pozwala wybrać wygląd obramowania i jego grubość. Wybierz dowolny styl, który pasuje do Twojej prezentacji!

## Krok 7: Zapisz zmodyfikowany skoroszyt

Po wykonaniu całej tej ciężkiej pracy, zapiszmy zmiany poprzez wykonanie poniższej linii kodu:

```csharp
// Zapisz plik Excela.
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

Teraz Twój obraz został pomyślnie zintegrowany z wykresem, a plik wyjściowy jest gotowy do obejrzenia!

## Krok 8: Wskaż sukces

Na koniec możesz dodać prostą wiadomość potwierdzającą, że operacja się powiodła:

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## Wniosek

W tym samouczku sprawdziliśmy, jak dodać odrobinę osobowości do wykresów Excela, dodając obrazy za pomocą Aspose.Cells dla .NET. Za pomocą kilku prostych kroków możesz podnieść poziom swoich prezentacji z nudnych na niezapomniane. Na co więc czekasz? Spróbuj i pozwól swoim wykresom zabłysnąć!

## Najczęściej zadawane pytania

### Czy mogę dodać wiele zdjęć do jednego wykresu?
Tak! Możesz zadzwonić `AddPictureInChart` Metodę tę powtarzaj wielokrotnie, aby dodać tyle zdjęć, ile chcesz.

### Jakie formaty obrazów obsługuje Aspose.Cells?
Aspose.Cells obsługuje wiele formatów obrazów, w tym PNG, JPEG, BMP i GIF.

### Czy mogę dostosować położenie obrazu?
Oczywiście! Współrzędne X i Y w `AddPictureInChart` Metoda ta pozwala na precyzyjne pozycjonowanie.

### Czy korzystanie z Aspose.Cells jest bezpłatne?
Aspose.Cells oferuje bezpłatną wersję próbną, ale do korzystania z pełnych funkcji wymagana jest licencja. Cennik można znaleźć [Tutaj](https://purchase.aspose.com/buy).

### Gdzie mogę znaleźć więcej przykładów?
Sprawdź [Dokumentacja Aspose.Cells](https://reference.aspose.com/cells/net/) aby zobaczyć bardziej szczegółowe przykłady i funkcjonalności.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}