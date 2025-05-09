---
"description": "Dowiedz się, jak wyodrębnić tekst z SmartArt typu koła zębatego w programie Excel przy użyciu Aspose.Cells dla .NET. Zawiera przewodnik krok po kroku i przykład kodu."
"linktitle": "Wyodrębnij tekst z grafiki Smart Art typu koła zębatego w programie Excel"
"second_title": "Aspose.Cells .NET API przetwarzania programu Excel"
"title": "Wyodrębnij tekst z grafiki Smart Art typu koła zębatego w programie Excel"
"url": "/pl/net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnij tekst z grafiki Smart Art typu koła zębatego w programie Excel

## Wstęp
Podczas pracy z programem Excel możesz napotkać grafiki SmartArt, które pomagają przekazywać wiadomości w wizualnie atrakcyjny sposób. Wśród tych grafik, SmartArt typu koła zębatego jest ulubionym ze względu na hierarchiczne i kierunkowe przepływy, często używane w zarządzaniu projektami lub modelowaniu systemów. Ale co, jeśli musisz wyodrębnić tekst z tych kształtów programowo? Tutaj przydaje się Aspose.Cells dla .NET! W tym wpisie na blogu przeprowadzimy Cię przez przewodnik krok po kroku, jak wyodrębnić tekst z kształtów SmartArt typu koła zębatego w programie Excel przy użyciu Aspose.Cells dla .NET.
## Wymagania wstępne
Zanim przejdziemy do konkretów, musisz spełnić kilka podstawowych warunków wstępnych. Nie martw się, to proste, a ja cię przez to przeprowadzę.
### Środowisko .NET
Upewnij się, że masz środowisko programistyczne .NET skonfigurowane na swoim komputerze. Może to być Visual Studio lub dowolne wybrane przez Ciebie IDE, które obsługuje programowanie .NET.
### Aspose.Cells dla .NET
Następnie musisz zainstalować bibliotekę Aspose.Cells. To potęga, która umożliwi Ci bezproblemową manipulację plikami Excel. Możesz ją pobrać ze strony [Strona wydań Aspose](https://releases.aspose.com/cells/net/). Jeśli chcesz to najpierw zbadać, skorzystaj z [bezpłatny okres próbny](https://releases.aspose.com/).
### Podstawowa wiedza z języka C#
Podstawowa znajomość programowania w języku C# to dokładnie to, czego potrzebujesz, aby korzystać z tego samouczka. Jeśli jesteś w tym nowy, nie martw się — zaprojektuję kroki tak, aby były jak najbardziej przyjazne dla początkujących.
### Przykładowy plik Excela
Do tego samouczka będziesz potrzebować również przykładowego pliku Excel, który zawiera kształty SmartArt typu koła zębatego. Możesz łatwo utworzyć taki lub znaleźć szablon online. Upewnij się tylko, że SmartArt zawiera co najmniej jeden kształt typu koła zębatego.
## Importuj pakiety
Aby rozpocząć kodowanie, musisz zaimportować niezbędne pakiety. Oto jak to zrobić:
### Utwórz nowy projekt
1. Otwórz środowisko IDE .NET.
2. Utwórz nowy projekt. Na przykład wybierz „Aplikacja konsolowa” w opcjach .NET.
3. Nadaj nazwę swojemu projektowi i ustaw żądany framework. 
### Dodaj odniesienia
Aby użyć Aspose.Cells, musisz dodać odwołania do biblioteki do swojego projektu:
1. Kliknij prawym przyciskiem myszy nazwę projektu w Eksploratorze rozwiązań.
2. Wybierz „Zarządzaj pakietami NuGet”.
3. Wyszukaj „Aspose.Cells” i zainstaluj.
Po zainstalowaniu możesz rozpocząć kodowanie!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Teraz rozłóżmy kod, którego użyjesz do wyodrębnienia tekstu. Zrobimy to krok po kroku.
## Krok 1: Skonfiguruj katalog źródłowy
Zacznij od zdefiniowania katalogu, w którym znajduje się plik Excel:
```csharp
// Katalog źródłowy
string sourceDir = "Your Document Directory";
```
Pamiętaj o wymianie `"Your Document Directory"` z rzeczywistą ścieżką do pliku Excel.
## Krok 2: Załaduj skoroszyt programu Excel
Następnie załadujemy skoroszyt programu Excel. Oto jak możemy uzyskać dostęp do jego zawartości:
```csharp
// Załaduj przykładowy plik Excela zawierający kształt koła zębatego w formie sztuki Smart Art.
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
Ten fragment załaduje Twój przykładowy skoroszyt programu Excel.
## Krok 3: Uzyskaj dostęp do pierwszego arkusza kalkulacyjnego
Teraz, gdy załadowaliśmy skoroszyt, przejdźmy do pierwszego arkusza, w którym znajduje się nasza grafika SmartArt:
```csharp
// Otwórz pierwszy arkusz kalkulacyjny.
Worksheet ws = wb.Worksheets[0];
```
Powoduje to pobranie pierwszego arkusza kalkulacyjnego do dalszej obróbki.
## Krok 4: Uzyskaj dostęp do pierwszego kształtu
Następnie musimy uzyskać dostęp do pierwszego kształtu w naszym arkuszu kalkulacyjnym. Dzięki temu możemy poruszać się po naszych grafikach SmartArt:
```csharp
// Uzyskaj dostęp do pierwszego kształtu.
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
Tutaj skupimy się na pierwszym kształcie, który, jak zakładamy, jest potrzebną nam grafiką SmartArt.
## Krok 5: Uzyskaj kształt grupy
Gdy już mamy kształt, czas uzyskać wynik naszej reprezentacji SmartArt:
```csharp
// Uzyskaj wynik inteligentnego kształtu koła zębatego w formie kształtu grupy.
Aspose.Cells.Drawing.GroupShape gs = sh.GetResultOfSmartArt();
```
Powoduje to pobranie naszego obiektu SmartArt przedstawiającego koło zębate jako zgrupowanego kształtu.
## Krok 6: Wyodrębnij poszczególne kształty
Teraz wyodrębnijmy poszczególne kształty, które tworzą naszą grafikę SmartArt:
```csharp
// Pobierz listę pojedynczych kształtów składającą się z kształtów grupy.
Aspose.Cells.Drawing.Shape[] shps = gs.GetGroupedShapes();
```
Ta tablica będzie zawierać wszystkie pojedyncze kształty, przez które będziemy przechodzić w pętli.
## Krok 7: Wyodrębnij i wydrukuj tekst
Na koniec możemy przejść przez tablicę kształtów i wyodrębnić tekst z dowolnego kształtu przypominającego koło zębate:
```csharp
// Wyodrębnij tekst kształtów kół zębatych i wydrukuj go na konsoli.
for (int i = 0; i < shps.Length; i++)
{
    Aspose.Cells.Drawing.Shape s = shps[i];
    if (s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear9 || s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear6)
    {
        Console.WriteLine("Gear Type Shape Text: " + s.Text);
    }
}
```
W tej pętli sprawdzamy rodzaj kształtu i drukujemy tekst, jeśli jest to kształt koła zębatego.
## Krok 8: Potwierdzenie wykonania
Na koniec możesz dodać komunikat potwierdzający, który pojawi się po pomyślnym zakończeniu procesu:
```csharp
Console.WriteLine("ExtractTextFromGearTypeSmartArtShape executed successfully.");
```
W ten sposób ekstrakcja jest ukończona, a na konsoli powinieneś zobaczyć wynikowy tekst!
## Wniosek
Gratulacje! Właśnie nauczyłeś się wyodrębniać tekst z kształtów SmartArt typu koła zębatego w programie Excel przy użyciu Aspose.Cells dla .NET. Ta przydatna technika otwiera drzwi do automatyzacji raportów lub dokumentacji, która opiera się na wizualnej reprezentacji danych. Niezależnie od tego, czy jesteś doświadczonym programistą, czy dopiero zaczynasz, kontrolowanie i wyodrębnianie informacji z SmartArt może usprawnić Twój przepływ pracy i zwiększyć Twoją wydajność. Nie zapomnij zapoznać się ze szczegółowymi [Dokumentacja Aspose.Cells](https://reference.aspose.com/cells/net/) dla dalszych możliwości.
## Najczęściej zadawane pytania
### Czym jest Aspose.Cells?
Aspose.Cells to biblioteka .NET umożliwiająca programistom łatwe tworzenie i modyfikowanie plików Excel.
### Czy mogę używać Aspose.Cells z innymi językami?
Tak! Aspose.Cells jest dostępny w wielu językach programowania, w tym Java i Python.
### Czy muszę kupić Aspose.Cells dla .NET?
Aspose.Cells oferuje bezpłatną wersję próbną, ale do dłuższego użytkowania wymagany jest zakup. Możesz znaleźć opcje zakupu [Tutaj](https://purchase.aspose.com/buy).
### Czy użytkownicy Aspose.Cells mogą liczyć na pomoc techniczną?
Oczywiście! Możesz znaleźć wsparcie społeczności na [Forum Aspose.Cells](https://forum.aspose.com/c/cells/9).
### Czy mogę wyodrębnić inne typy obiektów SmartArt za pomocą tej metody?
Tak, po wprowadzeniu niewielkich modyfikacji można wyodrębnić tekst z różnych kształtów SmartArt, zmieniając warunki w kodzie.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}