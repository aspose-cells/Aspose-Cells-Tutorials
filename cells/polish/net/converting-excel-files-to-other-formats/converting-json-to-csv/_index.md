---
title: Konwersja JSON do CSV programowo w .NET
linktitle: Konwersja JSON do CSV programowo w .NET
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak programowo przekonwertować JSON na CSV w .NET przy użyciu Aspose.Cells. Postępuj zgodnie z naszym przewodnikiem krok po kroku, aby zapewnić bezproblemową transformację danych.
weight: 15
url: /pl/net/converting-excel-files-to-other-formats/converting-json-to-csv/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwersja JSON do CSV programowo w .NET

## Wstęp
dzisiejszym cyfrowym świecie obsługa danych w wielu formatach stała się powszechna, a JSON (JavaScript Object Notation) jest jednym z najczęściej używanych formatów wymiany danych. Ale co się stanie, gdy trzeba przekształcić JSON do formatu, który jest bardziej dostępny do analizy, takiego jak CSV (Comma Separated Values)? Ten samouczek przeprowadzi Cię przez proces konwersji JSON do CSV programowo przy użyciu Aspose.Cells dla .NET — łatwego w użyciu, ale potężnego interfejsu API do manipulacji arkuszami kalkulacyjnymi. 
## Wymagania wstępne
Zanim zagłębimy się w kod, ważne jest, aby upewnić się, że masz wszystkie niezbędne komponenty i podstawową wiedzę na temat narzędzi, których będziemy używać. Opiszmy, czego potrzebujesz:
-  Aspose.Cells dla .NET: To jest podstawowa biblioteka, której będziemy używać do konwersji JSON do CSV. Możesz[pobierz tutaj](https://releases.aspose.com/cells/net/).
- Visual Studio: Będziesz potrzebować zintegrowanego środowiska programistycznego (IDE), takiego jak Visual Studio, aby pisać i wykonywać kod .NET.
- .NET Framework: Upewnij się, że masz zainstalowany .NET Framework. Aspose.Cells jest zgodny zarówno z .NET Core, jak i .NET Framework.
- Podstawowa wiedza o języku C#: Chociaż ten przewodnik szczegółowo opisuje każdy fragment kodu, przyda Ci się pewna znajomość języka C#.
## Importuj pakiety
Aby użyć Aspose.Cells w projekcie .NET, musisz najpierw zainstalować bibliotekę. Możesz to zrobić za pomocą NuGet Package Manager:
1. Otwórz program Visual Studio.
2. Przejdź do Narzędzia > Menedżer pakietów NuGet > Zarządzaj pakietami NuGet dla rozwiązania.
3. Wyszukaj Aspose.Cells i zainstaluj najnowszą wersję.
Po zainstalowaniu upewnij się, że w kodzie uwzględniłeś następujące przestrzenie nazw:
```csharp
using Aspose.Cells.Utility;
using System;
using System.IO;
```
Teraz, gdy wszystko jest już skonfigurowane, przeanalizujmy kod krok po kroku, aby pokazać, jak łatwo przekonwertować plik JSON na plik CSV za pomocą Aspose.Cells.
## Krok 1: Odczytaj plik JSON
 Pierwszą rzeczą, którą musimy zrobić, jest odczytanie danych JSON z pliku. Załóżmy, że masz już plik JSON (nazwijmy go`SampleJson.json`) zapisane w katalogu w Twoim systemie.
Możesz użyć`File.ReadAllText()` Metoda w C# umożliwiająca odczytanie zawartości pliku JSON do ciągu znaków.
```csharp
// Katalog źródłowy
string sourceDir = "Your Document Directory";
// Odczytaj plik JSON
string str = File.ReadAllText(sourceDir + "SampleJson.json");
```

Ten krok jest kluczowy, ponieważ potrzebujesz surowych danych JSON, aby rozpocząć proces konwersji. Odczytując je jako ciąg, przygotowujesz je do przetworzenia przez Aspose.Cells.
## Krok 2: Utwórz pusty skoroszyt
Aspose.Cells działa głównie na skoroszytach (plikach Excel). Aby rozpocząć importowanie danych JSON, najpierw musisz utworzyć pusty skoroszyt, do którego zostaną wstawione te dane.
```csharp
// Utwórz pusty skoroszyt
Workbook workbook = new Workbook();
```
Tutaj inicjujesz pusty skoroszyt, który ostatecznie będzie zawierał dane w formacie CSV. Pomyśl o tym jak o tworzeniu pustego arkusza kalkulacyjnego w programie Excel, który wkrótce zostanie wypełniony danymi JSON.
## Krok 3: Dostęp do komórek w skoroszycie
 Teraz, gdy mamy pusty skoroszyt, musimy uzyskać dostęp do jego komórek.`Cells` kolekcja w Aspose.Cells reprezentuje wszystkie komórki w arkuszu kalkulacyjnym, w których będziesz umieszczać dane JSON.
```csharp
// Pobierz komórki
Cells cells = workbook.Worksheets[0].Cells;
```
Ten fragment kodu wybiera pierwszy arkusz roboczy (arkusz roboczy o indeksie 0) i pobiera jego`Cells` kolekcja. Komórki te są jak siatka arkusza kalkulacyjnego, do której będą dodawane dane.
## Krok 4: Ustaw JsonLayoutOptions
 Aspose.Cells zapewnia kilka opcji dostosowywania sposobu importowania danych JSON. Tutaj definiujemy`JsonLayoutOptions` aby określić sposób, w jaki Aspose ma obsługiwać tablice, dane liczbowe i tytuły obiektów.
```csharp
// Ustaw JsonLayoutOptions
JsonLayoutOptions importOptions = new JsonLayoutOptions();
importOptions.ConvertNumericOrDate = true;
importOptions.ArrayAsTable = true;
importOptions.IgnoreArrayTitle = true;
importOptions.IgnoreObjectTitle = true;
```

- ConvertNumericOrDate: Automatycznie konwertuje wartości ciągów, które są wartościami liczbowymi lub wartościami daty.
- ArrayAsTable: traktuj tablice w formacie JSON jako tabele w skoroszycie.
- IgnoreArrayTitle i IgnoreObjectTitle: Opcje te ignorują tytuły tablic i obiektów, co zapewnia, że importowane są tylko surowe dane.
## Krok 5: Importowanie danych JSON
 Po ustawieniu opcji układu nadszedł czas na wprowadzenie danych JSON.`JsonUtility.ImportData()` Metoda ta wykonuje tutaj najtrudniejszą pracę, wstawiając dane JSON do komórek skoroszytu.
```csharp
JsonUtility.ImportData(str, cells, 0, 0, importOptions);
```
Ta metoda przyjmuje kilka parametrów:
- `str`:Ciąg JSON odczytany w kroku 1.
- `cells`:Zbiór komórek, w którym zostaną umieszczone dane.
- `0, 0`:Są to indeksy wierszy i kolumn wskazujące, gdzie dane powinny się zaczynać (tj. w lewym górnym rogu).
- `importOptions`:Opcje układu ustawiliśmy w kroku 4.
## Krok 6: Zapisz skoroszyt jako plik CSV
Teraz, gdy dane JSON znajdują się w skoroszycie, możemy łatwo zapisać skoroszyt jako plik CSV. CSV to prosty, lekki format do przechowywania danych tabelarycznych, co czyni go idealnym do analizy danych.
```csharp
// Katalog wyjściowy
string outputDir = "Your Document Directory";
// Zapisz skoroszyt
workbook.Save(outputDir + @"SampleJson_out.csv");
```
W tym kroku zapisujemy skoroszyt jako plik CSV. Określ ścieżkę i nazwę pliku (`SampleJson_out.csv`) gdzie plik CSV zostanie zapisany.
## Krok 7: Potwierdź proces
Aby mieć pewność, że wszystko przebiegło zgodnie z oczekiwaniami, możemy wyświetlić komunikat potwierdzający na konsoli.
```csharp
Console.WriteLine("ConvertJsonToCsv executed successfully.");
```
Prosty komunikat o powodzeniu pozwala potwierdzić, że proces przebiegł bez zakłóceń.
## Wniosek
Konwersja JSON do CSV przy użyciu Aspose.Cells dla .NET to prosty, ale potężny proces. Za pomocą zaledwie kilku linijek kodu możesz przekształcić złożone dane JSON w bardziej dostępny format CSV. Niezależnie od tego, czy masz do czynienia z tablicami, obiektami czy danymi liczbowymi, Aspose.Cells ułatwia skonfigurowanie procesu konwersji zgodnie z Twoimi potrzebami.
## Najczęściej zadawane pytania
### Czy Aspose.Cells obsługuje duże pliki JSON?
Tak, Aspose.Cells jest zaprojektowany do wydajnej obsługi dużych zbiorów danych, dzięki czemu nadaje się do przetwarzania dużych plików JSON bez problemów z wydajnością.
### Jak mogę dostosować dane wyjściowe w formacie CSV?
 Możesz dostosować dane wyjściowe CSV, dostosowując`JsonLayoutOptions` lub zmieniając formatowanie skoroszytu przed zapisaniem go w formacie CSV.
### Czy istnieje sposób na wykluczenie pewnych danych z JSON podczas konwersji?
Tak, modyfikując kod JSON lub stosując niestandardową logikę kodu przed importowaniem, można wykluczyć lub odfiltrować określone pola danych.
### Czy Aspose.Cells obsługuje inne formaty plików poza CSV?
Oczywiście! Aspose.Cells obsługuje szeroki zakres formatów, w tym Excel (XLS, XLSX), PDF, HTML i wiele innych.
### Jak mogę wypróbować Aspose.Cells za darmo?
 Możesz[pobierz bezpłatną wersję próbną tutaj](https://releases.aspose.com/) aby przetestować wszystkie funkcje przed zakupem.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
