---
category: general
date: 2026-03-22
description: Jak używać wyrażeń lambda w C# do pracy z formułami Excela. Naucz się
  zapisywać formułę do komórki, konwertować zakres na tablicę, wyświetlać tablicę
  w konsoli oraz obliczać cotangens w Excelu.
draft: false
keywords:
- how to use lambda
- display array in console
- convert range to array
- write formula to cell
- calculate cotangent in excel
language: pl
og_description: Jak używać wyrażeń lambda w C# do manipulacji formułami Excela, konwertowania
  zakresu na tablicę, zapisywania formuły w komórce, wyświetlania tablicy w konsoli
  oraz obliczania cotangensa w Excelu.
og_title: Jak używać lambdy w C# z formułami Excela – krok po kroku
tags:
- C#
- Aspose.Cells
- Excel Automation
- Lambda Expressions
title: Jak używać lambdy w C# z formułami Excela – Kompletny przewodnik
url: /pl/net/formulas-functions/how-to-use-lambda-in-c-with-excel-formulas-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać Lambda w C# z formułami Excel – Kompletny przewodnik

Zastanawiałeś się kiedyś **jak używać lambda**, gdy automatyzujesz Excel z C#? Nie jesteś sam. Wielu programistów napotyka trudności, gdy muszą połączyć moc nowych funkcji dynamicznych tablic Excela z możliwościami `LAMBDA` w C#. Dobra wiadomość? To w rzeczywistości dość proste, gdy zobaczysz, jak elementy do siebie pasują.

W tym tutorialu przejdziemy przez **zapisywanie formuły do komórki**, **przekształcanie zakresu w tablicę**, **wyświetlanie tej tablicy w konsoli**, a nawet **obliczanie cotangensa w Excelu** — wszystko pokazując **jak używać lambda** wewnątrz wywołania `REDUCE`. Na końcu będziesz mieć działający fragment kodu, który możesz wkleić do dowolnego projektu .NET odwołującego się do Aspose.Cells (lub podobnej biblioteki).

---

## Co się nauczysz

- Jak **zapisać formułę do komórki** przy użyciu C#.
- Jak **przekształcić zakres w tablicę** przy użyciu funkcji `EXPAND`.
- Jak **wyświetlić tablicę w konsoli** po obliczeniach.
- Jak **obliczyć cotangens w Excelu** używając `COT` i `COTH`.
- Dokładna składnia **jak używać lambda** wewnątrz funkcji `REDUCE` Excela z poziomu C#.

> **Wymagania wstępne:** Potrzebujesz aktualnej wersji .NET (Core 6+ lub .NET Framework 4.7+) oraz biblioteki Aspose.Cells dla .NET zainstalowanej przez NuGet.

---

## Krok 1: Przygotuj skoroszyt i zapisz formułę do komórki

Pierwszą rzeczą, którą robimy, jest utworzenie nowego skoroszytu i pobranie pierwszego arkusza. Następnie **zapisujemy formułę do komórki** – w tym przypadku `A1` będzie zawierać wynik wywołania `EXPAND`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write formula to A1 – we’ll expand B1:C2 into a 4‑by‑5 array later
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";
```

**Dlaczego to ważne:** Zapisywanie formuły bezpośrednio z kodu oznacza, że możesz generować złożone arkusze w locie, nie otwierając nigdy Excela. To także przygotowuje scenę do kolejnego kroku, w którym **przekształcamy zakres w tablicę**.

---

## Krok 2: Przekształć zakres w tablicę przy użyciu EXPAND

`EXPAND` to sposób Excela na zamianę małego zakresu w większą macierz. Umieszczając formułę w `A1`, Excel rozleje blok 4 × 5 zaczynający się od tej komórki. Z poziomu C# nie musimy ręcznie kopiować wartości – biblioteka wykona ciężką pracę, gdy wywołamy `Calculate`.

```csharp
        // The EXPAND formula will spill into A1:E4 (4 rows × 5 columns)
        // No extra code needed – the workbook will handle the spill.
