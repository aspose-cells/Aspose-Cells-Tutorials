---
category: general
date: 2026-03-30
description: Dowiedz się, jak formatować liczbę z separatorem przy użyciu Aspose.Cells
  w C#. Zawiera ustawianie własnego formatu liczby, dodawanie separatora tysięcy,
  formatowanie miejsc dziesiętnych oraz sposób formatowania komórki.
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: pl
og_description: Formatuj liczbę z separatorem w C#. Ten przewodnik pokazuje, jak ustawić
  własny format liczby, dodać separator tysięcy, sformatować miejsca dziesiętne oraz
  jak sformatować komórkę przy użyciu Aspose.Cells.
og_title: Formatowanie liczb z separatorem w C# – Poradnik Aspose.Cells
tags:
- C#
- Aspose.Cells
- Number Formatting
title: Formatowanie liczb z separatorem w C# – Kompletny przewodnik Aspose.Cells
url: /pl/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formatuj liczbę z separatorem w C# – Kompletny przewodnik Aspose.Cells

Kiedykolwiek potrzebowałeś **formatować liczbę z separatorem** w arkuszu kalkulacyjnym, ale nie byłeś pewien, którego wywołania API użyć? Nie jesteś jedyny — programiści nieustannie zmagają się z separatorami tysięcy, miejscami dziesiętnymi i niestandardowymi wzorcami przy eksportowaniu danych.  

Dobre wieści: Aspose.Cells sprawia, że to dziecinnie proste. W tym samouczku przeprowadzimy Cię przez praktyczny przykład, który **ustawia niestandardowy format liczby**, **dodaje separator tysięcy**, **formatuje miejsca dziesiętne** i pokazuje **jak formatować komórkę** jako ciąg znaków. Po zakończeniu będziesz mieć gotowy fragment kodu, który możesz wkleić do dowolnego projektu .NET.

## Co obejmuje ten przewodnik

* Dokładny pakiet NuGet, którego potrzebujesz, oraz sposób jego instalacji.  
* Krok po kroku kod, który tworzy skoroszyt, zapisuje wartość liczbową i stosuje niestandardowy format.  
* Dlaczego `ExportTableOptions.ExportAsString` jest preferowanym sposobem pobierania sformatowanej wartości.  
* Typowe pułapki — np. zapomnienie o włączeniu `ExportAsString` lub użycie niewłaściwej maski formatowania.  
* Jak dostosować maskę formatu, jeśli potrzebujesz innej liczby miejsc dziesiętnych lub innego stylu separatora.  

Nie są potrzebne żadne zewnętrzne linki do dokumentacji; wszystko, czego potrzebujesz, znajduje się tutaj. Zanurzmy się.

---

## Prerequisites

