---
category: general
date: 2026-03-30
description: Jak skopiować arkusz w C# przy użyciu Aspose.Cells – krok po kroku przewodnik
  obejmujący kopiowanie zakresu komórek, kopiowanie kolumn między arkuszami, kopiowanie
  tabeli przestawnej arkusza oraz dodawanie kodu nowego arkusza.
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: pl
og_description: Dowiedz się, jak kopiować arkusz w C# przy użyciu Aspose.Cells. Ten
  przewodnik pokazuje, jak kopiować zakres komórek, zachować tabele przestawne, kopiować
  kolumny między arkuszami oraz dodać kod nowego arkusza.
og_title: Jak skopiować arkusz w C# – Pełny samouczek Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Jak skopiować arkusz w C# przy użyciu Aspose.Cells – kompletny przewodnik
url: /pl/net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak skopiować arkusz w C# przy użyciu Aspose.Cells – Kompletny przewodnik

Zastanawiałeś się kiedyś **how to copy worksheet** w C# bez utraty żadnej tabeli przestawnej ani formuły? Nie jesteś sam — wielu programistów napotyka problem, gdy muszą zduplikować arkusz, zachowując wszystkie elementy w niezmienionej formie. W tym samouczku przeprowadzimy Cię przez praktyczne, kompleksowe rozwiązanie, które nie tylko kopiuje dane, ale także zachowuje **copy worksheet pivot table**, obsługuje **copy cell range** i pokazuje **add new worksheet code**, którego będziesz potrzebował.

Omówimy wszystko, od wczytania źródłowego skoroszytu po zapisanie pliku docelowego, abyś mógł **copy columns between sheets**, zachować obiekty i utrzymać kod w czystości. Bez niejasnych odniesień, tylko kompletny, gotowy do uruchomienia przykład, który możesz od razu wkleić do swojego projektu.

## Co obejmuje ten samouczek

- Ładowanie istniejącego pliku Excel przy użyciu Aspose.Cells  
- Użycie **add new worksheet code** do utworzenia arkusza docelowego  
- Definiowanie **copy cell range**, które zawiera tabelę przestawną  
- Konfigurowanie **CopyOptions**, aby zachować wykresy, formuły i tabele przestawne w niezmienionej formie  
- Wykonywanie **copy columns between sheets** z precyzją wiersz po wierszu  
- Zapis wyniku i weryfikacja, że arkusz został skopiowany poprawnie  

Po zakończeniu tego przewodnika będziesz w stanie pewnie odpowiedzieć na pytanie „how to copy worksheet”, niezależnie od tego, czy automatyzujesz raporty, czy tworzysz interfejs oparty na arkuszach kalkulacyjnych.

## Jak skopiować arkusz – przegląd

Zanim przejdziemy do kodu, przedstawmy ogólny przebieg. Pomyśl o tym jak o przepisie:

1. **Load** źródłowy skoroszyt (`Source.xlsx`).  
2. **Add** nowy arkusz, w którym umieścisz kopię (`add new worksheet code`).  
3. **Define** obszar, który chcesz zduplikować (`copy cell range`).  
4. **Configure** opcje kopiowania, aby tabela przestawna przetrwała (`copy worksheet pivot table`).  
5. **Copy** wiersze i kolumny (`copy columns between sheets`).  
6. **Save** nowy skoroszyt (`Destination.xlsx`).  

To wszystko — sześć kroków, bez magii. Każdy krok jest wyjaśniony poniżej wraz z fragmentami kodu i uzasadnieniem.

## Krok 1 – Ładowanie źródłowego skoroszytu

Na początek: potrzebujesz instancji `Workbook`, wskazującej na plik, który chcesz zduplikować. Ten krok jest niezbędny, ponieważ Aspose.Cells działa bezpośrednio na systemie plików, a nie w interfejsie Office.

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*Dlaczego to ważne:* Ładowanie pliku tworzy w pamięci reprezentację każdego arkusza, komórki i obiektu. Bez tego nie ma nic do skopiowania, a każda próba użycia `add new worksheet code` później zakończy się niepowodzeniem, ponieważ dane źródłowe nie istnieją.

## Krok 2 – Dodanie nowego arkusza (add new worksheet code)

