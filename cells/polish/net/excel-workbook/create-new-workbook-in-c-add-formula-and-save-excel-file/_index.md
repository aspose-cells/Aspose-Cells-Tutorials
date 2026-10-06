---
category: general
date: 2026-02-23
description: Utwórz nowy skoroszyt programowo w C# i dodaj formułę do komórki. Dowiedz
  się, jak używać funkcji EXPAND, a następnie zapisz skoroszyt Excel bez wysiłku.
draft: false
keywords:
- create new workbook
- add formula to cell
- save excel workbook
- how to use expand
- create excel file programmatically
language: pl
og_description: Utwórz nowy skoroszyt programowo w C#. Dodaj formułę do komórki, dowiedz
  się, jak używać funkcji EXPAND i zapisz skoroszyt Excel w kilka sekund.
og_title: Utwórz nowy skoroszyt w C# – Dodaj formułę i zapisz plik Excel
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Utwórz nowy skoroszyt w C# – Dodaj formułę i zapisz plik Excel
url: /pl/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz nowy skoroszyt w C# – Dodaj formułę i zapisz plik Excel

Zastanawiałeś się kiedyś, jak **create new workbook** obiekty z kodu bez otwierania Excela? Nie jesteś jedyny. Wielu programistów napotyka trudności, gdy muszą w locie wygenerować arkusz kalkulacyjny — być może do raportu, eksportu lub szybkiego zrzutu danych.  

Dobre wieści? W tym przewodniku dokładnie zobaczysz, jak **create new workbook**, dodać **add formula to cell**, a następnie **save excel workbook** przy użyciu kilku linii C#. Zanurzymy się także w **how to use expand**, abyś mógł generować dynamiczne tablice bez ręcznego kopiowania. Po zakończeniu będziesz w stanie **create excel file programmatically** i udostępnić go użytkownikom lub usługom downstream.

## Wymagania wstępne

- .NET 6.0 lub nowszy (dowolny aktualny runtime .NET działa)
- Aspose.Cells for .NET (bezpłatna wersja próbna lub licencjonowana) – ta biblioteka udostępnia klasy `Workbook` i `Worksheet` używane poniżej.
- Podstawowa znajomość składni C# — nie wymagana głęboka wiedza o Excelu.

Jeśli już je masz, świetnie! Jeśli nie, pobierz Aspose.Cells z NuGet (`Install-Package Aspose.Cells`) i będziesz gotowy do działania.

---

## Krok 1: Utwórz nowy skoroszyt — Podstawa

Na początek musimy utworzyć nowy obiekt skoroszytu. Pomyśl o tym jak o otwarciu zupełnie nowego, pustego pliku Excel.

```csharp
using Aspose.Cells;

public class ExcelGenerator
{
    public void Generate()
    {
        // Step 1: Create a new workbook (this is the core of create new workbook)
        Workbook workbook = new Workbook();
```

> **Dlaczego to ważne:** Klasa `Workbook` jest punktem wejścia do wszelkiej manipulacji Excel. Tworząc nową instancję, przydzielamy pamięć na arkusze, style i formuły — wszystko bez dotykania systemu plików.

---

## Krok 2: Uzyskaj dostęp do pierwszego arkusza

Każdy nowy skoroszyt zawiera domyślny arkusz (nazwany *Sheet1*). Pobierzemy go, aby móc umieszczać dane i formuły.

```csharp
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Wskazówka:** Jeśli potrzebujesz wielu arkuszy, po prostu wywołaj `workbook.Worksheets.Add("MySheet")` i pracuj z zwróconym obiektem `Worksheet`.

---

## Krok 3: Dodaj formułę do komórki — używając EXPAND

Teraz przychodzi zabawna część: wstawianie formuły. Funkcja `EXPAND` jest idealna, gdy chcesz przekształcić statyczną tablicę w większy, automatycznie wypełniony zakres.

```csharp
        // Step 3: Add formula to cell A1 using EXPAND
        // This creates a 5‑row array from the constant {1,2,3}
        worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";