| Wymaganie | Powód |
|-------------|--------|
| .NET 6.0 lub nowszy | Aspose.Cells 23.10+ celuje w .NET Standard 2.0+, więc .NET 6 jest bezpieczny i aktualny. |
| Visual Studio 2022 (lub dowolne IDE C#) | Ułatwia debugowanie i zarządzanie pakietami. |
| Aspose.Cells for .NET NuGet package | Dostarcza klasy `Workbook`, `Worksheet` i `ExportTableOptions`, których użyjemy. |

Możesz zainstalować pakiet za pomocą konsoli Menedżera Pakietów:

```powershell
Install-Package Aspose.Cells
```

To wszystko — żadnych dodatkowych DLL, żadnego COM interop, tylko pojedyncze odwołanie NuGet.

---

## Krok 1: Inicjalizacja nowego skoroszytu (Jak formatować komórkę)

Pierwszą rzeczą, którą robimy, jest stworzenie nowej instancji `Workbook`. Traktuj to jak pusty plik Excel gotowy do przyjęcia danych.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Dlaczego to ważne:** `Workbook` jest punktem wejścia dla każdej operacji w Aspose.Cells. Pobierając pierwszą arkusz (`Worksheets[0]`) uzyskujemy czyste płótno bez konieczności nadawania nazwy arkuszowi.

---

## Krok 2: Zapisz wartość liczbową w docelowej komórce

Następnie umieszczamy surową liczbę w komórce **A1**. Sama wartość nie jest jeszcze sformatowana — to po prostu typ double.

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **Wskazówka:** Używaj `PutValue` zamiast `PutString`, gdy zamierzasz później zastosować formatowanie liczbowe. To zachowuje podstawowy typ danych, umożliwiając obliczenia zgodne z Excelem.

---

## Krok 3: Ustaw niestandardowy format liczby (Dodaj separator tysięcy i formatuj miejsca dziesiętne)

Teraz przychodzi serce samouczka: definiowanie maski formatu, która mówi Aspose.Cells, jak wyświetlić liczbę. Maska `#,##0.00` robi trzy rzeczy:

1. **`#,##0`** – dodaje separator tysięcy (domyślnie przecinek).  
2. **`.00`** – wymusza dokładnie dwie miejsca dziesiętne.  

Jeśli potrzebujesz innej liczby miejsc dziesiętnych, po prostu zmień liczbę `0` po przecinku.

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **Dlaczego używamy `ExportAsString`**: Domyślnie `ExportString` zwraca surową wartość. Ustawienie `ExportAsString = true` zmusza API do zastosowania maski `NumberFormat` przed konwersją na tekst. Jest to niezbędne, gdy potrzebujesz dokładnej reprezentacji ciągu znaków dla raportów, ładunków JSON lub wyświetlania w interfejsie użytkownika.

---

## Krok 4: Eksportowanie sformatowanego tekstu (Jak formatować komórkę)

Mając gotowe opcje, wywołujemy `ExportString` na tej samej komórce. Metoda respektuje maskę, którą właśnie zdefiniowaliśmy, i zwraca ładnie sformatowany ciąg znaków.

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

Uruchomienie programu wypisuje **`12,345.68`** w konsoli — dokładnie w żądanym formacie.

> **Przypadek brzegowy:** Jeśli źródłowa liczba ma więcej niż dwie miejsca dziesiętne, maska ją zaokrągla. Jeśli potrzebujesz przycięcia zamiast zaokrąglenia, musisz wstępnie przetworzyć wartość przy użyciu `Math.Truncate` przed wywołaniem `PutValue`.

---

## Krok 5: Dostosowywanie formatu – typowe wariacje

### 5.1 Zmiana precyzji dziesiętnej

Chcesz trzy miejsca dziesiętne? Po prostu zamień maskę:

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 Użycie innego separatora tysięcy

Niektóre lokalizacje preferują spację lub kropkę. Możesz wstawić znak bezpośrednio:

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

Albo polegać na ustawieniach kultury skoroszytu:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 Prefiks lub sufiks (Waluta, Procent)

Dodaj znak dolara lub procenta bezpośrednio w masce:

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **Uwaga:** Maska jest rozróżniająca wielkość liter. `$` i `%` są symbolami literałowymi; nie wpływają na podstawową wartość liczbową.

---

## Krok 6: Pełny działający przykład (Gotowy do kopiowania i wklejenia)

Poniżej znajduje się kompletny program, który możesz skopiować do nowej aplikacji konsolowej. Zawiera wszystkie kroki, komentarze oraz weryfikację końcowego wyniku.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

Uruchom program (`dotnet run` w terminalu lub naciśnij F5 w Visual Studio) i zobaczysz sformatowaną liczbę wypisaną dokładnie tak, jak na ekranie.

---

## Najczęściej zadawane pytania (FAQ)

**P:** Czy to działa ze starszymi wersjami Excela?  
**O:** Tak. Maska formatu podąża za natywną składnią formatowania liczb w Excelu, więc każda wersja rozumiejąca `#,##0.00` wyświetli ten sam ciąg znaków.

**P:** Co zrobić, jeśli muszę sformatować zakres komórek?  
**O:** Przejdź pętlą po żądanym zakresie i zastosuj te same `ExportTableOptions` do każdej komórki, albo ustaw właściwość `Style.Custom` na zakresie i następnie wywołaj `ExportString` na jednej komórce.

**P:** Czy mogę wyeksportować bezpośrednio do CSV z zastosowanymi formatami?  
**O:** Oczywiście. Użyj `Workbook.Save("output.csv", SaveFormat.CSV);` po ustawieniu formatu w każdej komórce. Aspose.Cells respektuje `Style` komórki przy generowaniu CSV.

---

## Zakończenie

Właśnie pokazaliśmy, jak **formatować liczbę z separatorem** w C# przy użyciu Aspose.Cells, obejmując wszystko od **ustawiania niestandardowego formatu liczby** po **dodawanie separatora tysięcy**, **formatowanie miejsc dziesiętnych** oraz niezbędne **jak formatować komórkę** przy eksporcie do ciągu znaków. Kod jest w pełni samodzielny, działa z .NET 6+ i może być dostosowany do dowolnej lokalizacji lub wymagań precyzji.

Następnie możesz zbadać:

* Zastosowanie tej samej techniki do dat i godzin (`NumberFormat = "dd‑MMM‑yyyy"`).  
* Automatyzację masowych eksportów, w których każda kolumna wymaga innej maski.  
* Integrację sformatowanych ciągów znaków w raportach PDF przy użyciu Aspose.Words.

Wypróbuj je, a szybko staniesz się osobą, do której zespół zwróci się po pomoc w formatowaniu arkuszy kalkulacyjnych. Szczęśliwego kodowania!   (Image: ![Screenshot showing formatted number with separator in Aspose.Cells](image-placeholder.png){alt="Sformatowana liczba z separatorem wyświetlona w wyniku Aspose.Cells"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}