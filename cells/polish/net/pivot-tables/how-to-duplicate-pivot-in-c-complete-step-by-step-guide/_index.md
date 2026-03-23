---
category: general
date: 2026-03-22
description: Dowiedz się, jak duplikować tabelę przestawną w C# przy użyciu Aspose.Cells.
  Ten przewodnik pokazuje również, jak kopiować wiersze i ładować skoroszyt Excel
  w C# w celu płynnej automatyzacji Excela oraz kopiowania wierszy.
draft: false
keywords:
- how to duplicate pivot
- how to copy rows
- load excel workbook c#
- excel automation copy rows
language: pl
og_description: Jak zduplikować tabelę przestawną w C#? Zapoznaj się z tym zwięzłym
  samouczkiem, aby załadować skoroszyt Excela w C#, kopiować wiersze i opanować automatyzację
  Excela przy kopiowaniu wierszy.
og_title: Jak zduplikować Pivot w C# – Kompletny przewodnik
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Jak zduplikować Pivot w C# – Kompletny przewodnik krok po kroku
url: /pl/net/pivot-tables/how-to-duplicate-pivot-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zduplikować tabelę przestawną w C# – Kompletny przewodnik krok po kroku

Zastanawiałeś się kiedyś **jak zduplikować tabelę przestawną** programowo, bez ręcznego przeciągania jej w Excelu? Nie jesteś jedyny. W wielu procesach raportowania ten sam układ tabeli przestawnej jest potrzebny na nowym zestawie wierszy, a ręczne kopiowanie to strata czasu.  

Dobre wieści? Kilkoma liniami C# możesz wczytać skoroszyt Excel, określić obszar zawierający tabelę przestawną i **jak kopiować wiersze**, aby tabela pojawiła się w nowej lokalizacji — wszystko w jednym zautomatyzowanym uruchomieniu. W tym samouczku omówimy także podstawy **load excel workbook c#** oraz zapewnimy solidne podstawy do zadań **excel automation copy rows**.

> **Co wyniesiesz z tego**  
> • Pełny, uruchamialny przykład, który duplikuje tabelę przestawną.  
> • Wyjaśnienie, dlaczego każda linia ma znaczenie.  
> • Wskazówki dotyczące obsługi przypadków brzegowych, takich jak ukryte arkusze lub wiele tabel przestawnych.

---

## Wymagania wstępne

Before we dive in, make sure you have:

- **.NET 6.0** (lub dowolna nowsza wersja .NET) zainstalowana.  
- **Aspose.Cells for .NET** – biblioteka, której użyjemy do manipulacji plikami Excel. Możesz ją pobrać przez NuGet:  

```bash
dotnet add package Aspose.Cells
```  

- Źródłowy skoroszyt (`Source.xlsx`) zawierający już tabelę przestawną w zakresie **A1:J20** (zakres, który będziemy duplikować).  
- Podstawowa znajomość składni C# – nic skomplikowanego, tylko typowe instrukcje `using` i metoda `Main`.

If any of these sound unfamiliar, pause a moment and install the package; the rest of the guide assumes the library is ready to go.

Jeśli coś z tego jest Ci nieznane, zatrzymaj się na chwilę i zainstaluj pakiet; dalsza część przewodnika zakłada, że biblioteka jest gotowa do użycia.

