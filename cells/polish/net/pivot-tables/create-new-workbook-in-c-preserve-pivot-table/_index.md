---
category: general
date: 2026-02-15
description: Utwórz nowy skoroszyt w C# i skopiuj tabelę przestawną, nie tracąc jej
  definicji. Dowiedz się, jak kopiować wiersze, zachować tabelę przestawną i łatwo
  duplikować tabelę przestawną.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- duplicate pivot table
language: pl
og_description: Utwórz nowy skoroszyt w C# i skopiuj tabelę przestawną, zachowując
  jej definicję. Przewodnik krok po kroku dla programistów.
og_title: Utwórz nowy skoroszyt w C# – zachowaj tabelę przestawną
tags:
- Aspose.Cells
- C#
- Excel automation
title: Utwórz nowy skoroszyt w C# – zachowaj tabelę przestawną
url: /pl/net/pivot-tables/create-new-workbook-in-c-preserve-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz nowy skoroszyt w C# – Zachowaj tabelę przestawną

Czy kiedykolwiek potrzebowałeś **create new workbook** w C#, który zawiera dokładną kopię tabeli przestawnej z innego pliku? Nie jesteś jedyny. W wielu procesach raportowania tabela przestawna jest sercem analizy, a utrata jej definicji przy przenoszeniu danych to koszmar.

Dobre wieści? Kilka linii kodu Aspose.Cells pozwala skopiować wiersze — w tym tabelę przestawną — do nowego skoroszytu i zachować wszystko w nienaruszonym stanie. Poniżej zobaczysz **how to copy rows**, **preserve pivot table** settings oraz nawet **duplicate pivot table** w różnych plikach bez łamania formuł czy pamięci podręcznej.

## Co obejmuje ten samouczek

1. Ładowanie skoroszytu źródłowego, który już zawiera tabelę przestawną.  
2. **Create new workbook** obiekty dla docelowego.  
3. Użycie `CopyRows` do przeniesienia zakresu zawierającego tabelę przestawną.  
4. Zapisanie wyniku przy zapewnieniu, że tabela przestawna pozostaje funkcjonalna.  

Nie wymagana jest zewnętrzna dokumentacja — tylko kod, wyjaśnienie oraz kilka praktycznych wskazówek, które możesz wkleić bezpośrednio do swojego projektu.

> **Pro tip:** Aspose.Cells działa z .NET Core, .NET Framework oraz nawet Xamarin, więc ten sam fragment kodu działa wszędzie tam, gdzie go potrzebujesz.

![Utwórz nowy skoroszyt z skopiowaną tabelą przestawną](/images/create-new-workbook-pivot.png "utwórz nowy skoroszyt z skopiowaną tabelą przestawną")

## Krok 1 – Utwórz nowy skoroszyt i załaduj plik źródłowy

Pierwszą rzeczą, którą robimy, jest **create new workbook** obiekty. Jeden przechowuje oryginalne dane, drugi otrzyma skopiowany zakres.

```csharp
using Aspose.Cells;

// Load the source workbook that already contains a pivot table
var sourceWorkbook = new Workbook(@"C:\Data\source.xlsx");

// Create an empty workbook that will become the destination
var destinationWorkbook = new Workbook();
```

*Dlaczego to ważne:*  
`Workbook` jest punktem wejścia do wszelkiej manipulacji plikami Excel w Aspose.Cells. Tworząc nowy skoroszyt, zapewniamy czystą kartę — bez ukrytych stylów czy niepotrzebnych arkuszy, które mogłyby później zakłócić działanie.

## Krok 2 – Jak skopiować wiersze, w tym tabelę przestawną

Teraz przechodzi do sedna problemu: **how to copy rows**, które obejmują tabelę przestawną bez jej spłaszczania. Metoda `CopyRows` robi dokładnie to.

```csharp
// Copy the first 20 rows (adjust as needed) from the source to the destination
// Parameters: startRow, totalRows, targetCells, targetStartRow
sourceWorkbook.Worksheets[0].Cells.CopyRows(
    startRow: 0,
    totalRows: 20,
    targetCells: destinationWorkbook.Worksheets[0].Cells,
    targetStartRow: 0);
```

Kilka rzeczy do zauważenia:

* `startRow` i `totalRows` definiują blok zawierający tabelę przestawną.  
* Metoda kopiuje **zarówno** surowe dane, jak i pamięć podręczną tabeli przestawnej, więc skoroszyt docelowy wie, jak odtworzyć tabelę przestawną w locie.  
* Jeśli twoja tabela przestawna zaczyna się głębiej w arkuszu, po prostu zmień indeksy — nie potrzebujesz innego wywołania API.

> **Common question:** *Czy skopiowana tabela przestawna straci odniesienie do źródłowych danych?*  
> Nie. Aspose.Cells osadza pamięć podręczną bezpośrednio w arkuszu, więc tabela przestawna staje się samodzielna w nowym pliku.

## Krok 3 – Zachowaj tabelę przestawną przy zapisywaniu docelowego

