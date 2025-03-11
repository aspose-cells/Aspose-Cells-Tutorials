---
title: Pobierz wymiary strony arkusza kalkulacyjnego
linktitle: Pobierz wymiary strony arkusza kalkulacyjnego
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak uzyskać wymiary strony w arkuszu kalkulacyjnym programu Excel za pomocą Aspose.Cells dla .NET. Przewodnik krok po kroku, jak dostosować rozmiary papieru A2, A3, A4 i Letter.
weight: 13
url: /pl/net/worksheet-page-setup-features/get-page-dimensions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pobierz wymiary strony arkusza kalkulacyjnego

## Wstęp
Jeśli pracujesz z plikami Excel programowo, używając Aspose.Cells dla .NET, czasami musisz uzyskać dostęp do wymiarów strony arkusza kalkulacyjnego i je ustawić. Znajomość wymiarów może pomóc w układach, drukowaniu i dostosowywaniu arkuszy Excel do określonych celów. W tym artykule przyjrzymy się, jak pobierać i wyświetlać różne wymiary strony w Excelu, używając Aspose.Cells dla .NET. Przejdziemy przez samouczek krok po kroku, aby upewnić się, że znasz wszystkie szczegóły, aby zacząć pewnie.
## Wymagania wstępne
Zanim zaczniesz, upewnij się, że masz wszystko, czego potrzebujesz, aby móc skorzystać z tego samouczka.
1.  Aspose.Cells dla .NET: Upewnij się, że masz zainstalowane Aspose.Cells dla .NET. Możesz[pobierz bibliotekę tutaj](https://releases.aspose.com/cells/net/) lub zainstaluj go poprzez NuGet w swoim projekcie .NET.
2. Środowisko .NET: zgodne środowisko programistyczne .NET (np. Visual Studio).
3.  Konfiguracja licencji: Aby uzyskać pełną funkcjonalność Aspose.Cells, zastosuj licencję. Możesz[poproś o bezpłatną licencję tymczasową](https://purchase.aspose.com/temporary-license/) w celach ewaluacyjnych.
Jeśli testujesz Aspose.Cells po raz pierwszy, zacznij od bezpłatnej wersji próbnej.
## Importuj pakiety
Zanim przejdziemy do kodu, musisz zaimportować przestrzeń nazw Aspose.Cells do swojego projektu, aby uzyskać dostęp do wszystkich niezbędnych klas i metod.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Podzielmy proces na proste kroki. Tutaj uzyskamy dostęp do różnych rozmiarów papieru, zastosujemy je do arkusza kalkulacyjnego i wydrukujemy wymiary dla każdego z nich.
## Krok 1: Utwórz instancję skoroszytu
 Pierwszym krokiem jest utworzenie instancji`Workbook` Klasa. Ten obiekt będzie działał jako nasz główny skoroszyt zawierający arkusze, którymi możemy manipulować.
```csharp
Workbook book = new Workbook();
```
 Myśleć`Workbook` jako główny kontener dla pliku Excel. Potrzebujemy go do dostępu i kontroli poszczególnych arkuszy kalkulacyjnych.
## Krok 2: Uzyskaj dostęp do pierwszego arkusza kalkulacyjnego
 Następnie przejdźmy do pierwszego arkusza w skoroszycie. Domyślnie nowy skoroszyt zawiera jeden arkusz, więc możemy bezpośrednio odwołać się do niego, używając indeksu`0`.
```csharp
Worksheet sheet = book.Worksheets[0];
```
 Ten`Worksheets` kolekcja w`Workbook` pozwala nam uzyskać dostęp do każdego arkusza roboczego według indeksu. Tutaj chwytamy pierwszy arkusz, aby rozpocząć ustawianie wymiarów strony.
## Krok 3: Ustaw rozmiar papieru na A2 i wymiary wyświetlania
Teraz, gdy mamy dostęp do naszego arkusza kalkulacyjnego, ustawmy jego rozmiar papieru na A2. Ustawienie rozmiaru papieru jest przydatne do formatowania strony przed wydrukowaniem lub wyeksportowaniem. Po ustawieniu rozmiaru papieru wydrukujemy wymiary strony w calach.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
 Tutaj zmieniamy`PaperSize` nieruchomość do`PaperA2` . Po ustawieniu rozmiaru,`PageSetup.PaperWidth` I`PageSetup.PaperHeight` pobierz szerokość i wysokość arkusza w calach. Daje nam to szybki przegląd wymiarów strony.
## Krok 4: Ustaw rozmiar papieru na A3 i wymiary wyświetlania
Wykonując te same kroki, co powyżej, dostosujmy wymiary strony do rozmiaru A3. Ta zmiana jest przydatna w przypadku nieco większych wydruków lub w celu umieszczenia większej ilości treści na jednej stronie.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Rozmiar A3 jest dwukrotnie większy od rozmiaru A4, co czyni go dobrym wyborem do dużych tabel lub szczegółowych wykresów. Zmiana rozmiaru papieru pomaga odpowiednio dostosować układ arkusza kalkulacyjnego.
## Krok 5: Ustaw rozmiar papieru na A4 i wymiary wyświetlania
Teraz ustawmy rozmiar papieru na A4. Jest to najczęściej używany rozmiar strony do drukowania dokumentów. Później wyświetlimy zaktualizowane wymiary.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Jeśli Twoim celem jest standardowy format dokumentu, A4 jest zazwyczaj najbardziej odpowiednim rozmiarem. Znajomość wymiarów może pomóc w dostosowaniu układu treści, aby uniknąć problemów z drukowaniem.
## Krok 6: Ustaw rozmiar papieru na Letter i wymiary wyświetlania
Na koniec ustawimy rozmiar papieru na format Letter, który jest powszechnie używany w Ameryce Północnej. Wydrukujmy wymiary po raz ostatni.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Rozmiar Letter jest powszechnie używany w dokumentach w Ameryce Północnej, więc ustawienie tego rozmiaru jest pomocne podczas współpracy z zespołami lub klientami z tego regionu.
## Wniosek
tym samouczku przeprowadziliśmy przez proces ustawiania i pobierania wymiarów stron dla różnych rozmiarów papieru za pomocą Aspose.Cells dla .NET. Konfigurując rozmiary stron, takie jak A2, A3, A4 i Letter, możesz formatować arkusze kalkulacyjne programu Excel, aby odpowiadały konkretnym potrzebom drukowania i układu. Ta kontrola nad wymiarami stron jest szczególnie cenna w przypadku profesjonalnych raportów i prezentacji, ponieważ zapewnia, że Twoja treść idealnie pasuje do każdego rozmiaru strony.
## Najczęściej zadawane pytania
### Jak mogę zmienić orientację strony w Aspose.Cells?  
 Możesz zmienić orientację za pomocą`PageSetup.Orientation` właściwość, ustawiając ją na`PageOrientationType.Portrait` Lub`PageOrientationType.Landscape`.
### Czy mogę ustawić niestandardowe wymiary strony w Aspose.Cells?  
 Tak, możesz ustawić niestandardowe wymiary strony, dostosowując marginesy i opcje skalowania w obszarze`PageSetup` dla większej kontroli.
### Jaki jest domyślny rozmiar papieru w Aspose.Cells?  
Domyślny rozmiar papieru to zazwyczaj A4. Może to jednak zależeć od ustawień regionalnych i można je dostosować w razie potrzeby.
### Czy w Aspose.Cells można wyświetlać podgląd układu strony?  
Chociaż Aspose.Cells nie oferuje podglądu graficznego, można programowo skonfigurować układy i używać podglądów wydruku w programie Excel.
### Jak zainstalować Aspose.Cells dla .NET?  
 Możesz zainstalować Aspose.Cells za pomocą Menedżera pakietów NuGet w programie Visual Studio lub pobrać bibliotekę DLL z[Strona pobierania Aspose.Cells](https://releases.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
