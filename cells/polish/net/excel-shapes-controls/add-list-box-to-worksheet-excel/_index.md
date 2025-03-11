---
title: Dodaj pole listy do arkusza kalkulacyjnego w programie Excel
linktitle: Dodaj pole listy do arkusza kalkulacyjnego w programie Excel
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak dodać pole listy do arkusza kalkulacyjnego programu Excel za pomocą Aspose.Cells dla .NET. Postępuj zgodnie z naszym prostym przewodnikiem krok po kroku i spraw, aby Twoje arkusze kalkulacyjne programu Excel były interaktywne.
weight: 20
url: /pl/net/excel-shapes-controls/add-list-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj pole listy do arkusza kalkulacyjnego w programie Excel

## Wstęp
Dodanie interaktywnych elementów do arkuszy kalkulacyjnych programu Excel, takich jak pole listy, może znacznie usprawnić zarządzanie danymi i prezentację. Niezależnie od tego, czy tworzysz formularz interaktywny, czy niestandardowe narzędzie do wprowadzania danych, możliwość kontrolowania danych wprowadzanych przez użytkownika za pomocą pola listy jest nieoceniona. Aspose.Cells dla .NET zapewnia wydajny sposób dodawania i zarządzania tymi elementami sterującymi w plikach programu Excel. W tym przewodniku przeprowadzimy Cię przez proces dodawania pola listy do arkusza kalkulacyjnego za pomocą Aspose.Cells dla .NET.
## Wymagania wstępne
Zanim zaczniesz kodować, upewnij się, że dysponujesz następującymi narzędziami i zasobami:
-  Biblioteka Aspose.Cells dla .NET: Można ją pobrać ze strony[Strona pobierania Aspose.Cells dla .NET](https://releases.aspose.com/cells/net/).
- Środowisko programistyczne: dowolne środowisko IDE obsługujące programowanie w środowisku .NET, np. Visual Studio.
- .NET Framework: Upewnij się, że Twój projekt jest ukierunkowany na obsługiwaną wersję środowiska .NET Framework.
 Warto również rozważyć zakup[licencja tymczasowa](https://purchase.aspose.com/temporary-license/) jeśli chcesz poznać wszystkie funkcje bez ograniczeń.
## Importuj pakiety
Zanim zaczniesz, upewnij się, że zaimportowałeś niezbędne przestrzenie nazw Aspose.Cells. Oto jak to zrobić:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
W tym samouczku podzielimy proces dodawania pola listy na kilka prostych kroków. Postępuj dokładnie według każdego kroku, aby upewnić się, że wszystko działa zgodnie z oczekiwaniami.
## Krok 1: Konfigurowanie katalogu dokumentów
Zanim utworzysz plik Excel, potrzebujesz lokalizacji, w której go zapiszesz. Oto jak skonfigurować katalog:
```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";
// Utwórz katalog, jeśli jeszcze nie istnieje.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
W tym kroku definiujesz, gdzie będzie przechowywany Twój plik. Kod sprawdza, czy katalog istnieje, a jeśli nie, tworzy go dla Ciebie. Dzięki temu masz pewność, że później nie napotkasz żadnych błędów „plik nie został znaleziony”.
## Krok 2: Utwórz nowy skoroszyt i uzyskaj dostęp do pierwszego arkusza kalkulacyjnego
Następnie utworzymy nowy skoroszyt i przejdziemy do pierwszego arkusza, w którym dodamy naszą listę rozwijaną.
```csharp
// Utwórz nowy skoroszyt.
Workbook workbook = new Workbook();
// Pobierz pierwszy arkusz.
Worksheet sheet = workbook.Worksheets[0];
```
Skoroszyt to zasadniczo plik Excela. Tutaj tworzymy nowy skoroszyt i uzyskujemy dostęp do pierwszego arkusza, w którym umieścimy pole listy. Wyobraź sobie, że tworzysz puste płótno, na którym będziesz malować kontrolki.
## Krok 3: Wprowadź dane do pola listy
Zanim dodamy pole listy, musimy uzupełnić dane, do których będzie się odwoływać pole listy.
```csharp
// Pobierz kolekcję komórek arkusza kalkulacyjnego.
Cells cells = sheet.Cells;
// Wprowadź wartość dla etykiety.
cells["B3"].PutValue("Choose Dept:");
// Ustaw etykietę na pogrubioną.
cells["B3"].GetStyle().Font.IsBold = true;
// Wprowadź wartości dla pola listy.
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
Tutaj dodajemy tekst do arkusza kalkulacyjnego. Etykieta „Choose Dept:” jest umieszczona w komórce B3, a jej czcionka jest ustawiona na pogrubioną. W kolumnie A wstawiamy wartości, które będą służyć jako zakres wejściowy dla naszego pola listy, reprezentując różne działy. Ten zakres wejściowy to to, co użytkownicy będą wybierać podczas interakcji z polem listy.
## Krok 4: Dodaj pole listy do arkusza kalkulacyjnego
Teraz, gdy skonfigurowaliśmy dane, możemy dodać samą kontrolkę listy rozwijanej.
```csharp
// Dodaj nową listę rozwijaną.
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
Ten kod dodaje pole listy do arkusza kalkulacyjnego. Parametry definiują pozycję i rozmiar pola listy. Pole listy jest umieszczone w wierszu 2, kolumnie 0, o szerokości 122 i wysokości 100. Są to współrzędne i rozmiar, które określają, gdzie pole listy pojawi się w arkuszu kalkulacyjnym.
## Krok 5: Ustaw właściwości pola listy
Następnie ustawimy różne właściwości listy rozwijanej, aby była w pełni funkcjonalna.
```csharp
// Ustaw typ umiejscowienia.
listBox.Placement = PlacementType.FreeFloating;
// Ustaw połączoną komórkę.
listBox.LinkedCell = "A1";
// Ustaw zakres wejściowy.
listBox.InputRange = "A2:A7";
// Ustaw typ zaznaczenia.
listBox.SelectionType = SelectionType.Single;
// Ustaw listę rozwijaną z cieniowaniem 3-D.
listBox.Shadow = true;
```
- PlacementType.FreeFloating: Ta właściwość zapewnia, że pole listy rozwijanej pozostanie w swoim położeniu niezależnie od sposobu modyfikacji arkusza kalkulacyjnego.
- LinkedCell: Ustawia komórkę (w tym przypadku A1), w której będzie wyświetlana wartość wybrana z listy.
- InputRange: Wskazuje polu listy, gdzie ma szukać listy opcji (od A2 do A7, które ustawiliśmy wcześniej).
- SelectionType.Single: Ogranicza użytkownika do wybrania tylko jednego elementu z listy.
- Cień: Efekt cienia nadaje polu listy bardziej trójwymiarowy wygląd, co czyni je atrakcyjniejszymi wizualnie.
## Krok 6: Zapisz plik Excel
Na koniec zapiszmy nasz skoroszyt z dołączoną listą rozwijaną.
```csharp
// Zapisz skoroszyt.
workbook.Save(dataDir + "book1.out.xls");
```
Ta linia kodu zapisuje skoroszyt do katalogu, który skonfigurowaliśmy wcześniej. Plik nazywa się „book1.out.xls”, ale możesz wybrać dowolną nazwę, która pasuje do Twojego projektu.
## Wniosek
I masz! Udało Ci się dodać pole listy do arkusza kalkulacyjnego programu Excel przy użyciu Aspose.Cells dla .NET. Za pomocą zaledwie kilku linijek kodu utworzyliśmy w pełni funkcjonalne pole listy, dzięki czemu arkusz kalkulacyjny stał się bardziej interaktywny i dynamiczny. Ten samouczek powinien dać Ci solidne podstawy do eksplorowania innych kontrolek i funkcji w Aspose.Cells dla .NET. Eksperymentuj dalej, a wkrótce opanujesz rozległą funkcjonalność biblioteki!
## Najczęściej zadawane pytania
### Czy mogę zezwolić na wielokrotny wybór w polu listy?  
 Tak, możesz zmienić`SelectionType` Do`SelectionType.Multi` aby umożliwić wybór wielu opcji.
### Czy mogę zmienić wygląd listy rozwijanej?  
Oczywiście! Aspose.Cells pozwala dostosować wygląd pola listy, w tym jego rozmiar, czcionkę, a nawet kolor.
### Co się stanie, jeśli później będę musiał usunąć pole listy?  
 Możesz uzyskać dostęp do pola listy i usunąć je z niego.`Shapes` kolekcja używająca`sheet.Shapes.RemoveAt(index)`.
### Czy mogę połączyć pole listy z inną komórką?  
 Tak, po prostu zmień`LinkedCell` właściwość do dowolnej innej komórki, w której chcesz wyświetlić wybraną wartość.
### Jak dodać więcej elementów do pola listy?  
Wystarczy zaktualizować zakres wejściowy, wstawiając więcej wartości do określonych komórek, a lista rozwijana zostanie automatycznie zaktualizowana.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
