---
title: Arkusz kalkulacyjny do kopiowania w programie Excel
linktitle: Arkusz kalkulacyjny do kopiowania w programie Excel
second_title: Aspose.Cells dla .NET API Reference
description: Dowiedz się, jak skopiować arkusz kalkulacyjny programu Excel za pomocą Aspose.Cells dla .NET dzięki temu łatwemu w użyciu przewodnikowi krok po kroku. Idealny dla programistów .NET, którzy chcą zautomatyzować zadania programu Excel.
weight: 20
url: /pl/net/excel-copy-worksheet/excel-copy-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Arkusz kalkulacyjny do kopiowania w programie Excel

## Wstęp

świecie obsługi danych arkusze kalkulacyjne są wszędzie — od zarządzania liczbami sprzedaży po organizowanie danych projektu. Ale jak zarządzać tymi plikami, gdy automatyzacja staje się konieczna? Cóż, jeśli pracujesz w .NET, Aspose.Cells to doskonałe narzędzie do programowego manipulowania plikami Excel. W tym artykule przeprowadzimy Cię przez kopiowanie arkusza kalkulacyjnego w pliku Excel przy użyciu Aspose.Cells dla .NET. Jest to typowe zadanie, gdy musisz zduplikować dane w nowych arkuszach bez zaczynania od zera.

Więc zapnijcie pasy! Zamierzamy zagłębić się w ten proces, ale w sposób prosty, konwersacyjny i jasny.

## Wymagania wstępne

Zanim rozpoczniesz zabawę, upewnijmy się, że masz wszystko, czego potrzebujesz, aby rozpocząć pracę z tym samouczkiem.

### Zainstaluj Aspose.Cells dla .NET
Po pierwsze — jeśli nie masz jeszcze zainstalowanego Aspose.Cells for .NET, musisz go pobrać i zainstalować. Najnowszą wersję możesz pobrać ze strony wydania.

