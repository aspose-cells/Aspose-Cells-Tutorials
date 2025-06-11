---
"date": "2025-04-05"
"description": "Dowiedz się, jak tworzyć dynamiczne wykresy kołowe z liniami odniesienia za pomocą Aspose.Cells dla .NET. Postępuj zgodnie z tym przewodnikiem, aby udoskonalić swoje umiejętności wizualizacji danych."
"title": "Tworzenie wykresów kołowych z liniami odniesienia w Aspose.Cells .NET&#58; Kompleksowy przewodnik"
"url": "/pl/net/charts-graphs/create-pie-charts-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Tworzenie wykresów kołowych z liniami odniesienia za pomocą Aspose.Cells .NET

## Wstęp
Ulepsz wizualizację danych, tworząc bardziej informacyjne wykresy kołowe za pomocą Aspose.Cells dla .NET. Ten przewodnik krok po kroku pokazuje, jak dodawać linie wiodące do segmentów wykresu kołowego, ułatwiając identyfikację odpowiadających kategorii danych na pierwszy rzut oka. Postępując zgodnie z tym samouczkiem, Twoje wizualizacje będą zarówno atrakcyjne wizualnie, jak i wysoce funkcjonalne.

**Czego się nauczysz:**
- Konfigurowanie Aspose.Cells dla .NET w Twoim środowisku
- Tworzenie niestandardowych wykresów kołowych z liniami wiodącymi przy użyciu języka C#
- Zapisywanie wykresu jako obrazu lub w skoroszycie programu Excel

Upewnij się, że masz wszystko gotowe, aby móc skutecznie śledzić przebieg prac.

## Wymagania wstępne
Przed rozpoczęciem upewnij się, że spełniasz poniższe wymagania wstępne:

- **Biblioteki i wersje**: Zainstaluj Aspose.Cells dla .NET. Upewnij się, że Twój projekt jest skonfigurowany z najnowszą wersją.
- **Konfiguracja środowiska**:W tym przewodniku założono, że środowisko .NET jest zgodne z Aspose.Cells.
- **Wymagania wstępne dotyczące wiedzy**:Podstawowa znajomość programowania w języku C# i obsługi programu Excel będzie przydatna.

## Konfigurowanie Aspose.Cells dla .NET
Aby rozpocząć, zainstaluj Aspose.Cells w swoim projekcie za pomocą:

**Interfejs wiersza poleceń .NET**
```bash
dotnet add package Aspose.Cells
```

**Menedżer pakietów**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

