---
title: Zastosuj format 3D do wykresu
linktitle: Zastosuj format 3D do wykresu
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak tworzyć oszałamiające wykresy 3D w programie Excel przy użyciu Aspose.Cells dla .NET. Postępuj zgodnie z naszym prostym przewodnikiem krok po kroku.
weight: 10
url: /pl/net/advanced-chart-operations/apply-3d-format-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zastosuj format 3D do wykresu

## Wstęp

W czasach, w których wizualizacja danych jest najważniejsza, sposób, w jaki prezentujemy nasze dane, wykracza poza podstawowe wykresy i diagramy. Dzięki narzędziom takim jak Aspose.Cells dla .NET możesz ulepszyć swoje prezentacje danych za pomocą oszałamiających wykresów 3D, które nie tylko przyciągają uwagę, ale także skutecznie przekazują informacje. Ten przewodnik przeprowadzi Cię przez kroki, aby zastosować format 3D do wykresu za pomocą Aspose.Cells, przekształcając Twoje surowe dane w angażujący wyświetlacz.

## Wymagania wstępne

Zanim zagłębimy się w szczegóły dotyczące stosowania formatu 3D do wykresu, upewnijmy się, że masz wszystko, czego potrzebujesz.

### Wymagania programowe

- Visual Studio: Upewnij się, że masz zainstalowany program Visual Studio, aby móc pracować z aplikacjami .NET.
-  Aspose.Cells dla .NET: Jeśli jeszcze tego nie zrobiłeś, pobierz i zainstaluj Aspose.Cells z[Tutaj](https://releases.aspose.com/cells/net/).

### Konfiguracja środowiska kodowania

1. Utwórz nowy projekt .NET: Otwórz program Visual Studio, wybierz opcję „Utwórz nowy projekt” i wybierz aplikację konsolową.
2. Dodaj odniesienie do Aspose.Cells: za pomocą Menedżera pakietów NuGet dodaj Aspose.Cells, wyszukując je lub za pomocą konsoli Menedżera pakietów:

```bash
Install-Package Aspose.Cells
```

3. Konfiguracja katalogu wyjściowego: Wskaż katalog wyjściowy, w którym będą zapisywane wygenerowane pliki. Może to być po prostu utworzenie folderu na pulpicie.

Teraz, gdy wszystko jest już skonfigurowane, czas zagłębić się w kod i stworzyć olśniewające wykresy 3D!

## Importuj pakiety

Na początek musisz zaimportować niezbędne przestrzenie nazw. Pomoże Ci to uzyskać dostęp do klas i metod udostępnianych przez Aspose.Cells. Oto, jak to zrobić:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

tej sekcji podzielimy cały proces na łatwe do opanowania kroki, co pozwoli Ci zrozumieć każdy etap.

## Krok 1: Zainicjuj swój skoroszyt

 Najpierw musisz utworzyć instancję`Workbook` Klasa. Ten obiekt będzie stanowić podstawę dla Twojego dokumentu Excel.

```csharp
//Katalog wyjściowy
string outputDir = "Your Document Directory";
Workbook book = new Workbook();
```
 Pomyśl o tym`Workbook` jako puste płótno, gotowe do wypełnienia kolorowymi danymi i efektownymi wizualizacjami.

## Krok 2: Zmień nazwę pierwszego arkusza kalkulacyjnego

Następnie zmieńmy nazwę pierwszego arkusza. Dzięki temu będzie jasne, z jakimi danymi pracujemy.

```csharp
book.Worksheets[0].Name = "DataSheet";
```

Nazwy powinny być intuicyjne. W tym przypadku nazywamy je „DataSheet”, aby wiedzieć, gdzie znajdują się nasze dane.

## Krok 3: Utwórz dane dla wykresu

Teraz dodamy trochę danych do naszego „Arkusza danych”. Wypełnijmy go wartościami, których będzie używał nasz wykres.

```csharp
Worksheet dataSheet = book.Worksheets["DataSheet"];
dataSheet.Cells["B1"].PutValue(1);
dataSheet.Cells["B2"].PutValue(2);
dataSheet.Cells["B3"].PutValue(3);
dataSheet.Cells["A1"].PutValue("A");
dataSheet.Cells["A2"].PutValue("B");
dataSheet.Cells["A3"].PutValue("C");
```

Podobnie jak przepis zależy od składników, skuteczność wykresu zależy od jakości i organizacji danych wejściowych.

## Krok 4: Skonfiguruj nowy arkusz wykresu

Czas utworzyć nowy arkusz kalkulacyjny dla samego wykresu. Pomaga to zachować porządek w wizualizacji danych.

```csharp
Worksheet sheet = book.Worksheets.Add("MyChart");
```

Potraktuj ten arkusz jako scenę, na której ujawnia się wydajność Twoich danych.

## Krok 5: Dodaj wykres

Tutaj dodamy wykres kolumnowy do nowo utworzonego arkusza kalkulacyjnego.  

```csharp
ChartCollection charts = sheet.Charts;
int chartSheetIdx = charts.Add(ChartType.Column, 5, 0, 25, 15);
```

Definiujemy przestrzeń dla naszego wykresu i określamy, jaki jest jego typ. Pomyśl o tym jak o wyborze typu ramki dla swojej grafiki.

## Krok 6: Dostosuj wygląd wykresu

Teraz dostosujemy wygląd naszego wykresu ustawiając kolory tła. 

```csharp
Aspose.Cells.Charts.Chart chart = book.Worksheets["MyChart"].Charts[0];
chart.PlotArea.Area.BackgroundColor = Color.White;
chart.ChartArea.Area.BackgroundColor = Color.White;
chart.PlotArea.Area.ForegroundColor = Color.White;
chart.ChartArea.Area.ForegroundColor = Color.White;
chart.ShowLegend = false;
```

Czyste, białe tło często uwydatnia kolory danych, zwiększając ich widoczność.

## Krok 7: Dodaj serię danych do wykresu

Czas napełnić nasz wykres danymi. Dodamy serię danych z naszego „DataSheet”, aby upewnić się, że nasz wykres odzwierciedla dane, których potrzebujemy.

```csharp
chart.NSeries.Add("DataSheet!B1:B3", true);
chart.NSeries.CategoryData = "DataSheet!A1:A3";
```

To jest analogiczne do szefa kuchni przygotowującego danie ze specyficznych składników. Każdy punkt danych ma znaczenie!

## Krok 8: Dostęp i formatowanie serii danych

Teraz, gdy połączyliśmy nasze dane, możemy pobrać serię danych i zacząć stosować efekty 3D.

```csharp
Aspose.Cells.Charts.Series ser = chart.NSeries[0];
ShapePropertyCollection spPr = ser.ShapeProperties;
Format3D fmt3d = spPr.Format3D;
```

Przygotowujemy się do dodania naszemu daniu odrobiny smaku – pomyśl o tym jak o przyprawie, która podkreśla ogólny smak.

## Krok 9: Zastosuj efekty fazowania 3D

Następnie dodamy efekt ścięcia, aby nadać naszemu wykresowi pewien wymiar.

```csharp
Bevel bevel = fmt3d.TopBevel;
bevel.Type = BevelPresetType.Circle;
bevel.Height = 2;
bevel.Width = 5;
```

Tak jak rzeźbiarz kształtuje kamień, my tworzymy głębię, która sprawia, że nasz wykres ożywa!

## Krok 10: Dostosuj materiał powierzchni i oświetlenie

Sprawmy, aby nasz wykres zabłysnął! Dostosujemy materiał powierzchni i ustawienia oświetlenia.

```csharp
fmt3d.SurfaceMaterialType = PresetMaterialType.WarmMatte;
fmt3d.SurfaceLightingType = LightRigType.ThreePoint;
fmt3d.LightingAngle = 20;
```

Odpowiednie oświetlenie i materiały mogą przekształcić płaski obiekt w urzekający obraz. Pomyśl o planie filmowym fachowo oświetlonym, aby uwydatnić każdą scenę.

## Krok 11: Ostatnie szlify nad wyglądem serialu

Teraz nadszedł czas na dopracowanie wyglądu serii danych poprzez dostosowanie jej koloru.

```csharp
ser.Area.BackgroundColor = Color.Maroon;
ser.Area.ForegroundColor = Color.Maroon;
ser.Border.Color = Color.Maroon;
```

Odpowiedni kolor może wywoływać określone uczucia i reakcje — bordowy dodaje elegancji i wyrafinowania.

## Krok 12: Zapisz swój skoroszyt

W końcu nadszedł czas, aby zapisać swoje arcydzieło! Nie zapomnij określić miejsca docelowego, w którym chcesz je zapisać.

```csharp
book.Save(outputDir + "outputApplying3DFormat.xlsx");
Console.WriteLine("Applying3DFormat executed successfully.");
```

Zapisywanie swojej pracy jest jak wystawianie jej w galerii; to chwila, którą należy pielęgnować i dzielić się nią z innymi.

## Wniosek

Gratulacje! Udało Ci się stworzyć atrakcyjny wizualnie wykres 3D przy użyciu Aspose.Cells dla .NET. Postępując zgodnie z tymi krokami, masz teraz potężne narzędzie do ulepszania prezentacji danych, dzięki czemu będą one nie tylko informacyjne, ale także wizualnie wciągające. Podczas udoskonalania wykresów pamiętaj, że każda wizualizacja to historia — spraw, aby była angażująca, przejrzysta i wywierała wpływ!

## Najczęściej zadawane pytania

### Czym jest Aspose.Cells dla .NET?
Aspose.Cells for .NET to zaawansowana biblioteka umożliwiająca programistom programowe manipulowanie dokumentami Excela, w tym tworzenie wykresów i diagramów.

### Czy mogę dostosować typy wykresów w Aspose.Cells?
Tak! Aspose.Cells obsługuje różne typy wykresów, takie jak kolumnowy, liniowy, kołowy i wiele innych, które można łatwo dostosować.

### Czy jest dostępna bezpłatna wersja próbna Aspose.Cells?
 Oczywiście! Możesz pobrać bezpłatną wersję próbną z[Tutaj](https://releases.aspose.com/).

### Czy mogę stosować na wykresach inne efekty niż te w formacie 3D?
Tak, możesz stosować różne efekty, takie jak cienie, gradienty i różne style, aby wzbogacić swoje wykresy o elementy wykraczające poza 3D.

### Gdzie mogę znaleźć pomoc dotyczącą Aspose.Cells?
 Aby uzyskać pomoc, możesz odwiedzić stronę[Forum Aspose](https://forum.aspose.com/c/cells/9) w celu uzyskania pomocy i wsparcia ze strony społeczności.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
