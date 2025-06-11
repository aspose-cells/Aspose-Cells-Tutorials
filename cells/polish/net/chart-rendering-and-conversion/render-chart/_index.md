---
"description": "Dowiedz się, jak renderować wykresy w .NET za pomocą Aspose.Cells. Postępuj zgodnie z naszym samouczkiem krok po kroku, aby bez wysiłku tworzyć oszałamiające wizualizacje."
"linktitle": "Wykres renderowania"
"second_title": "Aspose.Cells .NET API przetwarzania programu Excel"
"title": "Wykres renderowania"
"url": "/pl/net/chart-rendering-and-conversion/render-chart/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Wykres renderowania

## Wstęp

Wykresy są niezbędnym elementem prezentacji i analizy danych, dzięki czemu złożone informacje stają się łatwe do przyswojenia. Jeśli pracujesz z .NET i musisz generować wykresy programowo, Aspose.Cells to potężna biblioteka, która zapewnia intuicyjne i zaawansowane funkcje do obsługi plików i wykresów Excel. W tym przewodniku przeprowadzimy Cię przez proces renderowania wykresu przy użyciu Aspose.Cells dla .NET. Przygotuj się na zanurzenie się w tym szczegółowym samouczku, który jest zaprojektowany tak, aby był angażujący i łatwy do naśladowania!

## Wymagania wstępne

Zanim przejdziemy do kodu, upewnijmy się, że masz wszystko gotowe. Oto, czego potrzebujesz:

1. Środowisko .NET: Upewnij się, że masz skonfigurowane środowisko programistyczne .NET. Możesz użyć Visual Studio lub dowolnego innego IDE, które obsługuje .NET.
2. Aspose.Cells dla .NET: Musisz mieć zainstalowaną bibliotekę Aspose.Cells. Możesz ją pobrać z [Strona wydania Aspose](https://releases.aspose.com/cells/net/).
3. Podstawowa wiedza o języku C#: Znajomość programowania w języku C# pomoże Ci lepiej zrozumieć przykłady, ale nie martw się, jeśli jesteś nowy — ten przewodnik wyjaśni wszystko krok po kroku!

## Importuj pakiety

Pierwszym krokiem w Twojej podróży kodowania jest zaimportowanie niezbędnych pakietów. Otwórz swój projekt w swoim IDE i dodaj następującą przestrzeń nazw:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
```

Te przestrzenie nazw zapewnią Ci dostęp do funkcjonalności oferowanej przez bibliotekę Aspose.Cells, umożliwiając bezproblemowe tworzenie i manipulowanie wykresami.


Teraz, gdy omówiliśmy już wymagania wstępne i importy, zagłębmy się w szczegóły renderowania wykresu! Podzielimy to na jasne, łatwe do opanowania kroki.

## Krok 1: Skonfiguruj swój katalog wyjściowy

Zanim utworzymy nasz skoroszyt i wykres, musimy ustalić, gdzie będą zapisywane nasze wyniki. W ten sposób, gdy nasz wykres zostanie wygenerowany, będziesz dokładnie wiedział, gdzie go znaleźć.

```csharp
string outputDir = "Your Output Directory"; // Tutaj podaj katalog wyjściowy.
```

Pamiętaj, aby zastąpić „Katalog wyjściowy” ścieżką, w której chcesz zapisać obrazy wykresów.

## Krok 2: Utwórz skoroszyt

Następnie zainicjujemy nowy skoroszyt. To tutaj dzieje się cała magia!

```csharp
Workbook workbook = new Workbook();
```

Ten wiersz tworzy nową instancję `Workbook` Klasa umożliwiająca pracę z arkuszami i wykresami.

## Krok 3: Dodaj nowy arkusz kalkulacyjny

Teraz, gdy mamy nasz skoroszyt, czas dodać nowy arkusz. Pomyśl o arkuszach jako o różnych stronach w notatniku, gdzie możesz uporządkować swoje dane.

```csharp
int sheetIndex = workbook.Worksheets.Add();
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```

Tutaj dodajemy nowy arkusz kalkulacyjny i uzyskujemy do niego odniesienie. Będziesz pracować z tym arkuszem kalkulacyjnym, aby wprowadzać dane i wykresy.

## Krok 4: Wprowadź wartości przykładowe

Mając utworzony arkusz kalkulacyjny, dodajmy do komórek przykładowe dane. Na tych danych będzie oparty Twój wykres, więc wybierz wartości, które mają sens dla Twojego typu wykresu!

```csharp
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```

W tym fragmencie kodu wypełniamy komórki „A1” do „A3” pewnymi wartościami liczbowymi, a komórki „B1” do „B3” innym zestawem wartości. Możesz swobodnie dostosować te liczby do swoich potrzeb!

## Krok 5: Utwórz wykres

Teraz czas na stworzenie wykresu. Dodamy typ wykresu kolumnowego, który świetnie nadaje się do porównywania wartości.

```csharp
int chartIndex = worksheet.Charts.Add(ChartType.Column, 5, 0, 15, 5);
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

Tutaj dodajemy wykres w określonym miejscu poprzez zdefiniowanie jego układu: pierwszy zestaw liczb reprezentuje pozycję wykresu na siatce.

## Krok 6: Dodawanie serii danych do wykresu

Po utworzeniu wykresu musimy teraz powiązać go z danymi wprowadzonymi w poprzednich krokach.

```csharp
chart.NSeries.Add("A1:B3", true);
```

Ta linia łączy serię danych wykresu z wartościami w komórkach „A1” do „B3”. Oznacza to, że wykres będzie wizualnie reprezentował dane zgodnie z zamierzeniem.

## Krok 7: Zapisz wykres jako obraz

Teraz przekonwertujemy nasz wykres do formatu obrazu, aby można go było łatwo udostępniać i przeglądać.

```csharp
chart.ToImage(outputDir + "outputChartRendering.emf", System.Drawing.Imaging.ImageFormat.Emf);
```

W tym kroku zapisujemy wykres jako obraz EMF (Enhanced Metafile) w określonym katalogu wyjściowym. Możesz również zapisać go w różnych formatach, takich jak BMP lub PNG.

## Krok 8: Konwersja wykresu na mapę bitową

Jeśli wolisz pracować z mapami bitowymi, poniżej znajdziesz instrukcję, jak przekonwertować wykres do formatu mapy bitowej.

```csharp
System.Drawing.Bitmap bitmap = chart.ToImage();
bitmap.Save(outputDir + "outputChartRendering.bmp", System.Drawing.Imaging.ImageFormat.Bmp);
```

To zapisze Twój wykres jako obraz BMP. Pamiętaj, pliki BMP są zazwyczaj większe, ale mają niewiarygodnie wysoką jakość!

## Krok 9: Renderowanie z opcjami zaawansowanymi

Możemy również renderować wykres za pomocą niektórych zaawansowanych opcji obrazu, aby uzyskać lepszą jakość i rozdzielczość. Ustawmy kilka opcji:

```csharp
ImageOrPrintOptions options = new ImageOrPrintOptions()
{
    VerticalResolution = 300,
    HorizontalResolution = 300,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.AntiAlias
};
```

Opcje te pomagają poprawić jakość wizualną generowanego obrazu, co jest szczególnie przydatne w prezentacjach i publikacjach.

## Krok 10: Konwersja wykresu na obraz z opcjami zaawansowanymi

Teraz przekonwertujemy wykres, korzystając z zaawansowanych opcji, które właśnie ustawiliśmy.

```csharp
chart.ToImage(outputDir + "outputChartRendering.png", options);
```

Wykres zostanie zapisany jako plik PNG z ulepszonymi ustawieniami jakości.

## Krok 11: Eksportowanie wykresu do pliku PDF

Na koniec, jeśli chcesz uzyskać dopracowany dokument, który będzie można łatwo udostępniać, możesz wyeksportować wykres bezpośrednio do formatu PDF.

```csharp
chart.ToPdf(outputDir + "outputChartRendering.pdf");
```

Ten krok spowoduje utworzenie pliku PDF zawierającego wykres, który doskonale nadaje się do tworzenia raportów cyfrowych lub udostępniania współpracownikom.

## Wniosek 

Gratulacje! Udało Ci się wyrenderować wykres przy użyciu Aspose.Cells dla .NET. Ta potężna biblioteka upraszcza tworzenie i manipulowanie plikami i wykresami Excela, dzięki czemu Twoje dane są znacznie bardziej dostępne i atrakcyjne wizualnie. Niezależnie od tego, czy przygotowujesz raporty, analizy czy prezentacje, wykresy mają znaczący wpływ, a dzięki Aspose możesz je łatwo tworzyć programowo.

## Najczęściej zadawane pytania

### Jakie typy wykresów mogę tworzyć za pomocą Aspose.Cells dla .NET?
Można tworzyć różnorodne wykresy, m.in. wykresy kolumnowe, liniowe, kołowe i słupkowe.

### Czy mogę dostosować wygląd wykresów?
Tak, Aspose.Cells pozwala na szeroką personalizację, obejmującą kolory, style i elementy wykresów.

### Czy jest dostępna bezpłatna wersja próbna?
Oczywiście! Możesz pobrać darmową wersję próbną z [Tutaj](https://releases.aspose.com/).

### Gdzie mogę uzyskać pomoc dotyczącą Aspose.Cells?
Wsparcie społeczności i zasoby można znaleźć na stronie [Forum wsparcia Aspose](https://forum.aspose.com/c/cells/9).

### Czy potrzebuję licencji, aby korzystać z Aspose.Cells?
Tak, do dalszego korzystania z usługi po zakończeniu okresu próbnego wymagana jest licencja, ale możesz ubiegać się o licencję tymczasową [Tutaj](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}