Uzyskaj licencję na pełną funkcjonalność wybierając spośród następujących opcji:
- **Bezpłatna wersja próbna**:Rozpocznij bezpłatny okres próbny na [Strona pobierania Aspose](https://releases.aspose.com/cells/net/).
- **Licencja tymczasowa**:Uzyskaj tymczasową licencję [Tutaj](https://purchase.aspose.com/temporary-license/).
- **Zakup**:Aby uzyskać dostęp do pełnej funkcjonalności, należy zakupić licencję [Tutaj](https://purchase.aspose.com/buy).

Zainicjuj Aspose.Cells w swoim projekcie, tworząc wystąpienie `Workbook` klasa.

## Przewodnik wdrażania

### Tworzenie skoroszytu i arkusza kalkulacyjnego
1. **Zainicjuj skoroszyt**
   Utwórz nowy skoroszyt w formacie XLSX:
   ```csharp
   Workbook workbook = new Workbook(FileFormatType.Xlsx);
   ```

2. **Dostęp do pierwszego arkusza kalkulacyjnego**
   Wprowadź dane do pierwszego arkusza:
   ```csharp
   Worksheet worksheet = workbook.Worksheets[0];
   ```

3. **Dodawanie danych do wykresu kołowego**
   Wypełnij arkusz kategoriami i wartościami:
   ```csharp
   worksheet.Cells["A1"].PutValue("Retail");
   // Dodaj pozostałe nazwy kategorii...
   worksheet.Cells["B1"].PutValue(10.4);
   // Dodaj odpowiednie wartości...
   ```

### Dodawanie wykresu kołowego do arkusza kalkulacyjnego
1. **Utwórz wykres kołowy**
   Wygeneruj wykres kołowy i dodaj go do kolekcji wykresów w arkuszu kalkulacyjnym:
   ```csharp
   int id = worksheet.Charts.Add(ChartType.Pie, 3, 3, 23, 13);
   ```

2. **Konfigurowanie danych serii i kategorii**
   Połącz dane dla serii i kategorii:
   ```csharp
   Chart chart = worksheet.Charts[id];
   chart.NSeries.Add("B1:B16", true);
   chart.NSeries.CategoryData = "A1:A16";
   ```

3. **Dostosuj etykiety danych**
   Wyłącz wyświetlanie legendy, ustaw etykiety danych tak, aby pokazywały nazwy kategorii i procenty:
   ```csharp
   chart.ShowLegend = false;
   DataLabels dataLabels = chart.NSeries[0].DataLabels;
   dataLabels.ShowCategoryName = true;
   dataLabels.ShowPercentage = true;
   dataLabels.Position = LabelPositionType.OutsideEnd;
   ```

### Wdrażanie linii wiodących
1. **Włącz linie odniesienia**
   Włącz linie pomocnicze, aby uzyskać wyraźniejsze połączenia wizualne:
   ```csharp
   chart.NSeries[0].HasLeaderLines = true;
   ```

2. **Dostosuj położenie etykiet danych**
   Zapewnij widoczność, dostosowując położenie etykiet:
   ```csharp
   int DELTA = 100;
   foreach (var point in chart.NSeries[0].Points)
   {
       int X = point.DataLabels.X;
       if (X > 2000) 
           point.DataLabels.X += DELTA;
       else 
           point.DataLabels.X -= DELTA;
   }
   ```

### Zapisywanie wykresu i skoroszytu
1. **Zapisz jako obraz**
   Wyrenderuj wykres do pliku obrazu:
   ```csharp
   ImageOrPrintOptions options = new ImageOrPrintOptions { ImageType = Drawing.ImageType.Png, HorizontalResolution = 200, VerticalResolution = 200 };
   chart.ToImage("output_out.png", options);
   ```

2. **Zapisz skoroszyt**
   Zapisz skoroszyt, aby wyświetlić wykres w programie Excel:
   ```csharp
   workbook.Save("output_out.xlsx");
   ```

## Zastosowania praktyczne
- **Sprawozdania finansowe**:Jasno przedstawiaj podział budżetu.
- **Analityka marketingowa**:Efektywna wizualizacja danych dotyczących udziału w rynku w prezentacjach lub raportach.
- **Analiza sprzedaży**:Łatwe wyświetlanie podziału sprzedaży pomiędzy różnymi regionami/produktami.

Możliwości integracji obejmują eksportowanie tych wizualizacji do aplikacji internetowych lub osadzanie ich w zautomatyzowanych narzędziach do raportowania.

## Rozważania dotyczące wydajności
Podczas korzystania z Aspose.Cells, aby uzyskać optymalną wydajność, należy wziąć pod uwagę następujące kwestie:
- Minimalizuj duże zbiory danych ładowane do pamięci na raz.
- Używaj wydajnych pętli i unikaj niepotrzebnych obliczeń w ich obrębie.
- Regularnie czyść zasoby, takie jak obiekty skoroszytu, aby zapobiegać wyciekom pamięci.

## Wniosek
Nauczyłeś się, jak tworzyć wykresy kołowe z liniami odniesienia za pomocą Aspose.Cells dla .NET. Ta funkcjonalność zwiększa przejrzystość wizualizacji danych, czyniąc je bardziej dostępnymi i efektownymi. 

**Następne kroki:**
Poznaj dalsze możliwości dostosowywania wyglądu wykresów lub eksperymentuj z innymi typami wykresów dostępnymi w Aspose.Cells.

## Sekcja FAQ
1. **Czym jest linia odniesienia na wykresie kołowym?**
   Linie pomocnicze łączą etykiety danych z odpowiednimi segmentami, zwiększając czytelność.

2. **Czy mogę używać Aspose.Cells za darmo?**
   Tak, możesz zacząć od bezpłatnego okresu próbnego, ale pełny dostęp do funkcji wymaga licencji.

3. **Czy można eksportować wykresy jako obrazy?**
   Oczywiście! Użyj `ImageOrPrintOptions` aby zapisać wykres w formatach graficznych, takich jak PNG lub JPEG.

4. **Jak ręcznie dostosować położenie etykiet danych?**
   Modyfikuj współrzędne X i Y etykiet danych w pętli punktów serii.

5. **Czy Aspose.Cells można zintegrować z innymi systemami?**
   Tak, można go używać w połączeniu z bazami danych, usługami sieciowymi i innymi rozwiązaniami do automatycznego raportowania.

## Zasoby
- [Dokumentacja Aspose.Cells](https://reference.aspose.com/cells/net/)
- [Pobierz Aspose.Cells](https://releases.aspose.com/cells/net/)
- [Kup licencję](https://purchase.aspose.com/buy)
- [Bezpłatna wersja próbna](https://releases.aspose.com/cells/net/)
- [Licencja tymczasowa](https://purchase.aspose.com/temporary-license/)
- [Forum wsparcia](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}