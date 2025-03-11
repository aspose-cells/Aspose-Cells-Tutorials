---
title: Aktualizuj element formuły Power Query
linktitle: Aktualizuj element formuły Power Query
second_title: Aspose.Cells dla .NET API Reference
description: Łatwa aktualizacja elementów formuły Power Query w programie Excel przy użyciu Aspose.Cells dla .NET. Przewodnik krok po kroku, który usprawni procesy manipulacji danymi.
weight: 160
url: /pl/net/excel-workbook/update-power-query-formula-item/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aktualizuj element formuły Power Query

## Wstęp

Jeśli kiedykolwiek pracowałeś z programem Excel, wiesz, jak potężny może być — szczególnie, gdy zaczynasz zagłębiać się w Power Queries. To sekretny składnik, który pozwala Ci bez wysiłku przekształcać, czyścić i analizować dane. Jednym ze sprytnych sposobów manipulowania formułami Power Query w programie Excel jest Aspose.Cells dla .NET. Dzisiaj poprowadzimy Cię przez aktualizację elementów formuł Power Query krok po kroku. Więc chwyć swój kapelusz kodera i zaczynajmy!

## Wymagania wstępne

Zanim zagłębisz się w kod, jest kilka rzeczy, które powinieneś skonfigurować:

1. Visual Studio: Będziesz potrzebować zintegrowanego środowiska programistycznego (IDE), aby pisać i uruchamiać kod .NET. Visual Studio jest najlepszym wyborem.
2.  Biblioteka Aspose.Cells: Upewnij się, że biblioteka Aspose.Cells jest dostępna w Twoim projekcie. Możesz ją pobrać z[strona](https://releases.aspose.com/cells/net/).
3. Podstawowa znajomość języka C#: Choć przejdziemy przez ten proces wspólnie, z pewnością pomocna okaże się podstawowa znajomość języka C#, zwłaszcza podczas poruszania się po różnych klasach i metodach.
4. Przykładowe pliki Excela: Będziesz potrzebować plików Excela wymienionych we fragmencie kodu. Upewnij się, że masz:
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET Framework: Upewnij się, że Twój projekt jest ukierunkowany na zgodną wersję .NET Framework.

Teraz, gdy mamy już nasz zestaw gotowy, możemy przejść do przyjemniejszej części: pisania kodu!

## Importuj pakiety

Po pierwsze, musisz zaimportować niezbędne przestrzenie nazw. Oto jak to zrobić:

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

Dodając te przestrzenie nazw, dajesz znać kompilatorowi, że zamierzasz używać klas i metod z biblioteki Aspose.Cells. Ten krok jest kluczowy, ponieważ stanowi podstawę dla następującego kodu.

Rozłóżmy na czynniki pierwsze fragment kodu, który nam dostarczyłeś. Ten samouczek przeprowadzi Cię przez każdą część, upewniając się, że rozumiesz, co się dzieje.

## Krok 1: Skonfiguruj katalogi robocze

tym kroku zdefiniujemy, gdzie znajdują się nasze pliki źródłowe i wyjściowe. Dzięki temu Aspose będzie wiedział, gdzie szukać plików Excel.

```csharp
// Katalogi robocze
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## Krok 2: Załaduj skoroszyt

Teraz załadujemy plik Excela, w którym znajduje się Power Query.

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
 Ten`Workbook` class jest punktem wejścia do pliku Excel. Przekazując ścieżkę do naszego pliku źródłowego, tworzymy instancję, która pozwala nam nim manipulować. Możesz to sobie wyobrazić jak otwieranie książki — przygotowujesz się do przeczytania (lub edycji) jej zawartości.

## Krok 3: Uzyskaj dostęp do Data Mashup

Następnie uzyskamy dostęp do formuł Power Query zapisanych w Data Mashup skoroszytu.

```csharp
DataMashup mashupData = workbook.DataMashup;
```
 Ten`DataMashup` Klasa zawiera wszystkie formuły Power Query powiązane z Twoim skoroszytem. To tutaj wykonamy ciężką pracę, podobnie jak otwierasz skrzynkę z narzędziami do naprawy.

## Krok 4: Przejrzyj formuły Power Query

Teraz nadchodzi część, w której przechodzimy przez formuły Power Query, aby znaleźć tę konkretną, którą chcemy zaktualizować.

```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```

-  Przechodzimy przez każdy`PowerQueryFormula` W`mashupData`.
-  ramach tej pętli zagłębiamy się w każdy`PowerQueryFormulaItem`.
- Sprawdzamy, czy nazwa elementu pasuje do „Źródła”. Jeśli tak, aktualizujemy jej wartość, aby połączyć ją z naszym nowym plikiem źródłowym.

Można to porównać do znalezienia właściwej strony w podręczniku, a następnie wprowadzenia niezbędnych aktualizacji — to prosty i skrupulatny proces.

## Krok 5: Zapisz zaktualizowany skoroszyt

Po wprowadzeniu aktualizacji nadszedł czas na zapisanie zmian.

```csharp
// Zapisz skoroszyt wyjściowy.
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
 Ten`Save` Metoda zapisuje zaktualizowany skoroszyt do określonego katalogu wyjściowego. To tak, jakby zapieczętować swoje edycje w nowej wersji podręcznika, gotowej do użycia przez innych!

## Wniosek

Gratulacje! Pomyślnie zaktualizowałeś element formuły Power Query przy użyciu Aspose.Cells dla .NET. Dzięki tej metodzie możesz zautomatyzować modyfikację formuł Power Query w plikach Excel, oszczędzając cenny czas i wysiłek.

## Najczęściej zadawane pytania

### Czym jest Aspose.Cells?
Aspose.Cells to potężna biblioteka umożliwiająca przetwarzanie plików Excel w aplikacjach .NET bez konieczności instalowania programu Microsoft Excel.

### Czy do uruchomienia Aspose.Cells potrzebuję programu Microsoft Excel?
Nie, Aspose.Cells umożliwia programowe tworzenie i edycję plików Excela, bez konieczności instalowania programu Excel na serwerze lub komputerze deweloperskim.

### Z jakimi typami plików Excel mogę pracować, korzystając z Aspose.Cells?
Za pomocą Aspose.Cells można pracować z plikami .xlsx, .xls, .xlsm i wieloma innymi formatami programu Excel.

### Czy jest dostępna wersja próbna Aspose.Cells?
 Tak, możesz pobrać bezpłatną wersję próbną ze strony[Strona wydania Aspose Cells](https://releases.aspose.com/).

### Gdzie mogę uzyskać pomoc techniczną dotyczącą Aspose.Cells?
 Dostęp do pomocy technicznej można uzyskać za pośrednictwem[Forum Aspose](https://forum.aspose.com/c/cells/9), gdzie możesz zadać pytania i znaleźć odpowiedzi od społeczności i zespołu Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