Po skopiowaniu wierszy tabela przestawna znajduje się w skoroszycie docelowym dokładnie tak, jak w źródłowym. Zapisanie pliku jest proste.

```csharp
// Save the destination workbook; the pivot table remains functional
destinationWorkbook.Save(@"C:\Data\destination.xlsx");
```

Gdy otworzysz `destination.xlsx` w Excelu, zobaczysz tabelę przestawną gotową do odświeżenia. Zachowanie **preserve pivot table** jest automatyczne, ponieważ pamięć podręczna przeszła wraz z wierszami.

### Weryfikacja wyniku

Otwórz plik i:

1. Kliknij tabelę przestawną.  
2. Zauważ, że pojawia się lista pól — to oznacza, że pamięć podręczna jest nienaruszona.  
3. Spróbuj odświeżyć; dane aktualizują się bez błędów.

Jeśli napotkasz błąd *#REF!*, sprawdź ponownie, czy skopiowany zakres obejmuje ukryte wiersze pamięci podręcznej (zazwyczaj tuż po widocznych danych).

## Krok 4 – Duplikuj tabelę przestawną do wielu skoroszytów (Opcjonalnie)

Czasami potrzebujesz tej samej tabeli przestawnej w kilku raportach. Wzorzec, którego właśnie użyliśmy, skaluje się dobrze — po prostu powtórz kopiowanie dla każdego nowego skoroszytu.

```csharp
string[] targets = {
    @"C:\Reports\Q1.xlsx",
    @"C:\Reports\Q2.xlsx",
    @"C:\Reports\Q3.xlsx"
};

foreach (var path in targets)
{
    var wb = new Workbook(); // fresh workbook each loop
    sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 20, wb.Worksheets[0].Cells, 0);
    wb.Save(path);
}
```

Ten fragment **duplicates pivot table** trzy razy w jednej pętli. Dostosuj tablicę `targets` do swojego harmonogramu raportowania.

### Przypadki brzegowe, o których należy pamiętać

| Sytuacja | Na co zwrócić uwagę | Rozwiązanie |
|-----------|-------------------|-----|
| Tabela przestawna używa zewnętrznego źródła danych | Pamięć podręczna może odwoływać się do połączenia, które nie istnieje na nowym komputerze | Osadź źródło danych lub odtwórz połączenie w skoroszycie docelowym |
| Bardzo duża tabela przestawna ( > 100 tys. wierszy ) | `CopyRows` może być intensywny pod względem pamięci | Użyj `CopyRows` w partiach lub rozważ `Copy` z `PasteOptions`, aby ograniczyć zużycie pamięci |
| Arkusz ma ukryte wiersze/kolumny | Ukryte wiersze pamięci podręcznej mogą zostać pominięte, jeśli kopiujesz tylko widoczne wiersze | Zawsze kopiuj dokładny zakres wierszy zawierający pamięć podręczną, a nie tylko widoczny obszar |

## Pełny działający przykład

Łącząc wszystko razem, oto samodzielny program, który możesz wkleić do aplikacji konsolowej.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook (contains the original pivot)
            var sourcePath = @"C:\Data\source.xlsx";
            var sourceWorkbook = new Workbook(sourcePath);

            // 2️⃣ Prepare destination workbook
            var destinationWorkbook = new Workbook();

            // 3️⃣ Copy rows that include the pivot (adjust range as needed)
            sourceWorkbook.Worksheets[0].Cells.CopyRows(
                startRow: 0,
                totalRows: 20,
                targetCells: destinationWorkbook.Worksheets[0].Cells,
                targetStartRow: 0);

            // 4️⃣ Save – the pivot table is preserved
            var destPath = @"C:\Data\destination.xlsx";
            destinationWorkbook.Save(destPath);

            Console.WriteLine("Pivot table successfully copied!");
        }
    }
}
```

Uruchom program, otwórz `destination.xlsx`, a zobaczysz tę samą tabelę przestawną gotową do analizowania danych. Nie wymaga ręcznego odtwarzania.

## Podsumowanie

Właśnie pokazaliśmy, jak **create new workbook** w C# i **copy pivot table**, zachowując wszystkie ustawienia. Korzystając z `CopyRows`, otrzymujesz niezawodny sposób na **preserve pivot table** funkcjonalność, odpowiadając na odwieczne pytanie „**how to copy rows**”, a także **duplicate pivot table** w wielu raportach przy minimalnym kodzie.

Kolejne kroki? Spróbuj zmienić kopiowany zakres, aby obejmował wykresy odwołujące się do tej samej tabeli przestawnej, lub poeksperymentuj z `PasteOptions`, aby dokładnie zachować formatowanie. Ten sam wzorzec działa dla innych obiektów Aspose.Cells, takich jak tabele i nazwy zakresów, więc możesz go swobodnie rozbudować.

Masz problem, z którym się mierzysz — może tabela przestawna pobierająca dane z zewnętrznej bazy, albo skoroszyt w chmurze? Dodaj komentarz poniżej, a rozwiążemy go razem. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}