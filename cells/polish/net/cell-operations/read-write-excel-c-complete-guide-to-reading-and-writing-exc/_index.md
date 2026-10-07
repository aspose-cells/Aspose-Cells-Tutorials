---
category: general
date: 2026-03-01
description: Samouczek Read write Excel C# pokazuje, jak odczytać wartość komórki
  w Excelu i zapisać datę i godzinę do Excela przy użyciu C# oraz Aspose.Cells w kilku
  prostych krokach.
draft: false
keywords:
- read write excel c#
- read excel cell value
- write datetime to excel
- c# excel interop
- aspnet excel automation
language: pl
og_description: Samouczek Read write Excel C# wyjaśnia, jak odczytać wartość komórki
  w Excelu i zapisać datę i godzinę do Excela, z przejrzystymi przykładami kodu i
  najlepszymi praktykami.
og_title: Odczyt i zapis Excela w C# – Przewodnik krok po kroku
tags:
- C#
- Excel
- Aspose.Cells
title: Odczyt i zapis Excel w C# – Kompletny przewodnik po odczytywaniu i zapisywaniu
  komórek Excela
url: /pl/net/cell-operations/read-write-excel-c-complete-guide-to-reading-and-writing-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Read Write Excel C# – Kompletny przewodnik po odczytywaniu i zapisywaniu komórek Excel

Czy kiedykolwiek próbowałeś **read write Excel C#** i skończyło się to niejasnym wyjątkiem lub nieprawidłową datą? Nie jesteś sam. Wielu programistów napotyka problemy, gdy muszą wyciągnąć japońską datę z epoką z arkusza i następnie zapisać prawidłowy `DateTime` z powrotem do tej samej komórki.  

W tym przewodniku pokażemy dokładnie, jak **read excel cell value** i **write datetime to excel** przy użyciu C# oraz potężnej biblioteki Aspose.Cells. Po zakończeniu będziesz mieć samodzielny, gotowy do uruchomienia przykład, który możesz wkleić do dowolnego projektu .NET.

## Czego się nauczysz

- Jak zainstalować i odwołać się do Aspose.Cells w projekcie .NET 6+.  
- Dokładny kod potrzebny do pobrania komórki zawierającej japoński ciąg epoki, np. `"R3/5/12"`.  
- Jak sparsować ten ciąg do `DateTime` przy użyciu kultury `"ja-JP"`.  
- Kroki, aby umieścić otrzymany `DateTime` z powrotem w tej samej komórce arkusza.  
- Wskazówki dotyczące obsługi przypadków brzegowych, takich jak puste komórki lub nieoczekiwane formaty epok.  

Wcześniejsze doświadczenie z interop Excel nie jest wymagane — wystarczy podstawowa znajomość C# i .NET. Zaczynajmy.