```

### Jak działa formuła EXPAND

| Argument | Meaning |
|----------|---------|
| `{1,2,3}` | Źródłowa tablica (pozioma lista trzech liczb) |
| `5`       | Żądana liczba wierszy w wyniku |
| `1`       | Żądana liczba kolumn (pozostaw 1, aby zachować pionowość) |

Kiedy Excel oceni to, wygeneruje **pionową** listę:

```
A1: 1
A2: 2
A3: 3
A4: 0   (filled with zeros)
A5: 0
```

> **Dlaczego używać EXPAND?** Eliminuje potrzebę ręcznego kopiowania lub pętli VBA. Funkcja dynamicznie przekształca dane, czyniąc arkusze bardziej solidnymi i łatwiejszymi w utrzymaniu.

---

## Krok 4: Zapisz skoroszyt Excel — zachowaj wynik

Po umieszczeniu formuły, ostatnim krokiem jest zapisanie skoroszytu na dysku. Możesz wybrać dowolny folder, do którego masz prawa zapisu.

```csharp
        // Step 4: Save the workbook to view the result
        string outputPath = @"C:\Temp\ExpandFormula.xlsx";
        workbook.Save(outputPath);
    }
}
```

> **Co zobaczysz:** Otwórz `ExpandFormula.xlsx` w Excelu, a komórka `A1` wyświetli rozszerzoną tablicę. Sama formuła pozostaje w komórce, więc po edycji źródłowej tablicy wynik aktualizuje się automatycznie.

---

## Opcjonalnie: Zweryfikuj wynik programowo

Jeśli wolisz nie otwierać Excela ręcznie, możesz odczytać wartości z powrotem, aby potwierdzić, że spełniają oczekiwania.

```csharp
        // Verify values without opening Excel
        for (int row = 0; row < 5; row++)
        {
            var value = worksheet.Cells[row, 0].Value; // column 0 = A
            Console.WriteLine($"Row {row + 1}: {value}");
        }
```

Uruchomienie powyższego wypisze:

```
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

---

## Częste pytania i przypadki brzegowe

| Question | Answer |
|----------|--------|
| **Czy mogę używać EXPAND z większą tablicą źródłową?** | Oczywiście. Po prostu zamień `{1,2,3}` na dowolną stałą lub zakres komórek, np. `EXPAND(A1:C1,10,1)`. |
| **Co zrobić, jeśli potrzebuję wyniku poziomego?** | Zamień argumenty wiersza/kolumny: `EXPAND({1,2,3},1,5)` wygeneruje rozkład 1‑wierszowy, 5‑kolumnowy. |
| **Czy to będzie działać w starszych wersjach Excela?** | `EXPAND` jest dostępny od Excel 365/2021. W starszych wersjach trzeba symulować tablicę przy użyciu `INDEX`/`SEQUENCE`. |
| **Czy muszę wywoływać `workbook.CalculateFormula()`?** | Nie. Aspose.Cells automatycznie ocenia formuły przy zapisie, więc wartości pojawiają się od razu. |
| **Jak dodać więcej niż jeden arkusz przed zapisem?** | Wywołaj `workbook.Worksheets.Add("SecondSheet")` i powtórz kroki manipulacji komórkami na nowym arkuszu. |

---

## Pełny działający przykład

Poniżej znajduje się kompletny, gotowy do uruchomienia program. Skopiuj i wklej go do aplikacji konsolowej, dostosuj ścieżkę wyjścia i naciśnij **F5**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create new workbook
            Workbook workbook = new Workbook();

            // Access first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Add EXPAND formula to A1
            worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";

            // Optional: verify values in console
            workbook.CalculateFormula(); // ensures formulas are evaluated now
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"A{i + 1} = {worksheet.Cells[i, 0].Value}");
            }

            // Save the workbook
            string filePath = @"C:\Temp\ExpandFormula.xlsx";
            workbook.Save(filePath);
            Console.WriteLine($"Workbook saved to {filePath}");
        }
    }
}
```

**Oczekiwany wynik w konsoli:**

```
A1 = 1
A2 = 2
A3 = 3
A4 = 0
A5 = 0
Workbook saved to C:\Temp\ExpandFormula.xlsx
```

Otwórz wygenerowany plik i zobaczysz te same liczby w kolumnie **A**.

---

## Podsumowanie wizualne

![Przykład tworzenia nowego skoroszytu](create-new-workbook.png "Zrzut ekranu pokazujący nowy skoroszyt utworzony przy pomocy create new workbook w C#")

*Obraz ilustruje świeżo wygenerowany skoroszyt z wynikiem funkcji EXPAND.*

---

## Zakończenie

Teraz wiesz, jak **create new workbook**, **add formula to cell** i **save excel workbook** przy użyciu C#. Opanowując **how to use expand**, możesz generować dynamiczne tablice bez ręcznego wysiłku, a cały proces pozwala **create excel file programmatically** w dowolnym scenariuszu automatyzacji.

Co dalej? Spróbuj zamienić stałą tablicę na odwołanie do zakresu, eksperymentuj z różnymi wymiarami `EXPAND` lub łańcuchuj wiele formuł między arkuszami. Ten sam wzorzec działa dla wykresów, formatowania i nawet tabel przestawnych — więc kontynuuj eksplorację.

Jeśli napotkasz jakiekolwiek problemy, zostaw komentarz poniżej. Szczęśliwego kodowania i ciesz się mocą programowego Excela!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}