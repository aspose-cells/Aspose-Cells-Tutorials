---
"date": "2025-04-05"
"description": "Dowiedz się, jak dodawać i dostosowywać znaki wodne w arkuszach Excela przy użyciu Aspose.Cells dla .NET. Ten przewodnik obejmuje konfigurację, implementację i funkcje zabezpieczeń."
"title": "Jak dodać znaki wodne w programie Excel za pomocą Aspose.Cells .NET&#58; Kompleksowy przewodnik"
"url": "/pl/net/headers-footers/excel-watermark-aspose-cells-net-tutorial/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Jak dodać znaki wodne w programie Excel za pomocą Aspose.Cells .NET

dzisiejszym cyfrowym świecie ochrona poufnych danych jest kluczowa podczas udostępniania dokumentów, takich jak arkusze kalkulacyjne. Dodawanie znaków wodnych — subtelnej, ale silnej wskazówki wizualnej — może wskazywać na poufność lub własność. Ten kompleksowy przewodnik przeprowadzi Cię przez korzystanie z Aspose.Cells dla .NET w celu dodawania i dostosowywania efektów tekstowych znaków wodnych w arkuszach Excela.

## Czego się nauczysz
- Konfigurowanie Aspose.Cells dla platformy .NET w środowisku programistycznym.
- Dodawanie znaku wodnego do arkusza Excel za pomocą języka C#.
- Dostosowywanie wyglądu znaków wodnych, w tym ustawień koloru i przezroczystości.
- Blokowanie kształtów w programie Excel w celu uniemożliwienia nieautoryzowanych modyfikacji.
- Praktyczne zastosowania w celu zwiększenia bezpieczeństwa dokumentów.

Przyjrzyjmy się, jak możesz wdrożyć te funkcjonalności w swoich projektach.

## Wymagania wstępne
Zanim zaczniemy, upewnij się, że masz:
- **Studio wizualne** zainstalowana na Twoim komputerze (dowolna wersja od 2017 r.).
- Podstawowa znajomość programowania w języku C# i .NET.
- Ogólna wiedza na temat manipulowania plikami Excela za pomocą interfejsów API.

Dodatkowo zainstaluj Aspose.Cells dla .NET za pomocą konsoli NuGet Package Manager lub .NET CLI:

**Menedżer pakietów NuGet**
```bash
PM> Install-Package Aspose.Cells
```

**Interfejs wiersza poleceń .NET**
```bash
dotnet add package Aspose.Cells
```

