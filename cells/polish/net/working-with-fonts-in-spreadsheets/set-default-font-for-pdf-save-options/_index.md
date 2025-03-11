---
title: Ustaw domyślną czcionkę dla opcji zapisywania PDF
linktitle: Ustaw domyślną czcionkę dla opcji zapisywania PDF
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak ustawić domyślne czcionki dla opcji zapisywania plików PDF przy użyciu Aspose.Cells for .NET, aby mieć pewność, że Twoje dokumenty będą za każdym razem wyglądać idealnie.
weight: 11
url: /pl/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ustaw domyślną czcionkę dla opcji zapisywania PDF

## Wstęp
Jeśli chodzi o generowanie raportów, faktur lub innych dokumentów w formacie PDF, najważniejsze jest zapewnienie, że treść wygląda idealnie. Czcionki odgrywają kluczową rolę w utrzymaniu atrakcyjności wizualnej i czytelności dokumentów. Co się jednak stanie, gdy czcionka użyta w pliku Excel nie będzie dostępna w systemie, w którym generujesz plik PDF? W tym miejscu przydaje się Aspose.Cells dla .NET. Ta potężna biblioteka umożliwia ustawienie domyślnych czcionek dla opcji zapisywania pliku PDF, zapewniając, że dokumenty będą wyglądać profesjonalnie i spójnie, niezależnie od tego, gdzie zostaną otwarte.
## Wymagania wstępne
Zanim zaczniemy, upewnij się, że masz następujące rzeczy:
1. Visual Studio: Będziesz potrzebować środowiska programistycznego, takiego jak Visual Studio, aby pisać i wykonywać kod.
2.  Aspose.Cells dla .NET: Najnowszą wersję można pobrać ze strony[ten link](https://releases.aspose.com/cells/net/)Alternatywnie możesz zainstalować go za pomocą Menedżera pakietów NuGet w programie Visual Studio.
3. Podstawowa wiedza o języku C#: Zrozumienie podstaw języka C# pomoże Ci zrozumieć przykłady kodu.
4. Przykładowy plik Excela: Przygotuj przykładowy plik Excela do testowania. Możesz utworzyć plik z różnymi czcionkami i stylami, aby zobaczyć, jak Aspose.Cells radzi sobie z brakującymi czcionkami.
## Importuj pakiety
Zanim będziesz mógł użyć Aspose.Cells w swoim projekcie, musisz zaimportować niezbędne pakiety. Oto jak to zrobić:
1. Otwórz swój projekt: Uruchom program Visual Studio i otwórz istniejący projekt lub utwórz nowy.
2. Dodaj odwołania: Kliknij prawym przyciskiem myszy swój projekt w Eksploratorze rozwiązań i wybierz opcję „Zarządzaj pakietami NuGet”.
3. Zainstaluj Aspose.Cells: Wyszukaj „Aspose.Cells” i kliknij przycisk „Zainstaluj”.
4. Dodaj dyrektywy Using: Na górze pliku C# dodaj następujące przestrzenie nazw:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## Krok 1: Skonfiguruj swoje katalogi
Przed rozpoczęciem pracy z plikami ważne jest zdefiniowanie katalogów źródłowych i wyjściowych. Ułatwi to zlokalizowanie pliku wejściowego Excel i zapisanie wygenerowanych plików wyjściowych.
```csharp
// Katalog źródłowy
string sourceDir = "Your Document Directory";
// Katalog wyjściowy
string outputDir = "Your Document Directory";
```
 Zastępować`"Your Document Directory"` z rzeczywistą ścieżką do Twoich katalogów.
## Krok 2: Otwórz plik Excel
 Teraz, gdy mamy już skonfigurowane katalogi, otwórzmy plik Excela, z którym chcesz pracować.`Workbook` Klasa w Aspose.Cells służy do załadowania dokumentu Excel.
```csharp
// Otwórz plik Excel
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
Pamiętaj o zastąpieniu nazwy pliku rzeczywistą nazwą pliku.
## Krok 3: Skonfiguruj opcje renderowania obrazu
Następnie musimy skonfigurować opcje renderowania, aby przekonwertować nasz arkusz Excela na format obrazu. Utworzymy wystąpienie`ImageOrPrintOptions`, określając typ obrazu i domyślną czcionkę.
```csharp
// Renderowanie do formatu pliku PNG
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
 W tym fragmencie kodu ustawiamy`CheckWorkbookDefaultFont` nieruchomość do`false`, co oznacza, że jeśli brakuje którejkolwiek czcionki, zamiast niej zostanie użyta określona czcionka domyślna („Times New Roman”).
## Krok 4: Renderuj arkusz jako obraz
 Teraz wyrenderujmy pierwszy arkusz skoroszytu jako obraz PNG. Użyjemy`SheetRender` klasa, aby to osiągnąć.
```csharp
// Wyrenderuj pierwszy arkusz kalkulacyjny do obrazu
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## Krok 5: Zmień typ obrazu i renderuj do TIFF
 Jeśli chcesz wyrenderować ten sam arkusz w innym formacie obrazu, np. TIFF, możesz po prostu zmienić`ImageType` właściwość i powtórz proces renderowania.
```csharp
// Ustaw na format TIFF
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## Krok 6: Skonfiguruj opcje zapisywania pliku PDF
 Następnie skonfigurujmy opcje zapisu PDF. Utworzymy wystąpienie`PdfSaveOptions`ustaw domyślną czcionkę i określ, że chcesz sprawdzić, czy brakuje niektórych czcionek.
```csharp
// Konfiguruj opcje zapisywania PDF
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## Krok 7: Zapisz skoroszyt jako plik PDF
Po skonfigurowaniu opcji zapisu nadszedł czas na zapisanie skoroszytu programu Excel jako pliku PDF. 
```csharp
// Zapisz skoroszyt w formacie PDF
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## Krok 8: Potwierdź wykonanie
Na koniec, dobrym zwyczajem jest poinformowanie użytkownika, że proces zakończył się pomyślnie. Można to osiągnąć, używając prostego komunikatu konsoli.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## Wniosek
Aspose.Cells zapewnia elastyczny i solidny sposób obsługi manipulacji plikami Excela, ułatwiając programistom tworzenie atrakcyjnych wizualnie dokumentów, które zachowują swoje formatowanie. Niezależnie od tego, czy pracujesz nad raportami, dokumentami finansowymi czy jakąkolwiek inną formą prezentacji danych, kontrola nad renderowaniem czcionek może znacznie poprawić jakość wyników.
## Najczęściej zadawane pytania
### Czym jest Aspose.Cells?
Aspose.Cells to potężna biblioteka .NET, która umożliwia programistom manipulowanie plikami Excel bez konieczności instalowania programu Microsoft Excel. Obsługuje różne formaty plików i oferuje bogate funkcje do pracy z arkuszami kalkulacyjnymi.
### Jak mogę ustawić domyślną czcionkę dla plików Excel?
 Możesz ustawić domyślną czcionkę za pomocą`PdfSaveOptions` class i określ żądaną nazwę czcionki. Dzięki temu nawet jeśli brakuje czcionki, Twój dokument użyje domyślnej czcionki, którą określiłeś.
### Czy mogę konwertować pliki Excel do formatów innych niż PDF?
Oczywiście! Aspose.Cells pozwala konwertować pliki Excela do różnych formatów, w tym obrazów (PNG, TIFF), HTML, CSV i innych.
### Czy korzystanie z Aspose.Cells jest bezpłatne?
Aspose.Cells jest produktem komercyjnym, ale możesz wypróbować go za darmo w ograniczonej wersji próbnej. Aby uzyskać pełną funkcjonalność, musisz kupić licencję.
### Gdzie mogę znaleźć pomoc dotyczącą Aspose.Cells?
 Pomoc dotyczącą Aspose.Cells można znaleźć na stronie[Forum Aspose](https://forum.aspose.com/c/cells/9), gdzie możesz zadawać pytania i dzielić się swoimi spostrzeżeniami z innymi użytkownikami i programistami.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
