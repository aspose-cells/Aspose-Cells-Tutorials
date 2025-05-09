---
"description": "Dowiedz się, jak dodać kontrolkę prostokąta do arkusza kalkulacyjnego programu Excel za pomocą Aspose.Cells dla platformy .NET, korzystając ze szczegółowego przewodnika krok po kroku."
"linktitle": "Dodaj kontrolkę prostokąta do arkusza kalkulacyjnego w programie Excel"
"second_title": "Aspose.Cells .NET API przetwarzania programu Excel"
"title": "Dodaj kontrolkę prostokąta do arkusza kalkulacyjnego w programie Excel"
"url": "/pl/net/excel-shapes-controls/add-rectangle-control-to-worksheet-excel/"
"weight": 25
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj kontrolkę prostokąta do arkusza kalkulacyjnego w programie Excel

## Wstęp
Jeśli chodzi o automatyzację zadań programu Excel, Aspose.Cells for .NET to potężne narzędzie, które może pomóc Ci osiągnąć wiele celów, z których jednym jest dodawanie kształtów, takich jak prostokąty, do arkuszy kalkulacyjnych. W tym przewodniku przyjrzymy się, jak dodać kontrolkę prostokąta do arkusza kalkulacyjnego programu Excel za pomocą Aspose.Cells for .NET. Na koniec będziesz w stanie utworzyć, dostosować i zapisać arkusz kalkulacyjny z osadzoną w nim kontrolką prostokąta.
Zanim jednak przejdziemy do konkretów, omówmy wymagania wstępne.
## Wymagania wstępne
Aby móc korzystać z tego samouczka, upewnij się, że spełnione są następujące wymagania wstępne:
1. Biblioteka Aspose.Cells dla .NET: Jeśli jeszcze tego nie zrobiłeś, [pobierz bibliotekę](https://releases.aspose.com/cells/net/) lub zainstaluj go za pomocą NuGet w Visual Studio.
2. .NET Framework: Na swoim komputerze musisz mieć skonfigurowane środowisko programistyczne .NET.
3. Podstawowa znajomość języka C#: Chociaż poprowadzimy Cię krok po kroku, podstawowa znajomość języka C# i programowania obiektowego będzie pomocna.
4. Licencja: Używanie Aspose.Cells w trybie oceny działa dobrze w przypadku podstawowych zadań, ale aby uzyskać pełną funkcjonalność, należy rozważyć uzyskanie [licencja tymczasowa](https://purchase.aspose.com/temporary-license/) lub kupując jeden z [Tutaj](https://purchase.aspose.com/buy).
A teraz zajmijmy się kodem!
## Importuj pakiety
Aby rozpocząć pracę z Aspose.Cells, upewnij się, że zaimportowałeś niezbędne przestrzenie nazw do swojego projektu. Te importy umożliwią dostęp do różnych klas i metod, których potrzebujesz do interakcji z plikami Excel.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Te wiersze zapewniają, że Twój projekt może wchodzić w interakcje z katalogami plików (`System.IO`), skoroszyty programu Excel (`Aspose.Cells`) i rysowanie kształtów (`Aspose.Cells.Drawing`).
Teraz podzielimy ten proces na proste kroki, abyś mógł je łatwo prześledzić i powtórzyć we własnych projektach.
## Krok 1: Konfigurowanie ścieżki katalogu
Pierwszą rzeczą, którą musisz zrobić, jest zdefiniowanie katalogu, w którym zostanie zapisany plik Excel. Ten krok zapewnia, że Twój projekt wie, gdzie utworzyć i zapisać plik wyjściowy.
### Definiowanie katalogu danych
```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";
```
Tutaj określasz ścieżkę katalogu, w którym będzie przechowywany plik Excel. Możesz zastąpić `"Your Document Directory"` ze ścieżką, która jest rzeczywista na Twoim komputerze, lub dynamicznie utwórz folder, jeśli on nie istnieje.
### Sprawdzanie i tworzenie katalogu
```csharp
// Utwórz katalog, jeśli jeszcze go nie ma.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Ten blok sprawdza, czy katalog istnieje. Jeśli nie, tworzy go. Pomyśl o tym jak o przygotowaniu szafki na dokumenty przed przechowywaniem jakichkolwiek dokumentów.
## Krok 2: Tworzenie nowego skoroszytu
W tym kroku utworzysz nowy skoroszyt programu Excel, używając `Aspose.Cells.Workbook` klasa. Będzie to służyć jako pojemnik na arkusz roboczy i kształty.
```csharp
// Utwórz nowy skoroszyt.
Workbook excelbook = new Workbook();
```
Dzwoniąc do `Workbook` konstruktorze, masz teraz pusty skoroszyt programu Excel gotowy do dostosowania.
## Krok 3: Dodawanie kontrolki prostokąta
Tutaj dzieje się magia. Dodasz kształt prostokąta do pierwszego arkusza kalkulacyjnego swojego skoroszytu.
```csharp
// Dodaj kontrolkę prostokąta.
Aspose.Cells.Drawing.RectangleShape rectangle = excelbook.Worksheets[0].Shapes.AddRectangle(3, 0, 2, 0, 70, 130);
```
Przyjrzyjmy się temu bliżej:
- `excelbook.Worksheets[0]`:Uzyskuje dostęp do pierwszego arkusza kalkulacyjnego w skoroszycie.
- `.Shapes.AddRectangle(3, 0, 2, 0, 70, 130)`: Dodaje prostokątny kształt do arkusza kalkulacyjnego. Parametry tutaj definiują pozycję (wiersz i kolumna), a także szerokość i wysokość prostokąta.
## Krok 4: Dostosowywanie prostokąta
Samo dodanie prostokąta nie wystarczy — będziesz chciał go dostosować. W tym kroku ustawimy położenie, grubość linii i styl kreskowania prostokąta.
### Ustawianie umiejscowienia
```csharp
// Ustaw położenie prostokąta.
rectangle.Placement = PlacementType.FreeFloating;
```
Oznacza to, że prostokąt jest swobodny, co oznacza, że nie będzie ograniczony wymiarami komórki.
### Ustawianie grubości linii
```csharp
// Ustaw grubość linii.
rectangle.Line.Weight = 4;
```
Tutaj ustawiamy grubość linii prostokąta na 4 punkty. Im wyższa liczba, tym grubsza linia.
### Ustawianie stylu Dash
```csharp
// Ustaw styl kreski prostokąta.
rectangle.Line.DashStyle = MsoLineDashStyle.Solid;
```
Ta linia ustawia styl kreski obramowania prostokąta na ciągły. Możesz eksperymentować z różnymi stylami, takimi jak `Dash` Lub `Dot` w zależności od Twoich wymagań.
## Krok 5: Zapisywanie skoroszytu
Po dodaniu i dostosowaniu prostokąta ostatnim krokiem jest zapisanie skoroszytu w określonym katalogu.
```csharp
// Zapisz plik Excela.
excelbook.Save(dataDir + "book1.out.xls");
```
Zapisuje skoroszyt jako `.xls` plik w folderze, który zdefiniowałeś wcześniej. Możesz zmodyfikować format pliku, zmieniając rozszerzenie, takie jak `.xlsx` jeśli wolisz nowszy format Excela.
## Wniosek
I masz! Dodanie kontrolki prostokąta do arkusza kalkulacyjnego Excel przy użyciu Aspose.Cells dla .NET to prosty proces, gdy rozłożysz go na części. Niezależnie od tego, czy chcesz dodać kształty dla atrakcyjności wizualnej, wyróżnić sekcje danych czy dostosować raporty, Aspose.Cells daje Ci elastyczność, aby zrobić to programowo.
Ten przewodnik powinien wyposażyć Cię w całą wiedzę, której potrzebujesz, aby zacząć dodawać kształty, takie jak prostokąty, do arkuszy Excela za pomocą Aspose.Cells. Teraz czas na eksperymenty i zobaczenie, co jeszcze możesz osiągnąć dzięki tej potężnej bibliotece!
## Najczęściej zadawane pytania
### Czy mogę dodać inne kształty, takie jak okręgi lub linie, korzystając z Aspose.Cells dla .NET?  
Tak, Aspose.Cells pozwala na dodawanie różnorodnych kształtów, w tym okręgów, linii, strzałek i innych.
### Jakie inne właściwości mogę ustawić dla kontrolki prostokąta?  
Możesz dostosować kolor wypełnienia, kolor linii, przezroczystość, a nawet dodać tekst wewnątrz prostokąta.
### Czy Aspose.Cells jest kompatybilny z .NET Core?  
Tak, Aspose.Cells obsługuje platformę .NET Core, a także .NET Framework i inne platformy oparte na technologii .NET.
### Czy mogę umieścić prostokąt względem konkretnej komórki?  
Tak, możesz umieścić prostokąt w określonych wierszach i kolumnach lub użyć `PlacementType` aby kontrolować sposób zakotwiczenia.
### Czy jest dostępna bezpłatna wersja próbna Aspose.Cells?  
Tak, możesz dostać [bezpłatny okres próbny](https://releases.aspose.com/) ze strony internetowej, aby przetestować funkcje biblioteki przed zakupem.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}