![Ilustracja jak zduplikować tabelę przestawną w C# przy użyciu Aspose.Cells](https://example.com/duplicate-pivot.png "ilustracja jak zduplikować tabelę przestawną w C#")

*Tekst alternatywny obrazu: "przykład jak zduplikować tabelę przestawną w C# pokazujący źródłowe i zduplikowane wiersze tabeli przestawnej".*

---

## Krok 1: Load Excel Workbook C# – Otwieranie pliku

The very first thing you need to do when you want to **load excel workbook c#** is create a `Workbook` instance pointing at your file. This object gives you access to every worksheet, cell, and pivot inside the file.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Load the source workbook
        string sourcePath = @"C:\Data\Source.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // From here on we can work with worksheets, ranges, and pivots.
```

**Dlaczego to ważne:**  
`Workbook` abstrahuje cały plik Excel do modelu w pamięci. Bez wcześniejszego wczytania nie możesz sprawdzić lokalizacji tabeli przestawnej ani kopiować wierszy. Ponadto konstruktor automatycznie wykrywa format pliku (XLS, XLSX, CSV itp.), więc nie potrzebujesz dodatkowego kodu do wykrywania formatu.

---

## Krok 2: How to Copy Rows – Definiowanie obszaru tabeli przestawnej

Now that the workbook is in memory, we need to tell Aspose.Cells which rows contain the pivot. In our example the pivot lives in **A1:J20**, which translates to rows **0‑19** (zero‑based indexing). We’ll wrap that in a `CellArea` structure.

```csharp
        // Step 2: Define the cell area that contains the pivot table (A1:J20)
        // Row indices are zero‑based, column indices are also zero‑based.
        CellArea copyRange = new CellArea(startRow: 0, startColumn: 0, endRow: 19, endColumn: 9);
```

**Dlaczego używamy `CellArea`:**  
To lekki sposób opisania prostokątnego bloku. Kiedy później wywołasz `CopyRows`, metoda odczytuje ten obiekt, aby dokładnie wiedzieć, które wiersze skopiować. Jeśli kiedykolwiek będziesz musiał dostosować zakres (np. tabela przestawna rozrośnie się do kolumny K), zmieniasz tylko wartość `endColumn`.

---

## Krok 3: Dostęp do docelowego arkusza

Most workbooks have a single sheet, but the API works the same for multiple sheets. Grab the first worksheet (index 0) – that’s where the original pivot lives.

```csharp
        // Step 3: Get the first worksheet from the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Pro tip:**  
Jeśli masz nazwane arkusze, możesz je także pobrać po nazwie: `workbook.Worksheets["Sheet1"]`. To pomaga uniknąć twardego kodowania indeksów, gdy struktura skoroszytu się zmienia.

---

## Krok 4: How to Copy Rows – Duplikowanie tabeli przestawnej

Here’s the heart of **how to duplicate pivot**: we copy the rows containing the pivot to a new location. In our case we start at row 31 (zero‑based index 30). The `CopyRows` method copies *both* the data and the underlying pivot cache, so the new rows behave exactly like the original.

```csharp
        // Step 4: Copy the rows of the defined range to a new location (starting at row 31)
        // The third argument is the destination start row (zero‑based).
        worksheet.Cells.CopyRows(copyRange.StartRow, copyRange.EndRow, destinationRow: 30);
```

**Co się dzieje w tle?**  
`CopyRows` klonuje każdy wiersz, zachowując formuły, style i definicje tabeli przestawnej. Ponieważ pamięć podręczna tabeli przestawnej istnieje na poziomie skoroszytu, zduplikowana tabela automatycznie odwołuje się do tego samego źródła danych – nie wymaga dodatkowej konfiguracji.

**Przypadek brzegowy – ukryte wiersze:**  
Jeśli którykolwiek z wierszy w zakresie źródłowym jest ukryty, pozostanie ukryty po skopiowaniu. Jeśli chcesz je odkryć, wywołaj `worksheet.Rows[destRow].IsHidden = false` po kopiowaniu.

---

## Krok 5: Zapisz skoroszyt – weryfikacja duplikatu

Finally, write the changes back to disk. You can overwrite the original file or, safer, save to a new name so you can compare the before/after.

```csharp
        // Step 5: Save the workbook – the pivot table is now duplicated in the new rows
        string outputPath = @"C:\Data\CopyWithPivot.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine("Pivot duplicated successfully! Check " + outputPath);
    }
}
```

**Wynik, który powinieneś zobaczyć:**  
Otwórz `CopyWithPivot.xlsx`. Znajdziesz oryginalną tabelę przestawną w **A1:J20** oraz identyczną kopię zaczynającą się od **A31:J50**. Obie tabele mogą być odświeżane niezależnie, a wszelkie segmentatory podłączone do oryginału będą nadal działać dla kopii, ponieważ korzystają z tej samej pamięci podręcznej.

---

## Częste pytania i warianty

### Czy mogę zduplikować wiele tabel przestawnych jednocześnie?

Absolutely. Loop through all pivot tables (`worksheet.PivotTables`) and copy each one’s range to a different destination. Just make sure the destination ranges don’t overlap.

### Co jeśli źródłowy skoroszyt jest chroniony hasłem?

Aspose.Cells pozwala otworzyć chroniony plik, przekazując hasło do konstruktora `Workbook`:

```csharp
Workbook workbook = new Workbook(sourcePath, new LoadOptions { Password = "mySecret" });
```

### Jak kopiować wiersze bez wpływu na formuły?

If you only need the *values* (no formulas), use `CopyRows` with the `CopyOptions` flag:

```csharp
worksheet.Cells.CopyRows(sourceStart, sourceEnd, destStart, new CopyOptions { CopyValues = true });
```

### Czy istnieje sposób, aby skopiować wiersze do *innego* skoroszytu?

Yes. After copying rows in the source sheet, you can clone the worksheet into another `Workbook` instance via `targetWorkbook.Worksheets.AddCopy(worksheet)`.

---

## Porady eksperta dla niezawodnej automatyzacji Excela – kopiowanie wierszy

- **Sprawdź zakres** przed kopiowaniem. Krótkie `if (copyRange.EndRow >= worksheet.Cells.MaxDataRow)` zapobiega błędom poza zakresem.  
- **Wyłącz obliczenia** podczas kopiowania dużych zakresów: `workbook.Settings.CalcMode = CalcMode.Manual;` – to znacząco przyspiesza operację.  
- **Zwolnij obiekty** (`workbook.Dispose()`), jeśli przetwarzasz wiele plików w pętli, aby zwolnić zasoby natywne.  
- **Loguj operację** – szczególnie w pipeline'ach produkcyjnych – aby móc śledzić, które pliki zostały przetworzone i wczesniej wykrywać błędy.

---

## Zakończenie

You now know **how to duplicate pivot** tables in C# using Aspose.Cells, and you’ve seen the full workflow from **load excel workbook c#** to **excel automation copy rows** and finally saving the result. The example is self‑contained, runs out of the box, and can be extended to handle multiple pivots, protected files, or cross‑workbook copying.

Next steps? Try adapting the script to:

- Odśwież zduplikowaną tabelę przestawną programowo (`pivotTable.RefreshData();`).  
- Wyeksportuj zduplikowany obszar do CSV do dalszego przetwarzania.  
- Zintegruj kod z API ASP.NET Core, aby użytkownicy mogli wgrać plik i natychmiast otrzymać wersję z duplikowaną tabelą przestawną.

Happy coding, and may your Excel automation be ever smooth!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}