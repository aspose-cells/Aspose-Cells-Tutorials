---
"date": "2025-04-05"
"description": "Dowiedz się, jak renderować pliki Excel do formatów PNG, TIFF i PDF, używając niestandardowych czcionek z Aspose.Cells dla .NET. Zapewnij spójną typografię we wszystkich konwersjach dokumentów."
"title": "Renderowanie plików Excel do formatu PNG, TIFF, PDF z niestandardowymi czcionkami w środowisku .NET przy użyciu Aspose.Cells"
"url": "/pl/net/workbook-operations/render-excel-custom-fonts-aspose-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Renderuj pliki Excel do formatów PNG, TIFF i PDF z niestandardowymi czcionkami za pomocą Aspose.Cells dla .NET

## Wstęp

Utrzymanie integralności czcionek podczas konwersji plików Excel na obrazy lub pliki PDF jest kluczowe dla spójności marki. Aspose.Cells dla .NET oferuje solidne rozwiązanie, umożliwiając określenie niestandardowych domyślnych czcionek w konwersjach dokumentów.

W tym samouczku przeprowadzimy Cię przez renderowanie plików Excel do formatów PNG, TIFF i PDF przy użyciu Aspose.Cells dla .NET z określonymi niestandardowymi czcionkami domyślnymi. Jest to idealne rozwiązanie, jeśli:
- Dąż do zachowania spójnej typografii w generowanych dokumentach.
- Podczas konwersji należy dostosować ustawienia czcionek.
- Chcesz poznać opcje konfiguracji Aspose.Cells dla .NET?

Skonfigurujmy Twoje środowisko i bezproblemowo wdróżmy te funkcje.

### Wymagania wstępne

Przed rozpoczęciem upewnij się, że masz następujące rzeczy:
- **Środowisko .NET**: Skonfiguruj na swoim komputerze (najlepiej .NET Core lub .NET Framework).
- **Biblioteka Aspose.Cells dla .NET**: Zainstalowano w Twoim projekcie.
- **Plik Excela**: Skoroszyt programu Excel z danymi do konwersji.

### Konfigurowanie Aspose.Cells dla .NET

Na początek dodaj bibliotekę Aspose.Cells do swojego projektu:

**Korzystanie z interfejsu wiersza poleceń .NET:**
```bash
dotnet add package Aspose.Cells
```

**Korzystanie z Menedżera pakietów:**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

