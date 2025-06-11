---
"date": "2025-04-05"
"description": "Dowiedz się, jak zaimplementować niestandardowe formaty liczb w .NET przy użyciu Aspose.Cells do precyzyjnej prezentacji danych w programie Excel. Ten przewodnik obejmuje konfigurowanie, formatowanie dat, procentów i walut."
"title": "Jak używać niestandardowych formatów liczbowych w .NET z Aspose.Cells? Przewodnik krok po kroku"
"url": "/pl/net/formatting/custom-number-formats-net-aspose-cells-guide/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Jak używać niestandardowych formatów liczbowych w .NET z Aspose.Cells: przewodnik krok po kroku

## Wstęp

Ulepsz swoje manipulacje plikami Excela za pomocą C# i .NET, zapewniając precyzyjną kontrolę nad formatami liczb. Ten samouczek przeprowadzi Cię przez ustawianie niestandardowych formatów liczb w aplikacjach .NET za pomocą Aspose.Cells dla .NET, potężnej biblioteki zaprojektowanej do manipulacji Excelem.

Wykorzystując Aspose.Cells, stosuj różne style do danych bez wysiłku, zapewniając przejrzystość i precyzję w swoich raportach. Niezależnie od tego, czy formatujesz daty, procenty czy wartości walutowe, opanowanie tej funkcjonalności usprawnia Twój przepływ pracy.

**Czego się nauczysz:**
- Konfigurowanie Aspose.Cells dla .NET
- Implementacja niestandardowych formatów liczbowych za pomocą języka C#
- Stosowanie stylów programowo do komórek programu Excel
- Zastosowania w świecie rzeczywistym niestandardowego formatowania liczb

## Wymagania wstępne

Przed rozpoczęciem upewnij się, że masz następujące rzeczy:
1. **Środowisko programistyczne**:Działająca konfiguracja .NET z programem Visual Studio lub dowolnym kompatybilnym środowiskiem IDE.
2. **Biblioteka Aspose.Cells dla .NET**:Do korzystania z tego przewodnika wymagana jest wersja 22.x lub nowsza.
3. **Podstawowa wiedza o C#**:Znajomość składni języka C# i koncepcji programowania pomoże Ci płynnie nadążać za nauką.

## Konfigurowanie Aspose.Cells dla .NET

Aby użyć Aspose.Cells w swoim projekcie, zainstaluj bibliotekę za pomocą interfejsu wiersza poleceń .NET CLI lub konsoli Menedżera pakietów w programie Visual Studio.

**Instalacja .NET CLI:**
```bash
dotnet add package Aspose.Cells
```

**Instalacja Menedżera Pakietów:**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

### Nabycie licencji