- [Pobierz Aspose.Cells dla .NET](https://releases.aspose.com/cells/net/)

Możesz użyć NuGet w Visual Studio lub pobrać go ręcznie. Jeśli wolisz trasę NuGet, po prostu uruchom to polecenie:

```bash
Install-Package Aspose.Cells
```

### Uzyskaj licencję
Aby w pełni odblokować funkcjonalność Aspose.Cells, najlepiej jest uzyskać licencję.

- [Kup licencję](https://purchase.aspose.com/buy) Lub[Poproś o licencję tymczasową](https://purchase.aspose.com/temporary-license/)

Korzystanie z biblioteki bez licencji spowoduje dodanie znaków wodnych do plików wyjściowych, dlatego upewnij się, że masz przygotowaną licencję!

### Skonfiguruj swoje środowisko programistyczne
Upewnij się, że zainstalowałeś następujące oprogramowanie:
- Visual Studio (lub dowolne środowisko IDE zgodne z .NET)
- .NET Framework czy .NET Core

Gdy wszystko jest już zainstalowane i skonfigurowane, możemy zacząć kodowanie!

## Importuj pakiety

Aby pracować z Aspose.Cells, musisz najpierw zaimportować wymagane przestrzenie nazw w swoim projekcie. Oto fragment kodu, aby upewnić się, że masz poprawne odniesienia:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Teraz, gdy już uporaliśmy się z formalnościami, możemy przejść do właściwej pracy — kopiowania arkusza kalkulacyjnego do skoroszytu programu Excel.

## Krok 1: Zdefiniuj ścieżki katalogów
Pierwszą rzeczą, której potrzebujesz, jest określenie katalogu, w którym znajdują się pliki Excela. Jest to kluczowe dla załadowania pliku do projektu i zapisania zmodyfikowanego skoroszytu.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string InputPath = dataDir + "book1.xls";
```

-  Ten`dataDir` zmienna przechowuje ścieżkę katalogu, w którym znajdują się pliki Excela. Zmień`"YOUR DOCUMENT DIRECTORY"` do rzeczywistej ścieżki folderu.
- `InputPath` przechowuje lokalizację pliku Excel, nad którym będziemy pracować (w tym przypadku „book1.xls”).

Dobrym pomysłem jest korzystanie ze ścieżek dynamicznych, dzięki czemu można łatwo przełączać się między środowiskami (programistycznym, przejściowym, produkcyjnym).

## Krok 2: Otwórz skoroszyt programu Excel
Następnie załadujemy plik Excela korzystając z klasy Workbook, która reprezentuje cały plik Excela.

```csharp
Workbook wb = new Workbook(InputPath);
```

-  Ten`Workbook` obiekt ładuje plik Excel znajdujący się w`InputPath`. Aspose.Cells zajmuje się parsowaniem pliku, więc nie musisz się martwić o złożoność formatu Excela.

## Krok 3: Uzyskaj dostęp do kolekcji arkuszy roboczych
Każdy skoroszyt ma wiele arkuszy (pomyśl o nich jak o kartach w pliku Excel). Aby skopiować arkusz, najpierw musisz mieć dostęp do tych arkuszy.

```csharp
WorksheetCollection sheets = wb.Worksheets;
```

- `WorksheetCollection` jest zasadniczo listą wszystkich arkuszy roboczych w skoroszycie. To jest to, z czym będziemy pracować, aby skopiować nasz arkusz.

## Krok 4: Kopiowanie istniejącego arkusza kalkulacyjnego
Teraz ekscytująca część — duplikowanie arkusza kalkulacyjnego! Tutaj skopiujemy zawartość „Arkusza1” do nowego arkusza.

```csharp
sheets.AddCopy("Sheet1");
```

-  Ten`AddCopy` Metoda duplikuje istniejący arkusz (w tym przypadku „Arkusz1”) i dodaje nowy arkusz do skoroszytu.
-  Możesz zastąpić`"Sheet1"` z dowolną nazwą arkusza, który chcesz skopiować.

## Krok 5: Zapisz skoroszyt
Na koniec, po skopiowaniu arkusza kalkulacyjnego, czas zapisać zaktualizowany plik Excela. Użyjemy metody Save, aby zapisać zmiany w nowym pliku.

```csharp
wb.Save(dataDir + "CopyWithinWorkbook_out.xls");
```

-  Ten`Save` Metoda zapisuje zaktualizowany skoroszyt do nowego pliku (`CopyWithinWorkbook_out.xls` ). Możesz wybrać dowolną nazwę dla pliku wyjściowego, ale pamiętaj, aby zapisać go w odpowiednim formacie (np.`.xls`, `.xlsx`).

To wszystko! Udało Ci się zduplikować arkusz kalkulacyjny w pliku Excel.

## Wniosek

Kopiowanie arkusza kalkulacyjnego w Aspose.Cells dla .NET jest nie tylko proste, ale również bardzo wydajne. Za pomocą zaledwie kilku linijek kodu możesz zautomatyzować powtarzające się zadania programu Excel, co znacznie ułatwi Ci życie w przypadku dużych zestawów danych lub szablonowych raportów. Niezależnie od tego, czy automatyzujesz raporty finansowe, dzienniki inwentaryzacji, czy cokolwiek innego, co wymaga programu Excel, Aspose.Cells jest Twoim rozwiązaniem.

## Najczęściej zadawane pytania

### Czy mogę skopiować wiele arkuszy kalkulacyjnych jednocześnie, używając Aspose.Cells dla .NET?
 Nie, musisz je skopiować jeden po drugim, używając`AddCopy` Metoda. Możesz jednak łatwo przejść przez wiele arkuszy i skopiować je po kolei.

### Czy Aspose.Cells dla .NET obsługuje kopiowanie arkuszy kalkulacyjnych między różnymi skoroszytami?
 Tak, możesz kopiować arkusze kalkulacyjne między różnymi skoroszytami, otwierając oba skoroszyty i używając`AddCopy` metodę między nimi.

### Jakie formaty plików Excel obsługuje Aspose.Cells?
Aspose.Cells obsługuje szeroką gamę formatów Excela, w tym:`.xls`, `.xlsx`, `.csv`, `.html`i wiele więcej.

### Czy potrzebuję licencji, aby używać Aspose.Cells dla .NET?
 Tak, aby uniknąć znaków wodnych i odblokować pełny potencjał biblioteki, potrzebujesz ważnej licencji. Możesz jednak poprosić o[bezpłatna licencja tymczasowa](https://purchase.aspose.com/temporary-license) aby wypróbować przed zakupem.

### Czy mogę uruchomić Aspose.Cells na platformie .NET Core?
Tak, Aspose.Cells jest w pełni kompatybilny z .NET Framework i .NET Core, co czyni go uniwersalnym rozwiązaniem dla aplikacji wieloplatformowych.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