Uzyskaj licencję zapewniającą pełny dostęp do funkcji:
- **Bezpłatna wersja próbna**: Odwiedzać [Bezpłatna wersja próbna Aspose](https://releases.aspose.com/cells/net/) w celu uzyskania wstępnego dostępu.
- **Licencja tymczasowa**:Uzyskaj to z [Licencja tymczasowa Aspose](https://purchase.aspose.com/temporary-license/).
- **Zakup**Aby uzyskać stałą licencję, przejdź do [Zakup Aspose](https://purchase.aspose.com/buy).

Po nabyciu licencji zainicjuj Aspose.Cells w swojej aplikacji:
```csharp
// Ustaw licencję dla Aspose.Cells.
License license = new License();
license.SetLicense("path_to_your_license_file");
```

## Przewodnik wdrażania

### Renderowanie do PNG z niestandardową domyślną czcionką

Renderowanie arkusza kalkulacyjnego Excela do PNG podczas ustawiania niestandardowej domyślnej czcionki zapewnia spójność wizualną. Oto jak:

#### Krok 1: Skonfiguruj opcje obrazu

Skonfiguruj opcje renderowania dla wyjściowego obrazu.
```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Określ katalogi.
string SourceDir = @"YOUR_SOURCE_DIRECTORY";
string outputDir = @"YOUR_OUTPUT_DIRECTORY";

// Otwórz plik Excel.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// Skonfiguruj opcje renderowania obrazu.
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false; // Użyj niestandardowej czcionki w celu uzupełnienia brakujących czcionek w skoroszycie.
imgOpt.DefaultFont = "Times New Roman";
```

#### Krok 2: Renderowanie i zapisywanie

Wyrenderuj arkusz kalkulacyjny do pliku obrazu, korzystając z tych ustawień.
```csharp
// Wyrenderuj pierwszy arkusz do obrazu PNG.
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```

### Renderowanie do TIFF z niestandardową domyślną czcionką

Format TIFF jest idealny do obrazów wysokiej jakości. Oto jak możesz renderować cały skoroszyt jako plik TIFF:

#### Krok 3: Skonfiguruj opcje obrazu dla TIFF

Skonfiguruj opcje renderowania specjalnie pod kątem wyjścia TIFF.
```csharp
// Ponownie wykorzystaj wcześniej zdefiniowane katalogi i otwórz plik Excela.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// Skonfiguruj opcje renderowania obrazu dla formatu TIFF.
imgOpt.ImageType = Drawing.ImageType.Tiff;
```

#### Krok 4: Renderowanie całego skoroszytu do formatu TIFF

Konwertuj cały skoroszyt do pojedynczego pliku TIFF.
```csharp
// Wyrenderuj skoroszyt jako obraz TIFF.
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```

### Renderowanie do pliku PDF z niestandardową domyślną czcionką

Zapisywanie skoroszytu programu Excel w formacie PDF przy jednoczesnym zachowaniu spójności czcionek ma kluczowe znaczenie w przypadku profesjonalnej dokumentacji.

#### Krok 5: Skonfiguruj opcje zapisywania pliku PDF

Skonfiguruj niezbędne opcje, aby zapisać plik w formacie PDF.
```csharp
using Aspose.Cells;

// Otwórz ponownie skoroszyt.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// Skonfiguruj opcje zapisywania pliku PDF.
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false; // Użyj niestandardowej czcionki w celu uzupełnienia brakujących czcionek w skoroszycie.
```

#### Krok 6: Zapisz jako PDF

Eksportuj skoroszyt do dokumentu PDF.
```csharp
// Zapisz skoroszyt jako plik PDF.
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```

## Zastosowania praktyczne

- **Raporty biznesowe**: Zapewnij spójność marki we wszystkich eksportowanych raportach, używając niestandardowych czcionek.
- **Archiwizacja dokumentów**:Konwertuj starsze pliki programu Excel do formatu PDF, aby łatwo je udostępniać i archiwizować, zachowując jednolitą typografię.
- **Projektowanie graficzne**:Twórz obrazy TIFF o wysokiej rozdzielczości zawierające dane z programu Excel na potrzeby prezentacji lub projektów.

Integracja z innymi systemami, takimi jak platformy CRM lub rozwiązania do zarządzania dokumentacją, może dodatkowo usprawnić te przypadki użycia poprzez automatyzację eksportu na podstawie określonych wyzwalaczy lub zdarzeń.

## Rozważania dotyczące wydajności

Optymalizacja procesu renderowania jest kluczowa:
- **Zarządzanie pamięcią**:Pozbądź się `Workbook`, `SheetRender`, I `WorkbookRender` obiektów w celu szybkiego zwolnienia zasobów.
- **Przetwarzanie wsadowe**W przypadku wielu plików należy wdrożyć przetwarzanie wsadowe w celu zapewnienia wydajnej obsługi.
- **Operacje asynchroniczne**:W miarę możliwości należy wykorzystywać metody asynchroniczne w celu zwiększenia responsywności aplikacji.

## Wniosek

Opanowałeś już renderowanie skoroszytów programu Excel do formatów PNG, TIFF i PDF, ustawiając niestandardowe domyślne czcionki za pomocą Aspose.Cells dla .NET. Ta możliwość zapewnia, że Twoje dokumenty zachowują integralność wizualną na różnych platformach i w różnych zastosowaniach.

Poznaj dodatkowe funkcje oferowane przez Aspose.Cells, aby jeszcze bardziej udoskonalić możliwości obsługi dokumentów. Aby uzyskać więcej informacji lub pomocy, odwiedź stronę [Forum Aspose](https://forum.aspose.com/c/cells/9).

## Sekcja FAQ

**1. Czym jest Aspose.Cells dla .NET?**
   — Aspose.Cells dla .NET to biblioteka oferująca rozbudowane funkcje umożliwiające programowe zarządzanie plikami Excel i ich konwersję.

**2. Czy mogę używać Aspose.Cells w aplikacjach internetowych?**
   — Tak, Aspose.Cells można zintegrować z ASP.NET lub dowolną inną aplikacją internetową opartą na technologii .NET.

**3. Jak poradzić sobie z brakującymi czcionkami podczas renderowania?**
   — Ustawiając `CheckWorkbookDefaultFont` na fałsz i określając `DefaultFont`, masz pewność, że cały tekst będzie zawierał wybraną przez Ciebie czcionkę, nawet jeśli oryginał jest niedostępny.

**4. Czy są obsługiwane inne formaty niż PNG, TIFF i PDF?**
   — Tak, Aspose.Cells obsługuje różne formaty obrazów, takie jak JPEG, BMP itp. i oferuje rozbudowane możliwości konwersji dokumentów.

**5. Jakie są najlepsze praktyki korzystania z Aspose.Cells w aplikacjach na dużą skalę?**
   — Wykorzystuj efektywne techniki zarządzania pamięcią, przetwarzanie wsadowe w celu obsługi wielu plików i rozważ operacje asynchroniczne w celu zwiększenia wydajności aplikacji.

## Zasoby
- **Dokumentacja**: [Dokumentacja Aspose.Cells](https://reference.aspose.com/cells/net/)
- **Pobierać**: [Wydania Aspose.Cells](https://releases.aspose.com/cells/net/)
- **Zakup**: [Kup Aspose.Cells](https://purchase.aspose.com/buy)
- **Bezpłatna wersja próbna**: [Wypróbuj Aspose.Cells za darmo](https://releases.aspose.com/cells/net/)
- **Licencja tymczasowa**: [Uzyskaj tymczasową licencję](https://purchase.aspose.com/temporary-license/) 


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}