Aspose.Cells oferuje bezpłatną wersję próbną w celu przetestowania i możliwość dłuższego użytkowania na podstawie licencji tymczasowej lub zakupionej.
- **Bezpłatna wersja próbna**: Pobierz z [Tutaj](https://releases.aspose.com/cells/net/).
- **Licencja tymczasowa**:Złóż wniosek w [Strona tymczasowej licencji Aspose](https://purchase.aspose.com/temporary-license/) aby usunąć ograniczenia oceny.
- **Zakup**:Aby uzyskać pełny dostęp, odwiedź stronę [Strona zakupu](https://purchase.aspose.com/buy).

Aby zainicjować Aspose.Cells w projekcie:
```csharp
// Importuj przestrzeń nazw
using Aspose.Cells;

// Zainicjuj nowy obiekt skoroszytu
Workbook workbook = new Workbook();
```

## Przewodnik wdrażania

Omówimy najważniejsze funkcje dostosowywania formatów liczb za pomocą Aspose.Cells.

### Dodawanie niestandardowego formatu daty
**Przegląd**:Naucz się formatować daty w komórkach programu Excel przy użyciu niestandardowego stylu.
1. **Utwórz lub uzyskaj dostęp do arkusza kalkulacyjnego**
   ```csharp
   int sheetIndex = workbook.Worksheets.Add();
   Worksheet worksheet = workbook.Worksheets[sheetIndex];
   ```
2. **Ustaw bieżącą datę systemową w niestandardowym formacie**
   Dodaj bieżącą datę do komórki „A1” i zastosuj niestandardowy format wyświetlania.
   ```csharp
   // Wstaw bieżącą datę systemową do A1
   worksheet.Cells["A1"].PutValue(DateTime.Now);

   // Pobierz obiekt stylu do dostosowania
   Style style = worksheet.Cells["A1"].GetStyle();

   // Ustaw niestandardowy format liczbowy na „d-mmm-rr”
   style.Custom = "d-mmm-yy";

   // Zastosuj ponownie dostosowany styl do komórki A1
   worksheet.Cells["A1"].SetStyle(style);
   ```

### Formatowanie wartości liczbowych jako procentów
**Przegląd**: Wyświetla wartości liczbowe w formacie procentowym.
1. **Wstaw i sformatuj wartość**
   ```csharp
   // Dodaj wartość liczbową do komórki A2
   worksheet.Cells["A2"].PutValue(20);

   // Pobierz styl formatowania
   Style style = worksheet.Cells["A2"].GetStyle();

   // Zastosuj niestandardowy format liczbowy jako procent
   style.Custom = "0.0%";

   // Przywróć sformatowany styl komórki A2
   worksheet.Cells["A2"].SetStyle(style);
   ```

### Stosowanie formatu waluty
**Przegląd**:Pokaż liczby w formacie walutowym, ze specjalnym formatowaniem dla wartości ujemnych.
1. **Wstaw i styl wartości waluty**
   ```csharp
   // Dodaj wartość do komórki A3
   worksheet.Cells["A3"].PutValue(2546);

   // Uzyskaj dostęp do obiektu stylu
   Style style = worksheet.Cells["A3"].GetStyle();

   // Ustaw niestandardowy format waluty
   style.Custom = "\u00a3#,##0;[Red]$-#,##0";

   // Zastosuj do komórki A3
   worksheet.Cells["A3"].SetStyle(style);
   ```

## Zastosowania praktyczne

Niestandardowe formatowanie liczb jest nieocenione w następujących sytuacjach:
1. **Sprawozdania finansowe**:Formatowanie wartości walutowych w celu zapewnienia przejrzystości.
2. **Panele sprzedaży**:Wyświetlanie danych sprzedaży jako procentów w celu uwypuklenia wskaźników wydajności.
3. **Planowanie wydarzeń**:Wykorzystywanie formatów dat do płynnej organizacji i prezentacji harmonogramów wydarzeń.

## Rozważania dotyczące wydajności
Podczas pracy z dużymi zbiorami danych należy zoptymalizować wydajność Aspose.Cells:
- Zminimalizuj użycie pamięci, szybko usuwając obiekty za pomocą `GC.Collect()` po zapisaniu plików.
- Wykorzystuj strumienie do odczytu/zapisu plików Excela zamiast ładowania całych dokumentów do pamięci.
- Wdrażaj najlepsze praktyki w zakresie zarządzania pamięcią .NET, aby zachować wydajność.

## Wniosek
Postępując zgodnie z tym przewodnikiem, nauczyłeś się, jak implementować niestandardowe formaty liczb w swoich aplikacjach .NET przy użyciu Aspose.Cells. Ta możliwość poprawia prezentację danych i zapewnia dokładność i atrakcyjność wizualną w raportach i arkuszach kalkulacyjnych.

**Następne kroki**:Eksperymentuj z innymi opcjami formatowania dostępnymi w Aspose.Cells, takimi jak formatowanie warunkowe lub ulepszenia wykresów.

## Sekcja FAQ
1. **Jak uzyskać tymczasową licencję na Aspose.Cells?**
   - Złóż wniosek w [Strona licencji tymczasowej](https://purchase.aspose.com/temporary-license/).
2. **Jakie formaty są obsługiwane dla niestandardowych stylów liczbowych w Aspose.Cells?**
   - Data, procent, waluta i inne dane przy użyciu standardowych ciągów znaków w formacie programu Excel.
3. **Czy mogę używać Aspose.Cells z innymi językami .NET, takimi jak VB.NET?**
   - Tak, biblioteka jest kompatybilna ze wszystkimi językami obsługiwanymi przez platformę .NET.
4. **Co zrobić, jeśli sformatowane liczby nie wyświetlają się prawidłowo?**
   - Sprawdź dokładnie swój niestandardowy ciąg formatu liczbowego pod kątem literówek i błędów składniowych.
5. **Gdzie mogę znaleźć więcej przykładów użycia Aspose.Cells?**
   - Zapoznaj się ze szczegółową dokumentacją i przykładowymi kodami na stronie [Dokumentacja Aspose](https://reference.aspose.com/cells/net/).

## Zasoby
- [Dokumentacja Aspose.Cells dla .NET](https://reference.aspose.com/cells/net/)
- [Pobierz najnowszą wersję](https://releases.aspose.com/cells/net/)
- [Kup licencję](https://purchase.aspose.com/buy)
- [Bezpłatna wersja próbna do pobrania](https://releases.aspose.com/cells/net/)
- [Wniosek o licencję tymczasową](https://purchase.aspose.com/temporary-license/)
- [Forum wsparcia Aspose](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}