### Nabycie licencji
Aby zacząć korzystać z Aspose.Cells dla platformy .NET, możesz skorzystać z bezpłatnej licencji próbnej i poznać jej możliwości:
1. **Bezpłatna wersja próbna:** Odwiedź [Załóż tymczasową stronę licencyjną](https://purchase.aspose.com/temporary-license/) i poproś o tymczasową licencję.
2. **Zakup:** W celu długoterminowego użytkowania należy zakupić licencję za pośrednictwem [Strona zakupu Aspose](https://purchase.aspose.com/buy).

### Podstawowa konfiguracja
Po pobraniu pakietu Aspose.Cells za pomocą NuGet lub CLI zainicjuj go w swoim projekcie C#:
```csharp
using Aspose.Cells;
```

## Konfigurowanie Aspose.Cells dla .NET
Poniżej znajduje się krótki przegląd konfiguracji i inicjalizacji Aspose.Cells:
1. **Zainstalować** Aspose.Cells przy użyciu konsoli Menedżera pakietów lub .NET CLI, jak pokazano powyżej.
2. **Zainicjuj:** Zacznij od utworzenia `Workbook` obiekt reprezentujący plik Excela.

```csharp
Workbook workbook = new Workbook();
```
3. **Zastosuj licencję:** Jeśli posiadasz licencję, użyj jej, aby odblokować pełną funkcjonalność.

## Przewodnik wdrażania

### Funkcja 1: Dodaj znak wodny do arkusza Excel
#### Przegląd
Dodanie znaku wodnego wiąże się z utworzeniem efektów tekstowych, które subtelnie nakładają się na dane, sygnalizując status dokumentu, np. „POUFNE”.

#### Wdrażanie krok po kroku
##### Utwórz skoroszyt i arkusz kalkulacyjny
```csharp
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

##### Dodaj efekt tekstowy jako znak wodny
Utwórz kształt efektu tekstowego ze specjalnymi atrybutami, takimi jak styl czcionki, rozmiar, położenie i wygląd.

```csharp
Shape wordart = sheet.Shapes.AddTextEffect(
    MsoPresetTextEffect.TextEffect1,
    "CONFIDENTIAL", 
    "Arial Black",
    50,   // Rozmiar czcionki
    false, // Jest kursywą
    true, // Jest odważny
    18,   // Pozycja lewa
    8,    // Najwyższa pozycja
    1,    // Szerokość
    1,    // Wysokość
    130,  // Kąt obrotu
    800   // Współczynnik skali
);
```

##### Dostosuj wygląd
Ustaw kolor gradientu i przezroczystość, aby uzyskać dopracowany wygląd.
```csharp
FillFormat wordArtFormat = wordart.Fill;
wordArtFormat.SetOneColorGradient(Color.Red, 0.2, GradientStyleType.Horizontal, 2); 
wordArtFormat.Transparency = 0.9; // Uczyń to lekko przezroczystym

wordart.HasLine = false; // Usuń linię graniczną, aby uzyskać czystszy wygląd
```

##### Zapisz swój skoroszyt
```csharp
workbook.Save("YOUR_OUTPUT_DIRECTORY\output_out.xlsx");
```

### Funkcja 2: Zablokuj aspekty kształtu w arkuszu Excel
#### Przegląd
Blokowanie kształtów uniemożliwia nieautoryzowanym użytkownikom zmianę znaku wodnego i innych kształtów, co gwarantuje integralność dokumentu.

#### Wdrażanie krok po kroku
##### Zablokuj różne właściwości znaku wodnego
Zabezpiecz swój znak wodny blokując jego aspekty.
```csharp
wordart.IsLocked = true;
wordart.SetLockedProperty(ShapeLockType.Selection, true);
wordart.SetLockedProperty(ShapeLockType.ShapeType, true);
wordart.SetLockedProperty(ShapeLockType.Move, true);
wordart.SetLockedProperty(ShapeLockType.Resize, true);
wordart.SetLockedProperty(ShapeLockType.Text, true);
```

##### Zapisz zmiany
Upewnij się, że zmiany zostały zapisane w skoroszycie.
```csharp
workbook.Save("YOUR_OUTPUT_DIRECTORY\output_out.xlsx");
```

## Zastosowania praktyczne
1. **Raporty poufne:** Używaj znaków wodnych w przypadku raportów wewnętrznych zawierających poufne informacje.
2. **Informacje o prawach autorskich:** Umieść informacje o prawach autorskich w szablonach udostępnianych klientom.
3. **Kontrola wersji:** Wskaż wersje robocze lub ostateczne dokumentów za pomocą odpowiedniego tekstu znaku wodnego.

## Rozważania dotyczące wydajności
- **Optymalizacja zasobów:** Zminimalizuj wykorzystanie zasobów, ładując tylko niezbędne arkusze kalkulacyjne i kształty.
- **Zarządzanie pamięcią:** Pozbywaj się przedmiotów prawidłowo, używając `Dispose()` metody, w stosownych przypadkach, zapewniające efektywne zarządzanie pamięcią w aplikacjach .NET.

## Wniosek
Opanowując użycie Aspose.Cells for .NET do dodawania znaków wodnych i blokowania kształtów w arkuszach Excela, zwiększasz bezpieczeństwo dokumentów i przekazujesz kluczowe informacje na pierwszy rzut oka. Ten przewodnik wyposażył Cię w niezbędne umiejętności, aby skutecznie wdrożyć te funkcje.

### Następne kroki
Odkryj więcej opcji dostosowywania w [Dokumentacja Aspose.Cells](https://reference.aspose.com/cells/net/) lub spróbuj zintegrować te funkcjonalności z większymi systemami wymagającymi solidnego zarządzania dokumentacją.

## Sekcja FAQ
1. **Jak zmienić tekst znaku wodnego?**
   - Zmodyfikuj drugi parametr `AddTextEffect()` metodę z żądanym tekstem.
2. **Czy mogę użyć różnych czcionek w znaku wodnym?**
   - Tak, określ dowolną czcionkę, zmieniając trzeci parametr w `AddTextEffect()`.
3. **Co zrobić, gdy mój plik Excel jest duży i ładowanie przebiega powoli?**
   - Rozważ zoptymalizowanie kodu tak, aby ładował tylko niezbędne części skoroszytu, lub skorzystaj z opcji dostrajania wydajności dostępnych w Aspose.Cells.
4. **Czy można później usunąć znak wodny?**
   - Tak, możesz usuwać kształty z arkusza kalkulacyjnego, w którym się znajdują.
5. **Jak zastosować to rozwiązanie w przetwarzaniu wsadowym?**
   - Przeprowadzaj iteracje po wielu skoroszytach, stosując podobną logikę w pętlach lub zadaniach asynchronicznych w celu zwiększenia wydajności.

## Zasoby
- [Dokumentacja Aspose.Cells](https://reference.aspose.com/cells/net/)
- [Pobierz Aspose.Cells](https://releases.aspose.com/cells/net/)
- [Kup licencję](https://purchase.aspose.com/buy)
- [Uzyskaj bezpłatną wersję próbną](https://releases.aspose.com/cells/net/)
- [Poproś o licencję tymczasową](https://purchase.aspose.com/temporary-license/)
- [Forum wsparcia Aspose](https://forum.aspose.com/c/cells/9)

Teraz, gdy posiadasz już tę wiedzę, czas zastosować te techniki w praktyce i skutecznie zabezpieczyć swoje dokumenty Excel!


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}