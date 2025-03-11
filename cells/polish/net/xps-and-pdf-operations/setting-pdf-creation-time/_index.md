---
title: Ustawianie czasu utworzenia pliku PDF w .NET
linktitle: Ustawianie czasu utworzenia pliku PDF w .NET
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak ustawić czas utworzenia pliku PDF w .NET za pomocą Aspose.Cells. Postępuj zgodnie z naszym przewodnikiem krok po kroku, aby bezproblemowo konwertować pliki Excel do PDF.
weight: 11
url: /pl/net/xps-and-pdf-operations/setting-pdf-creation-time/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ustawianie czasu utworzenia pliku PDF w .NET

## Wstęp
dzisiejszej erze cyfrowej możliwość konwersji dokumentów do różnych formatów jest kluczowa dla wielu aplikacji. Jedną z powszechnych potrzeb jest konwersja arkuszy kalkulacyjnych Excela do plików PDF. Nie tylko zachowuje to formatowanie, ale także znacznie ułatwia udostępnianie i drukowanie. Jeśli jesteś programistą pracującym z .NET, Aspose.Cells to fantastyczna biblioteka, która upraszcza ten proces. W tym samouczku zagłębimy się w to, jak ustawić czas utworzenia PDF podczas konwersji pliku Excela do PDF za pomocą Aspose.Cells dla .NET.
## Wymagania wstępne
Zanim przejdziemy do szczegółów kodu, upewnijmy się, że masz wszystko, czego potrzebujesz, aby zacząć.
### Czego potrzebujesz
1. Visual Studio: Upewnij się, że masz zainstalowane Visual Studio na swoim komputerze. To będzie Twoje środowisko programistyczne.
2.  Aspose.Cells dla .NET: Pobierz bibliotekę Aspose.Cells ze strony[strona internetowa](https://releases.aspose.com/cells/net/). Możesz również rozpocząć bezpłatny okres próbny, aby przetestować jego funkcjonalności.
3. Podstawowa wiedza o języku C#: Znajomość programowania w języku C# pomoże Ci lepiej zrozumieć fragmenty kodu.
4.  Plik Excel: Przygotuj plik Excel do konwersji. W tym przykładzie użyjemy pliku o nazwie`Book1.xlsx`.
Teraz, gdy już zadbałeś o wymagania wstępne, możemy zająć się przyjemniejszą częścią — zaimportowaniem niezbędnych pakietów i napisaniem kodu!
## Importuj pakiety
Na początek musisz zaimportować wymagane przestrzenie nazw do pliku C#. Jest to kluczowe, ponieważ umożliwia dostęp do klas i metod udostępnianych przez bibliotekę Aspose.Cells.
### Otwórz swój projekt C#
Otwórz program Visual Studio i utwórz nowy projekt lub otwórz istniejący, w którym chcesz zaimplementować funkcję konwersji do formatu PDF.
### Dodaj odniesienie Aspose.Cells
Możesz dodać bibliotekę Aspose.Cells do swojego projektu, klikając prawym przyciskiem myszy na projekt w Eksploratorze rozwiązań, wybierając „Zarządzaj pakietami NuGet” i wyszukując „Aspose.Cells”. Zainstaluj pakiet.
### Importuj przestrzenie nazw
Na górze pliku C# należy uwzględnić następujące przestrzenie nazw:
```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Charts;
```
Te przestrzenie nazw dadzą ci dostęp do klasy Workbook i innych niezbędnych funkcjonalności.

Teraz, gdy zaimportowaliśmy pakiety, przeanalizujmy szczegółowo proces konwersji pliku Excel do pliku PDF, ustawiając jednocześnie czas utworzenia.
## Krok 1: Zdefiniuj katalog dokumentów
Najpierw musisz określić katalog, w którym przechowywane są Twoje dokumenty. To tutaj znajduje się Twój plik Excel i gdzie zostanie zapisany wyjściowy plik PDF.
```csharp
string dataDir = "Your Document Directory"; // Określ katalog dokumentów
```
 Zastępować`"Your Document Directory"` z rzeczywistą ścieżką, gdzie jesteś`Book1.xlsx` plik jest zlokalizowany. Ta ścieżka pomoże aplikacji zlokalizować plik do przetworzenia.
## Krok 2: Załaduj plik Excel
 Następnie załadujesz plik Excel do`Workbook` obiekt. To właśnie tutaj Aspose.Cells się wyróżnia, ponieważ pozwala na bezproblemową pracę z plikami Excela.
```csharp
string inputPath = dataDir + "Book1.xlsx"; // Ścieżka do pliku Excel
Workbook workbook = new Workbook(inputPath); // Załaduj plik Excel
```
 Ten`Workbook` Klasa służy do ładowania i manipulowania plikami Excela. Przekazując ścieżkę wejściową, informujesz aplikację, z którym plikiem ma pracować.
## Krok 3: Utwórz PdfSaveOptions
 Teraz nadszedł czas na utworzenie instancji`PdfSaveOptions`Ta klasa umożliwia określenie różnych opcji zapisywania skoroszytu w formacie PDF, w tym czasu utworzenia.
```csharp
PdfSaveOptions options = new PdfSaveOptions(); // Utwórz instancję PdfSaveOptions
options.CreatedTime = DateTime.Now; // Ustaw czas utworzenia na teraz
```
 Poprzez ustawienie`options.CreatedTime` Do`DateTime.Now`, masz pewność, że plik PDF będzie zawierał aktualną datę i godzinę utworzenia.
## Krok 4: Zapisz skoroszyt jako plik PDF
Na koniec zapiszesz skoroszyt jako plik PDF, korzystając z właśnie zdefiniowanych opcji.
```csharp
workbook.Save(dataDir + "output.pdf", options); //Zapisz jako PDF
```
 Ta linia kodu pobiera skoroszyt i zapisuje go w formacie PDF w określonej lokalizacji.`options` Przekazywany jest parametr, który pozwala uwzględnić czas utworzenia w metadanych PDF.

## Wniosek
I masz! Udało Ci się przekonwertować plik Excela na PDF przy użyciu Aspose.Cells dla .NET, wraz z sygnaturą czasową utworzenia. Ta funkcja może być niezwykle przydatna, gdy musisz śledzić wersje dokumentu lub gdy chcesz przekazać odbiorcom informacje o tym, kiedy dokument został utworzony.
 Jeśli chcesz poznać więcej funkcji Aspose.Cells, nie wahaj się sprawdzić[dokumentacja](https://reference.aspose.com/cells/net/).
## Najczęściej zadawane pytania
### Czym jest Aspose.Cells?
Aspose.Cells to zaawansowana biblioteka dla platformy .NET umożliwiająca programistom tworzenie, edytowanie i konwertowanie plików Excel.
### Czy mogę używać Aspose.Cells za darmo?
 Tak, możesz zacząć od bezpłatnego okresu próbnego dostępnego na stronie[Strona internetowa Aspose](https://releases.aspose.com/).
### Jak ustawić inne właściwości pliku PDF?
 Możesz ustawić różne właściwości PDF za pomocą`PdfSaveOptions` klasy, takie jak rozmiar strony, kompresja i inne.
### Czy można konwertować wiele plików Excela jednocześnie?
Tak, możesz przejrzeć listę plików i zastosować ten sam proces konwersji do każdego z nich.
### Gdzie mogę uzyskać pomoc dotyczącą Aspose.Cells?
 Możesz uzyskać wsparcie od społeczności Aspose na ich stronie[forum wsparcia](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
