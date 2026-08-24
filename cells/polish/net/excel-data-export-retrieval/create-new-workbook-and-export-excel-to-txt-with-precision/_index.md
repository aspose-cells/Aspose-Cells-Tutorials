---
category: general
date: 2026-02-15
description: Utwórz nowy skoroszyt i wyeksportuj Excel do TXT, ustawiając precyzję
  numeryczną. Dowiedz się, jak ustawić znaczące cyfry i ograniczyć liczbę znaczących
  cyfr w C#.
draft: false
keywords:
- create new workbook
- export excel to txt
- set significant digits
- limit significant digits
- set numeric precision
language: pl
og_description: Utwórz nowy skoroszyt i wyeksportuj Excel do TXT, ustawiając istotne
  cyfry dla precyzji numerycznej. Przewodnik krok po kroku w C#.
og_title: Utwórz nowy skoroszyt – Eksportuj Excel do TXT z precyzją
tags:
- C#
- Aspose.Cells
- Excel automation
title: Utwórz nowy skoroszyt i wyeksportuj Excel do TXT z precyzją
url: /pl/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz nowy skoroszyt – Eksportuj Excel do TXT z precyzyjnym formatowaniem liczb

Zastanawiałeś się kiedyś, jak **create new workbook** obiekty w C# i natychmiast zapisać je do pliku tekstowego? Nie jesteś jedyny. W wielu scenariuszach pipeline danych musimy **export Excel to TXT**, zachowując czytelność liczb, co oznacza ograniczenie liczby cyfr po przecinku.  

W tym samouczku przeprowadzimy Cię przez cały proces: od utworzenia nowego skoroszytu, przez skonfigurowanie eksportu tak, aby **sets significant digits** (czyli ograniczanie istotnych cyfr), aż po zapisanie pliku na dysku. Po zakończeniu będziesz mieć gotowy fragment kodu, który spełnia Twoje wymagania dotyczące **numeric precision** — bez dodatkowych bibliotek, bez magii.

> **Pro tip:** Jeśli już używasz Aspose.Cells, klasy pokazane poniżej są częścią tej biblioteki. Jeśli pracujesz na innej platformie, koncepcje nadal mają zastosowanie; po prostu zamień wywołania API.

---

## Czego będziesz potrzebować

- .NET 6+ (kod kompiluje się zarówno na .NET Core, jak i .NET Framework)  
- Aspose.Cells for .NET (bezpłatna wersja próbna lub licencjonowana) – zainstaluj przez NuGet: `dotnet add package Aspose.Cells`  
- Dowolne IDE, które lubisz (Visual Studio, Rider, VS Code)  

To wszystko. Bez dodatkowych plików konfiguracyjnych, bez ukrytych kroków.

---

## Krok 1: Utwórz nowy skoroszyt

Pierwszą rzeczą jest **create new workbook**. Pomyśl o klasie `Workbook` jako o pustym pliku Excel, czekającym na arkusze, komórki i dane.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a fresh workbook – this is the core of create new workbook logic
        Workbook workbook = new Workbook();

        // (Optional) Add some sample data so you can see the effect of numeric precision later
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);
```

> **Dlaczego to ważne:** Rozpoczynając od czystego skoroszytu, unikasz ukrytego formatowania, które mogłoby zakłócić ustawienia precyzji później.

---

## Krok 2: Skonfiguruj opcje zapisu tekstu – Ustaw istotne cyfry

Teraz informujemy Aspose.Cells, ile **significant digits** chcemy przy zapisie do pliku `.txt`. Klasa `TxtSaveOptions` udostępnia właściwość `SignificantDigits`, która robi dokładnie to.

```csharp
        // Step 2: Prepare save options – limit numeric precision to 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            // This limits the output to 5 digits that matter, rounding the rest
            SignificantDigits = 5
        };
```

> **Wyjaśnienie:** `SignificantDigits = 5` oznacza, że eksporter zachowa najważniejsze pięć cyfr każdej liczby, niezależnie od położenia przecinka dziesiętnego. To wygodny sposób na **set numeric precision** bez ręcznego formatowania każdej komórki.

---

## Krok 3: Zapisz skoroszyt jako plik tekstowy

Mając gotowy skoroszyt i opcje, w końcu **export Excel to txt**. Metoda `Save` przyjmuje ścieżkę pliku oraz obiekt opcji, który właśnie skonfigurowaliśmy.

```csharp
        // Step 3: Write the workbook out as a TXT file using our precision settings
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        System.Console.WriteLine($"Workbook exported to {outputPath} with 5 significant digits.");
    }
}
```

Uruchomienie programu generuje plik, który wygląda tak:

```
12346
0.00012346
3.1416
```

Zauważ, że każda liczba respektuje regułę **limit significant digits**, którą ustawiliśmy wcześniej.

---

## Krok 4: Zweryfikuj wynik (opcjonalnie, ale zalecane)

Łatwo otworzyć wygenerowany `numbers.txt` w dowolnym edytorze, ale możesz chcieć zautomatyzować krok weryfikacji, szczególnie w pipeline'ach CI.

```csharp
        // Quick verification – read back the file and print each line
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            System.Console.WriteLine($"Line: {line}");
        }
