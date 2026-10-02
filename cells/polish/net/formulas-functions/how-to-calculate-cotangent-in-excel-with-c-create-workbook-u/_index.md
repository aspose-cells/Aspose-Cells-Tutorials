---
category: general
date: 2026-05-04
description: Jak obliczyć cotangens podczas tworzenia skoroszytu Excel w C#. Dowiedz
  się, jak używać funkcji EXPAND, zapisywać skoroszyt i automatyzować obliczenia.
draft: false
keywords:
- how to calculate cotangent
- create excel workbook
- how to use expand
- how to save workbook
- use expand function
language: pl
og_description: Jak obliczyć cotangens w Excelu przy użyciu C#. Ten tutorial pokazuje,
  jak utworzyć skoroszyt Excela, użyć funkcji EXPAND i zapisać plik.
og_title: Jak obliczyć cotangens w Excelu – Kompletny przewodnik po skoroszycie C#
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Jak obliczyć cotangens w Excelu przy użyciu C# – Utwórz skoroszyt, użyj funkcji
  EXPAND i zapisz
url: /pl/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak obliczyć cotangens w Excelu przy użyciu C# – Kompletny przewodnik

Zastanawiałeś się kiedyś **jak obliczyć cotangens** bezpośrednio w pliku Excel generowanym przez C#? Być może tworzysz model finansowy, raport naukowy lub po prostu automatyzujesz nudne zadanie w arkuszu kalkulacyjnym. Dobra wiadomość? Można to zrobić w kilku linijkach kodu — bez ręcznych formuł, bez kopiowania‑wklejania.

W tym tutorialu przejdziemy przez tworzenie skoroszytu Excel, rozszerzanie tablicy przy pomocy funkcji **EXPAND**, wstawianie formuły **COT** do obliczenia cotangensa 45°, a na koniec zapisanie pliku, aby móc otworzyć go w Excelu i zobaczyć wyniki. Po drodze omówimy także **jak używać expand**, **jak zapisać skoroszyt** oraz kilka przydatnych wskazówek, które często są pomijane.

> **Szybka odpowiedź:** Użyj Aspose.Cells (lub Microsoft Interop), aby utworzyć skoroszyt, ustaw `ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"`, ustaw `ws.Cells["B1"].Formula = "=COT(PI()/4)"`, a następnie wywołaj `workbook.Save("output.xlsx")`.

---

## Co będzie potrzebne

- **.NET 6+** (lub dowolny nowoczesny runtime .NET).  
- **Aspose.Cells for .NET** (wersja trial lub licencjonowana).  
- Podstawowa znajomość składni C#.  
- Visual Studio, Rider lub dowolny edytor, którego używasz.

Nie są wymagane dodatkowe dodatki do Excela; wszystko działa po stronie serwera, a wygenerowany plik działa w każdej współczesnej wersji Excela.

---

## Krok 1: Utwórz skoroszyt Excel z C#

Utworzenie skoroszytu to podstawa. Pomyśl o tym jak o otwarciu czystego notatnika przed rozpoczęciem pisania.

```csharp
using Aspose.Cells;

// Step 1: Initialize a new workbook object
Workbook workbook = new Workbook();               // Empty workbook
Worksheet ws = workbook.Worksheets[0];            // Grab the first sheet
```

**Dlaczego to ważne:**  
`Workbook` reprezentuje cały pakiet `.xlsx`. Domyślnie zawiera jeden arkusz, do którego odwołujemy się przez `Worksheets[0]`. Jeśli później potrzebujesz więcej arkuszy, możesz dodać je metodą `workbook.Worksheets.Add()`.

> **Pro tip:** Jeśli tworzysz aplikację na .NET Core, upewnij się, że pakiet NuGet Aspose.Cells jest zgodny z Twoim środowiskiem uruchomieniowym, aby uniknąć brakujących zależności natywnych.

---

## Krok 2: Użyj funkcji EXPAND, aby wypełnić kolumnę  

Funkcja **EXPAND** to sposób Excela na przekształcenie statycznej tablicy w dynamiczny zakres. Idealna, gdy chcesz wygenerować kolumnę wartości bez ręcznego wpisywania każdej komórki.

```csharp
// Step 2: Write an EXPAND formula in cell A1
ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"; // Expands to a 5‑row column
```

### Jak to działa  

- `{1,2,3}` to tablica źródłowa (trzy liczby).  
- `5` mówi Excelowi, aby wyprodukował **5 wierszy**.  
- `1` mówi Excelowi, aby wyprodukował **1 kolumnę**.  

Po otwarciu zapisanego pliku komórki od A1 do A5 będą zawierały `1, 2, 3, 0, 0` (dodatkowe wiersze wypełnione zerami).  

**Przypadek brzegowy:** Jeśli argument `rows` jest mniejszy niż długość tablicy źródłowej, Excel obcina tablicę. Tak więc `=EXPAND({1,2,3},2,1)` pokaże tylko `1` i `2`.

---

## Krok 3: Wstaw formułę COT, aby obliczyć cotangens  

Teraz gwiazda programu: **jak obliczyć cotangens** w Excelu. Funkcja `COT` przyjmuje kąt w radianach, więc podajemy jej `PI()/4` (co równa się 45°).

```csharp
// Step 3: Write a COT formula in cell B1
ws.Cells["B1"].Formula = "=COT(PI()/4)"; // Returns 1
```

