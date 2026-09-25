---
category: general
date: 2026-03-30
description: Utwórz skoroszyt Excel w C# przy użyciu Aspose.Cells. Naucz się stosować
  funkcję lambda w Excelu, funkcję SEQUENCE w Excelu, funkcję EXPAND w Excelu oraz
  zapisać skoroszyt jako plik xlsx.
draft: false
keywords:
- create excel workbook c#
- lambda function excel
- save workbook as xlsx
- sequence function excel
- expand array excel
language: pl
og_description: Szybko utwórz skoroszyt Excel w C#. Ten przewodnik pokazuje, jak używać
  funkcji lambda w Excelu, funkcji sekwencji w Excelu, rozszerzania tablic w Excelu
  oraz zapisać skoroszyt jako xlsx.
og_title: Tworzenie skoroszytu Excel w C# – Przewodnik po Lambda, SEQUENCE i EXPAND
tags:
- Aspose.Cells
- C#
- Excel automation
title: Tworzenie skoroszytu Excel w C# – Lambda, SEQUENCE i EXPAND – przewodnik
url: /pl/net/formulas-functions/create-excel-workbook-c-lambda-sequence-expand-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz skoroszyt Excel w C# – Lambda, SEQUENCE i EXPAND – Przewodnik

Kiedykolwiek potrzebowałeś **create Excel workbook C#** do automatycznego raportu, ale nie byłeś pewien, które wywołania API użyć? Nie jesteś sam — wielu programistów napotyka ten sam problem, gdy po raz pierwszy zagłębia się w programowe generowanie Excela. W tym przewodniku zobaczysz kompletny, działający przykład, który obejmuje wszystko, od nowej **SEQUENCE function Excel** po potężną **LAMBDA function Excel**, a nawet jak **expand array Excel** zwraca wyniki.  

Pokażemy Ci także dokładne kroki, aby **save workbook as xlsx**, dzięki czemu możesz przekazać plik każdemu, kto używa Excela. Po zakończeniu tego tutorialu będziesz mieć solidny, gotowy do produkcji fragment kodu, który możesz wstawić do dowolnego projektu .NET. Bez niejasnych odnośników „zobacz dokumentację” — po prostu kod, który działa już dziś.

## Czego będziesz potrzebować

- **.NET 6.0 lub nowszy** – przykład jest skierowany do .NET 6, ale każda nowsza wersja zadziała.  
- **Aspose.Cells for .NET** – zainstaluj przez NuGet (`Install-Package Aspose.Cells`).  
- Podstawowa znajomość składni C# (zmienne, obiekty i wyrażenia lambda).  
- IDE, w którym czujesz się komfortowo (Visual Studio, Rider lub VS Code).  

To wszystko. Bez dodatkowego COM interop, bez instalacji Office na serwerze — Aspose.Cells obsługuje wszystko w pamięci.

## Utwórz skoroszyt Excel w C# – Implementacja krok po kroku

Poniżej dzielimy proces na małe, przystępne kroki. Każdy krok ma wyraźny nagłówek, krótki fragment kodu i wyjaśnienie **dlaczego** to robimy. Śmiało skopiuj pełny blok na końcu i uruchom go jako aplikację konsolową.

### Krok 1 – Inicjalizacja nowego skoroszytu

