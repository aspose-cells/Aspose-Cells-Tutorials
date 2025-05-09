---
"description": "Dowiedz się, jak dodać owal do arkusza kalkulacyjnego programu Excel przy użyciu Aspose.Cells dla .NET. Przewodnik krok po kroku ze szczegółowymi wyjaśnieniami kodu."
"linktitle": "Dodaj owal do arkusza kalkulacyjnego w programie Excel"
"second_title": "Aspose.Cells .NET API przetwarzania programu Excel"
"title": "Dodaj owal do arkusza kalkulacyjnego w programie Excel"
"url": "/pl/net/excel-shapes-controls/add-oval-to-worksheet-excel/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj owal do arkusza kalkulacyjnego w programie Excel

## Wstęp
Tworzenie oszałamiających i interaktywnych plików Excela może obejmować więcej niż tylko liczby i formuły. Kształty takie jak owale mogą dodać atrakcyjności wizualnej lub zapewnić funkcjonalne elementy w arkuszach kalkulacyjnych. W tym samouczku przyjrzymy się, jak używać Aspose.Cells dla .NET, aby programowo dodawać owale do arkusza kalkulacyjnego Excela. Niezależnie od tego, czy chcesz dodać trochę polotu, czy funkcjonalności, mamy dla Ciebie przewodnik krok po kroku, który wszystko rozbija.
## Wymagania wstępne
Zanim zagłębisz się w kod, musisz zadbać o kilka rzeczy:
1. Biblioteka Aspose.Cells dla .NET: Można ją pobrać ze strony [Tutaj](https://releases.aspose.com/cells/net/) lub zainstaluj go za pomocą NuGet w Visual Studio.
2. Środowisko programistyczne: AC# IDE, np. Visual Studio.
3. Podstawowa znajomość języka C#: Powinieneś znać podstawowe koncepcje kodowania w języku C#.
Pamiętaj również o skonfigurowaniu projektu poprzez zainstalowanie biblioteki Aspose.Cells for .NET. Jeśli jeszcze nie masz licencji, możesz złożyć wniosek o [licencja tymczasowa](https://purchase.aspose.com/temporary-license/) lub użyj [bezpłatny okres próbny](https://releases.aspose.com/) wersja.
## Importuj pakiety
Przed napisaniem jakiegokolwiek kodu upewnij się, że uwzględniłeś wymagane przestrzenie nazw. Oto fragment kodu C#, aby upewnić się, że używasz właściwych bibliotek:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Krok 1: Skonfiguruj swój katalog
Pierwszym krokiem w dodawaniu owalu do arkusza Excel jest określenie miejsca, w którym plik Excel zostanie zapisany. Zdefiniujmy ścieżkę katalogu i upewnijmy się, że katalog istnieje, zanim zapiszemy naszą pracę.

Utworzymy ścieżkę katalogu i sprawdzimy, czy istnieje. Jeśli folder nie istnieje, zostanie utworzony.
```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";
// Utwórz katalog, jeśli jeszcze go nie ma.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Ten krok jest bardzo ważny, gdyż gwarantuje, że plik zostanie zapisany we właściwej lokalizacji i nie będziesz mieć później problemów ze ścieżką dostępu do pliku.
## Krok 2: Zainicjuj nowy skoroszyt
Następnie musimy utworzyć nowy skoroszyt, w którym dodamy nasze owalne kształty. Skoroszyt reprezentuje plik Excela i możemy do niego dodawać zawartość lub kształty.

W tym kroku tworzymy nową instancję `Workbook` obiekt, który będzie służył jako kontener na pliki Excela.
```csharp
// Utwórz nowy skoroszyt.
Workbook excelbook = new Workbook();
```
## Krok 3: Dodaj pierwszy kształt owalny
Teraz nadchodzi zabawna część — dodanie owalu do arkusza kalkulacyjnego. Ten owal może reprezentować element wizualny, taki jak przycisk lub wyróżnienie. Zaczniemy od dodania pierwszego owalu do pierwszego arkusza kalkulacyjnego naszego skoroszytu.

Tutaj używamy `Shapes.AddOval()` metoda tworzenia owalu na arkuszu kalkulacyjnym w określonym wierszu i kolumnie.
```csharp
// Dodaj kształt owalny.
Aspose.Cells.Drawing.Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```
Parametry wewnątrz `AddOval()` są następujące:
- Pierwsze dwie liczby oznaczają wiersz i kolumnę w lewym górnym rogu owalu.
- Następne dwie liczby oznaczają wysokość i szerokość owalu.
## Krok 4: Ustaw położenie i styl owalu
Po utworzeniu owalu możemy ustawić jego pozycję, grubość linii i styl kreski. `Placement` Właściwość ta określa zachowanie owalu podczas zmiany rozmiaru lub przenoszenia komórek w arkuszu kalkulacyjnym.

Sprawiamy, że owal staje się swobodnie pływający i dostosowujemy jego wygląd.
```csharp
// Ustaw położenie owalu.
oval1.Placement = PlacementType.FreeFloating;
// Ustaw grubość linii.
oval1.Line.Weight = 1;
// Ustaw styl kreski owalu.
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Dzięki temu owal może się swobodnie przemieszczać w arkuszu, a grubość i styl linii są ustawione tak, aby zapewnić spójność wizualną.
## Krok 5: Dodaj kolejny kształt owalny (koło)
Dlaczego zatrzymać się na jednym? W tym kroku dodamy kolejny kształt owalny, tym razem tworząc idealne koło, dzięki czemu wysokość i szerokość będą takie same.

Tworzymy kolejny owal, umieszczamy go w innym miejscu i upewniamy się, że ma kształt koła, ustawiając równą wysokość i szerokość.
```csharp
// Dodaj kolejny kształt owalny (koło).
Aspose.Cells.Drawing.Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```
## Krok 6: Stylizacja drugiego owalu
Podobnie jak poprzednio, dostosujemy rozmieszczenie, grubość i styl linii drugiego owalu (lub okręgu).

Zastosowujemy podobne właściwości do drugiego owalu, aby dopasować go stylem do pierwszego.
```csharp
// Ustaw położenie owalu.
oval2.Placement = PlacementType.FreeFloating;
// Ustaw grubość linii.
oval2.Line.Weight = 1;
// Ustaw styl kreski owalu.
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Krok 7: Zapisz skoroszyt
Na koniec musimy zapisać skoroszyt z owalami, które właśnie dodaliśmy. Zapisanie pliku zapewnia, że wszystkie nasze zmiany zostaną zapisane.

Zapisujemy skoroszyt w ścieżce katalogu, którą zdefiniowaliśmy wcześniej.
```csharp
// Zapisz plik Excela.
excelbook.Save(dataDir + "book1.out.xls");
```
I to wszystko! Udało Ci się dodać owale do arkusza kalkulacyjnego Excel i zapisać plik.
## Wniosek
Dodawanie kształtów, takich jak owale, do arkusza Excela przy użyciu Aspose.Cells dla .NET jest nie tylko proste, ale także zabawnym sposobem na wzbogacenie arkuszy kalkulacyjnych o dodatkowe elementy wizualne. Niezależnie od tego, czy chodzi o cele projektowe, czy o dodawanie klikalnych elementów, kształty mogą odgrywać znaczącą rolę w wyglądzie i działaniu plików Excela. Tak więc następnym razem, gdy będziesz pracować nad projektem, który wymaga interaktywnych lub wizualnie atrakcyjnych arkuszy Excela, będziesz dokładnie wiedział, jak dodać te idealne owale!
## Najczęściej zadawane pytania
### Czy mogę dodać inne kształty, takie jak prostokąty lub linie, korzystając z Aspose.Cells dla .NET?
Tak, możesz dodawać różne kształty, takie jak prostokąty, linie i strzałki, używając `Shapes` kolekcja w Aspose.Cells.
### Czy można zmienić rozmiar owali po ich dodaniu?
Oczywiście! Możesz modyfikować właściwości wysokości i szerokości owali po ich dodaniu.
### W jakich formatach plików oprócz XLS mogę zapisać skoroszyt?
Aspose.Cells obsługuje wiele formatów, m.in. XLSX, CSV i PDF.
### Czy mogę zmienić kolor obrysu owalu?
Tak, możesz zmienić kolor linii owalu za pomocą `Line.Color` nieruchomość.
### Czy konieczne jest posiadanie licencji na Aspose.Cells?
Chociaż możesz wypróbować Aspose.Cells za darmo, będziesz potrzebować [licencja](https://purchase.aspose.com/buy) do długotrwałego użytkowania lub dostępu do zaawansowanych funkcji.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}