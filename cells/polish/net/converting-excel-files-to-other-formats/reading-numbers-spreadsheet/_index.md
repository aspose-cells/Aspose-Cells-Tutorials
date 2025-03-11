---
title: Odczyt arkusza kalkulacyjnego liczb programowo w .NET
linktitle: Odczyt arkusza kalkulacyjnego liczb programowo w .NET
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: W tym szczegółowym samouczku dowiesz się, jak odczytywać arkusze kalkulacyjne Numbers i konwertować je do formatu PDF za pomocą Aspose.Cells dla .NET.
weight: 18
url: /pl/net/converting-excel-files-to-other-formats/reading-numbers-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Odczyt arkusza kalkulacyjnego liczb programowo w .NET

## Wstęp
W dzisiejszym cyfrowym świecie zarządzanie danymi jest kluczową umiejętnością, a arkusze kalkulacyjne są na czele organizacji danych. Ale co, jeśli musisz pracować z arkuszem kalkulacyjnym Numbers — plikami utworzonymi przez aplikację Numbers firmy Apple — przy użyciu .NET? Nie martw się; nie jesteś sam! W tym samouczku przeprowadzimy Cię przez proces odczytywania arkusza kalkulacyjnego Numbers programowo za pomocą Aspose.Cells dla .NET. Dowiesz się, jak załadować plik Numbers i przekonwertować go do formatu PDF.
## Wymagania wstępne
Zanim zaczniemy, jest kilka rzeczy, które musisz mieć na miejscu:
1. Aspose.Cells dla .NET: Upewnij się, że masz zainstalowaną bibliotekę Aspose.Cells. Możesz ją pobrać[Tutaj](https://releases.aspose.com/cells/net/).
2. Visual Studio: Zaleca się, aby na komputerze było zainstalowane środowisko Visual Studio (lub inne środowisko IDE zgodne ze standardem .NET).
3. Podstawowa znajomość języka C#: Niewielka znajomość programowania w języku C# pomoże Ci płynnie nadążać za nauką.
4. Katalog dokumentów: Będziesz potrzebować katalogu, w którym przechowywany jest plik Numbers, a także miejsca, w którym zostanie zapisany przekonwertowany plik PDF.
Gdy już spełnisz te wymagania wstępne, będziesz gotowy do rozpoczęcia!
## Importuj pakiety
Na początek musimy zaimportować niezbędne pakiety do naszego projektu C#. Jest to kluczowy krok, ponieważ pozwala nam wykorzystać funkcjonalności dostarczane przez bibliotekę Aspose.Cells.
1. Otwórz projekt C# w programie Visual Studio.
2. Dodaj odwołanie do biblioteki Aspose.Cells:
   - Jeśli używasz NuGet, po prostu uruchom następujące polecenie w konsoli Menedżera pakietów:
```
 Install-Package Aspose.Cells
 ```
3. Zaimportuj niezbędne przestrzenie nazw do swojego kodu:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Teraz, gdy zaimportowaliśmy niezbędne pakiety, możemy przejść do przewodnika krok po kroku, który przedstawia sposób odczytywania arkusza kalkulacyjnego Numbers.
## Krok 1: Określ katalogi źródłowe i wyjściowe
W tym kroku skonfigurujemy katalogi, w których znajduje się plik źródłowy Numbers i w których chcesz zapisać wyjściowy plik PDF.
```csharp
// Katalog źródłowy
string sourceDir = "Your Document Directory"; // Zaktualizuj to do swojego aktualnego katalogu
// Katalog wyjściowy
string outputDir = "Your Document Directory"; // Zaktualizuj to do swojego aktualnego katalogu
```
 Tutaj definiujemy dwie zmienne łańcuchowe,`sourceDir` I`outputDir` , aby określić lokalizacje plików wejściowych i wyjściowych. Upewnij się, że zastąpiłeś`"Your Document Directory"` z rzeczywistymi ścieżkami w Twoim systemie.
## Krok 2: Skonfiguruj opcje ładowania dla formatu liczb
Następnie określimy opcje ładowania do odczytu arkusza kalkulacyjnego Numbers. Ten krok jest niezbędny, ponieważ informuje Aspose, jak interpretować plik Numbers.
```csharp
// Określ opcje ładowania; chcemy załadować arkusz kalkulacyjny Numbers
LoadOptions opts = new LoadOptions(LoadFormat.Numbers);
```
 Tworzymy`LoadOptions` obiekt i określ format jako`LoadFormat.Numbers`Informuje bibliotekę Aspose.Cells, że pracujemy z plikiem Numbers. 
## Krok 3: Załaduj arkusz kalkulacyjny z liczbami do skoroszytu
Teraz czas załadować arkusz kalkulacyjny Numbers do`Workbook` obiekt.
```csharp
// Załaduj arkusz kalkulacyjny Numbers do skoroszytu, korzystając z powyższych opcji ładowania
Workbook wb = new Workbook(sourceDir + "sampleNumbersByAppleInc.numbers", opts);
```
 Tworzymy instancję`Workbook` obiekt i przekaż ścieżkę pliku Numbers wraz z naszymi opcjami ładowania. Upewnij się, że nazwa pliku (`sampleNumbersByAppleInc.numbers`) odpowiada rzeczywistej nazwie pliku Numbers.
## Krok 4: Zapisz skoroszyt jako plik PDF
Po pomyślnym załadowaniu pliku Numbers następnym krokiem jest zapisanie go w innym formacie, konkretnie PDF.
```csharp
// Zapisz skoroszyt w formacie PDF
wb.Save(outputDir + "outputNumbersByAppleInc.pdf", SaveFormat.Pdf);
```
 Tutaj nazywamy`Save` metoda na`Workbook` obiekt, określając ścieżkę do pliku wyjściowego i format, w jakim chcemy go zapisać. W tym przypadku zapisujemy go jako PDF. Upewnij się, że nazwa pliku wyjściowego (`outputNumbersByAppleInc.pdf`) jest unikalny i nie nadpisuje żadnych istniejących plików.
## Krok 5: Potwierdź powodzenie
Na koniec dodajmy komunikat potwierdzający, że nasza operacja zakończyła się powodzeniem.
```csharp
Console.WriteLine("ReadNumbersSpreadsheet executed successfully.\r\n");
```
Ta linijka kodu wydrukuje komunikat o powodzeniu na konsoli, gdy wszystko zostanie wykonane. Zawsze miło jest otrzymać informację zwrotną, prawda?
## Wniosek
I masz to! Udało Ci się odczytać arkusz kalkulacyjny Numbers i przekonwertować go do formatu PDF za pomocą Aspose.Cells dla .NET. Ta potężna biblioteka pozwala na bezproblemowe manipulowanie arkuszami kalkulacyjnymi, dzięki czemu zadania związane z zarządzaniem danymi stają się proste. Niezależnie od tego, czy tworzysz aplikacje, czy po prostu potrzebujesz wydajniej obsługiwać arkusze kalkulacyjne, Aspose.Cells to fantastyczne narzędzie, które warto mieć w swoim zestawie narzędzi.
## Najczęściej zadawane pytania
### Jakie typy plików może odczytać Aspose.Cells?  
Aspose.Cells potrafi odczytywać różnorodne formaty plików, w tym XLS, XLSX, CSV i pliki Numbers. 
### Czy mogę edytować pliki Numbers za pomocą Aspose.Cells?  
Tak, możesz odczytywać, edytować i zapisywać pliki Numbers za pomocą Aspose.Cells.
### Czy korzystanie z Aspose.Cells jest bezpłatne?  
 Aspose.Cells oferuje bezpłatną wersję próbną, ale do dłuższego użytkowania potrzebna będzie licencja. Sprawdź ceny[Tutaj](https://purchase.aspose.com/buy).
### Co zrobić, jeśli podczas ładowania pliku Numbers wystąpi błąd?  
 Upewnij się, że używasz prawidłowych opcji ładowania i że ścieżka pliku jest prawidłowa. Aby uzyskać więcej pomocy, odwiedź stronę[Forum wsparcia Aspose](https://forum.aspose.com/c/cells/9).
### Jak mogę uzyskać tymczasową licencję na Aspose.Cells?  
 Możesz złożyć wniosek o tymczasową licencję[Tutaj](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
