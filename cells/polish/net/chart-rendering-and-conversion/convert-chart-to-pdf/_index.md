---
title: Konwertuj wykres do PDF
linktitle: Konwertuj wykres do PDF
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Naucz się konwertować wykresy Excela do PDF za pomocą Aspose.Cells dla .NET dzięki temu prostemu przewodnikowi krok po kroku. Poznaj podstawowe wskazówki i przykłady kodowania.
weight: 11
url: /pl/net/chart-rendering-and-conversion/convert-chart-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwertuj wykres do PDF

## Wstęp

Jeśli chodzi o obsługę arkuszy kalkulacyjnych, wykresy często odgrywają kluczową rolę w skutecznej wizualizacji danych. Niezależnie od tego, czy przygotowujesz raport, prowadzisz prezentację, czy po prostu ułatwiasz analizę danych, konwersja tych wykresów do formatu PDF zapewnia profesjonalny akcent. Tutaj przeprowadzimy Cię przez kroki konwersji wykresu programu Excel do formatu PDF przy użyciu Aspose.Cells dla .NET, potężnej biblioteki zaprojektowanej w celu uproszczenia manipulacji w programie Excel.

## Wymagania wstępne

Zanim przejdziesz do samouczka, musisz upewnić się, że masz odpowiednią konfigurację. Oto, czego potrzebujesz:

### .NET Framework
Upewnij się, że masz zainstalowany .NET Framework na swoim komputerze. Aspose.Cells jest kompatybilny z różnymi wersjami, ale najlepiej współpracuje z najnowszymi.

