---
"date": "2025-04-05"
"description": "Samouczek dotyczący kodu dla Aspose.Cells Net"
"title": "Tworzenie wykresu kołowego w .NET za pomocą Aspose.Cells&#58; Kompletny przewodnik"
"url": "/pl/net/charts-graphs/create-pie-chart-dotnet-aspose-cells-guide/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Jak utworzyć wykres kołowy w .NET przy użyciu Aspose.Cells: przewodnik krok po kroku

## Wstęp

Tworzenie wizualnych reprezentacji danych jest podstawową umiejętnością, zwłaszcza gdy próbujesz przekazać złożone informacje w prosty i skuteczny sposób. Niezależnie od tego, czy pracujesz nad raportem biznesowym, czy analizujesz statystyki demograficzne, wykresy kołowe oferują prosty sposób na zilustrowanie części całości. Ten przewodnik przeprowadzi Cię przez proces tworzenia wykresu kołowego w .NET przy użyciu Aspose.Cells — potężnej biblioteki, która upraszcza programową pracę z dokumentami Excela.

**Czego się nauczysz:**
- Jak zainicjować i skonfigurować skoroszyt programu Excel.
- Wprowadzanie danych do komórek arkusza kalkulacyjnego w celu wizualizacji.
- Tworzenie i konfigurowanie wykresu kołowego przy użyciu Aspose.Cells dla .NET.
- Dostosowywanie kolorów wycinków na wykresie kołowym w celu zwiększenia atrakcyjności wizualnej.
- Automatyczne dopasowywanie kolumn i zapisywanie skoroszytu.

Przyjrzyjmy się bliżej, jak możesz wykorzystać Aspose.Cells, aby bez wysiłku tworzyć atrakcyjne wykresy kołowe. Zanim zaczniemy, upewnij się, że spełniasz wymagania wstępne, aby płynnie kontynuować.

## Wymagania wstępne

Aby rozpocząć korzystanie z tego samouczka, upewnij się, że posiadasz:

- **Wymagane biblioteki:** Będziesz potrzebować biblioteki Aspose.Cells for .NET. Upewnij się, że Twój projekt jest skonfigurowany do jej używania.
- **Wymagania dotyczące konfiguracji środowiska:** Odpowiednie środowisko programistyczne, np. Visual Studio, zainstalowane w systemie.
- **Wymagania wstępne dotyczące wiedzy:** Podstawowa znajomość programowania w języku C# i znajomość struktur dokumentów programu Excel.

## Konfigurowanie Aspose.Cells dla .NET

Zanim zagłębisz się w kod, musisz zainstalować bibliotekę Aspose.Cells w swoim projekcie. Oto jak to zrobić:

### Instalacja poprzez CLI
Otwórz terminal lub wiersz poleceń i uruchom:
```bash
dotnet add package Aspose.Cells
```

### Instalacja za pomocą Menedżera Pakietów
Jeśli używasz programu Visual Studio, otwórz konsolę Menedżera pakietów NuGet i wykonaj polecenie:
```powershell
PM> Install-Package Aspose.Cells
```

#### Etapy uzyskania licencji
Możesz zacząć od bezpłatnego okresu próbnego, aby ocenić Aspose.Cells. W przypadku dłuższego użytkowania rozważ uzyskanie tymczasowej licencji lub zakup bezpośrednio z ich strony internetowej.

#### Podstawowa inicjalizacja i konfiguracja

Aby zainicjować bibliotekę w projekcie C#:
```csharp
using Aspose.Cells;

// Utwórz instancję klasy Workbook
Workbook workbook = new Workbook();
```

Ta podstawowa konfiguracja umożliwia rozpoczęcie programowej pracy z plikami Excela.

## Przewodnik wdrażania

### Funkcja 1: Zainicjuj skoroszyt i arkusz kalkulacyjny

**Przegląd:** Ta funkcja umożliwia utworzenie nowego skoroszytu i uzyskanie dostępu do pierwszego arkusza kalkulacyjnego, co przygotowuje grunt pod wprowadzanie danych i tworzenie wykresów.

#### Inicjalizacja krok po kroku
```csharp
using Aspose.Cells;

class InitializeWorkbook {
    public void Run() {
        // Utwórz nowy obiekt skoroszytu
        Workbook workbook = new Workbook();
        
        // Uzyskaj dostęp do pierwszego arkusza w skoroszycie
        Worksheet worksheet = workbook.Worksheets[0];
    }
}
```
Tutaj, `Workbook` reprezentuje plik Excela i dostęp do niego `Worksheets[0]` daje ci pierwszą kartkę.

