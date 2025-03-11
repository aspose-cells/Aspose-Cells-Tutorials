---
title: Wykrywanie odwołań cyklicznych w programie Excel programowo
linktitle: Wykrywanie odwołań cyklicznych w programie Excel programowo
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Łatwe wykrywanie odwołań cyklicznych w programie Excel przy użyciu Aspose.Cells dla .NET. Postępuj zgodnie z naszym przewodnikiem krok po kroku, aby zapewnić dokładne obliczenia w arkuszach kalkulacyjnych.
weight: 13
url: /pl/net/excel-formulas-and-calculation-options/detecting-circular-reference/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wykrywanie odwołań cyklicznych w programie Excel programowo

## Wstęp
Jeśli chodzi o pracę z plikami Excela, jednym z najbardziej frustrujących problemów, na jakie możesz się natknąć, jest odwołanie cykliczne. Dzieje się tak, gdy formuła odwołuje się do własnej komórki, bezpośrednio lub pośrednio, tworząc pętlę, która może zdezorientować silnik obliczeniowy Excela. Ale nie obawiaj się! Dzięki Aspose.Cells dla .NET możesz programowo wykrywać te irytujące odwołania cykliczne, zapewniając, że Twoje arkusze kalkulacyjne pozostaną funkcjonalne i dokładne. W tym przewodniku przeprowadzimy Cię przez proces krok po kroku, dzięki czemu będzie on tak prosty jak bułka z masłem.
## Wymagania wstępne
Zanim zagłębimy się w szczegóły wykrywania odwołań cyklicznych, upewnijmy się, że masz wszystko, czego potrzebujesz, aby zacząć:
1. Visual Studio: Upewnij się, że masz zainstalowane Visual Studio na swoim komputerze. To będzie Twoje środowisko programistyczne.
2. .NET Framework: Upewnij się, że używasz zgodnej wersji .NET Framework (co najmniej .NET Framework 4.0).
3.  Biblioteka Aspose.Cells: Musisz mieć bibliotekę Aspose.Cells. Możesz ją pobrać ze strony[Strona internetowa Aspose](https://releases.aspose.com/cells/net/).
4. Podstawowa znajomość języka C#: Znajomość programowania w języku C# będzie przydatna, ponieważ będziemy pisać kod w tym języku.
5. Plik Excel: Przygotuj plik Excel zawierający odwołania cykliczne do testowania. Możesz utworzyć prosty plik lub pobrać próbkę.
Teraz, gdy spełniliśmy już wszystkie wymagania wstępne, możemy przejść do najprzyjemniejszej części!
## Importuj pakiety
Zanim zaczniesz kodować, musisz zaimportować niezbędne pakiety. Oto jak to zrobić:
### Utwórz nowy projekt
- Otwórz program Visual Studio i utwórz nowy projekt aplikacji konsolowej C#.
### Dodaj odniesienie Aspose.Cells
- Kliknij prawym przyciskiem myszy swój projekt w Eksploratorze rozwiązań.
- Wybierz „Zarządzaj pakietami NuGet”.
- Wyszukaj „Aspose.Cells” i zainstaluj najnowszą wersję.
### Importuj wymagane przestrzenie nazw
 Na szczycie twojego`Program.cs` plik, zaimportuj niezbędne przestrzenie nazw:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Teraz, gdy wszystko mamy już skonfigurowane, możemy przejść do kodu wykrywającego odwołania cykliczne w pliku Excel.
## Krok 1: Zdefiniuj katalog wejściowy
Najpierw musisz określić katalog, w którym znajduje się plik Excel. To tutaj załadujesz plik Excel.
```csharp
// Katalog wejściowy
string sourceDir = "Your Document Directory";
```
 Zastępować`"Your Document Directory"` z rzeczywistą ścieżką do pliku Excel.
## Krok 2: Załaduj skoroszyt za pomocą LoadOptions
Następnie załadujesz skoroszyt programu Excel. To tutaj zaczyna się magia!
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
 Tutaj tworzymy nową instancję`LoadOptions` i ładowanie skoroszytu ze wskazanej ścieżki. Upewnij się, że nazwa pliku Excel jest taka sama!
## Krok 3: Włącz ustawienia iteracji
Aby umożliwić odwołania cykliczne, należy włączyć ustawienia iteracji w skoroszycie.
```csharp
objWB.Settings.Iteration = true;
```
Informuje Aspose.Cells, aby zezwolił na odwołania cykliczne podczas obliczeń.
## Krok 4: Utwórz opcje obliczeń i monitor kołowy
Teraz utwórzmy opcje obliczeń i nasz niestandardowy monitor kołowy.
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
 Tutaj tworzymy instancję`CalculationOptions` i zwyczaj`CircularMonitor`Ten monitor pomoże śledzić wszelkie odniesienia cykliczne znalezione podczas obliczeń.
## Krok 5: Oblicz wzory
Teraz nadszedł czas na obliczenie formuł w skoroszycie.
```csharp
objWB.CalculateFormula(copts);
```
Ten wiersz wykonuje obliczenia i sprawdza, czy występują odwołania cykliczne.
## Krok 6: Policz odwołania cykliczne
Po wykonaniu obliczeń można policzyć, ile odniesień cyklicznych zostało znalezionych.
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
Spowoduje to wyświetlenie liczby odwołań cyklicznych wykrytych w pliku Excel.
## Krok 7: Wyświetl wyniki
Na koniec wyświetlmy wyniki i potwierdźmy, że nasza metoda została wykonana pomyślnie.
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## Krok 8: Implementacja klasy CircularMonitor
 Aby ukończyć proces, musisz wdrożyć`CircularMonitor` klasa. Ta klasa będzie dziedziczyć po`AbstractCalculationMonitor` i radzi sobie z wykrywaniem odniesień cyklicznych.
```csharp
public class CircularMonitor : AbstractCalculationMonitor
{
    public ArrayList circulars = new ArrayList();
    public ArrayList Circulars { get { return circulars; } }
    public override bool OnCircular(IEnumerator circularCellsData)
    {
        CalculationCell cc = null;
        ArrayList cur = new ArrayList();
        while (circularCellsData.MoveNext())
        {
            cc = (CalculationCell)circularCellsData.Current;
            cur.Add(cc.Worksheet.Name + "!" + CellsHelper.CellIndexToName(cc.CellRow, cc.CellColumn));
        }
        circulars.Add(cur);
        return true;
    }
}
```
Ta klasa przechwytuje szczegóły każdego znalezionego odwołania cyklicznego, w tym nazwę arkusza kalkulacyjnego i indeks komórki.
## Wniosek
Wykrywanie odwołań cyklicznych w programie Excel przy użyciu Aspose.Cells dla .NET to prosty proces, gdy podzielisz go na łatwe do opanowania kroki. Postępując zgodnie z tym przewodnikiem, możesz łatwo identyfikować i obsługiwać odwołania cykliczne w arkuszach kalkulacyjnych, zapewniając dokładność i niezawodność obliczeń. Niezależnie od tego, czy jesteś doświadczonym programistą, czy dopiero zaczynasz, Aspose.Cells zapewnia potężne narzędzia do zwiększania możliwości manipulacji w programie Excel. 
## Najczęściej zadawane pytania
### Czym jest odwołanie cykliczne w programie Excel?
Odwołanie cykliczne występuje wtedy, gdy formuła odwołuje się do własnej komórki, powodując nieskończoną pętlę w obliczeniach.
### Jak mogę programowo wykrywać odwołania cykliczne?
Bibliotekę Aspose.Cells w środowisku .NET można wykorzystać do programowego wykrywania odwołań cyklicznych poprzez implementację niestandardowego monitora obliczeń.
### Jakie są wymagania wstępne, aby móc korzystać z Aspose.Cells?
Potrzebne są zainstalowane programy Visual Studio, .NET Framework i biblioteka Aspose.Cells.
### Czy mogę używać Aspose.Cells za darmo?
Tak, Aspose.Cells oferuje bezpłatny okres próbny, dzięki któremu możesz poznać jego funkcje.
### Gdzie mogę znaleźć więcej informacji na temat Aspose.Cells?
 Możesz odwiedzić[Dokumentacja Aspose.Cells](https://reference.aspose.com/cells/net/) aby uzyskać szczegółowe informacje i przykłady.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
