---
category: general
date: 2026-02-09
description: Jak stworzyć tablicę w Excelu przy użyciu C# wyjaśnione w kilka minut
  – dowiedz się, jak generować liczby sekwencyjne, używać COT i zapisać skoroszyt
  jako XLSX.
draft: false
keywords:
- how to create array
- create excel workbook c#
- generate sequence numbers
- save workbook as xlsx
- how to use cot
language: pl
og_description: Jak utworzyć tablicę w Excelu przy użyciu C# jest opisane krok po
  kroku, w tym generowanie numerów sekwencyjnych, użycie COT oraz zapisanie skoroszytu
  w formacie XLSX.
og_title: Jak utworzyć tablicę w Excelu przy użyciu C# – szybki przewodnik
tags:
- C#
- Excel
- Aspose.Cells
title: Jak utworzyć tablicę w Excelu przy użyciu C# – Przewodnik krok po kroku
url: /pl/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć tablicę w Excelu przy użyciu C# – Przewodnik krok po kroku

Zastanawiałeś się kiedyś **jak utworzyć tablicę** w Excelu przy użyciu C# bez spędzania godzin na przeszukiwaniu dokumentacji? Nie jesteś sam. Wielu programistów napotyka problem, gdy potrzebują dynamicznego zakresu spill, szybkiej wartości trygonometrycznej lub po prostu czystego pliku XLSX zapisanego na dysku. W tym samouczku rozwiążemy ten problem od razu — tworząc mały skoroszyt, który zapisuje rosnącą formułę tablicową, wstawia obliczenie cotangensa i zapisuje wszystko jako plik XLSX.  

Dodamy też kilka dodatkowych sztuczek: generowanie numerów sekwencji, opanowanie funkcji `COT` oraz zapewnienie, że plik trafi tam, gdzie chcesz. Po zakończeniu będziesz mieć wielokrotnego użytku fragment kodu, który możesz wkleić do dowolnego projektu .NET. Bez zbędnych dodatków, po prostu działający kod.

> **Wskazówka:** Przykład używa popularnej biblioteki **Aspose.Cells**, ale koncepcje można przenieść na inne pakiety automatyzacji Excela (EPPlus, ClosedXML) z jedynie drobnymi zmianami.

---

## Czego będziesz potrzebować

- **.NET 6** lub nowszy (kod kompiluje się również na .NET Framework 4.7+)
- **Aspose.Cells for .NET** – możesz go pobrać z NuGet (`Install-Package Aspose.Cells`)
- Edytor tekstu lub IDE (Visual Studio, Rider, VS Code…)
- Uprawnienia do zapisu w folderze, w którym zostanie zapisany plik wyjściowy

To wszystko — bez dodatkowej konfiguracji, bez interfejsu COM, po prostu czysta zarządzana biblioteka.

---

## Krok 1: Jak utworzyć tablicę w Excelu – Inicjalizacja skoroszytu

Pierwszą rzeczą, gdy chcesz **jak utworzyć tablicę** w arkuszu Excel, jest utworzenie obiektu skoroszytu. Traktuj skoroszyt jak czyste płótno; arkusz jest miejscem, w którym narysujesz swoje formuły.

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // <- fresh workbook
        Worksheet worksheet = workbook.Worksheets[0];    // first (and only) sheet

        // The rest of the steps follow...
```

Dlaczego używać `Workbook()` bez parametrów? Daje to skoroszyt w pamięci z domyślnym arkuszem, co jest idealne do szybkich, programowych zadań. Jeśli potrzebujesz otworzyć istniejący plik, po prostu przekaż ścieżkę do konstruktora.

---

## Krok 2: Generowanie numerów sekwencji przy użyciu EXPAND i SEQUENCE

Teraz, gdy mamy arkusz, odpowiedzmy na część zagadki dotyczącą **generowania numerów sekwencji**. Nowe dynamiczne funkcje tablicowe Excela (`SEQUENCE`, `EXPAND`) pozwalają nam stworzyć pionistą listę 3‑wierszową i automatycznie rozlać ją na zakres 3 × 5.

```csharp
        // Write a dynamic array formula that expands a 3‑row sequence into a 3×5 spill range
        // EXPAND pads the result to 5 columns, SEQUENCE generates numbers 1‑3 vertically
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

**Co się tutaj dzieje?**  
- `SEQUENCE(3,1,1,1)` → tworzy pionową tablicę `{1;2;3}`.  
- `EXPAND(...,5,1)` → rozciąga tę trzy‑wierszową kolumnę do pięciu kolumn, wypełniając dodatkowe komórki pustymi wartościami.  

Po otwarciu wygenerowanego pliku `output.xlsx` zobaczysz blok 3 × 5 zaczynający się od **A1**, gdzie pierwsza kolumna zawiera 1, 2, 3, a pozostałe cztery kolumny są puste. Ta technika jest podstawą zakresów spill w stylu **jak utworzyć tablicę** bez ręcznego wpisywania każdej komórki.

---

## Krok 3: Jak używać COT – Dodawanie formuły trygonometrycznej

