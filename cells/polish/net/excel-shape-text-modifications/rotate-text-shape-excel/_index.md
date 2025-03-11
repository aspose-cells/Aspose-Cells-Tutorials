---
title: Obróć tekst z kształtem w programie Excel
linktitle: Obróć tekst z kształtem w programie Excel
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak obracać tekst z kształtami w programie Excel za pomocą Aspose.Cells dla .NET. Postępuj zgodnie z tym przewodnikiem krok po kroku, aby uzyskać idealną prezentację w programie Excel.
weight: 12
url: /pl/net/excel-shape-text-modifications/rotate-text-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obróć tekst z kształtem w programie Excel

## Wstęp
W świecie Excela reprezentacja wizualna jest równie ważna, co same dane. Niezależnie od tego, czy tworzysz raport, czy projektujesz dynamiczny pulpit nawigacyjny, sposób rozmieszczenia informacji może mieć ogromny wpływ na ich czytelność i ogólny wygląd. Czy kiedykolwiek chciałeś obrócić tekst, aby stylowo dopasować go do kształtów? Masz szczęście! W tym samouczku zagłębimy się w to, jak obracać tekst za pomocą kształtów przy użyciu Aspose.Cells dla .NET, zapewniając, że Twoje arkusze kalkulacyjne nie tylko informują, ale i robią wrażenie.
## Wymagania wstępne
Zanim zaczniemy, upewnijmy się, że masz wszystko, czego potrzebujesz:
1. Visual Studio: Upewnij się, że na Twoim komputerze jest zainstalowany program Visual Studio, ponieważ to właśnie w nim będziemy pisać kod.
2.  Aspose.Cells dla .NET: Będziesz potrzebować biblioteki Aspose.Cells. Możesz[pobierz najnowszą wersję tutaj](https://releases.aspose.com/cells/net/) lub wypróbuj za darmo z[bezpłatny okres próbny](https://releases.aspose.com/).
3. Podstawowa znajomość języka C#: Znajomość języka C# i środowiska .NET będzie pomocna, aczkolwiek poprowadzimy Cię przez każdy krok.
4.  Plik Excela: Nazwijmy to przykładowym plikiem Excela`sampleRotateTextWithShapeInsideWorksheet.xlsx`, jest potrzebne do przetestowania naszego kodu. Powinieneś umieścić ten plik w katalogu, do którego masz łatwy dostęp.
Wszystko gotowe? Fantastycznie! Przejdźmy do zabawy.
## Importuj pakiety
Aby rozpocząć, musimy zaimportować niezbędne pakiety do naszego projektu. Oto jak to zrobić:
### Utwórz nowy projekt
1. Otwórz program Visual Studio.
2. Wybierz „Utwórz nowy projekt”.
3. Wybierz „Aplikację konsolową” i wybierz C# jako preferowany język programowania.
### Zainstaluj Aspose.Cells
Teraz dodajmy Aspose.Cells do Twojego projektu. Możesz to zrobić za pomocą NuGet Package Manager:
1. Otwórz „Narzędzia” w górnym menu.
2. Wybierz „Menedżer pakietów NuGet”, a następnie „Zarządzaj pakietami NuGet dla rozwiązania”.
3. Wyszukaj „Aspose.Cells”.
4. Kliknij „Zainstaluj”, aby dodać do projektu.
### Dodaj dyrektywę Using
Na górze głównego pliku C# należy dodać następującą dyrektywę:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Teraz możemy zacząć kodować!
Podzielmy proces na łatwe do przyswojenia kroki. Oto jak obrócić tekst z kształtami w pliku Excel:
## Krok 1: Skonfiguruj ścieżki katalogów
Najpierw musisz skonfigurować katalogi źródłowe i wyjściowe, w których będą przechowywane pliki Excela. Oto jak to zrobić:
```csharp
//Katalog źródłowy
string sourceDir = "Your Document Directory"; // Ustaw katalog dokumentów
//Katalog wyjściowy
string outputDir = "Your Document Directory"; // Ustaw swój katalog wyjściowy
```
 Zastępować`"Your Document Directory"` z rzeczywistą ścieżką, gdzie jesteś`sampleRotateTextWithShapeInsideWorksheet.xlsx` plik się znajduje.
## Krok 2: Załaduj przykładowy plik Excel
Teraz załadujmy przykładowy plik Excel. Jest to kluczowe, ponieważ chcemy manipulować istniejącymi danymi.
```csharp
//Załaduj przykładowy plik Excel.
Workbook wb = new Workbook(sourceDir + "sampleRotateTextWithShapeInsideWorksheet.xlsx");
```
## Krok 3: Uzyskaj dostęp do arkusza kalkulacyjnego
Po załadowaniu pliku musimy uzyskać dostęp do konkretnego arkusza kalkulacyjnego, który chcemy zmodyfikować. W naszym przypadku jest to pierwszy arkusz kalkulacyjny.
```csharp
//Otwórz pierwszy arkusz kalkulacyjny.
Worksheet ws = wb.Worksheets[0];
```
## Krok 4: Modyfikowanie komórki
Następnie zmodyfikujemy konkretną komórkę, aby wyświetlić wiadomość. W naszym przykładzie użyjemy komórki B4.
```csharp
//Przejdź do komórki B4 i dodaj do niej wiadomość.
Cell b4 = ws.Cells["B4"];
b4.PutValue("Text is not rotating with shape because RotateTextWithShape is false.");
```
Ten krok ma na celu komunikację — upewnienie się, że osoba otwierająca ten arkusz rozumie, co zmieniamy.
## Krok 5: Uzyskaj dostęp do pierwszego kształtu
Aby obrócić tekst, potrzebujemy kształtu, z którym możemy pracować. Tutaj uzyskamy dostęp do pierwszego kształtu w arkuszu.
```csharp
//Uzyskaj dostęp do pierwszego kształtu.
Shape sh = ws.Shapes[0];
```
## Krok 6: Dostosuj wyrównanie tekstu kształtu
Tutaj dzieje się magia. Dostosujemy właściwości wyrównania tekstu kształtu.
```csharp
//Uzyskaj dostęp do wyrównania tekstu kształtu.
Aspose.Cells.Drawing.Texts.ShapeTextAlignment shapeTextAlignment = sh.TextBody.TextAlignment;
//Nie obracaj tekstu razem z kształtem, ustawiając właściwość RotateTextWithShape na false.
shapeTextAlignment.RotateTextWithShape = false;
```
 Poprzez ustawienie`RotateTextWithShape` jeśli ustawimy ją jako fałsz, upewniamy się, że tekst pozostaje w pozycji pionowej i nie obraca się wraz z kształtem, dzięki czemu wszystko pozostaje uporządkowane i zorganizowane.
## Krok 7: Zapisz plik wyjściowy Excela
Na koniec zapiszmy nasze zmiany w nowym pliku Excel. Dzięki temu upewnimy się, że nie stracimy naszych edycji i będziemy mieć uporządkowany wynik.
```csharp
//Zapisz plik wyjściowy Excela.
wb.Save(outputDir + "outputRotateTextWithShapeInsideWorksheet.xlsx");
```
I to wszystko! Twój plik wyjściowy jest teraz zapisany, w tym tekst w komórce B4 i zmiany kształtu.
## Krok 8: Wykonaj kod
 W twoim`Main` metoda, owiń wszystkie powyższe fragmenty kodu i uruchom swój projekt. Zobacz zmiany odzwierciedlone w pliku wyjściowym!
```csharp
Console.WriteLine("RotateTextWithShapeInsideWorksheet executed successfully.");
```
## Wniosek
Obracanie tekstu za pomocą kształtów w programie Excel przy użyciu Aspose.Cells dla .NET może wydawać się skomplikowanym procesem na początku, ale staje się całkiem proste, gdy się go rozłoży na czynniki pierwsze. Postępując zgodnie z tymi prostymi krokami, możesz dostosować arkusze kalkulacyjne, aby wyglądały bardziej profesjonalnie i wizualnie. Teraz, niezależnie od tego, czy robisz to dla klienta, czy w ramach swoich osobistych projektów, wszyscy będą zachwycać się jakością Twojej pracy!
## Najczęściej zadawane pytania
### Czy mogę używać Aspose.Cells za darmo?
 Tak! Możesz użyć[bezpłatny okres próbny](https://releases.aspose.com/) aby wypróbować bibliotekę.
### Jakie wersje programu Excel obsługuje Aspose.Cells?
Aspose.Cells obsługuje wiele formatów plików Excel, w tym XLS, XLSX, CSV i inne.
### Czy w starszych wersjach programu Excel można obracać tekst za pomocą kształtów?
Tak, tę funkcjonalność można zastosować do starszych formatów obsługiwanych przez Aspose.Cells.
### Gdzie mogę znaleźć więcej dokumentacji na temat Aspose.Cells?
 Możesz zapoznać się z kompleksową ofertą[dokumentacja](https://reference.aspose.com/cells/net/) aby uzyskać więcej informacji.
### Jak uzyskać pomoc techniczną dotyczącą Aspose.Cells?
 Możesz poprosić o wsparcie odwiedzając stronę[Forum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