### Funkcja 2: Wypełnianie danych dla wykresu kołowego

**Przegląd:** Wypełnianie danych jest kluczowe, ponieważ stanowi podstawę wykresu. Ten krok obejmuje wprowadzanie nazw krajów i odpowiadających im procentów populacji świata do określonych komórek.

#### Populacja danych krok po kroku
```csharp
using Aspose.Cells;

class PopulateData {
    public void Run() {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        
        // Wprowadź dane kraju w kolumnie C
        worksheet.Cells["C3"].PutValue("India");
        worksheet.Cells["C4"].PutValue("China");
        worksheet.Cells["C5"].PutValue("United States");
        worksheet.Cells["C6"].PutValue("Russia");
        worksheet.Cells["C7"].PutValue("United Kingdom");
        worksheet.Cells["C8"].PutValue("Others");

        // Wprowadź dane procentowe w kolumnie D
        worksheet.Cells["D2"].PutValue("% of world population");
        worksheet.Cells["D3"].PutValue(25);
        worksheet.Cells["D4"].PutValue(30);
        worksheet.Cells["D5"].PutValue(10);
        worksheet.Cells["D6"].PutValue(13);
        worksheet.Cells["D7"].PutValue(9);
        worksheet.Cells["D8"].PutValue(13);
    }
}
```
Ten krok gwarantuje, że Twoje dane będą gotowe do wizualizacji.

### Funkcja 3: Tworzenie i konfiguracja wykresu kołowego

**Przegląd:** Funkcja ta obejmuje utworzenie wykresu kołowego, ustawienie danych serii i skonfigurowanie różnych właściwości, takich jak tytuł i położenie legendy.

#### Tworzenie wykresu kołowego krok po kroku
```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;

class CreatePieChart {
    public void Run() {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        
        // Dodaj wykres kołowy do arkusza kalkulacyjnego
        int pieIdx = worksheet.Charts.Add(ChartType.Pie, 1, 6, 15, 14);
        Chart pie = worksheet.Charts[pieIdx];

        // Ustaw serię danych dla wykresu
        pie.NSeries.Add("D3:D8", true);

        // Zdefiniuj dane kategorii i skonfiguruj tytuł
        pie.NSeries.CategoryData = "=Sheet1!$C$3:$C$8";
        pie.Title.LinkedSource = "D2";
        pie.Legend.Position = LegendPositionType.Bottom;
        pie.Title.Font.Name = "Calibri";
        pie.Title.Font.Size = 18;
    }
}
```
Ten kod tworzy atrakcyjny wizualnie wykres powiązany z Twoimi danymi.

### Funkcja 4: Dostosuj kolory wycinków na wykresie kołowym

**Przegląd:** Personalizacja wyglądu każdego wycinka zwiększa czytelność i estetykę. Ten krok obejmuje przypisanie unikalnych kolorów do różnych wycinków.

#### Dostosowywanie kolorów krok po kroku
```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;

class CustomizeSliceColors {
    public void Run() {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        int pieIdx = worksheet.Charts.Add(ChartType.Pie, 1, 6, 15, 14);
        Chart pie = worksheet.Charts[pieIdx];
        
        Series srs = pie.NSeries[0];

        // Przypisz niestandardowe kolory do każdego wycinka
        srs.Points[0].Area.ForegroundColor = Color.FromArgb(0, 246, 22, 219);
        srs.Points[1].Area.ForegroundColor = Color.FromArgb(0, 51, 34, 84);
        srs.Points[2].Area.ForegroundColor = Color.FromArgb(0, 46, 74, 44);
        srs.Points[3].Area.ForegroundColor = Color.FromArgb(0, 19, 99, 44);
        srs.Points[4].Area.ForegroundColor = Color.FromArgb(0, 208, 223, 7);
        srs.Points[5].Area.ForegroundColor = Color.FromArgb(0, 222, 69, 8);
    }
}
```
Ten krok doda Twojemu wykresowi żywego akcentu.

### Funkcja 5: Automatyczne dopasowanie kolumn i zapisywanie skoroszytu

**Przegląd:** Ostatnie kroki obejmują dostosowanie szerokości kolumn w celu uzyskania lepszej widoczności danych i zapisanie skoroszytu w formacie Excela.

#### Regulacja i zapisywanie kolumn krok po kroku
```csharp
using Aspose.Cells;

class SaveWorkbook {
    public void Run() {
        string outputDir = "YOUR_OUTPUT_DIRECTORY";
        
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        
        // Automatyczne dopasowywanie kolumn do zawartości
        worksheet.AutoFitColumns();

        // Zapisz skoroszyt jako plik Excela
        workbook.Save(outputDir + "outputCustomSliceSectorColorsPieChart.xlsx", SaveFormat.Xlsx);
    }
}
```
Dzięki temu masz pewność, że Twój dokument końcowy będzie dopracowany i gotowy do prezentacji.

