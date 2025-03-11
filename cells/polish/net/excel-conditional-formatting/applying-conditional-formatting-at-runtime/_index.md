---
title: Stosowanie formatowania warunkowego w czasie wykonywania w programie Excel
linktitle: Stosowanie formatowania warunkowego w czasie wykonywania w programie Excel
second_title: Aspose.Cells .NET API przetwarzania programu Excel
description: Dowiedz się, jak stosować formatowanie warunkowe w czasie wykonywania w programie Excel za pomocą Aspose.Cells dla platformy .NET, korzystając z tego kompleksowego przewodnika krok po kroku.
weight: 11
url: /pl/net/excel-conditional-formatting/applying-conditional-formatting-at-runtime/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Stosowanie formatowania warunkowego w czasie wykonywania w programie Excel

## Wstęp

są to potężne narzędzia do analizy i wizualizacji danych. Jedną z wyróżniających się funkcji programu Excel jest formatowanie warunkowe, które pozwala użytkownikom stosować określone style formatowania do komórek na podstawie ich wartości. Może to ułatwić identyfikację trendów, wyróżnianie ważnych punktów danych lub po prostu uczynić dane bardziej czytelnymi. Jeśli chcesz programowo zaimplementować formatowanie warunkowe w plikach programu Excel, jesteś we właściwym miejscu! W tym przewodniku pokażemy, jak stosować formatowanie warunkowe w czasie wykonywania przy użyciu Aspose.Cells dla .NET.

## Wymagania wstępne
Zanim zagłębisz się w kod, upewnijmy się, że masz wszystko, czego potrzebujesz, aby zacząć:

1. Visual Studio: Upewnij się, że masz zainstalowany program Visual Studio na swoim komputerze. Możesz użyć dowolnej wersji, która obsługuje rozwój .NET.
2.  Aspose.Cells dla .NET: Musisz mieć zainstalowany Aspose.Cells dla .NET. Możesz go pobrać ze strony[Strona internetowa Aspose](https://releases.aspose.com/cells/net/).
3. Podstawowa wiedza o języku C#: Znajomość programowania w języku C# pomoże Ci lepiej zrozumieć fragmenty kodu.
4. .NET Framework: Upewnij się, że Twój projekt jest ukierunkowany na zgodną wersję .NET Framework.

Teraz, gdy omówiliśmy już wszystkie wymagania wstępne, możemy przejść do najfajniejszej części!

## Importuj pakiety
Aby rozpocząć pracę z Aspose.Cells, musisz zaimportować niezbędne przestrzenie nazw do swojego projektu C#. Oto, jak możesz to zrobić:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Te przestrzenie nazw dadzą ci dostęp do klas i metod wymaganych do manipulowania plikami Excela i stosowania formatowania warunkowego.

Teraz podzielimy proces stosowania formatowania warunkowego na łatwiejsze do wykonania kroki.

## Krok 1: Skonfiguruj swój projekt
Po pierwsze, musisz utworzyć nowy projekt C# w Visual Studio. Oto jak to zrobić:

1. Otwórz program Visual Studio i wybierz polecenie Plik > Nowy > Projekt.
2. Wybierz aplikację konsolową (.NET Framework) i nadaj nazwę swojemu projektowi.
3. Kliknij Utwórz.

## Krok 2: Dodaj odniesienie Aspose.Cells
Po skonfigurowaniu projektu należy dodać odwołanie do biblioteki Aspose.Cells:

1. Kliknij prawym przyciskiem myszy swój projekt w Eksploratorze rozwiązań.
2. Wybierz opcję Zarządzaj pakietami NuGet.
3. Wyszukaj Aspose.Cells i zainstaluj.

Umożliwi to wykorzystanie wszystkich funkcji udostępnianych przez bibliotekę Aspose.Cells.

## Krok 3: Utwórz obiekt skoroszytu
Następnie utwórzmy nowy skoroszyt i arkusz kalkulacyjny. To tutaj dzieje się cała magia:

```csharp
// Ścieżka do katalogu dokumentów.
string dataDir = "Your Document Directory";
string filePath = dataDir + "Book1.xlsx";

// Tworzenie instancji obiektu skoroszytu
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

W tym kroku zdefiniujemy katalog, w którym zostanie zapisany plik programu Excel, utworzymy nowy skoroszyt i uzyskamy dostęp do pierwszego arkusza kalkulacyjnego.

## Krok 4: Dodaj formatowanie warunkowe
Teraz dodajmy trochę formatowania warunkowego. Zaczniemy od utworzenia pustego obiektu formatowania warunkowego:

```csharp
// Dodaje puste formatowanie warunkowe
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```

Tutaj dodajemy do naszego arkusza kalkulacyjnego nowy zbiór formatowania warunkowego, który będzie zawierał nasze reguły formatowania.

## Krok 5: Zdefiniuj zakres formatu
Następnie musimy określić zakres komórek, do których będzie stosowane formatowanie warunkowe. Powiedzmy, że chcemy sformatować pierwszy wiersz i drugą kolumnę:

```csharp
// Ustawia zakres formatu warunkowego.
CellArea ca = new CellArea();
ca.StartRow =0;
ca.EndRow =0;
ca.StartColumn =0;
ca.EndColumn =0;
fcs.AddArea(ca);

ca = new CellArea();
ca.StartRow =1;
ca.EndRow =1;
ca.StartColumn =1;
ca.EndColumn =1;
fcs.AddArea(ca);
```

W tym kodzie definiujemy dwa obszary dla formatowania warunkowego. Pierwszy obszar jest dla komórki w (0,0), a drugi dla (1,1). Możesz swobodnie dostosować te zakresy w zależności od swoich konkretnych potrzeb!

## Krok 6: Dodaj warunki formatowania warunkowego
Teraz czas zdefiniować warunki naszego formatowania. Powiedzmy, że chcemy wyróżnić komórki na podstawie ich wartości:

```csharp
// Dodaje warunek.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "=A2", "100");

// Dodaje warunek.
int conditionIndex2 = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```

 W tym kroku dodajemy dwa warunki: jeden dla wartości pomiędzy`A2` I`100` i inny dla wartości pomiędzy`50` I`100`. Pozwala to na dynamiczne wyróżnianie komórek na podstawie ich wartości.

## Krok 7: Ustaw style formatowania
Mając nasze warunki, możemy teraz ustawić style formatowania. Zmieńmy kolor tła dla naszych warunków:

```csharp
// Ustawia kolor tła.
FormatCondition fc = fcs[conditionIndex];
fc.Style.BackgroundColor = Color.Red;
```

Tutaj ustawiamy kolor tła pierwszego warunku na czerwony. Możesz go dalej dostosować, zmieniając kolor czcionki, obramowania i inne style według potrzeb!

## Krok 8: Zapisz plik Excel
Na koniec, czas zapisać naszą pracę! Zapiszemy skoroszyt w określonym katalogu:

```csharp
// Zapisywanie pliku Excel
workbook.Save(dataDir + "output.xls");
```

Ta linia kodu zapisuje plik Excela z zastosowanym formatowaniem warunkowym. Upewnij się, że sprawdziłeś określony katalog dla swojego pliku wyjściowego!

## Wniosek
masz to! Udało Ci się zastosować formatowanie warunkowe w czasie wykonywania w programie Excel przy użyciu Aspose.Cells dla .NET. Ta potężna biblioteka ułatwia programowe manipulowanie plikami programu Excel, umożliwiając automatyzację żmudnych zadań i ulepszanie prezentacji danych. Niezależnie od tego, czy pracujesz nad małym projektem, czy aplikacją na dużą skalę, Aspose.Cells może pomóc Ci usprawnić przepływ pracy i zwiększyć produktywność.

## Najczęściej zadawane pytania

### Czym jest Aspose.Cells?
Aspose.Cells to biblioteka .NET umożliwiająca programistom programowe tworzenie, edytowanie i konwertowanie plików Excel.

### Czy mogę używać Aspose.Cells z innymi językami programowania?
Tak, Aspose.Cells jest dostępny dla wielu języków programowania, w tym Java, Python i innych.

### Czy jest dostępna bezpłatna wersja próbna Aspose.Cells?
 Tak, możesz pobrać bezpłatną wersję próbną ze strony[Strona internetowa Aspose](https://releases.aspose.com/).

### Gdzie mogę uzyskać pomoc techniczną dotyczącą Aspose.Cells?
 Możesz uzyskać pomoc odwiedzając stronę[Forum wsparcia Aspose](https://forum.aspose.com/c/cells/9).

### Czy potrzebuję licencji, aby korzystać z Aspose.Cells?
 Tak, licencja jest wymagana do użytku komercyjnego, ale możesz poprosić o licencję tymczasową[Tutaj](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
