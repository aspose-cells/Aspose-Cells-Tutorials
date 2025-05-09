---
"description": "Dowiedz się, jak wysyłać kształty do przodu lub do tyłu w programie Excel za pomocą Aspose.Cells dla .NET. Ten przewodnik zawiera samouczek krok po kroku z poradami."
"linktitle": "Wyślij kształt do przodu lub do tyłu w programie Excel"
"second_title": "Aspose.Cells .NET API przetwarzania programu Excel"
"title": "Wyślij kształt do przodu lub do tyłu w programie Excel"
"url": "/pl/net/excel-shape-text-modifications/send-shape-front-back-excel/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Wyślij kształt do przodu lub do tyłu w programie Excel

## Wstęp
Podczas pracy z plikami programu Excel możesz potrzebować większej kontroli nad elementami wizualnymi w arkuszu kalkulacyjnym. Kształty, takie jak obrazy i grafiki, mogą ulepszyć prezentację danych. Ale co się stanie, gdy te kształty się nałożą lub trzeba je będzie uporządkować? To właśnie tutaj Aspose.Cells dla .NET się wyróżnia. W tym samouczku przeprowadzimy Cię przez kroki manipulowania kształtami w arkuszu kalkulacyjnym programu Excel, w szczególności wysyłając kształty na przód lub tył innych kształtów. Jeśli jesteś gotowy, aby wzmocnić swoją grę w programie Excel, zanurzmy się w to!
## Wymagania wstępne
Zanim zaczniemy, musisz zadbać o kilka rzeczy:
1. Instalacja biblioteki Aspose.Cells: Upewnij się, że biblioteka Aspose.Cells jest zainstalowana dla .NET. Możesz ją znaleźć [Tutaj](https://releases.aspose.com/cells/net/).
2. Środowisko programistyczne: Upewnij się, że posiadasz środowisko programistyczne obsługujące technologię .NET, np. Visual Studio.
3. Podstawowa wiedza o języku C#: Znajomość programowania w języku C# pomoże Ci lepiej zrozumieć fragmenty kodu.
Dobrze, zaznaczyłeś wszystkie pola na liście wymagań wstępnych? Świetnie! Przejdźmy do zabawnej części – pisania kodu!
## Importuj pakiety
Zanim przejdziemy do właściwego kodowania, zaimportujmy niezbędne pakiety. Wystarczy dodać następującą dyrektywę using na górze pliku C#:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
Te przestrzenie nazw są kluczowe, ponieważ zawierają klasy i metody, których będziemy używać do manipulowania plikami i kształtami programu Excel.
## Krok 1: Zdefiniuj ścieżki plików
tym pierwszym kroku musimy ustalić katalogi źródłowe i wyjściowe. To tutaj znajduje się plik Excel i gdzie chcesz zapisać zmodyfikowany plik.
```csharp
//Katalog źródłowy
string sourceDir = "Your Document Directory";
//Katalog wyjściowy
string outputDir = "Your Document Directory";
```
Zastępować `"Your Document Directory"` z rzeczywistą ścieżką, w której przechowywane są pliki Excela.
## Krok 2: Załaduj skoroszyt
Teraz, gdy mamy już skonfigurowane katalogi, załadujmy skoroszyt (plik programu Excel) zawierający kształty, którymi chcemy manipulować.
```csharp
//Załaduj plik źródłowy Excel
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
Ta linia kodu inicjuje nowy `Workbook` obiekt, ładując określony plik Excel do pamięci, dzięki czemu możemy z nim pracować.
## Krok 3: Uzyskaj dostęp do arkusza kalkulacyjnego 
Następnie musimy uzyskać dostęp do konkretnego arkusza kalkulacyjnego, w którym znajdują się nasze kształty. W tym przykładzie użyjemy pierwszego arkusza kalkulacyjnego.
```csharp
//Uzyskaj dostęp do pierwszego arkusza kalkulacyjnego
Worksheet ws = wb.Worksheets[0];
```
Odwołując się `Worksheets[0]`, celujemy w pierwszy arkusz naszego skoroszytu. Jeśli twoje kształty są na innym arkuszu, dostosuj odpowiednio indeks.
## Krok 4: Uzyskaj dostęp do kształtów
Mając już dostęp do arkusza kalkulacyjnego, chwyćmy interesujące nas kształty. W tym przykładzie uzyskamy dostęp do pierwszego i czwartego kształtu.
```csharp
//Dostęp do pierwszego i czwartego kształtu
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
Linie te otrzymują określone kształty z arkusza kalkulacyjnego na podstawie swojego indeksu.
## Krok 5: Wydrukuj położenie kształtów w osi Z
Zanim przesuniemy jakiekolwiek kształty, wydrukujmy ich bieżącą pozycję Z-Order. Pomoże nam to śledzić ich położenie przed wprowadzeniem zmian.
```csharp
//Wydrukuj pozycję kształtu w osi Z
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
Dzwoniąc `ZOrderPosition`, możemy zobaczyć, gdzie każdy kształt znajduje się w kolejności rysowania.
## Krok 6: Przesuń pierwszy kształt na przód
Czas na działanie! Wyślijmy pierwszy kształt na przód Z-Order.
```csharp
//Wyślij ten kształt na przód
sh1.ToFrontOrBack(2);
```
Przechodząc `2` Do `ToFrontOrBack`, wydajemy polecenie Aspose.Cells, aby przeniósł ten kształt na wierzch. 
## Krok 7: Wydrukuj pozycję Z-Order drugiego kształtu
Zanim umieścimy drugi kształt na odwrocie, sprawdźmy jego położenie.
```csharp
//Wydrukuj pozycję kształtu w osi Z
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
Dzięki temu możemy określić położenie czwartego kształtu przed wprowadzeniem jakichkolwiek zmian.
## Krok 8: Przesuń czwarty kształt do tyłu
Na koniec prześlemy czwarty kształt na spód stosu Z-Order.
```csharp
//Wyślij ten kształt do tyłu
sh4.ToFrontOrBack(-2);
```
Używanie `-2` ponieważ parametr przesuwa kształt na koniec stosu, zapewniając, że nie będzie on zasłaniał innych kształtów ani tekstu.
## Krok 9: Zapisz skoroszyt 
Ostatnim krokiem jest zapisanie skoroszytu z nowo umieszczonymi kształtami.
```csharp
//Zapisz plik wyjściowy Excela
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
To polecenie zapisuje zmodyfikowany skoroszyt w określonym katalogu wyjściowym.
## Krok 10: Wiadomość potwierdzająca
Na koniec przekażmy proste potwierdzenie, że nasze zadanie zostało pomyślnie ukończone.
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
I tym oto kończymy kod naszego samouczka!
## Wniosek
Manipulowanie kształtami w programie Excel przy użyciu Aspose.Cells dla .NET jest nie tylko proste, ale i potężne. Postępując zgodnie z tym przewodnikiem, powinieneś teraz móc łatwo wysyłać kształty na przód lub tył, co pozwoli na lepszą kontrolę nad prezentacjami w programie Excel. Mając do dyspozycji te narzędzia, jesteś gotowy, aby poprawić atrakcyjność wizualną swoich arkuszy kalkulacyjnych.
## Najczęściej zadawane pytania
### Jakiego języka programowania potrzebuję dla Aspose.Cells?  
Aby pracować z Aspose.Cells, należy używać języka C# lub dowolnego języka obsługiwanego przez platformę .NET.
### Czy mogę wypróbować Aspose.Cells za darmo?  
Tak, możesz zacząć od bezpłatnego okresu próbnego Aspose.Cells [Tutaj](https://releases.aspose.com/).
### Jakie kształty mogę manipulować w programie Excel?  
Możesz manipulować różnymi kształtami, takimi jak prostokąty, okręgi, linie i obrazy.
### Gdzie mogę uzyskać pomoc techniczną dotyczącą Aspose.Cells?  
W celu uzyskania wsparcia lub zadania pytań możesz odwiedzić ich forum społecznościowe [Tutaj](https://forum.aspose.com/c/cells/9).
### Czy jest dostępna tymczasowa licencja na Aspose.Cells?  
Tak, możesz poprosić o tymczasową licencję [Tutaj](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}