### Dlaczego używać COT zamiast TAN?  

Cotangens jest odwrotnością tangensa (`cot = 1 / tan`). Można by napisać `=1/TAN(PI()/4)`, ale użycie `COT` jest czytelniejsze i unika błędów dzielenia przez zero, gdy kąt wynosi 0° lub 180°.

**Oczekiwany wynik:** Po otwarciu `output.xlsx` w komórce B1 pojawi się `1`, ponieważ cotangens 45° (π/4 radiana) wynosi 1.

**A co jeśli potrzebuję stopni?**  
Funkcje trygonometryczne w Excelu działają w radianach. Przelicz stopnie przy pomocy `RADIANS(deg)`. Przykład: `=COT(RADIANS(60))`.

---

## Krok 4: Zapisz skoroszyt, aby móc zobaczyć wyniki  

Zapis to ostatni element układanki. Możesz zapisać plik w dowolnym folderze, do którego masz prawo zapisu.

```csharp
// Step 4: Persist the workbook to disk
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "output.xlsx");

// Save the workbook (the default format is .xlsx)
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### Jak zapisywać w różnych formatach  

- **XLS** – `workbook.Save("output.xls", SaveFormat.Excel97To2003);`  
- **CSV** – `workbook.Save("output.csv", SaveFormat.CSV);`  

Jeśli kiedykolwiek będziesz musiał strumieniować plik (np. w API webowym), użyj `workbook.Save(stream, SaveFormat.Xlsx)`.

---

## Pełny działający przykład  

Łącząc wszystko razem, oto samodzielny program, który możesz skopiować i wkleić do aplikacji konsolowej.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Expand an array {1,2,3} into a 5‑row column starting at A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // 3️⃣ Calculate cotangent of 45° (π/4) in B1
        ws.Cells["B1"].Formula = "=COT(PI()/4)";

        // 4️⃣ Define where to save the file (Desktop for easy access)
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "output.xlsx");

        // 5️⃣ Save the workbook
        workbook.Save(outputPath);
        Console.WriteLine($"✅ Workbook saved at: {outputPath}");
    }
}
```

**Weryfikacja wyniku:**  
- Otwórz `output.xlsx`.  
- Kolumna A powinna zawierać `1, 2, 3, 0, 0`.  
- Komórka B1 powinna wyświetlać `1`.  

Jeśli zobaczysz te wartości, udało Ci się opanować **jak obliczyć cotangens** programistycznie oraz **jak tworzyć skoroszyt Excel**, **używać funkcji expand** i **zapisywać skoroszyt** — wszystko w jednym kroku.

---

## Częste pytania i pułapki  

### Czy `COT` działa w starszych wersjach Excela?  
Tak, `COT` istnieje od Excela 2007. Jeśli celujesz w Excel 2003 (`.xls`), musisz zastąpić ją wyrażeniem `1/TAN(...)`, ponieważ `COT` nie jest tam dostępny.

### Co zrobić, gdy formuła nie przelicza się automatycznie?  
Aspose.Cells ocenia formuły leniwie. Wywołaj `workbook.CalculateFormula()` przed zapisem, jeśli potrzebujesz, aby obliczone wartości były zapisane w pliku.

```csharp
workbook.CalculateFormula();
workbook.Save(outputPath);
```

### Czy mogę zapisać wynik od razu, bez formuły?  
Oczywiście, możesz obliczyć wartość w C# (`Math.Cos(Math.PI / 4) / Math.Sin(Math.PI / 4)`) i przypisać ją do `ws.Cells["B1"].Value = result;`. Tutorial skupia się na formułach Excel, ponieważ pozostają dynamiczne — zmiana kąta później automatycznie aktualizuje wynik.

---

## Pro tipy dla projektów produkcyjnych  

- **Operacje wsadowe:** Jeśli wypełniasz tysiące wierszy, wyłącz obliczenia (`workbook.Settings.CalculateFormulaOnOpen = false`) podczas zapisu, a po zakończeniu włącz je ponownie.  
- **Nazwane zakresy:** Użyj `ws.Cells.CreateRange("MyArray", "A1:A5")` i odwołuj się do nazwy w formułach, aby arkusz był czytelniejszy.  
- **Obsługa błędów:** Otocz `workbook.Save` blokiem try/catch, aby wyłapać problemy z uprawnieniami (`UnauthorizedAccessException`).

---

## Zakończenie  

Omówiliśmy **jak obliczyć cotangens** w arkuszu Excel generowanym przez C#, pokazaliśmy **jak używać expand** do wypełniania kolumny oraz **jak zapisać skoroszyt** do natychmiastowego podglądu. Pełny, gotowy do uruchomienia przykład powyżej daje solidne podstawy do automatyzacji dowolnego arkusza, który łączy statyczne dane z obliczeniami trygonometrycznymi.

Co dalej? Spróbuj zamienić kąt w formule `COT` na odwołanie do komórki (`=COT(PI()*A1/180)`), aby użytkownicy mogli wprowadzać stopnie. Albo eksploruj inne funkcje matematyczne, takie jak `SIN`, `COS` i `ATAN2` — działają w ten sam sposób w wygenerowanym skoroszycie.

Miłego kodowania i niech Twoje arkusze będą wolne od błędów! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}