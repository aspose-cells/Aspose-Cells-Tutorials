---
title: Uzyskaj punkty połączeń kształtu w programie Excel
linktitle: Uzyskaj punkty połączeń kształtu w programie Excel
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak uzyskać punkty połączenia kształtu w programie Excel za pomocą Aspose.Cells dla .NET. Postępuj zgodnie z naszym przewodnikiem krok po kroku, aby łatwo wyodrębnić i wyświetlić punkty kształtu programowo.
weight: 11
url: /pl/net/excel-shapes-controls/get-connection-points-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uzyskaj punkty połączeń kształtu w programie Excel

## Wstęp
Pracując programowo z plikami Excela, często musimy wchodzić w interakcje z kształtami osadzonymi w arkuszach. Jednym z bardziej zaawansowanych zadań, jakie możesz wykonać, jest wyodrębnianie punktów połączeń z kształtu. Punkty połączeń służą do łączenia kształtów z łącznikami i dokładniejszego zarządzania ich układem. Jeśli chcesz uzyskać punkty połączeń kształtu w programie Excel, Aspose.Cells for .NET jest narzędziem, którego potrzebujesz. W tym samouczku przeprowadzimy Cię przez proces krok po kroku, aby to osiągnąć.
## Wymagania wstępne
Zanim zaczniesz pisać kod, upewnij się, że spełniasz następujące wymagania wstępne:
- Aspose.Cells dla .NET: Musisz mieć Aspose.Cells zainstalowane w swoim środowisku programistycznym. Jeśli jeszcze go nie masz, możesz[pobierz najnowszą wersję tutaj](https://releases.aspose.com/cells/net/).
- Środowisko programistyczne: Upewnij się, że masz działającą instalację programu Visual Studio lub innego środowiska IDE zgodnego z platformą .NET.
- Podstawowa wiedza o języku C#: W tym samouczku zakładamy, że posiadasz podstawową wiedzę na temat programowania w języku C# i zasad programowania obiektowego.
 Możesz również zapisać się na[bezpłatna wersja próbna Aspose.Cells](https://releases.aspose.com/) jeśli jeszcze tego nie zrobiłeś. To da ci dostęp do wszystkich funkcji wymaganych w tym przewodniku.

## Importuj pakiety
Aby pracować z Aspose.Cells w swoim projekcie, musisz uwzględnić niezbędne przestrzenie nazw. Następujące polecenia importu powinny zostać umieszczone na górze kodu:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Te przestrzenie nazw zapewniają dostęp do podstawowej funkcjonalności Aspose.Cells i pozwalają na manipulowanie arkuszami kalkulacyjnymi i kształtami.

## Przewodnik krok po kroku, jak uzyskać punkty połączeń kształtu
tej sekcji przeprowadzimy Cię przez proces wyodrębniania punktów połączeń kształtu w arkuszu kalkulacyjnym programu Excel. Dokładnie wykonaj każdy krok, aby uzyskać jasne zrozumienie.
## Krok 1: Utwórz nowy skoroszyt
 Po pierwsze, musimy utworzyć instancję`Workbook` class. To reprezentuje plik Excel w Aspose.Cells. Jeśli nie masz istniejącego pliku, nie ma problemu — możesz zacząć od pustego skoroszytu.
```csharp
// Utwórz nowy skoroszyt
Workbook workbook = new Workbook();
```
 W tym kroku utworzyliśmy pusty skoroszyt programu Excel, ale możesz również załadować istniejący, przekazując ścieżkę do pliku`Workbook` konstruktor.
## Krok 2: Uzyskaj dostęp do pierwszego arkusza kalkulacyjnego
Następnie musimy uzyskać dostęp do arkusza, w którym chcemy pracować z kształtami. W tym przypadku użyjemy pierwszego arkusza skoroszytu.
```csharp
// Pobierz pierwszy arkusz w skoroszycie
Worksheet worksheet = workbook.Worksheets[0];
```
 Ten wiersz umożliwia dostęp do pierwszego arkusza roboczego ze zbioru arkuszy roboczych w skoroszycie. Jeśli pracujesz z konkretnym arkuszem, możesz zastąpić indeks`0` z żądanym indeksem.
## Krok 3: Dodaj nowe pole tekstowe (kształt)
Teraz dodajmy nowy kształt do arkusza kalkulacyjnego. Stworzymy pole tekstowe, które jest typem kształtu. Możesz również dodać inne typy kształtów, ale dla uproszczenia w tym samouczku pozostaniemy przy polu tekstowym.
```csharp
// Dodaj nowe pole tekstowe do kolekcji
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
Oto co zrobiliśmy:
-  Dodano pole tekstowe w wierszu`2` , kolumna`1`.
-  Ustaw wymiary pola tekstowego na`160` jednostki szerokości i`200` jednostki wysokości.
## Krok 4: Uzyskaj dostęp do kształtu z kolekcji kształtów
 Po dodaniu pola tekstowego staje się ono częścią kolekcji kształtów arkusza kalkulacyjnego. Teraz uzyskamy dostęp do tego kształtu za pomocą`Shapes`kolekcja.
```csharp
// Uzyskaj dostęp do kształtu (pola tekstowego) z kolekcji kształtów
Shape shape = workbook.Worksheets[0].Shapes[0];
```
W tym kroku pobieramy pierwszy kształt (nasze pole tekstowe) z kolekcji. Jeśli masz wiele kształtów, możesz określić indeks lub nawet znaleźć kształt według nazwy.
## Krok 5: Pobierz punkty połączeń
Teraz, gdy mamy już nasz kształt, wyodrębnijmy jego punkty połączeń. Punkty te służą do mocowania łączników do kształtu.`ConnectionPoints` Właściwość kształtu zwraca wszystkie dostępne punkty połączeń.
```csharp
// Uzyskaj wszystkie punkty połączeń w tym kształcie
var connectionPoints = shape.ConnectionPoints;
```
Dzięki temu otrzymujemy zbiór wszystkich punktów połączeń dostępnych dla danego kształtu.
## Krok 6: Wyświetl punkty połączeń
Na koniec chcemy wyświetlić współrzędne każdego punktu połączenia. Tutaj przechodzimy przez punkty połączenia i drukujemy je na konsoli.
```csharp
// Wyświetl wszystkie punkty kształtu
foreach (var pt in connectionPoints)
{
    System.Console.WriteLine(string.Format("X = {0}, Y = {1}", pt.X, pt.Y));
}
```
 Ta pętla przechodzi przez każdy punkt połączenia i drukuje`X` I`Y` współrzędne. Może to być przydatne do debugowania lub wizualnego potwierdzania punktów połączenia kształtu.
## Krok 7: Wykonaj i zakończ
Po skonfigurowaniu wszystkich powyższych kroków możesz uruchomić kod. Oto ostatni wiersz, który zapewnia pomyślne ukończenie procesu:
```csharp
System.Console.WriteLine("GetShapeConnectionPoints executed successfully.");
```
Ten wiersz po prostu rejestruje komunikat na konsoli informujący o zakończeniu procesu.

## Wniosek
W tym samouczku omówiliśmy, jak pobrać punkty połączeń kształtu w programie Excel przy użyciu Aspose.Cells dla .NET. Dzieląc zadanie na małe, przyswajalne kroki, zbadaliśmy proces tworzenia skoroszytu, dodawania kształtu i wyodrębniania punktów połączeń.
Rozumiejąc, jak programowo manipulować kształtami, otwierasz świat możliwości tworzenia dynamicznych i interaktywnych arkuszy Excela. Niezależnie od tego, czy tworzysz raporty, projektujesz pulpity nawigacyjne, czy tworzysz diagramy, ta wiedza okaże się przydatna.
## Najczęściej zadawane pytania
### Czym jest punkt połączenia w kształcie?
Punkt połączenia to określony punkt na kształcie, do którego można dołączyć łączniki lub połączyć go z innymi kształtami.
### Czy mogę pobrać punkty połączeń dla wszystkich kształtów w arkuszu kalkulacyjnym?
Tak, Aspose.Cells pozwala na pobieranie punktów połączeń dla dowolnego kształtu, który je obsługuje. Po prostu przejdź przez zbiór kształtów w arkuszu kalkulacyjnym.
### Czy potrzebuję licencji, aby korzystać z Aspose.Cells?
Tak, możesz wypróbować go za darmo, ale do uzyskania pełnych funkcji wymagana jest licencja. Możesz[kup licencję tutaj](https://purchase.aspose.com/buy)lub zdobądź[licencja tymczasowa](https://purchase.aspose.com/temporary-license/).
### Jak mogę dodać różne typy kształtów w Aspose.Cells?
Możesz użyć`Add` metoda dla kształtów takich jak prostokąty, elipsy i inne. Każdy kształt ma określone parametry, które możesz dostosować.
### Jak załadować istniejący plik Excela zamiast tworzyć nowy?
 Aby załadować istniejący plik, przekaż ścieżkę do pliku`Workbook` konstruktor, taki jak ten:  
```csharp
Workbook workbook = new Workbook("path_to_file.xlsx");
```
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
