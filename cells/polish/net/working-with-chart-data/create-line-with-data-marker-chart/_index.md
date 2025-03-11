---
title: Utwórz wykres liniowy z znacznikami danych
linktitle: Utwórz wykres liniowy z znacznikami danych
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak utworzyć wykres liniowy ze znacznikami danych w programie Excel przy użyciu Aspose.Cells dla .NET. Postępuj zgodnie z tym przewodnikiem krok po kroku, aby łatwo generować i dostosowywać wykresy.
weight: 10
url: /pl/net/working-with-chart-data/create-line-with-data-marker-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz wykres liniowy z znacznikami danych

## Wstęp

Czy kiedykolwiek zastanawiałeś się, jak programowo tworzyć oszałamiające wykresy w programie Excel? Cóż, zapnij pasy, ponieważ dzisiaj zagłębimy się w tworzenie wykresu liniowego z znacznikami danych przy użyciu Aspose.Cells dla .NET. Ten samouczek przeprowadzi Cię przez każdy krok, zapewniając, że masz solidne pojęcie o generowaniu wykresów, nawet jeśli dopiero zaczynasz pracę z Aspose.Cells.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że wszystko jest gotowe, by wszystko przebiegło bezproblemowo.

1. Aspose.Cells for .NET Library – Musisz to zainstalować. Możesz to pobrać[Tutaj](https://releases.aspose.com/cells/net/).
2. .NET Framework – Upewnij się, że Twoje środowisko programistyczne jest skonfigurowane przy użyciu najnowszej wersji .NET.
3. IDE (zintegrowane środowisko programistyczne) – zalecany jest program Visual Studio.
4.  Ważna licencja Aspose.Cells – jeśli jej nie posiadasz, możesz poprosić o[licencja tymczasowa](https://purchase.aspose.com/temporary-license/) lub sprawdź ich[bezpłatny okres próbny](https://releases.aspose.com/).

Gotowy do drogi? Rozłóżmy to na czynniki pierwsze!

## Importowanie niezbędnych pakietów

Na początek upewnij się, że importujesz następujące przestrzenie nazw do swojego projektu. Zapewnią one niezbędne klasy i metody do utworzenia wykresu.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Gdy już to opanujesz, możemy zacząć kodować!

## Krok 1: Skonfiguruj skoroszyt i arkusz kalkulacyjny

Najpierw musisz utworzyć nowy skoroszyt i uzyskać dostęp do pierwszego arkusza.

```csharp
//Katalog wyjściowy
static string outputDir = "Your Document Directory";
		
// Utwórz instancję skoroszytu
Workbook workbook = new Workbook();

// Uzyskaj dostęp do pierwszego arkusza kalkulacyjnego
Worksheet worksheet = workbook.Worksheets[0];
```

Myśl o skoroszycie jako o pliku Excela, a o arkuszu jako o konkretnym arkuszu w nim. W tym przypadku pracujemy z pierwszym arkuszem.

## Krok 2: Wypełnij arkusz danymi

Teraz, gdy mamy nasz arkusz kalkulacyjny, wypełnijmy go danymi. Tworzymy losowe punkty danych dla dwóch serii wartości.

```csharp
// Ustaw tytuł kolumny
worksheet.Cells[0, 0].Value = "X";
worksheet.Cells[0, 1].Value = "Y";

// Losowe dane do generowania wykresu
Random R = new Random();

// Utwórz losowe dane i zapisz je w komórkach
for (int i = 1; i < 21; i++)
{
    worksheet.Cells[i, 0].Value = i;
    worksheet.Cells[i, 1].Value = 0.8;
}

for (int i = 21; i < 41; i++)
{
    worksheet.Cells[i, 0].Value = i - 20;
    worksheet.Cells[i, 1].Value = 0.9;
}
```

W tym przypadku wykorzystujemy liczby losowe do symulacji danych, ale w rzeczywistych zastosowaniach możesz wypełnić je rzeczywistymi wartościami ze swojego zestawu danych.

## Krok 3: Dodaj wykres do arkusza kalkulacyjnego

Następnie dodajemy wykres do arkusza kalkulacyjnego i wybieramy typ – w tym przypadku wykres liniowy ze znacznikami danych.

```csharp
// Dodaj wykres do arkusza kalkulacyjnego
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

// Uzyskaj dostęp do nowo utworzonego wykresu
Chart chart = worksheet.Charts[idx];
```

Ten fragment kodu dodaje wykres liniowy z znacznikami danych do arkusza kalkulacyjnego, umieszczając go w określonym zakresie (1,3 do 20,20). Całkiem proste, prawda?

## Krok 4: Dostosuj wygląd wykresu

Po utworzeniu wykresu możesz nadać mu styl według własnego uznania. Zmieńmy tło, tytuł i styl wykresu.

```csharp
// Ustaw styl wykresu
chart.Style = 3;

// Ustaw wartość automatycznego skalowania na true
chart.AutoScaling = true;

// Ustaw kolor pierwszego planu na biały
chart.PlotArea.Area.ForegroundColor = Color.White;

//Ustaw właściwości tytułu wykresu
chart.Title.Text = "Sample Chart";

// Ustaw typ wykresu
chart.Type = ChartType.LineWithDataMarkers;
```

Tutaj nadajemy wykresowi przejrzysty wygląd, ustawiając białe tło, stosując automatyczne skalowanie i nadając mu znaczący tytuł.

## Krok 5: Zdefiniuj serie i nanieś punkty danych na wykres

Teraz, gdy nasz wykres wygląda już dobrze, musimy zdefiniować serie danych, które zostaną przedstawione na wykresie.

```csharp
// Ustaw właściwości tytułu osi kategorii
chart.CategoryAxis.Title.Text = "Units";

// Zdefiniuj dwie serie dla wykresu
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

Serie te odpowiadają zakresom punktów danych, które wypełniliśmy wcześniej.

## Krok 6: Dodaj kolory i dostosuj znaczniki serii

Uatrakcyjnijmy ten wykres, dodając niestandardowe kolory do znaczników danych.

```csharp
// Dostosuj pierwszą serię
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

// Dostosuj drugą serię
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

Dzięki dostosowaniu kolorów wykres staje się nie tylko funkcjonalny, ale i atrakcyjny wizualnie!

## Krok 7: Ustaw wartości X i Y dla każdej serii

Na koniec przypiszmy wartości X i Y każdemu z naszych szeregów.

```csharp
// Ustaw wartości X i Y pierwszej serii
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

// Ustaw wartości X i Y drugiej serii
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

Wartości opierają się na danych, które wprowadziliśmy w kroku 2.

## Krok 8: Zapisz skoroszyt

Teraz gdy wszystko jest już gotowe, możemy zapisać skoroszyt, abyśmy mogli zobaczyć wykres w działaniu.

```csharp
// Zapisz skoroszyt
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

I to wszystko! Właśnie utworzyłeś wykres liniowy z markerami danych przy użyciu Aspose.Cells dla .NET.

## Wniosek

Tworzenie wykresów programowo w programie Excel może wydawać się zniechęcające, ale dzięki Aspose.Cells dla .NET jest to tak proste, jak wykonanie przepisu krok po kroku. Od konfiguracji skoroszytu po dostosowywanie wyglądu wykresu, ta potężna biblioteka obsługuje wszystko. Niezależnie od tego, czy tworzysz raporty, pulpity nawigacyjne czy wizualizacje danych, Aspose.Cells pozwala Ci zrobić to w mgnieniu oka.

## Najczęściej zadawane pytania

### Czy mogę dodatkowo dostosować wykres?  
Oczywiście! Aspose.Cells oferuje mnóstwo opcji dostosowywania, od czcionek po linie siatki i wiele więcej.

### Czy potrzebuję licencji, aby korzystać z Aspose.Cells?  
 Tak, licencja jest wymagana do pełnej funkcjonalności. Możesz uzyskać[licencja tymczasowa](https://purchase.aspose.com/temporary-license/) lub zacznij od[bezpłatny okres próbny](https://releases.aspose.com/).

### Jak mogę dodać więcej serii danych?  
 Wystarczy dodać dodatkowe serie za pomocą`NSeries.Add` metoda, określająca zakresy komórek dla nowych danych.

### Czy mogę wyeksportować wykres jako obraz?  
 Tak, możesz eksportować wykresy bezpośrednio jako obrazy, korzystając z`Chart.ToImage` metoda.

### Czy Aspose.Cells obsługuje wykresy 3D?  
Tak, Aspose.Cells obsługuje szeroką gamę typów wykresów, w tym wykresy 3D.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