Jeśli jesteś również ciekawy **jak używać cot** w formule Excela, funkcja `COT` jest wygodnym sposobem na uzyskanie cotangensa kąta wyrażonego w radianach. Obliczmy `cot(π/4)`, które powinno dawać **1**.

```csharp
        // Write a simple trigonometric formula that calculates cotangent of 45° (π/4)
        // COT(π/4) evaluates to 1
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

Zauważ, że użyliśmy `PI()`, aby uzyskać wartość radianów dla 180°, a następnie podzieliliśmy przez 4, aby uzyskać 45°. Excel wykonuje ciężką pracę, a komórka **B1** pokaże `1` po otwarciu skoroszytu. To pokazuje **jak używać cot** do szybkich obliczeń inżynierskich lub finansowych bez korzystania z oddzielnej biblioteki matematycznej.

---

## Krok 4: Zapisz skoroszyt jako XLSX – Trwałe zapisanie pliku

Cała frajda z tworzenia tablicy i wstawiania formuł jest zmarnowana, jeśli nigdy nie zapiszesz pliku na dysku. Oto prosty sposób na **zapisanie skoroszytu jako xlsx** przy użyciu Aspose.Cells:

```csharp
        // Save the workbook to verify the formulas (optional)
        string outputPath = @"C:\Temp\output.xlsx";   // adjust to your folder
        workbook.Save(outputPath, SaveFormat.Xlsx);

        // Let the user know we’re done
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Dlaczego określamy `SaveFormat.Xlsx`? Gwarantuje to nowoczesny format OpenXML, który jest uniwersalnie odczytywalny (Excel, LibreOffice, Google Sheets). Jeśli potrzebujesz starszego pliku `.xls`, po prostu zamień enum.

---

## Pełny działający przykład (wszystkie kroki połączone)

Poniżej znajduje się kompletny, gotowy do uruchomienia program. Skopiuj i wklej go do projektu konsolowego, przywróć pakiet NuGet Aspose.Cells i naciśnij **F5**.

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Create a dynamic spill range (how to create array)
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";

        // Step 3: Calculate cotangent (how to use cot)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";

        // Step 4: Persist the file (save workbook as xlsx)
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Oczekiwany wynik** po otwarciu `output.xlsx`:

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 |   |   |   |
| 2 |   |   |   |   |
| 3 |   |   |   |   |

- Kolumna A pokazuje liczby 1‑3 wygenerowane przez `SEQUENCE`.  
- Kolumna B zawiera wartość **1** z formuły `COT`.  
- Kolumny C‑E są puste, ilustrując efekt wypełnienia funkcją `EXPAND`.

---

## Częste pytania i przypadki brzegowe

### Co zrobić, jeśli potrzebuję więcej wierszy lub kolumn?

Po prostu zmień argumenty `SEQUENCE` i `EXPAND`.  
- `SEQUENCE(10,2,5,2)` da macierz 10‑wierszy × 2‑kolumn, zaczynając od 5 i zwiększając o 2.  
- `EXPAND(...,10,5)` wypełni wynik do 10 kolumn i 5 wierszy.

### Czy to działa w starszych wersjach Excela?

Dynamiczne funkcje tablicowe (`SEQUENCE`, `EXPAND`) wymagają Excel 365 lub 2019+. Dla starszych plików możesz wrócić do klasycznych formuł lub zapisywać wartości bezpośrednio za pomocą `Cells[row, col].PutValue(value)`.

### Czy mogę zapisać formułę w stylu R1C1?

Oczywiście. Zastąp `A1` przez `Cells[0, 0]` i użyj właściwości `FormulaR1C1`:

```csharp
worksheet.Cells[0, 0].FormulaR1C1 = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

### Co z separatorami dziesiętnymi zależnymi od kultury?

Aspose.Cells respektuje ustawienia regionalne skoroszytu. Jeśli potrzebujesz konkretnej kultury, ustaw `workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");` przed zapisywaniem formuł.

---

## Podsumowanie wizualne

![jak utworzyć tablicę w Excelu przy użyciu C#](/images/how-to-create-array-excel-csharp.png "jak utworzyć tablicę w Excelu przy użyciu C#")

*Zrzut ekranu pokazuje ostateczny zakres spill oraz wynik cotangensa.*

---

## Wnioski

Oto masz — **jak utworzyć tablicę** w Excelu przy użyciu C# od podstaw, generować numery sekwencji, wykorzystać funkcję `COT` i **zapisać skoroszyt jako XLSX** w jednym, schludnym programie. Najważniejsze wnioski to:

1. Używaj obiektów `Workbook` i `Worksheet`, aby rozpocząć automatyzację Excela.  
2. Wykorzystuj dynamiczne funkcje tablicowe (`SEQUENCE`, `EXPAND`) do elastycznych zakresów spill.  
3. Wstawiaj funkcje trygonometryczne, takie jak `COT`, aby szybko wykonywać obliczenia bez dodatkowych bibliotek.  
4. Zachowaj wynik przy użyciu `SaveFormat.Xlsx`, aby uzyskać uniwersalnie czytelny plik.

Gotowy na kolejny krok? Spróbuj zamienić `COT(PI()/4)`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}