Teraz potrzebujemy miejsca, aby wkleić skopiowane dane. To właśnie **add new worksheet code** błyszczy. Możesz nazwać arkusz dowolnie; tutaj nazywamy go `"Copy"`.

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*Wskazówka:* Jeśli planujesz kopiować wiele arkuszy, wywołaj `Worksheets.Add` w pętli i nadaj każdemu arkuszowi unikalną nazwę. Dzięki temu unikniesz kolizji nazw i utrzymasz porządek w skoroszycie.

## Krok 3 – Definiowanie zakresu kopiowania komórek

**copy cell range** informuje Aspose.Cells dokładnie, które wiersze i kolumny należy zduplikować. W wielu rzeczywistych scenariuszach zakres zawiera tabelę przestawną, więc musimy być precyzyjni.

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*Dlaczego tego potrzebujemy:* Określając zakres explicite, unikamy kopiowania całego arkusza (co może być nieefektywne) i zapewniamy, że tabela przestawna znajduje się w skopiowanym obszarze. To jest sedno **how to copy worksheet**, gdy potrzebujesz tylko części arkusza.

## Krok 4 – Ustawienie opcji kopiowania (zachowanie copy worksheet pivot table)

Aspose.Cells udostępnia obiekt `CopyOptions`, który kontroluje, co zostaje wklejone. Aby zachować tabelę przestawną, wykresy i formuły, ustawiamy `PasteType.All` i włączamy `PasteSpecial`.

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*Wyjaśnienie:* `PasteType.All` jest najbardziej inkluzywną opcją, natomiast `PasteSpecial` instruuje silnik, aby prawidłowo obsługiwał złożone obiekty — takie jak tabele przestawne. Pominięcie tego kroku jest częstym pułapką; skopiowany arkusz straciłby interaktywne funkcje.

## Krok 5 – Kopiowanie wierszy i kolumn (copy columns between sheets)

Teraz następuje najcięższa część: faktyczne przenoszenie danych. Użyjemy `CopyRows` i `CopyColumns`, aby obsłużyć **copy columns between sheets**. Wykonanie obu zapewnia zachowanie scalonych komórek i szerokości kolumn.

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*Co się dzieje:* `CopyRows` przenosi dane wiersz po wierszu, natomiast `CopyColumns` robi to samo kolumna po kolumnie. Uruchomienie obu gwarantuje, że cały prostokątny blok zostanie zduplikowany, co jest niezbędne, gdy musisz **copy columns between sheets**, które mają różne szerokości kolumn lub ukryte kolumny.

## Krok 6 – Zapis skoroszytu

Na koniec zapisz zmiany na dysku. Ten krok finalizuje proces **how to copy worksheet**.

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*Wskazówka weryfikacyjna:* Otwórz `Destination.xlsx` i sprawdź, czy arkusz `"Copy"` wygląda identycznie jak oryginał, tabele przestawne działają, a szerokości kolumn się zgadzają. Jeśli coś jest nie tak, sprawdź ponownie ustawienia `CopyOptions`.

## Przypadki brzegowe i typowe wariacje

### Kopiowanie wielu arkuszy

Jeśli musisz zduplikować kilka arkuszy, otocz powyższą logikę pętlą `foreach`:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### Zachowanie formuł w różnych skoroszytach

Gdy źródłowy i docelowy skoroszyt mają różne nazwy zakresów, ustaw `copyOptions` na `PasteType.Formulas` oprócz `All`:

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### Duże zakresy i wydajność

Dla ogromnych zestawów danych (setki tysięcy wierszy) rozważ użycie wyłącznie `CopyRows` i pominięcie `CopyColumns`, jeśli szerokości kolumn nie są krytyczne. To może zaoszczędzić kilka sekund.

## Pełny działający przykład

Poniżej znajduje się kompletny, gotowy do uruchomienia program, który zawiera wszystko, o czym rozmawialiśmy. Wklej go do aplikacji konsolowej, dostosuj ścieżki plików i naciśnij **F5**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**Oczekiwany rezultat:** Otworzenie `Destination.xlsx` pokazuje arkusz o nazwie **Copy**, który odzwierciedla pierwszy arkusz `Source.xlsx` — włącznie z tabelami przestawnymi, formatowaniem i szerokościami kolumn. Oryginalny plik pozostaje niezmieniony.

## Najczęściej zadawane pytania

**Q: Czy to działa z plikami .xlsx utworzonymi w Excel 2019?**  
A: Zdecydowanie tak. Aspose.Cells obsługuje wszystkie współczesne formaty Excel, więc ten sam kod działa dla plików `.xlsx`, `.xlsm`, a nawet starszych `.xls`.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}