---
title: Manipulowanie kontrolkami TextBox w programie Excel
linktitle: Manipulowanie kontrolkami TextBox w programie Excel
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak manipulować polami tekstowymi w programie Excel za pomocą Aspose.Cells dla platformy .NET, korzystając z tego prostego w użyciu samouczka krok po kroku.
weight: 15
url: /pl/net/excel-shapes-controls/manipulate-textbox-controls-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Manipulowanie kontrolkami TextBox w programie Excel

## Wstęp
Jeśli kiedykolwiek pracowałeś z programem Excel, prawdopodobnie natknąłeś się na te małe pola tekstowe, które pozwalają dodawać tekst ruchomy do arkusza kalkulacyjnego. Ale co, jeśli musisz manipulować tymi polami tekstowymi programowo? Tutaj przydaje się Aspose.Cells dla .NET. Dzięki niemu możesz łatwo uzyskać dostęp do pól tekstowych i je modyfikować, co czyni je idealnym narzędziem do automatyzacji zadań lub dostosowywania raportów. W tym samouczku przeprowadzimy Cię przez proces manipulowania polami tekstowymi w programie Excel za pomocą Aspose.Cells dla .NET.
## Wymagania wstępne
Zanim przejdziemy do właściwego kodu, upewnijmy się, że wszystko jest poprawnie skonfigurowane:
1.  Aspose.Cells dla .NET: Musisz pobrać bibliotekę Aspose.Cells dla .NET. Link do pobrania znajdziesz[Tutaj](https://releases.aspose.com/cells/net/).
2. Środowisko programistyczne .NET: będzie działać każde środowisko IDE obsługujące platformę .NET, np. Visual Studio.
3. Podstawowa znajomość języka C#: W tym samouczku zakładamy, że znasz podstawową składnię języka C# i strukturę skoroszytów programu Excel.
4.  Plik Excel: Istniejący plik Excel z polami tekstowymi (będziemy używać`book1.xls` tym przykładzie).
5.  Licencja Aspose: Jeśli nie korzystasz z bezpłatnej wersji próbnej, musisz[kupić](https://purchase.aspose.com/buy) licencję lub uzyskać[tymczasowy](https://purchase.aspose.com/temporary-license/).
A teraz przejdźmy do szczegółów!
## Importuj pakiety
Zanim będziesz mógł manipulować skoroszytami i polami tekstowymi programu Excel za pomocą Aspose.Cells, musisz zaimportować niezbędne przestrzenie nazw. Oto fragment kodu, którego użyjesz na początku pliku C#:
```csharp
using System.IO;
using Aspose.Cells;
```
Pakiety te umożliwiają dostęp do skoroszytów, arkuszy kalkulacyjnych i obiektów rysunkowych (np. pól tekstowych).
Teraz, gdy wszystko już skonfigurowaliśmy, możemy podzielić proces manipulowania polami tekstowymi na łatwe do wykonania kroki.
## Krok 1: Skonfiguruj katalog skoroszytu
 Pierwszym krokiem jest określenie, gdzie znajdują się pliki Excela w systemie. Będziesz musiał zastąpić symbol zastępczy`Your Document Directory` z rzeczywistą ścieżką do pliku. Ta ścieżka jest przechowywana w`dataDir` zmienna, aby ułatwić odwoływanie się do niej w całym kodzie.
```csharp
string dataDir = "Your Document Directory";
```
Dzięki temu program będzie wiedział, gdzie znaleźć plik wejściowy programu Excel (`book1.xls`) i gdzie zapisać plik wyjściowy.
## Krok 2: Otwórz plik Excel
Następnie musisz załadować istniejący plik Excela do obiektu Aspose.Cells Workbook. Ten skoroszyt działa jako kontener dla danych Excela, dając Ci dostęp do jego arkuszy i wszelkich obiektów rysunkowych (takich jak pola tekstowe).
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 Ten`Workbook` Klasa z Aspose.Cells załaduje określony plik Excel z Twojego katalogu. Jeśli plik nie istnieje w określonym katalogu, zostanie zgłoszony wyjątek, więc upewnij się, że ścieżka jest poprawna.
## Krok 3: Uzyskaj dostęp do pierwszego arkusza kalkulacyjnego
Teraz, gdy masz załadowany skoroszyt, możesz uzyskać dostęp do jego arkuszy. W tym przykładzie uzyskujemy dostęp do pierwszego arkusza w skoroszycie, który jest przechowywany pod indeksem 0.
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
 Ten`Worksheets` Właściwość daje dostęp do wszystkich arkuszy w skoroszycie. Tutaj interesuje nas tylko pierwszy arkusz, ale możesz pracować z dowolnym arkuszem, podając poprawny indeks.
## Krok 4: Pobierz pierwszy obiekt TextBox
Pola tekstowe w arkuszu Excela są uważane za obiekty rysunkowe. Klasa Aspose.Cells.Drawing.TextBox udostępnia właściwości i metody umożliwiające manipulowanie nimi. Aby uzyskać dostęp do pierwszego pola tekstowego w arkuszu, wystarczy odwołać się do`TextBoxes` kolekcja według indeksu.
```csharp
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[0];
```
 Pobiera pierwszy obiekt pola tekstowego z`TextBoxes` kolekcja. Jeśli twój arkusz nie ma pola tekstowego pod tym indeksem, zostanie zgłoszony wyjątek, więc zawsze upewnij się, że indeks jest prawidłowy.
## Krok 5: Pobierz tekst z pierwszego pola tekstowego
 Po uzyskaniu dostępu do pola tekstowego możesz wyodrębnić zawarty w nim tekst, korzystając z`.Text` nieruchomość.
```csharp
string text0 = textbox0.Text;
```
 Spowoduje to przechwycenie tekstu z pierwszego pola tekstowego do`text0` string. Teraz możesz go wyświetlić, manipulować nim lub przetwarzać w swojej aplikacji.
## Krok 6: Uzyskaj dostęp do drugiego obiektu TextBox
Aby manipulować wieloma polami tekstowymi, możemy pobrać dodatkowe pola z arkusza kalkulacyjnego. Tutaj uzyskamy dostęp do drugiego pola tekstowego w podobny sposób, jak do pierwszego:
```csharp
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[1];
```
Ponownie uzyskujemy dostęp do drugiego pola tekstowego za pomocą indeksu 1 z`TextBoxes`kolekcja.
## Krok 7: Pobierz tekst z drugiego pola tekstowego
Podobnie jak w przypadku pierwszego pola tekstowego, możesz pobrać tekst z drugiego pola tekstowego i zapisać go w ciągu:
```csharp
string text1 = textbox1.Text;
```
Spowoduje to przechwycenie bieżącego tekstu z drugiego pola tekstowego.
## Krok 8: Modyfikuj tekst w drugim polu tekstowym
 Teraz powiedzmy, że chcesz zmodyfikować tekst wewnątrz drugiego pola tekstowego. Możesz to łatwo zrobić, przypisując nowy ciąg do`.Text` Właściwość obiektu pola tekstowego.
```csharp
textbox1.Text = "This is an alternative text";
```
Zmienia to tekst wewnątrz drugiego pola tekstowego na nową zawartość. Możesz wstawić tutaj dowolny tekst zgodnie ze swoimi wymaganiami.
## Krok 9: Zapisz zaktualizowany plik Excela
 Na koniec, po zmodyfikowaniu pól tekstowych, czas zapisać zmiany. Aspose.Cells pozwala zapisać zmodyfikowany skoroszyt za pomocą`.Save()` Metoda. Możesz określić nową nazwę pliku lub nadpisać istniejący plik.
```csharp
workbook.Save(dataDir + "output.out.xls");
```
Spowoduje to zapisanie zmodyfikowanego pliku Excel w wybranej ścieżce wyjściowej. Teraz, gdy otworzysz plik Excel, zobaczysz zmiany, które wprowadziłeś w polach tekstowych.
## Wniosek
I masz to! Właśnie nauczyłeś się manipulować polami tekstowymi w programie Excel za pomocą Aspose.Cells dla .NET. Niezależnie od tego, czy automatyzujesz generowanie raportów, dostosowujesz arkusze programu Excel, czy tworzysz dynamiczną zawartość, Aspose.Cells ułatwia programowe kontrolowanie każdego aspektu plików programu Excel. Od wyodrębniania i modyfikowania tekstu po zapisywanie zaktualizowanych plików, ta biblioteka jest potężnym narzędziem dla programistów pracujących z programem Excel w środowiskach .NET.
## Najczęściej zadawane pytania
### Czy za pomocą Aspose.Cells mogę manipulować innymi obiektami rysunkowymi oprócz pól tekstowych?
Tak, Aspose.Cells pozwala na manipulowanie innymi obiektami rysunkowymi, takimi jak kształty, wykresy i obrazy.
### Co się stanie, jeśli spróbuję uzyskać dostęp do pola tekstowego, które nie istnieje?
 Jeżeli indeks pola tekstowego jest poza zakresem,`IndexOutOfRangeException` zostanie rzucony.
### Czy mogę dodać nowe pola tekstowe do arkusza kalkulacyjnego Excel za pomocą Aspose.Cells?
 Tak, Aspose.Cells pozwala na dodawanie nowych pól tekstowych za pomocą`AddTextBox` metoda.
### Czy potrzebuję licencji, aby korzystać z Aspose.Cells?
 Tak, musisz kupić licencję, ale Aspose oferuje również[bezpłatny okres próbny](https://releases.aspose.com/).
### Czy mogę używać Aspose.Cells z innymi językami programowania oprócz C#?
Tak, Aspose.Cells można używać z dowolnym językiem obsługiwanym przez platformę .NET, np. VB.NET.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
