---
title: Pozycja obrazu (bezwzględna) w programie Excel
linktitle: Pozycja obrazu (bezwzględna) w programie Excel
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak pozycjonować obrazy w programie Excel za pomocą Aspose.Cells dla platformy .NET, korzystając z tego kompleksowego samouczka krok po kroku.
weight: 13
url: /pl/net/excel-ole-picture-objects/position-picture-absolute-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pozycja obrazu (bezwzględna) w programie Excel

## Wstęp
Czy kiedykolwiek miałeś problem z poprawnym pozycjonowaniem obrazów w arkuszu kalkulacyjnym programu Excel? Nie jesteś sam! Wielu użytkowników staje przed tym wyzwaniem, zwłaszcza gdy ich potrzeby wizualizacji danych wymagają pozycjonowania absolutnego dla lepszej estetyki lub przejrzystości. Cóż, nie szukaj dalej; ten przewodnik przeprowadzi Cię przez prosty proces pozycjonowania obrazów absolutnych w arkuszu kalkulacyjnym programu Excel przy użyciu Aspose.Cells dla .NET. Niezależnie od tego, czy jesteś programistą pracującym nad manipulacją w programie Excel, czy analitykiem danych chcącym ulepszyć swoje raporty, nasz samouczek krok po kroku jest tutaj, aby uprościć Twoje doświadczenia z obrazami w programie Excel!
## Wymagania wstępne
Zanim zagłębisz się w kod i szczegóły, musisz przygotować kilka rzeczy:
1.  Biblioteka Aspose.Cells: Upewnij się, że masz najnowszą wersję biblioteki Aspose.Cells dla .NET. Możesz ją pobrać ze strony[strona wydań](https://releases.aspose.com/cells/net/).
2. Środowisko programistyczne: Upewnij się, że masz działające środowisko programistyczne .NET. Możesz użyć Visual Studio lub dowolnego innego wybranego IDE.
3. Podstawowa znajomość języka C#: Znajomość języka programowania C# będzie korzystna dla zrozumienia fragmentów kodu.
4. Plik obrazu: Zapisz plik obrazu (np. „logo.jpg”) w wyznaczonym katalogu dokumentów, który zamierzasz wstawić do arkusza Excel.

## Importuj pakiety
Na początek upewnijmy się, że importujemy niezbędne pakiety dla naszego projektu. Twój plik projektu powinien zawierać następujące przestrzenie nazw:
```csharp
using System.IO;
using Aspose.Cells;
```
Importując te przestrzenie nazw, mamy pewność, że nasz program będzie mógł wykorzystać funkcje udostępniane przez Aspose.Cells.
Aby zwiększyć przejrzystość, podzielmy to na łatwiejsze do wykonania kroki.
## Krok 1: Skonfiguruj katalog dokumentów
tym początkowym kroku musisz zdefiniować katalog, w którym znajdują się Twoje dokumenty. Jest to niezbędne, aby program wiedział, gdzie zapisywać lub pobierać pliki. Oto, jak możesz to skonfigurować:
```csharp
string dataDir = "Your Document Directory";
```
 Po prostu zamień`"Your Document Directory"` z rzeczywistą ścieżką, gdzie znajduje się plik obrazu. Może to być coś takiego`"C:\\Users\\YourUsername\\Documents\\"`.
## Krok 2: Tworzenie instancji obiektu skoroszytu
 Następnie należy utworzyć nową instancję`Workbook` Klasa. Ten obiekt reprezentuje Twój plik Excel:
```csharp
Workbook workbook = new Workbook();
```
W tym momencie masz już skoroszyt gotowy do wypełnienia danymi i obrazami.
## Krok 3: Dodawanie nowego arkusza kalkulacyjnego
Teraz, gdy masz skoroszyt, musisz dodać do niego arkusz. To tutaj magia dodawania i pozycjonowania obrazów będzie miała miejsce:
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
 Ten wiersz tworzy nowy arkusz kalkulacyjny w skoroszycie i zwraca jego indeks, który przechowujemy w zmiennej`sheetIndex`.
## Krok 4: Uzyskanie nowego arkusza kalkulacyjnego
Odwołajmy się do nowo utworzonego arkusza kalkulacyjnego. Używając indeksu, który właśnie otrzymaliśmy, możemy uzyskać dostęp do arkusza kalkulacyjnego i nim manipulować:
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
 Teraz możesz pracować z`worksheet` obiekt umożliwiający dodanie treści, w tym obrazów.
## Krok 5: Dodawanie zdjęcia
Teraz ekscytująca część! Oto miejsce, w którym dodajemy obrazek do naszego arkusza kalkulacyjnego. Określamy indeksy wierszy i kolumn, w których chcemy zakotwiczyć obrazek (w tym przypadku w komórce „F6”, która jest wierszem 5 i kolumną 5):
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
Ta linia skutecznie blokuje obraz w określonej lokalizacji względem całego arkusza kalkulacyjnego. Jednak obecnie nadal podlega zmianie rozmiaru wraz z komórkami.
## Krok 6: Dostęp do nowo dodanego zdjęcia
Aby dalej manipulować obrazem, musisz uzyskać dostęp do jego właściwości:
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
Dzięki temu uzyskasz dostęp do właściwości obrazu, który właśnie dodaliśmy!
## Krok 7: Ustawianie pozycjonowania bezwzględnego dla obrazu
 Aby umieścić obraz w absolutnej pozycji (w pikselach), należy określić jego położenie za pomocą`Left` I`Top` właściwości. Tutaj będziesz mieć kontrolę nad tym, gdzie pojawi się obraz:
```csharp
picture.Left = 60;
picture.Top = 10;
```
W razie potrzeby możesz dostosować obie wartości, określają one odpowiednio poziome i pionowe położenie obrazu.
## Krok 8: Zapisywanie pliku Excel
Na koniec, po wprowadzeniu wszystkich modyfikacji, czas zapisać skoroszyt:
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
 Spowoduje to utworzenie pliku Excel o nazwie`book1.out.xls` w zdefiniowanym wcześniej katalogu dokumentów, zawierającym arkusz kalkulacyjny z umieszczonym absolutnie obrazkiem.

## Wniosek
I masz! Udało Ci się umieścić obraz w arkuszu Excela z pozycjonowaniem absolutnym przy użyciu Aspose.Cells dla .NET. Ten prosty proces nie tylko poprawia prezentację wizualną Twoich dokumentów Excela, ale także zapewnia, że obrazy pozostaną dokładnie tam, gdzie chcesz — niezależnie od zmian wprowadzonych do rozmiarów komórek i wysokości wierszy. Teraz, niezależnie od tego, czy przygotowujesz raport, czy tworzysz pulpit nawigacyjny, możesz mieć pewność, że Twoje obrazy będą za każdym razem idealnie umieszczone.
## Najczęściej zadawane pytania
### Czym jest Aspose.Cells dla .NET?
Aspose.Cells for .NET to biblioteka .NET umożliwiająca programistom tworzenie, edytowanie i konwertowanie arkuszy kalkulacyjnych programu Excel w sposób programowy, bez konieczności korzystania z programu Microsoft Excel.
### Czy mogę wykonywać inne manipulacje obrazami za pomocą Aspose.Cells?
Tak, oprócz pozycjonowania możesz również zmieniać rozmiar, obracać i modyfikować obrazy w arkuszach kalkulacyjnych programu Excel, korzystając z biblioteki Aspose.Cells.
### Czy korzystanie z Aspose.Cells jest bezpłatne?
 Aspose.Cells to produkt komercyjny, ale możesz zacząć od bezpłatnego okresu próbnego dostępnego na ich stronie[strona z bezpłatną wersją próbną](https://releases.aspose.com/).
### Jak uzyskać tymczasową licencję na Aspose.Cells?
 O licencję tymczasową możesz się ubiegać za pośrednictwem[tymczasowa strona licencji](https://purchase.aspose.com/temporary-license/) dostarczone przez Aspose.
### Gdzie mogę znaleźć więcej przykładów i dokumentacji?
 Ten[Dokumentacja Aspose.Cells](https://reference.aspose.com/cells/net/) zawiera obszerne zasoby, w tym przykłady kodu i bardziej szczegółowe funkcje.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
