---
category: general
date: 2026-03-29
description: Utwórz skoroszyt Excela i dowiedz się, jak używać funkcji WRAPCOLS do
  konwersji tablicy na macierz, wymuś obliczenia i zapisz skoroszyt jako plik XLSX.
draft: false
keywords:
- create excel workbook
- convert array to matrix
- save workbook as xlsx
- how to use wrapcols
- force workbook calculation
language: pl
og_description: Utwórz skoroszyt Excel w C#, przekształć tablicę w macierz przy użyciu
  WRAPCOLS, wymuś obliczenia skoroszytu i zapisz jako XLSX. Pełny kod i wskazówki.
og_title: Utwórz skoroszyt Excel – Przewodnik krok po kroku
tags:
- Aspose.Cells
- C#
- Excel automation
title: Utwórz skoroszyt Excel – konwertuj tablicę na macierz przy użyciu WRAPCOLS
url: /pl/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz skoroszyt Excel – konwersja tablicy na macierz przy użyciu WRAPCOLS

Czy kiedykolwiek musiałeś **utworzyć skoroszyt Excel** od zera i nagle napotkałeś problem przy przekształcaniu danych? Nie jesteś sam. Wielu programistów sięga po prostą tablicę, tylko po to, by odkryć, że Excel oczekuje prawidłowego zakresu 2‑D.  

W tym samouczku pokażemy dokładnie, jak **utworzyć skoroszyt Excel**, użyć funkcji `WRAPCOLS` do **konwersji tablicy na macierz**, **wymusić obliczenie skoroszytu**, a na koniec **zapisać skoroszyt jako XLSX**. Po zakończeniu będziesz mieć działający program w C#, który robi to wszystko w zaledwie kilku linijkach.

> **Porada:** Ten sam wzorzec działa z większymi zestawami danych, więc możesz skalować od demonstracji 4‑elementowej do tysięcy wierszy bez zmiany logiki.

## Czego będziesz potrzebować

- .NET 6 lub nowszy (dowolny aktualny runtime .NET)
- Aspose.Cells for .NET (biblioteka udostępniająca `Workbook`, `Worksheet` itp.)
- Edytor kodu lub IDE (Visual Studio, VS Code, Rider – wybierz swój ulubiony)
- Uprawnienia do zapisu w folderze, w którym zostanie zapisany plik wyjściowy

Nie są wymagane dodatkowe pakiety NuGet poza Aspose.Cells; reszta kodu to czysty C#.

## Krok 1 – Utwórz skoroszyt Excel (główne słowo kluczowe w akcji)

Na początek tworzymy nowy obiekt `Workbook` i pobieramy pierwszy arkusz. To podstawa dla wszystkiego, co nastąpi.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates a blank Excel file in memory
        Worksheet ws = workbook.Worksheets[0];           // default sheet is named "Sheet1"
```

**Dlaczego to ważne:**  
Programowe tworzenie skoroszytu daje pełną kontrolę nad formatowaniem, formułami i wstawianiem danych, zanim cokolwiek trafi na dysk. Oznacza to również, że możesz generować pliki na serwerze bez otwierania Excela.

## Krok 2 – Wstaw formułę WRAPCOLS, aby skonwertować tablicę na macierz

`WRAPCOLS` to wbudowana funkcja Excela, która przekształca jednowymiarową tablicę w macierz o określonej liczbie kolumn. Tutaj zamieniamy `{1,2,3,4}` na układ dwukolumnowy.

```csharp
        // Step 2: Insert a WRAPCOLS formula that converts a 1‑D array into a 2‑column matrix
        ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";
```

**Jak to działa:**  
- Pierwszy argument `{1,2,3,4}` to literał tablicy inline.  
- Drugi argument `2` mówi Excelowi, aby rozłożył wartości na dwie kolumny, co daje:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |

Jeśli potrzebujesz innego kształtu, po prostu zmień drugi parametr – `WRAPCOLS({1,2,3,4,5,6},3)` da trzy kolumny.

## Krok 3 – Wymuś obliczenie skoroszytu, aby formuła się zmaterializowała

Domyślnie Aspose.Cells ocenia formuły leniwie. Aby macierz pojawiła się w pliku, wywołujemy jawnie `Calculate()`.

```csharp
        // Step 3: Force calculation so the formula result is materialized
        workbook.Calculate();   // forces evaluation of all formulas in the workbook
```

**Dlaczego wymusić obliczenie?**  
Jeśli pominiesz ten krok, zapisany plik nadal będzie zawierał formułę, ale komórki będą puste, dopóki użytkownik nie otworzy skoroszytu i nie pozwoli Excelowi na ponowne przeliczenie. W zautomatyzowanych pipeline’ach zazwyczaj chcesz, aby wartości były już wstawione.

## Krok 4 – Zapisz skoroszyt jako XLSX (drugie słowo kluczowe włączone)

Teraz, gdy dane są gotowe, zapisujemy skoroszyt na dysku. Metoda `Save` automatycznie wykrywa format pliku na podstawie rozszerzenia.

```csharp
        // Step 4: (Optional) Save the workbook to inspect the result
        string outputPath = @"C:\Temp\output.xlsx";   // adjust folder as needed
        workbook.Save(outputPath);                    // creates a .xlsx file on disk
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Po otwarciu `output.xlsx` zobaczysz macierz ułożoną dokładnie tak, jak pokazano wcześniej. Nie są potrzebne żadne dodatkowe kroki.

