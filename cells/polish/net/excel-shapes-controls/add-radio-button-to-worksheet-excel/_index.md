---
title: Dodaj przycisk radiowy do arkusza kalkulacyjnego w programie Excel
linktitle: Dodaj przycisk radiowy do arkusza kalkulacyjnego w programie Excel
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak dodawać przyciski radiowe do arkusza kalkulacyjnego programu Excel za pomocą Aspose.Cells dla .NET dzięki temu prostemu przewodnikowi krok po kroku. Idealne do tworzenia interaktywnych formularzy programu Excel.
weight: 19
url: /pl/net/excel-shapes-controls/add-radio-button-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj przycisk radiowy do arkusza kalkulacyjnego w programie Excel

## Wstęp
Czy kiedykolwiek zastanawiałeś się, jak urozmaicić arkusze Excela interaktywnymi elementami, takimi jak przyciski radiowe? Niezależnie od tego, czy tworzysz ankietę, formularz czy narzędzie analityczne, dodawanie przycisków radiowych może naprawdę poprawić interakcję użytkownika. W tym samouczku przeprowadzimy Cię przez proces dodawania przycisków radiowych do arkuszy Excela przy użyciu Aspose.Cells dla .NET. Podzielimy wszystko na łatwe do wykonania kroki, zapewniając, że do końca tego artykułu będziesz profesjonalistą. Gotowy do zanurzenia się? Zaczynajmy!
## Wymagania wstępne
Zanim przejdziemy do przyjemnej części dodawania przycisków radiowych, upewnijmy się, że wszystko jest skonfigurowane.
1.  Aspose.Cells dla .NET: Najpierw upewnij się, że pobrałeś i zainstalowałeś[Aspose.Cells dla .NET](https://releases.aspose.com/cells/net/) biblioteka. Możesz ją pobrać przez NuGet w Visual Studio lub ze strony pobierania.
2. IDE (zintegrowane środowisko programistyczne): Do pisania i wykonywania kodu C# potrzebne będzie środowisko IDE, np. Visual Studio.
3. .NET Framework: Upewnij się, że na Twoim komputerze jest zainstalowany .NET Framework 4.0 lub nowszy. Aspose.Cells wymaga tego do działania.
4. Podstawowa znajomość języka C#: Znajomość składni języka C# i programowania .NET ułatwi Ci zrozumienie materiału.
Gdy już wszystko będzie na swoim miejscu, będziemy gotowi do działania!
## Importuj pakiety
Przed kodowaniem konieczne jest zaimportowanie niezbędnych przestrzeni nazw, aby uniknąć późniejszych błędów. Dodaj poniższe do swojego kodu:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Drawing;
```
Tego typu importy są niezbędne do uzyskania dostępu do funkcji skoroszytu, dodawania przycisków radiowych i obsługi operacji na plikach.
## Krok 1: Konfigurowanie skoroszytu
Zacznijmy od utworzenia nowego skoroszytu w programie Excel.
 Na początek musisz utworzyć nową instancję`Workbook` obiekt. Będzie to reprezentować plik Excel w kodzie.
```csharp
// Utwórz nowy skoroszyt.
Workbook excelbook = new Workbook();
```
W tym kroku tworzysz pusty skoroszyt. Wyobraź sobie go jako puste płótno, na którym będziesz dodawać przyciski radiowe w kolejnych krokach.
## Krok 2: Dodawanie i formatowanie wartości komórki
Następnie dodajmy tytuł do arkusza. Dodamy trochę tekstu do komórki`C2` i sformatuj go, aby był pogrubiony. Ten krok dodaje kontekst do przycisków radiowych.
### Wstaw tekst do komórki
```csharp
// Wpisz wartość do komórki C2.
excelbook.Worksheets[0].Cells["C2"].PutValue("Age Groups");
```
### Pogrub tekst
```csharp
// Ustaw czcionkę tekstu w komórce C2 na pogrubioną.
excelbook.Worksheets[0].Cells["C2"].GetStyle().Font.IsBold = true;
```
 Tutaj dodaliśmy prosty tytuł „Grupy wiekowe” w komórce`C2`i pogrubiłem, żeby się wyróżniało. Łatwe, prawda?
## Krok 3: Dodawanie pierwszego przycisku radiowego
A teraz zaczyna się ekscytująca część: dodanie pierwszego przycisku radiowego do arkusza kalkulacyjnego!
### Dodaj przycisk radiowy
```csharp
// Dodaj przycisk radiowy do pierwszego arkusza.
Aspose.Cells.Drawing.RadioButton radio1 = excelbook.Worksheets[0].Shapes.AddRadioButton(3, 0, 2, 0, 30, 110);
```
Ten wiersz dodaje przycisk radiowy do określonej pozycji na arkuszu kalkulacyjnym. Liczby oznaczają jego umiejscowienie i rozmiar. Pomyśl o tym jak o ustawieniu współrzędnych X i Y przycisku.
### Ustaw tekst przycisku radiowego
```csharp
// Ustaw ciąg tekstowy.
radio1.Text = "20-29";
```
Tutaj nadaliśmy przyciskowi opcji etykietę „20-29”, która reprezentuje grupę wiekową.
### Połącz przycisk radiowy z komórką
```csharp
// Ustaw komórkę A1 jako komórkę połączoną dla przycisku radiowego.
radio1.LinkedCell = "A1";
```
 Łączy przycisk radiowy z komórką`A1`co oznacza, że wynik wyboru przycisku zostanie zapisany w tej komórce.
### Dodaj efekt 3D
```csharp
// Zmień wygląd przycisku radiowego na trójwymiarowy.
radio1.Shadow = true;
```
Ponieważ chcieliśmy, aby ten przycisk się wyróżniał, dodaliśmy efekt 3D.
### Dostosuj linię przycisku radiowego
```csharp
// Ustaw grubość linii przycisku radiowego.
radio1.Line.Weight = 4;
// Ustaw styl myślnika dla linii przycisku radiowego.
radio1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Te wiersze kodu zmieniają grubość i styl linii obramowania przycisku radiowego, aby uczynić go bardziej atrakcyjnym wizualnie.
## Krok 4: Dodawanie dodatkowych przycisków radiowych
Dodajmy jeszcze dwa przyciski radiowe dla pozostałych grup wiekowych: „30-39” i „40-49”. Kroki są takie same, tylko z niewielkimi różnicami w współrzędnych i etykietach.
### Dodaj drugi przycisk radiowy
```csharp
// Dodaj kolejny przycisk opcji do pierwszego arkusza.
Aspose.Cells.Drawing.RadioButton radio2 = excelbook.Worksheets[0].Shapes.AddRadioButton(6, 0, 2, 0, 30, 110);
// Ustaw ciąg tekstowy.
radio2.Text = "30-39";
// Ustaw komórkę A1 jako komórkę połączoną dla przycisku radiowego.
radio2.LinkedCell = "A1";
// Zmień wygląd przycisku radiowego na trójwymiarowy.
radio2.Shadow = true;
// Ustaw wagę przycisku radiowego.
radio2.Line.Weight = 4;
// Ustaw styl myślnika przycisku radiowego.
radio2.Line.DashStyle = MsoLineDashStyle.Solid;
```
### Dodaj trzeci przycisk radiowy
```csharp
// Dodaj kolejny przycisk opcji do pierwszego arkusza.
Aspose.Cells.Drawing.RadioButton radio3 = excelbook.Worksheets[0].Shapes.AddRadioButton(9, 0, 2, 0, 30, 110);
// Ustaw ciąg tekstowy.
radio3.Text = "40-49";
// Ustaw komórkę A1 jako komórkę połączoną dla przycisku radiowego.
radio3.LinkedCell = "A1";
// Zmień wygląd przycisku radiowego na trójwymiarowy.
radio3.Shadow = true;
// Ustaw wagę przycisku radiowego.
radio3.Line.Weight = 4;
// Ustaw styl myślnika przycisku radiowego.
radio3.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Krok 5: Zapisywanie pliku Excel
Gdy wszystkie przyciski radiowe zostaną dodane i sformatowane, czas zapisać plik.
```csharp
// Zapisz plik Excela.
string dataDir = "Your Document Directory";
excelbook.Save(dataDir + "book1.out.xls");
```
tym kroku skoroszyt jest zapisywany w określonym katalogu. To takie proste — Twój interaktywny arkusz jest już gotowy!
## Wniosek
I gotowe! Właśnie dodałeś przyciski radiowe do arkusza kalkulacyjnego programu Excel za pomocą Aspose.Cells dla .NET. Ten samouczek obejmował wszystko, od konfiguracji skoroszytu, wstawiania i formatowania wartości, dodawania wielu przycisków radiowych i łączenia ich z komórką. Teraz jesteś gotowy do tworzenia interaktywnych arkuszy kalkulacyjnych programu Excel, które nie tylko wyglądają świetnie, ale także zapewniają ulepszone wrażenia użytkownika. Baw się dobrze, odkrywając więcej możliwości dzięki Aspose.Cells!
## Najczęściej zadawane pytania
### Czy mogę dodać więcej przycisków opcji do różnych arkuszy?  
Oczywiście! Możesz powtórzyć proces na dowolnym arkuszu w skoroszycie, określając poprawny indeks arkusza.
### Czy mogę dodatkowo dostosować wygląd przycisków radiowych?  
Tak, Aspose.Cells oferuje szereg opcji dostosowywania, w tym zmianę kolorów, rozmiarów i innych atrybutów formatowania.
### Jak mogę sprawdzić, który przycisk opcji jest zaznaczony?  
Połączona komórka (np. A1) pokaże indeks wybranego przycisku radiowego. Możesz sprawdzić wartość połączonej komórki, aby dowiedzieć się, który jest wybrany.
### Czy liczba przycisków radiowych, które mogę dodać, jest ograniczona?  
Nie, nie ma sztywnego limitu liczby przycisków radiowych, które możesz dodać. Jednak dobrze jest zachować przyjazny dla użytkownika interfejs.
### Czy mogę używać Aspose.Cells z innymi językami programowania?  
Tak, Aspose.Cells obsługuje wiele języków programowania, w tym Java. Jednak ten samouczek koncentruje się konkretnie na .NET.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