![Zrzut ekranu operacji read write Excel C# pokazujący komórkę B2 przed i po konwersji](read-write-excel-csharp.png "przykład read write excel c#")

## Krok 1: Przygotowanie projektu – Podstawy Read Write Excel C#  

Zanim zanurkujemy w kod, potrzebujemy solidnych podstaw.

1. **Utwórz nową aplikację konsolową** (lub dowolny projekt .NET) targetując .NET 6 lub nowszy:

   ```bash
   dotnet new console -n ExcelEraDemo
   cd ExcelEraDemo
   ```

2. **Dodaj pakiet NuGet Aspose.Cells**. To w pełni zarządzana biblioteka, działająca bez COM interop:

   ```bash
   dotnet add package Aspose.Cells
   ```

3. **Skopiuj plik Excel** (`EraDates.xlsx`) do katalogu głównego projektu. Ten skoroszyt powinien zawierać arkusz o nazwie `"Sheet1"` z komórką **B2** zawierającą wartość taką jak `"R3/5/12"` (Reiwa 3, maj 12).

To wszystko, czego potrzebujesz do przygotowania. Reszta poradnika koncentruje się na rzeczywistej logice **read excel cell value** i **write datetime to excel**.

## Krok 2: Odczyt wartości komórki Excel w C#

Teraz, gdy projekt jest gotowy, pobierzmy ciąg z arkusza. Poniższy fragment kodu demonstruje dokładny łańcuch wywołań:

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load the workbook (adjust the path as needed)
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // assumes the sheet is named Sheet1

        // Step 2: Get the cell that holds the Japanese era date string
        // B2 contains something like "R3/5/12"
        Cell dateCell = ws.Cells["B2"];  

        // Step 3: Read the string representation from the cell
        string eraDateString = dateCell.StringValue;  

        Console.WriteLine($"Original cell value: {eraDateString}");
        // -------------------------------------------------
        // From here we’ll convert the era string to a DateTime.
        // -------------------------------------------------
    }
}
```

**Dlaczego to działa:** `Cell.StringValue` zawsze zwraca wyświetlany tekst, niezależnie od ukrytego formatu liczbowego. Gwarantuje to, że pracujemy z dokładnym ciągiem `"R3/5/12"`, który widzi użytkownik.

### Typowe pułapki

- **Puste komórki** – `StringValue` zwraca pusty ciąg. Zabezpiecz się przed tym przed parsowaniem.  
- **Nieoczekiwane formaty** – Jeśli komórka zawiera `"2023/05/12"` parser epoki rzuci wyjątek; może być potrzebny fallback.

## Krok 3: Zapis DateTime do Excela w C#

Mając już ciąg epoki, parsujemy go przy użyciu `DateTime.ParseExact`. Format `"ggyy/MM/dd"` informuje .NET, że oczekuje japońskiej epoki (`gg`), dwucyfrowego roku (`yy`) oraz komponentów miesiąca i dnia.

```csharp
        // Step 4: Convert the era date string to a DateTime using the Japanese culture
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The cell value does not match the expected Japanese era format.");
            return;
        }

        Console.WriteLine($"Parsed DateTime (UTC): {parsedDate:u}");

        // Step 5: Store the resulting DateTime back into the same cell
        dateCell.PutValue(parsedDate);

        // Optional: Apply a standard date format so Excel shows it nicely
        dateCell.SetStyle(new Style { Number = 14 }); // 14 = "m/d/yyyy"

        // Save the workbook to a new file so we don’t overwrite the original
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Workbook saved as EraDates_Converted.xlsx");
```

**Dlaczego używamy `PutValue`**: Aspose.Cells automatycznie wykrywa typ .NET i zapisuje odpowiedni typ komórki Excel. Przekazanie `DateTime` skutkuje prawdziwą datą Excel, którą można formatować lub używać w formułach.

### Przypadki brzegowe i wskazówki

- **Strefy czasowe** – Obiekty `DateTime` są przechowywane bez informacji o strefie. Jeśli potrzebujesz UTC, wywołaj `DateTime.SpecifyKind`.  
- **Fallback kultury** – Jeśli przewidujesz inne kultury, otocz parsowanie pomocnikiem, który próbuje kilku obiektów `CultureInfo`.  
- **Wydajność** – Przy przetwarzaniu tysięcy wierszy, używaj jednej instancji `CultureInfo` zamiast tworzyć nową w każdej iteracji.

## Krok 4: Pełny działający przykład – składanie wszystkiego razem

Poniżej znajduje się kompletny, gotowy do uruchomienia program. Skopiuj go do `Program.cs`, upewnij się, że `EraDates.xlsx` znajduje się obok skompilowanego pliku binarnego i uruchom `dotnet run`.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load workbook
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // Change if your sheet has a different name

        // -------------------------------------------------
        // 1️⃣ Read the Japanese era string from B2
        // -------------------------------------------------
        Cell dateCell = ws.Cells["B2"];
        string eraDateString = dateCell.StringValue?.Trim();

        if (string.IsNullOrEmpty(eraDateString))
        {
            Console.WriteLine("Cell B2 is empty. Nothing to convert.");
            return;
        }

        Console.WriteLine($"Original cell value: {eraDateString}");

        // -------------------------------------------------
        // 2️⃣ Parse the era string into a DateTime
        // -------------------------------------------------
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The value does not match the expected Japanese era format (ggyy/MM/dd).");
            return;
        }

        Console.WriteLine($"Parsed DateTime: {parsedDate:u}");

        // -------------------------------------------------
        // 3️⃣ Write the DateTime back into the same cell
        // -------------------------------------------------
        dateCell.PutValue(parsedDate);

        // Apply a friendly date format (e.g., 2023/05/12)
        Style style = wb.CreateStyle();
        style.Number = 14; // Built‑in date format
        dateCell.SetStyle(style);

        // Save the updated workbook
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Conversion complete – saved as EraDates_Converted.xlsx");
    }
}
```

**Oczekiwany wynik**

```
Original cell value: R3/5/12
Parsed DateTime: 2021-05-12 00:00:00Z
Conversion complete – saved as EraDates_Converted.xlsx
```

Po otwarciu `EraDates_Converted.xlsx` komórka **B2** wyświetla zwykłą datę (np. `5/12/2021`) i może być używana w obliczeniach Excel tak jak każda inna wartość datowa.

## Profesjonalne wskazówki dla solidnego kodu Read Write Excel C#  

- **Waliduj przed zapisem** – Użyj `Cell.IsFormula` lub `Cell.Type`, aby nie nadpisać przypadkowo formuł.  
- **Przetwarzanie wsadowe** – Jeśli musisz skonwertować całą kolumnę, iteruj przez `ws.Cells.Columns[1]` (kolumna B) i zastosuj tę samą logikę.  
- **Bezpieczeństwo wątków** – Obiekty Aspose.Cells nie są bezpieczne wątkowo; twórz osobne instancje `Workbook` dla każdego wątku przy równoległym przetwarzaniu.  
- **Logowanie** – W skryptach produkcyjnych zamień `Console.WriteLine` na właściwy logger (np. Serilog), aby rejestrować niepowodzenia parsowania.  
- **Testowanie** – Napisz testy jednostkowe, które podają znane ciągi epok do metody pomocniczej i sprawdzają otrzymane wartości `DateTime`.

## Zakończenie

Właśnie opanowałeś **read write Excel C#**, ucząc się, jak **read excel cell value**, sparsować japoński ciąg epoki i **write datetime to excel** z pewnością. Pełny przykład demonstruje czysty, end‑to‑end przepływ, który możesz dostosować do operacji masowych, innych kultur lub nawet potoków Excel‑do‑bazy danych.

Co dalej? Spróbuj rozszerzyć skrypt, aby przetwarzał całą kolumnę dat epok, lub zbadaj bogate opcje formatowania Aspose.Cells, aby stylizować komórki wyjściowe. Możesz także poeksperymentować z innymi bibliotekami, takimi jak EPPlus lub ClosedXML — większość logiki pozostaje taka sama, zmieniają się jedynie wywołania API.

Masz pytania lub trudny scenariusz Excel? zostaw komentarz poniżej, i powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}