![przykład tworzenia skoroszytu Excel pokazujący macierz wygenerowaną przez WRAPCOLS](/images/create-excel-workbook.png)

*Tekst alternatywny obrazu: „przykład tworzenia skoroszytu Excel pokazujący macierz wygenerowaną przez WRAPCOLS”*

## Bonus: Konwersja większych tablic – przypadki użycia w rzeczywistości

Wyobraź sobie, że otrzymujesz płaską listę JSON z 100 liczbami z API i potrzebujesz ich w tabeli o 10 kolumnach. Możesz ponownie użyć tego samego wzorca:

```csharp
int[] numbers = Enumerable.Range(1, 100).ToArray();
string arrayLiteral = "{" + string.Join(",", numbers) + "}";
ws.Cells["A1"].Formula = $"=WRAPCOLS({arrayLiteral},10)";
workbook.Calculate();
```

**Przypadki brzegowe, na które warto zwrócić uwagę**

- **Zbyt wiele kolumn:** Excel ogranicza liczbę kolumn do 16 384. Jeśli poprosisz WRAPCOLS o więcej, funkcja zwróci błąd `#VALUE!`.
- **Dane nienumeryczne:** WRAPCOLS działa także z tekstem, ale musisz otoczyć ciągi podwójnymi cudzysłowami w literalnej tablicy (np. `{"Apple","Banana","Cherry"}`).
- **Wydajność:** Przy bardzo dużych tablicach budowanie łańcucha literału może stać się wąskim gardłem. W takich przypadkach rozważ bezpośrednie zapisywanie wartości do komórek zamiast używania formuły.

## Najczęściej zadawane pytania (FAQ)

**Czy to działa w starszych wersjach Excela?**  
Tak. `WRAPCOLS` został wprowadzony w Excel 365 i Excel 2019, ale Aspose.Cells może go emulować dla starszych formatów plików (np. `.xls`). Powstały plik nadal się otworzy, choć formuła może wyświetlić się jako zwykły tekst, jeśli przeglądarka jej nie obsługuje.

**Co zrobić, jeśli chcę zachować formułę do późniejszych aktualizacji?**  
Po prostu pomiń wywołanie `workbook.Calculate()`. Zapisany plik zachowa formułę `WRAPCOLS`, umożliwiając użytkownikom edycję źródłowej tablicy i automatyczną aktualizację macierzy.

**Czy mogę zastosować stylizację po pojawieniu się macierzy?**  
Oczywiście. Po `Calculate()` możesz odwołać się do wypełnionego zakresu (`A1:B2` w demonstracji) i zastosować czcionki, obramowania lub formaty liczb tak, jak w każdym innym zakresie komórek.

## Pełny działający przykład – gotowy do kopiowania i wklejenia

Poniżej znajduje się kompletny program, który możesz wkleić do aplikacji konsolowej i uruchomić od razu (pamiętaj tylko o dodaniu pakietu NuGet Aspose.Cells).

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Insert WRAPCOLS formula to convert a 1‑D array into a 2‑column matrix
        ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";

        // 3️⃣ Force calculation so the result is materialized
        workbook.Calculate();

        // 4️⃣ Save the workbook as XLSX
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"✅ Workbook created and saved to {outputPath}");
    }
}
```

**Oczekiwany wynik:**  
- Plik `output.xlsx` w lokalizacji `C:\Temp\`.  
- Komórki `A1:B2` wypełnione wartościami `1, 2, 3, 4` rozmieszczonymi w dwóch kolumnach.  
- Brak pozostałych formuł, jeśli wywołałeś `Calculate()`; w przeciwnym razie formuła pozostanie widoczna.

## Kolejne kroki – rozszerzanie rozwiązania

Teraz, gdy wiesz **jak używać WRAPCOLS**, możesz eksplorować:

1. **Dynamiczne liczby kolumn** – oblicz liczbę kolumn na podstawie rozmiaru danych (`Math.Ceiling(array.Length / desiredRows)`).
2. **Wiele arkuszy** – powtórz wzorzec na różnych arkuszach, aby stworzyć raport wielokartkowy.
3. **Automatyzacja stylizacji** – zastosuj style tabel, formatowanie warunkowe lub wykresy do wygenerowanej macierzy.
4. **Eksport do innych formatów** – Aspose.Cells może także zapisywać jako CSV, PDF czy nawet HTML, jeśli musisz udostępnić dane poza Excelem.

Te rozszerzenia zachowują podstawową ideę — **utwórz skoroszyt Excel**, **konwertuj tablicę na macierz**, **wymuś obliczenie skoroszytu**, i **zapisz skoroszyt jako XLSX** — jednocześnie dodając praktyczne udoskonalenia.

---

**Podsumowanie:** Masz teraz zwięzły, w pełni funkcjonalny sposób na stworzenie pliku Excel, przekształcenie płaskich danych przy użyciu `WRAPCOLS`, zapewnienie, że wartości zostaną obliczone, i zapisanie wyniku na dysku. Pobierz kod, zmodyfikuj tablicę i niech Twój kolejny eksport danych będzie pestką. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}