```

**Jak używać lambda:** Jeszcze nie, ale bądźcie czujni. Najpierw potrzebujemy danych w arkuszu, potem zredukujemy je przy pomocy lambda.

---

## Krok 3: Użyj LAMBDA wewnątrz REDUCE – rdzeń „Jak używać lambda”

Excel 365 wprowadził `REDUCE`, który przyjmuje **wartość początkową**, **zakres** oraz **LAMBDA**, określającą, jak połączyć każdy element. Z poziomu C# po prostu przypisujemy ciąg znaków formuły; lambda żyje wewnątrz formuły Excela, nie w kodzie C#.

```csharp
        // Reduce the spilled array by summing all its values.
        // This demonstrates how to use lambda inside REDUCE.
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";
```

**Wyjaśnienie:**  
- `0` to początkowy akumulator (`acc`).  
- `A1:D4` to zakres, który chcemy przetworzyć (pierwsze cztery kolumny rozlewu).  
- `LAMBDA(acc, x, acc + x)` mówi Excelowi, aby dodał każdą komórkę (`x`) do akumulatora.  

To istota **jak używać lambda** do agregacji w kontekście arkusza kalkulacyjnego.

---

## Krok 4: Oblicz cotangens w Excelu – od stopni do hiperbolicznych

Jeśli potrzebujesz wyników trygonometrycznych, funkcje `COT` i `COTH` Excela są bardzo proste w użyciu. Umieścimy je odpowiednio w `G1` i `G2`.

```csharp
        // Demonstrate trigonometric functions – cotangent and hyperbolic cotangent
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected result: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";      // Hyperbolic cotangent of 1
```

**Dlaczego to przydatne:** Znajomość **obliczania cotangensa w Excelu** może zaoszczędzić Ci pisania własnego kodu matematycznego, szczególnie gdy skoroszyt będzie udostępniany osobom niebędącym programistami.

---

## Krok 5: Wymuś obliczenia i pobierz rozszerzoną tablicę

Teraz nakazujemy skoroszytowi ocenić każdą formułę, a potem wyciągamy rozlewaną tablicę z `A1`. To właśnie miejsce, w którym **wyświetlamy tablicę w konsoli**.

```csharp
        // Force calculation of all formulas
        workbook.Calculate();

        // Retrieve the spilled array from A1 as a 2‑D object
        var expanded = worksheet.Cells["A1"].Value;

        // Pretty‑print the 2‑D array to the console
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show the result of the REDUCE lambda
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Co zobaczysz:**  
- Ładnie sformatowaną macierz 4 × 5 wydrukowaną wiersz po wierszu.  
- Sumę obliczoną przez lambda w `REDUCE`.  
- Dwie wartości cotangensa.

To kończy przepływ od **zapisu formuły do komórki** aż po **wyświetlenie tablicy w konsoli**.

---

## Pełny działający przykład (gotowy do kopiowania i wklejenia)

Poniżej znajduje się cały program, który możesz wkleić do aplikacji konsolowej. Pamiętaj, aby najpierw dodać pakiet NuGet `Aspose.Cells` (`dotnet add package Aspose.Cells`).

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write EXPAND formula (convert range to array)
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";

        // Step 3: Use REDUCE with LAMBDA (how to use lambda)
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";

        // Step 4: Calculate cotangent values (calculate cotangent in excel)
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";

        // Step 5: Force calculation
        workbook.Calculate();

        // Step 6: Retrieve and display the expanded array (display array in console)
        var expanded = worksheet.Cells["A1"].Value;
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show REDUCE result
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Oczekiwany wynik w konsoli (wartości będą się różnić w zależności od domyślnej zawartości B1:C2, które domyślnie wynoszą 0):**

```
Expanded array from A1 (4×5):
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0

Sum of A1:D4 (via REDUCE lambda): 0
Cotangent of π/4: 1
Hyperbolic cotangent of 1: 1.31303528549933
```

Śmiało wypełnij `B1:C2` własnymi liczbami przed uruchomieniem – macierz odzwierciedli te wartości.

---

## Porady profesjonalne i typowe pułapki

- **Porada:** Jeśli potrzebujesz, aby rozlewający się zakres zaczynał się w innym miejscu, po prostu zmień docelową komórkę (`A1`). Funkcja `EXPAND` respektuje punkt zaczepienia.
- **Uwaga:** Puste komórki w źródłowym zakresie stają się `0` w rozlewającej się tablicy, co może wpłynąć na sumę w `REDUCE`.
- **Przypadek brzegowy:** Gdy skoroszyt zawiera formuły zależne od funkcji zmiennych (np. `NOW()`), wywołaj `workbook.Calculate()` po ustawieniu wszystkich formuł, aby zapewnić aktualność danych.
- **Uwaga dotycząca wydajności:** Przy dużych rozlewach rozważ ograniczenie rozmiaru w wywołaniu `EXPAND`; w przeciwnym razie możesz przydzielić więcej pamięci niż potrzebne.
- **Compatibility:** The `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}