## Zastosowania praktyczne

- **Raporty biznesowe:** Użyj wykresów kołowych, aby przedstawić dystrybucję sprzedaży według regionów.
- **Badania demograficzne:** Wizualizuj dane dotyczące populacji w różnych krajach lub regionach.
- **Narzędzia edukacyjne:** Twórz angażujące pomoce wizualne dla studentów na kursach statystyki.
- **Analiza opieki zdrowotnej:** Wyświetlanie danych dotyczących pacjentów w placówkach służby zdrowia.

## Rozważania dotyczące wydajności

Aby zapewnić optymalną wydajność podczas korzystania z Aspose.Cells, należy wziąć pod uwagę następujące kwestie:

- **Efektywne przetwarzanie danych:** Zarządzaj dużymi zbiorami danych, przetwarzając je w częściach, jeśli to konieczne.
- **Zarządzanie pamięcią:** Prawidłowo pozbywaj się obiektów, aby zwolnić zasoby i uniknąć wycieków pamięci.
- **Zoptymalizowane konfiguracje wykresów:** Zminimalizuj złożone obliczenia i renderowanie podczas tworzenia wykresów, aby zapewnić szybszą wydajność.

## Wniosek

Teraz wiesz, jak utworzyć wykres kołowy w .NET przy użyciu Aspose.Cells. Ta potężna biblioteka upraszcza manipulację dokumentami Excela, pozwalając Ci skupić się na analizie danych, a nie na zawiłościach obsługi plików. Eksperymentuj z różnymi typami wykresów i opcjami dostosowywania dostępnymi w Aspose.Cells, aby jeszcze bardziej udoskonalić swoje aplikacje.

**Następne kroki:**
- Poznaj inne typy wykresów, takie jak wykresy słupkowe i liniowe.
- Zintegruj funkcjonalności Aspose.Cells z większymi projektami .NET w celu uzyskania zautomatyzowanego raportowania.

Gotowy, aby przenieść swoje umiejętności wizualizacji danych na wyższy poziom? Zanurz się głębiej, odkrywając więcej funkcji Aspose.Cells i zacznij wdrażać je w swoich projektach już dziś!

## Sekcja FAQ

1. **Do czego służy Aspose.Cells?**
   - Jest to biblioteka umożliwiająca programowe zarządzanie plikami Excela, umożliwiająca tworzenie, modyfikowanie i analizowanie arkuszy kalkulacyjnych.

2. **Czy mogę używać Aspose.Cells bez licencji?**
   - Tak, ale z ograniczeniami. Bezpłatna wersja próbna lub tymczasowa licencja umożliwia pełny dostęp do funkcji.

3. **Jak mogę jeszcze bardziej dostosować wygląd wykresu kołowego?**
   - Użyj dodatkowych właściwości, takich jak `pie.NSeries[0].Area.Formatting` dla większej kontroli nad estetyką.

4. **Jakie są najczęstsze problemy podczas tworzenia wykresów w Aspose.Cells?**
   - Przed renderowaniem sprawdź, czy zakresy danych są poprawnie określone i czy skonfigurowano wszystkie niezbędne właściwości wykresu.

5. **Jak mogę zintegrować Aspose.Cells z innymi bibliotekami .NET?**
   - Użyj Aspose.Cells jako części większego rozwiązania .NET, wykorzystując jego możliwości wraz z innymi bibliotekami do tworzenia kompleksowych aplikacji.

## Zasoby

- **Dokumentacja:** [Dokumentacja Aspose.Cells](https://reference.aspose.com/cells/net/)
- **Pobierać:** [Wydania Aspose.Cells](https://releases.aspose.com/cells/net/)
- **Zakup:** [Kup Aspose.Cells](https://purchase.aspose.com/buy)
- **Bezpłatna wersja próbna:** [Aspose.Cells Bezpłatna wersja próbna](https://releases.aspose.com/cells/net/)
- **Licencja tymczasowa:** [Uzyskaj tymczasową licencję](https://purchase.aspose.com/temporary-license/)
- **Wsparcie:** [Forum Aspose](https://forum.aspose.com/c/cells/9)

Postępując zgodnie z tym przewodnikiem, jesteś teraz wyposażony w narzędzia do tworzenia atrakcyjnych wizualnie wykresów kołowych w aplikacjach .NET przy użyciu Aspose.Cells. Miłego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}