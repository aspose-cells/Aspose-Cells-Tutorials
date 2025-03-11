---
title: Utwórz wykres kołowy
linktitle: Utwórz wykres kołowy
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak utworzyć wykres kołowy w programie Excel przy użyciu Aspose.Cells dla .NET dzięki temu przewodnikowi krok po kroku. Wizualizuj swoje dane bez wysiłku.
weight: 12
url: /pl/net/manipulating-chart-types/create-pie-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz wykres kołowy

## Wstęp

Tworzenie wykresów jest niezbędne do wizualnego przedstawiania danych, a wykresy kołowe są jednym z najpopularniejszych sposobów zilustrowania, w jaki sposób części składają się na całość. Dzięki Aspose.Cells dla .NET możesz łatwo zautomatyzować generowanie wykresów kołowych w plikach Excela. W tym samouczku zagłębimy się w to, jak utworzyć wykres kołowy od podstaw za pomocą Aspose.Cells dla .NET, z przewodnikiem krok po kroku, aby uczynić ten proces płynnym i prostym. Niezależnie od tego, czy jesteś nowy w tym narzędziu, czy chcesz poprawić swoje umiejętności automatyzacji programu Excel, ten przewodnik Cię obejmuje!

## Wymagania wstępne

Zanim zagłębisz się w kod, upewnij się, że masz następujące ustawienia:

1.  Aspose.Cells for .NET Library: Upewnij się, że Aspose.Cells jest zainstalowany w Twoim projekcie. Jeśli jeszcze go nie zainstalowałeś, możesz go pobrać z[Tutaj](https://releases.aspose.com/cells/net/).
2. Środowisko programistyczne .NET: upewnij się, że Twój projekt jest skonfigurowany do korzystania z .NET Framework lub .NET Core.
3. Podstawowa znajomość języka C#: Powinieneś znać podstawy programowania w języku C#, szczególnie programowania obiektowego (OOP).

 Dla zaawansowanych użytkowników, tymczasowa licencja może zostać zastosowana, aby odblokować wszystkie funkcje Aspose.Cells. Możesz poprosić o nią od[Tutaj](https://purchase.aspose.com/temporary-license/).

## Importuj pakiety

Aby rozpocząć, zaimportuj niezbędne przestrzenie nazw i pakiety wymagane w tym samouczku. Obejmują one podstawowe operacje wejścia/wyjścia i pakiet Aspose.Cells.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## Krok 1: Utwórz nowy skoroszyt

 Najpierw musimy utworzyć instancję`Workbook` Klasa, która reprezentuje plik Excel. Skoroszyt zawiera wiele arkuszy, a w naszym przykładzie będziemy pracować z dwoma arkuszami — jednym dla danych i jednym dla wykresu kołowego.

```csharp
Workbook workbook = new Workbook();
```

To inicjuje nowy skoroszyt programu Excel. Ale gdzie trafiają dane? Zajmiemy się tym w następnym kroku.

## Krok 2: Dodaj dane do arkusza kalkulacyjnego

Po utworzeniu skoroszytu musimy uzyskać dostęp do pierwszego arkusza i nadać mu nazwę. Tutaj wprowadzimy dane wymagane do wykresu kołowego.

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

Teraz możemy wprowadzić pewne fikcyjne dane sprzedażowe reprezentujące różne regiony:

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

Tutaj dodajemy dwie kolumny: jedną dla regionów i drugą dla danych sprzedaży. Dane te zostaną przedstawione na wykresie kołowym.

## Krok 3: Dodaj arkusz wykresu

Następnie dodajmy oddzielny arkusz, w którym umieścimy wykres kołowy.

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

Ten nowy arkusz będzie zawierał wykres kołowy. Nadanie mu nazwy, takiej jak „Wykres”, zapewnia, że użytkownicy wiedzą, czego się spodziewać po otwarciu pliku.

## Krok 4: Utwórz wykres kołowy

Teraz czas na stworzenie właściwego wykresu. Określimy, że chcemy wykres kołowy i zdefiniujemy jego pozycję na arkuszu.

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

 Metoda`Add()`akceptuje parametry dla typu wykresu (w tym przypadku`ChartType.Pie`) i jego położenie na arkuszu. Liczby oznaczają pozycje wierszy i kolumn.

## Krok 5: Dostosuj wygląd wykresu

Wykres kołowy nie byłby kompletny bez odrobiny personalizacji! Sprawmy, aby nasz wykres był wizualnie atrakcyjny, zmieniając kolory, etykiety i tytuł.

### Ustaw tytuł wykresu
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### Dostosuj obszar wykresu
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

Ustawiamy wypełnienie gradientowe dla obszaru wykresu i ukrywamy obramowanie, aby uzyskać bardziej przejrzysty wygląd.

## Krok 6: Zdefiniuj dane wykresu

 Czas połączyć wykres z naszymi danymi.`NSeries` Właściwość wykresu wiąże dane dotyczące sprzedaży i regionów z wykresem kołowym.

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

 Pierwszy wiersz określa, że korzystamy z danych sprzedaży z komórek`B2:B8` . Mówimy również wykresowi, aby używał nazw regionów z`A2:A8` jako etykiety kategorii.

## Krok 7: Dodaj etykiety danych

Dodawanie etykiet bezpośrednio do segmentów wykresu może ułatwić zrozumienie. Uwzględnijmy nazwy regionów i wartości sprzedaży w wycinkach wykresu kołowego.

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## Krok 8: Dostosuj obszar wykresu i legendę

Na koniec dopracujmy nieco obszar wykresu i legendę. To poprawi ogólną prezentację wykresu.

### Obszar wykresu
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### Legenda
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## Krok 9: Zapisz skoroszyt

Na koniec zapisujemy skoroszyt do pliku Excel. Możesz określić katalog wyjściowy i nazwę pliku według potrzeb.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## Wniosek

Tworzenie wykresu kołowego za pomocą Aspose.Cells dla .NET to prosty i konfigurowalny proces. Postępując zgodnie z tym przewodnikiem, możesz wygenerować profesjonalnie wyglądający wykres, który przekazuje cenne informacje w zaledwie kilku krokach. Niezależnie od tego, czy chodzi o raportowanie biznesowe, czy cele edukacyjne, opanowanie tworzenia wykresów podniesie Twoje umiejętności automatyzacji programu Excel. Pamiętaj, że Aspose.Cells zapewnia elastyczność potrzebną do tworzenia oszałamiających plików Excel opartych na danych bez wysiłku.

## Najczęściej zadawane pytania

### Czy mogę tworzyć inne typy wykresów za pomocą Aspose.Cells dla .NET?
Tak! Aspose.Cells obsługuje różne typy wykresów, w tym wykresy słupkowe, wykresy liniowe i wykresy punktowe.

### Czy potrzebuję płatnej licencji, aby używać Aspose.Cells dla .NET?
Możesz używać bezpłatnej wersji z pewnymi ograniczeniami. Aby korzystać z pełnych funkcji, będziesz potrzebować licencji, którą możesz kupić[Tutaj](https://purchase.aspose.com/buy).

### Czy mogę wyeksportować wykres do formatów PDF lub obrazów?
Oczywiście! Aspose.Cells pozwala eksportować wykresy do różnych formatów, w tym PDF i PNG.

### Czy można nadać każdemu wycinkowi ciasta inny kolor?
 Tak, możesz zastosować różne kolory do każdego wycinka, ustawiając`IsColorVaried` nieruchomość do`true`, jak pokazano w samouczku.

### Czy mogę zautomatyzować generowanie wielu wykresów w jednym skoroszycie?
Tak, w jednym pliku Excela można tworzyć i dostosowywać dowolną liczbę wykresów.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
