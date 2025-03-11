---
title: Dodawanie pola tekstowego do arkusza kalkulacyjnego w programie Excel
linktitle: Dodawanie pola tekstowego do arkusza kalkulacyjnego w programie Excel
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: W tym samouczku krok po kroku dowiesz się, jak dodawać konfigurowalne pola tekstowe do programu Excel za pomocą Aspose.Cells dla platformy .NET.
weight: 14
url: /pl/net/excel-shapes-controls/add-textbox-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodawanie pola tekstowego do arkusza kalkulacyjnego w programie Excel

## Wstęp
Czy chcesz ulepszyć swoje arkusze kalkulacyjne Excela za pomocą unikalnych elementów wizualnych, które mogą zainteresować odbiorców? Dodawanie pól tekstowych to świetny sposób na osiągnięcie tego celu! Dzięki Aspose.Cells dla .NET możesz łatwo zintegrować pola tekstowe z arkuszami kalkulacyjnymi Excela, dzięki czemu Twoje dokumenty będą bardziej informacyjne i atrakcyjne wizualnie. Ten przewodnik krok po kroku przeprowadzi Cię przez prosty proces dodawania pól tekstowych za pomocą Aspose.Cells, pokazując, jak je personalizować za pomocą tekstu, kolorów, hiperłączy i nie tylko!
## Wymagania wstępne
Zanim zagłębimy się w cud kodowania, przedstawiamy podstawowe wymagania, które zapewnią Ci płynne działanie:
1. Środowisko programistyczne .NET: Będziesz potrzebować działającego środowiska .NET wraz ze środowiskiem IDE, takim jak Visual Studio. Upewnij się, że jest zaktualizowane do najnowszej wersji!
2.  Aspose.Cells dla .NET: Upewnij się, że masz pobraną bibliotekę Aspose.Cells. Możesz pobrać najnowszą wersję z[Tutaj](https://releases.aspose.com/cells/net/).
3. Podstawowa wiedza programistyczna: Znajomość języka C# i kilku ogólnych koncepcji obsługi plików Excela ułatwi Ci korzystanie z tego samouczka!
## Importuj pakiety
Upewnij się, że importujesz niezbędne pakiety na początku pliku C#. Oto, jak możesz to zrobić:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Zainstaluj Aspose.Cells
Jeśli jeszcze tego nie zrobiłeś, możesz dodać Aspose.Cells za pomocą Menedżera pakietów NuGet w programie Visual Studio:
1. Otwórz program Visual Studio.
2.  Idź do`Tools` ->`NuGet Package Manager` ->`Manage NuGet Packages for Solution`.
3. Wyszukaj „Aspose.Cells” i zainstaluj go w swoim projekcie.
Teraz, gdy już przygotowaliśmy grunt, możemy przejść do najlepszej części!
## Krok 1: Konfigurowanie katalogu dokumentów
Najpierw skonfigurujmy katalog, w którym będą przechowywane wszystkie Twoje dokumenty Excela. Ważne jest, aby upewnić się, że ten katalog istnieje, zanim zaczniemy tworzyć nasz skoroszyt.
```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory"; 
// Utwórz katalog, jeśli jeszcze go nie ma.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists) 
    System.IO.Directory.CreateDirectory(dataDir);
```
Ten fragment kodu utworzy katalog o nazwie`Your Document Directory` (proszę zastąpić to swoją rzeczywistą ścieżką), jeśli jeszcze nie istnieje. Łatwizna, prawda?
## Krok 2: Tworzenie nowego skoroszytu
Następnie musimy utworzyć nowy skoroszyt, w którym będziemy dodawać nasze pola tekstowe. Można to łatwo zrobić za pomocą kilku linijek kodu:
```csharp
// Utwórz nowy skoroszyt.
Workbook workbook = new Workbook();
```
Ta linia kodu tworzy nowy skoroszyt programu Excel. Proste i przejrzyste!
## Krok 3: Dostęp do pierwszego arkusza kalkulacyjnego
Teraz, gdy mamy już gotowy skoroszyt, przygotujmy pierwszy arkusz, w którym dodamy pole tekstowe:
```csharp
// Pobierz pierwszy arkusz ćwiczeń z książki.
Worksheet worksheet = workbook.Worksheets[0];
```
 W ten sposób uzyskałeś dostęp do pierwszego arkusza kalkulacyjnego o nazwie`worksheet`Czas to rozświetlić!
## Krok 4: Dodawanie pola tekstowego
No dobrze, czas dodać nasze pierwsze pole tekstowe! Oto jak to zrobić:
```csharp
// Dodaj nowe pole tekstowe do kolekcji.
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
W tym wierszu określamy wiersz i kolumnę, w których zostanie umieszczone pole tekstowe, a także ustawiamy jego szerokość i wysokość (odpowiednio 160 i 200). Możesz swobodnie dostosować te liczby w zależności od swojego układu!
## Krok 5: Pobieranie obiektu TextBox
Po dodaniu pola tekstowego musimy uzyskać do niego odniesienie, aby móc dostosować jego zawartość:
```csharp
// Pobierz obiekt pola tekstowego.
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[textboxIndex];
```
 Teraz,`textbox0` jest Twoim złotym biletem do modyfikacji tego pola tekstowego!
## Krok 6: Wypełnianie pola tekstowego treścią
Następnie wprowadźmy tekst do pola tekstowego:
```csharp
// Wypełnij tekst.
textbox0.Text = "ASPOSE______The .NET & JAVA Component Publisher!";
```
Wstawianie tekstu do pola tekstowego jest takie proste! 
## Krok 7: Dostosuj wygląd pola tekstowego
Co powiesz na to, żebyśmy to trochę odświeżyli? Możesz dostosować kolory czcionek, style i wiele więcej!
```csharp
// Ustaw kolor czcionki.
textbox0.Font.Color = Color.Blue;
// Ustaw czcionkę na pogrubioną.
textbox0.Font.IsBold = true;
// Ustaw rozmiar czcionki.
textbox0.Font.Size = 14;
// Ustaw atrybut czcionki na kursywę.
textbox0.Font.IsItalic = true;
```
Możesz swobodnie eksperymentować z różnymi kolorami i stylami, aby znaleźć taki, który najlepiej się prezentuje!
## Krok 8: Dodawanie hiperłącza
Chcesz zamienić swoje pole tekstowe w klikalny link? Zróbmy to:
```csharp
// Dodaj hiperłącze do pola tekstowego.
textbox0.AddHyperlink("http://www.aspose.com/");
```
Teraz każdy, kto kliknie Twoje pole tekstowe, zostanie przeniesiony na stronę Aspose. To jak magia!
## Krok 9: Ustawianie typu umiejscowienia pola tekstowego
Masz różne możliwości wyboru, jak chcesz, aby pole tekstowe zachowywało się w odniesieniu do arkusza kalkulacyjnego. Oto przykład, jak ustawić je jako swobodnie pływające:
```csharp
// Ustaw rozmieszczenie.
textbox0.Placement = PlacementType.FreeFloating;
```
Alternatywnie, jeśli chcesz, aby zmieniał rozmiar i przesuwał się wraz z komórkami, możesz ustawić to w ten sposób:
```csharp
// Ustaw typ rozmieszczenia, ponieważ pole tekstowe będzie się przesuwać i zmieniać rozmiar wraz z komórkami.
textbox1.Placement = PlacementType.MoveAndSize;
```
## Krok 10: Dostosowywanie formatów linii i wypełnienia
Oto jak możesz zmienić wygląd obramowania i wypełnienia pola tekstowego:
```csharp
// Pobierz format wypełnienia pola tekstowego.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;            
// Pobierz typ formatu linii pola tekstowego.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;           
// Ustaw grubość linii.
lineformat.Weight = 6;
// Ustaw styl myślnika na kropkę kwadratową.
lineformat.DashStyle = MsoLineDashStyle.SquareDot;
```
Dzięki temu możesz jeszcze bardziej spersonalizować swoje pole tekstowe, dodając elementy wizualne odpowiadające Twojemu stylowi.
## Krok 11: Dodawanie kolejnego pola tekstowego
Nikt nie powiedział, że możemy dodać tylko jedno pole tekstowe! Wstawmy kolejne z innym tekstem:
```csharp
// Dodaj kolejne pole tekstowe.
textboxIndex = worksheet.TextBoxes.Add(15, 4, 85, 120);
// Pobierz drugie pole tekstowe.
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[textboxIndex];
// Wpisz do niego jakiś tekst.
textbox1.Text = "This is another simple text box";
```
Teraz naprawdę uatrakcyjnisz swój arkusz Excela dzięki wielu polom tekstowym!
## Krok 12: Zapisywanie skoroszytu
W końcu nadszedł czas, aby uratować nasze arcydzieło! Oto ostatnia linijka kodu na dziś:
```csharp
// Zapisz plik Excela.
workbook.Save(dataDir + "book1.out.xls");
```
Za pomocą tej jednej linijki kodu utworzyłeś i zmodyfikowałeś plik Excela z konfigurowalnymi polami tekstowymi!
## Wniosek
Gratulacje! Udało Ci się pomyślnie poruszać po świecie pól tekstowych w programie Excel, korzystając z Aspose.Cells dla .NET. Nauczyłeś się nie tylko, jak dodać pole tekstowe, ale także, jak je dostosować, aby uczynić arkusze kalkulacyjne bardziej angażującymi. Od zmiany kolorów i stylów po dodawanie hiperłączy, możliwości są praktycznie nieograniczone! 
Jesteś gotowy, aby zacząć przekształcać swoje dokumenty Excel? Pozwól swojej kreatywności zabłysnąć i eksperymentuj z różnymi układami!
## Najczęściej zadawane pytania
### Czym jest Aspose.Cells dla .NET?
Aspose.Cells for .NET to zaawansowana biblioteka umożliwiająca programistom łatwe tworzenie, edytowanie i konwertowanie plików Excel.
### Czy mogę wypróbować Aspose.Cells przed zakupem?
 Tak! Możesz pobrać i używać bezpłatnej wersji próbnej[Tutaj](https://releases.aspose.com/).
### Gdzie mogę znaleźć dokumentację Aspose.Cells?
 Dostęp do pełnej dokumentacji można uzyskać pod adresem[Dokumentacja Aspose.Cells](https://reference.aspose.com/cells/net/).
### Czy mogę liczyć na pomoc, jeśli wystąpią jakieś problemy?
 Oczywiście! Jeśli potrzebujesz pomocy, udaj się do[Forum Aspose](https://forum.aspose.com/c/cells/9) po pomoc.
### Czy mogę używać Aspose.Cells bez licencji?
 Chociaż możesz skorzystać z bezpłatnej wersji próbnej, aby uzyskać dostęp do pełnej funkcjonalności, musisz kupić licencję. Sprawdź cennik[Tutaj](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