### Biblioteka Aspose.Cells
 Będziesz potrzebować biblioteki Aspose.Cells dla .NET. Możesz ją pobrać z[Tutaj](https://releases.aspose.com/cells/net/)Biblioteka zawiera bogate API, które obejmuje wszystkie funkcje potrzebne do manipulacji w programie Excel.

### Studio wizualne
Zainstalowanie programu Visual Studio jest niezbędne, ponieważ jest to znakomite środowisko IDE umożliwiające bezproblemowe pisanie kodu .NET.

### Podstawowa wiedza z języka C#
Pewna znajomość języka programowania C# pomoże Ci lepiej zrozumieć segmenty kodu.

## Importuj pakiety

Aby pomyślnie używać Aspose.Cells w swoim projekcie, musisz zaimportować niezbędne pakiety. Oto, jak możesz to zrobić:

### Utwórz nowy projekt

Zacznij od utworzenia nowego projektu C# w programie Visual Studio:

1. Otwórz program Visual Studio.
2. Kliknij „Utwórz nowy projekt”.
3. Wybierz „Aplikacja konsolowa (.NET Core)” lub „Aplikacja konsolowa (.NET Framework)” w zależności od potrzeb.
4. Nadaj nazwę swojemu projektowi i kliknij „Utwórz”.

### Dodaj odniesienie Aspose.Cells

Po utworzeniu projektu należy dodać odwołanie do biblioteki Aspose.Cells:

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy swój projekt.
2. Wybierz „Zarządzaj pakietami NuGet”.
3. Wyszukaj „Aspose.Cells” i zainstaluj.

Gdy biblioteka zostanie uwzględniona w projekcie, możesz przejść do kodu.

### Importuj wymagane przestrzenie nazw

 Na szczycie twojego`Program.cs` plik, dodaj następujące przestrzenie nazw:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Charts;
using System.IO;
```

Oto jak przekonwertować wykres Excela do PDF w sposób systematyczny. Postępuj zgodnie z instrukcjami krok po kroku!

## Krok 1: Skonfiguruj katalogi wyjściowe i źródłowe

Aby rozpocząć pisanie kodu, musisz najpierw określić miejsce zapisu danych wyjściowych i lokalizację dokumentu źródłowego.

```csharp
// Katalog wyjściowy
string outputDir = "Your Output Directory";

// Katalog źródłowy
string sourceDir = "Your Document Directory";
```

 Pamiętaj o wymianie`"Your Output Directory"` I`"Your Document Directory"` z rzeczywistą ścieżką, gdzie znajdują się Twoje pliki.

## Krok 2: Załaduj skoroszyt programu Excel

Teraz załadujmy plik Excel zawierający wykresy, które chcesz przekonwertować. To jest dość proste:

```csharp
// Załaduj plik Excel zawierający wykresy
Workbook workbook = new Workbook(sourceDir + "sampleChartToPdf.xlsx");
```

Ten kod inicjuje nowy obiekt skoroszytu i ładuje określony plik Excela. Upewnij się, że nazwa pliku jest taka sama jak ta, którą masz w katalogu źródłowym.

## Krok 3: Uzyskaj dostęp do arkusza kalkulacyjnego

Następnie musisz uzyskać dostęp do arkusza kalkulacyjnego zawierającego wykres, który chcesz przekonwertować. Oto jak to zrobić:

```csharp
// Uzyskaj dostęp do pierwszego arkusza kalkulacyjnego
Worksheet worksheet = workbook.Worksheets[0];
```

Ten kod uzyskuje dostęp do pierwszego arkusza kalkulacyjnego w skoroszycie, umożliwiając pracę z nim.

## Krok 4: Uzyskaj dostęp do wykresu 

Gdy już masz arkusz kalkulacyjny, czas uzyskać dostęp do konkretnego wykresu, który chcesz przekonwertować:

```csharp
// Uzyskaj dostęp do pierwszego wykresu w arkuszu kalkulacyjnym
Chart chart = worksheet.Charts[0];
```

Ten wiersz pobiera pierwszy wykres zawarty w arkuszu. Jeśli arkusz zawiera wiele wykresów i musisz wybrać konkretny, dostosuj indeks odpowiednio.

## Krok 5: Konwertuj wykres do formatu PDF

Teraz nadchodzi ekscytująca część — konwersja wykresu do formatu PDF. Możesz zapisać go do pliku lub strumienia pamięci.

### Opcja 1: Zapisz wykres do pliku

Aby zapisać wykres bezpośrednio do pliku PDF, użyj następującego kodu:

```csharp
// Zapisz wykres w formacie PDF
chart.ToPdf(outputDir + "outputChartToPdf.pdf");
```

Aby uniknąć błędów, należy upewnić się, że katalog wyjściowy faktycznie istnieje.

### Opcja 2: Zapisywanie wykresu w strumieniu pamięci

Jeśli zamierzasz dalej modyfikować plik PDF lub musisz go od razu wykorzystać w swojej aplikacji, zapisanie go w strumieniu pamięci może okazać się lepszym wyborem:

```csharp
// Zapisz wykres w formacie PDF w strumieniu
MemoryStream ms = new MemoryStream();
chart.ToPdf(ms);
```

Tutaj zapisujesz plik PDF w strumieniu pamięci, który możesz wykorzystać w zależności od potrzeb swojej aplikacji.

## Krok 6: Wyświetl komunikat o powodzeniu

Na koniec, zawsze miło jest wskazać, że operacja się powiodła. Możesz po prostu wydrukować komunikat o powodzeniu na konsoli:

```csharp
Console.WriteLine("ChartToPdf executed successfully.");
```

## Wniosek

masz to! Dzięki wykorzystaniu Aspose.Cells dla .NET konwersja wykresów Excela do formatów PDF staje się spacerkiem. Niezależnie od tego, czy zdecydujesz się zapisać do pliku, czy strumienia pamięci, biblioteka obiecuje elastyczność i łatwość użytkowania. Więc dlaczego by nie spróbować? Twoje raporty będą wyglądać znacznie lepiej dzięki profesjonalnie sformatowanym wykresom PDF!

## Najczęściej zadawane pytania

### Czy Aspose.Cells może konwertować wiele wykresów jednocześnie?
 Tak, możesz przejść przez pętlę`worksheet.Charts` kolekcja umożliwiająca konwersję każdego wykresu indywidualnie.

### Czy Aspose.Cells nadaje się do dużych plików Excela?
Oczywiście! Aspose.Cells jest zoptymalizowany pod kątem wydajności i może wydajnie obsługiwać duże pliki Excel.

### Jakie wersje platformy .NET obsługuje Aspose.Cells?
Aspose.Cells obsługuje różne wersje platformy .NET, w tym .NET Framework i .NET Core.

### Gdzie mogę znaleźć szczegółową dokumentację?
 Odwiedź[Dokumentacja Aspose.Cells](https://reference.aspose.com/cells/net/) aby uzyskać szczegółowe informacje i przykłady.

### Czy jest dostępna bezpłatna wersja próbna?
 Tak! Możesz pobrać bezpłatną wersję próbną z[Tutaj](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