Najpierw potrzebujemy pustego obiektu workbook, który reprezentuje plik Excel w pamięci.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // empty workbook
Worksheet sheet = workbook.Worksheets[0];         // default first sheet
```

*Dlaczego to ważne:* `Workbook` jest punktem wejścia dla wszystkich operacji Aspose.Cells. Pobierając pierwszy `Worksheet`, otrzymujemy płótno, na którym możemy wpisywać formuły, wartości lub formatowanie.  

> **Pro tip:** Jeśli potrzebujesz wielu arkuszy, po prostu wywołaj `workbook.Worksheets.Add()` i zachowaj referencję do każdego z nich.

### Krok 2 – Użycie funkcji SEQUENCE Excel do generowania danych

**sequence function excel** tworzy dynamiczną tablicę liczb bez użycia VBA. Umieścimy ją w komórce `A1` i pozwolimy Excelowi automatycznie rozciągnąć wynik.

```csharp
// Step 2: Generate a 5‑row, 1‑column array from a SEQUENCE
sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)"; // 1..3 padded with blanks
```

*Dlaczego to ważne:* `SEQUENCE(3)` zwraca `[1,2,3]`. Otoczenie jej funkcją `EXPAND` wymusza wynik w zakresie 5‑wierszowym, wypełniając dodatkowe wiersze pustymi wartościami. To jednocześnie pokazuje **sequence function excel** i **expand array excel** w jednej operacji.

### Krok 3 – Agregacja liczb przy użyciu funkcji LAMBDA Excel

Teraz pokażemy możliwości **lambda function excel**. Zsumujemy liczby od 1 do 5, używając nowej funkcji `REDUCE`, która wewnętrznie korzysta z lambdy.

```csharp
// Step 3: Aggregate a sequence (sum 1..5) using REDUCE/LAMBDA
sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))"; // result = 15
```

*Dlaczego to ważne:* `REDUCE` iteruje po tablicy wygenerowanej przez `SEQUENCE(5)`, przekazując każdy element (`b`) do lambdy razem z akumulatorem (`a`). Lambda `a+b` sumuje je, pozostawiając `15` w `B1`. To czysty, wyłącznie formułowy sposób na redukcję bez pętli w C#.

### Krok 4 – Zastosowanie funkcji trygonometrycznych bezpośrednio w komórkach

Wbudowane funkcje matematyczne Excela są przydatne do szybkich obliczeń. Umieścimy cotangens i hiperboliczny cotangens w sąsiadujących komórkach.

```csharp
// Step 4: Trigonometric functions directly in Excel cells
sheet["C1"].Formula = "COT(PI()/4)";   // evaluates to 1
sheet["D1"].Formula = "COTH(1)";      // hyperbolic cotangent of 1
```

*Dlaczego to ważne:* Pokazuje, że możesz mieszać klasyczne funkcje matematyczne z nowszymi formułami dynamicznymi. Nie ma potrzeby obliczać tych wartości w C#, chyba że masz konkretny powód wydajnościowy.

### Krok 5 – Oblicz wszystkie formuły

Aspose.Cells nie ocenia automatycznie formuł po ich ustawieniu. Musisz poprosić go o obliczenie.

```csharp
// Step 5: Force calculation so that cells store the results
workbook.CalculateFormula();
```

*Dlaczego to ważne:* Po tym wywołaniu właściwość `Value` każdej komórki zawiera wyliczony wynik, gotowy do zapisania lub odczytania.

### Krok 6 – Zapisz skoroszyt jako Xlsx

Na koniec zapisujemy skoroszyt na dysku, używając wzorca **save workbook as xlsx**.

```csharp
// Step 6: Save the workbook to an Excel file (XLSX format)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "NewFunctions.xlsx");

workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

*Dlaczego to ważne:* Metoda `Save` automatycznie wykrywa rozszerzenie pliku. Używając „.xlsx”, zapewniamy kompatybilność z nowoczesnymi wersjami Excela. Ścieżka wskazuje na pulpit, co ułatwia dostęp podczas testów.

### Pełny działający przykład

Poniżej znajduje się kompletny program, który możesz wkleić do nowego projektu konsolowego. Zawiera wszystkie powyższe kroki oraz mały blok weryfikacyjny, który wypisuje obliczone wartości w konsoli.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Initialize workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // SEQUENCE + EXPAND
        sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)";

        // REDUCE with LAMBDA
        sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))";

        // Trig functions
        sheet["C1"].Formula = "COT(PI()/4)";
        sheet["D1"].Formula = "COTH(1)";

        // Calculate formulas
        workbook.CalculateFormula();

        // Verify results (optional)
        Console.WriteLine("A1‑A5 (expanded SEQUENCE):");
        for (int i = 0; i < 5; i++)
        {
            Console.WriteLine($"  Row {i + 1}: {sheet.Cells[i, 0].Value ?? "blank"}");
        }
        Console.WriteLine($"B1 (sum 1‑5): {sheet["B1"].Value}");
        Console.WriteLine($"C1 (cot(π/4)): {sheet["C1"].Value}");
        Console.WriteLine($"D1 (coth(1)): {sheet["D1"].Value}");

        // Save workbook
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "NewFunctions.xlsx");
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

**Oczekiwany wynik w konsoli**

```
A1‑A5 (expanded SEQUENCE):
  Row 1: 1
  Row 2: 2
  Row 3: 3
  Row 4: blank
  Row 5: blank
B1 (sum 1‑5): 15
C1 (cot(π/4)): 1
D1 (coth(1)): 1.31303528549933
Workbook saved to: C:\Users\YourName\Desktop\NewFunctions.xlsx
```

A gdy otworzysz *NewFunctions.xlsx*, zobaczysz te same liczby rozmieszczone w pierwszych czterech kolumnach.

![utwórz skoroszyt excel c# zrzut ekranu wynikowego arkusza](/images/create-excel-workbook-csharp.png)

## Przypadki brzegowe, wskazówki i najczęstsze pytania

- **Co zrobić, jeśli potrzebuję więcej niż jednego arkusza?**  
  Po prostu wywołaj `workbook.Worksheets.Add()` i powtórz przypisania formuł na każdym nowym obiekcie `Worksheet`.  

- **Czy mogę używać starszych wersji Excela?**  
  Funkcje dynamicznych tablic (`SEQUENCE`, `EXPAND`, `REDUCE`) wymagają Excel 365 lub Excel 2021+. Jeśli celujesz w starsze wersje, trzymaj się klasycznych formuł lub oblicz wartości w C# przed ich zapisaniem.  

- **Obawy dotyczące wydajności?**  
  Dla tysięcy wierszy ustawianie formuł na zakresie i późniejsze wywołanie `CalculateFormula` jest zazwyczaj szybsze niż iteracyjne przypisywanie wartości pojedynczo.  

- **Zapis do strumienia zamiast pliku?**  
  `work

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}