```

Jeśli konsola wyświetli trzy powyższe linie, udało Ci się **set significant digits** i eksport działa zgodnie z zamierzeniami.

---

## Typowe pułapki i jak ich uniknąć

| Problem | Dlaczego się pojawia | Rozwiązanie |
|-------|----------------|-----|
| Liczby wyświetlane zbyt wieloma miejscami po przecinku | `SignificantDigits` pozostawiono na domyślnej wartości (0) | Jawnie ustaw `SignificantDigits` na żądaną liczbę |
| Tworzony jest pusty plik | Skoroszyt nie otrzymał żadnych danych przed zapisem | Wypełnij komórki **przed** wywołaniem `Save` |
| Ścieżka pliku rzuca `UnauthorizedAccessException` | Próba zapisu do chronionego folderu | Użyj folderu, do którego masz uprawnienia zapisu (np. `C:\Temp` lub `%USERPROFILE%\Documents`) |
| Precyzja wydaje się nieprawidłowa dla bardzo małych liczb | Liczba istotnych cyfr obejmuje wiodące zera po przecinku | Pamiętaj, że „istotne” pomija wiodące zera; 0.000123456 przy 5 cyfrach staje się `0.00012346` |

---

## Pełny działający przykład (gotowy do kopiowania i wklejenia)

Poniżej znajduje się kompletny, samodzielny program. Wklej go do nowego projektu konsolowego i naciśnij **Run**.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Populate with sample numbers
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);

        // 2️⃣ Set up export options – limit significant digits to 5
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5
        };

        // 3️⃣ Export to TXT
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        Console.WriteLine($"✅ Export completed: {outputPath}");
        Console.WriteLine("🔎 Verifying content:");
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            Console.WriteLine($"   {line}");
        }
    }
}
```

**Oczekiwany wynik w konsoli**

```
✅ Export completed: C:\Temp\numbers.txt
🔎 Verifying content:
   12346
   0.00012346
   3.1416
```

A plik `numbers.txt` będzie zawierał trzy linie pokazane powyżej.

---

## Kolejne kroki: wyjście poza podstawy

- **Export other formats** – Aspose.Cells obsługuje także CSV, HTML i PDF. W razie potrzeby zamień `TxtSaveOptions` na `CsvSaveOptions` lub `PdfSaveOptions`.  
- **Dynamic precision** – możesz obliczyć `SignificantDigits` w czasie wykonywania na podstawie danych wejściowych użytkownika lub plików konfiguracyjnych.  
- **Multiple worksheets** – iteruj po `workbook.Worksheets` i eksportuj każdy arkusz do własnego pliku `.txt`.  
- **Localization** – kontroluj separator dziesiętny (`.` vs `,`) za pomocą `CultureInfo`, jeśli musisz dopasować ustawienia regionalne.  

Wszystkie te rozszerzenia nadal opierają się na głównej idei, którą omówiliśmy: **create new workbook**, skonfiguruj eksport i **set numeric precision**, aby dopasować je do wymagań raportowania.

---

## Podsumowanie

Użyliśmy nowej instancji **create new workbook**, wypełniliśmy ją danymi i pokazaliśmy, jak **export Excel to TXT**, jednocześnie **setting significant digits**, aby ograniczyć precyzję wyjścia. Pełny przykład działa od razu, a wyjaśnienie obejmuje *dlaczego* każda linia jest potrzebna, abyś mógł dostosować go do własnych projektów.

Śmiało eksperymentuj — zmień wartość `SignificantDigits`, dodaj więcej arkuszy lub zmień format wyjściowy. Jeśli napotkasz problem, sprawdź dokumentację Aspose.Cells lub zostaw komentarz poniżej. Szczęśliwego kodowania!

---

![Create new workbook example](/images/create-new-workbook.png "Screenshot showing a C# IDE with the create new workbook code")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}