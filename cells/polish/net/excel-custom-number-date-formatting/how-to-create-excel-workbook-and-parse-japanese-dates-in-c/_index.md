---
category: general
date: 2026-10-10
description: Utwórz skoroszyt Excel w C# i ustaw wartość komórki na datę w japońskim
  erze, następnie zastosuj niestandardowy format i odczytaj komórkę daty przy użyciu
  Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set cell value
- apply custom format
- read date cell
- excel date parsing
language: pl
lastmod: 2026-10-10
og_description: Utwórz skoroszyt Excel w C# i analizuj daty w japońskich erach. Dowiedz
  się, jak ustawić wartość komórki, zastosować niestandardowy format i odczytać komórkę
  z datą przy użyciu Aspose.Cells.
og_image_alt: Screenshot showing a C# program that creates an Excel workbook and parses
  a Japanese era date
og_title: Utwórz skoroszyt Excel w C# – pełny przewodnik po parsowaniu dat
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and set cell value with a Japanese era
    date, then apply custom format and read date cell using Aspose.Cells.
  headline: How to create Excel workbook and parse Japanese dates in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: Jak utworzyć skoroszyt Excel i parsować japońskie daty w C#
url: /pl/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć skoroszyt Excel i parsować japońskie daty w C#

Jeśli potrzebujesz **create Excel workbook** od podstaw, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Nauczysz się **set cell value** przy użyciu ciągu daty w japońskiej erze, **apply custom format**, który rozumie erę, oraz w końcu **read date cell**, aby uzyskać .NET `DateTime`. Pełny przykład działa z najnowszą wersją Aspose.Cells for .NET, więc możesz skopiować‑wkleić kod do dowolnego projektu C#.

Praca z datami zawierającymi japońskie ery może być trudna, ponieważ domyślny parser Excela nie rozpoznaje symboli er. Używając własnego formatu liczbowego (`[ja-JP-Era]`) informujesz Excel, jak interpretować ciąg znaków, co umożliwia niezawodne **excel date parsing**. Poniższe kroki obejmują cały przepływ pracy, od tworzenia skoroszytu po wyodrębnienie daty.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również na .NET Framework 4.7+)
- Aspose.Cells for .NET (pakiet NuGet `Aspose.Cells`)
- Podstawowa znajomość C# oraz Visual Studio lub dowolnego wybranego IDE

## Krok 1: Create Excel workbook i dodaj arkusz

Pierwszą operacją jest **create Excel workbook** w pamięci. Aspose.Cells automatycznie tworzy domyślny arkusz, ale w razie potrzeby możesz dodać kolejne.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Optional: rename the default worksheet for clarity
        workbook.Worksheets[0].Name = "Dates";
```

Tworzenie skoroszytu alokuje wewnętrzne struktury, które później przechowują komórki, style i formuły. Na tym etapie nie jest zapisywany żaden plik, co utrzymuje operację szybką i testowalną.

## Krok 2: Set cell value przy użyciu ciągu daty w japońskiej erze

Następnie **set cell value** na reprezentację japońskiej ery `"R5-04-01"` (Reiwa 5, 1 kwietnia). Ciąg podąża za wzorcem `EraYear-MM-DD`.

```csharp
        // Step 2: Reference cell A1 on the first worksheet
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Put the Japanese era date string into the cell
        dateCell.PutValue("R5-04-01");
```

Użycie `PutValue` zapisuje surowy tekst. Excel potraktuje go jako ciąg znaków, dopóki format liczbowy nie wskaże inaczej. To podejście działa dla dowolnej niestandardowej reprezentacji kalendarza, nie tylko japońskich er.

## Krok 3: Apply custom format, który rozumie japońską erę

Teraz **apply custom format**, aby Excel mógł przetłumaczyć ciąg ery na rzeczywistą datę seryjną. Format `[ja-JP-Era]yyyy/MM/dd` instruuje silnik, aby interpretował wiodący znak ery (`R` dla Reiwa) i obliczał datę gregoriańską.

```csharp
        // Step 3: Apply a custom number format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";
```

Niestandardowy format jest przechowywany w obiekcie stylu komórki. Aspose.Cells respektuje ten format zarówno podczas renderowania, jak i konwersji wartości, umożliwiając niezawodne **excel date parsing** później w potoku.

## Krok 4: Retrieve the parsed DateTime value from the cell

Wreszcie **read date cell**, aby uzyskać .NET `DateTime`. Właściwość `DateTimeValue` zwraca przeliczoną wartość na podstawie wcześniej zastosowanego niestandardowego formatu.

```csharp
        // Step 4: Retrieve the parsed DateTime value
        DateTime parsedDate = dateCell.DateTimeValue;

        // Output the result to the console for verification
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
```

Gdy program zostanie uruchomiony, konsola wypisze:

```
Parsed Gregorian date: 2023-04-01
```

Wynik potwierdza, że ciąg japońskiej ery `"R5-04-01"` został poprawnie zinterpretowany jako 1 kwietnia 2023.

## Pełny, gotowy do uruchomienia przykład

Połączenie wszystkich elementów daje samodzielny program, który możesz od razu skompilować i uruchomić.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Reference cell A1
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Insert Japanese era date string
        dateCell.PutValue("R5-04-01");

        // Apply custom format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";

        // Retrieve the parsed DateTime
        DateTime parsedDate = dateCell.DateTimeValue;

        // Show the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");

        // (Optional) Save the workbook to verify the visual format
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

Uruchomienie programu tworzy plik `JapaneseEraDate.xlsx` z komórką A1 wyświetlającą `2023/04/01`, podczas gdy konsola pokazuje tę samą datę gregoriańską. Plik można otworzyć w Excelu, aby zobaczyć sformatowaną wartość.

## Dlaczego to podejście działa

- **create excel workbook** – Instancjonowanie `Workbook` buduje pełną strukturę pliku Excel w pamięci, nie dotykając dysku.
- **set cell value** – `PutValue` zapisuje surowy tekst, co jest konieczne przed zastosowaniem formatu specyficznego dla kultury.
- **apply custom format** – Token `[ja-JP-Era]` mostkuje lukę między notacją ery a wewnętrznym systemem dat seryjnych Excela.
- **read date cell** – `DateTimeValue` automatycznie używa stylu komórki do konwersji, dostarczając natywny `DateTime`.
- **excel date parsing** – Przekazując parsowanie do stylu komórki, unikasz ręcznej manipulacji ciągami, zmniejszając liczbę błędów i poprawiając obsługę lokalizacji.

## Edge cases i praktyczne wskazówki

- **Different eras** – Użyj `S` dla Showa, `H` dla Heisei, `R` dla Reiwa. Ten sam ciąg formatu działa dla wszystkich er.
- **Invalid strings** – Jeśli komórka zawiera nieprawidłową datę w erze, `DateTimeValue` zwraca `DateTime.MinValue`. Sprawdź `dateCell.IsDate` przed odczytem.
- **Multiple cells** – Zastosuj niestandardowy format do całego zakresu (`range.ApplyStyle(style)`), gdy potrzebujesz parsować wiele dat.
- **Performance** – Ustawienie stylu raz na kolumnę jest szybsze niż na każdą komórkę w dużych arkuszach.
- **Saving options** – Aspose.Cells może eksportować do XLSX, XLS, CSV lub PDF. Wybierz format pasujący do dalszego przetwarzania.

## Frequently asked questions

**Czy mogę użyć wbudowanej kultury .NET zamiast własnego formatu?**  
Klasa .NET `CultureInfo` nie rozumie symboli japońskich er w taki sam sposób, jak Excel. Użycie własnego formatu liczbowego jest najpewniejszą metodą dla **excel date parsing** ciągów er.

**Co zrobić, jeśli muszę zapisać datę z powrotem do Excela w formacie ery?**  
Ustaw wartość komórki na `DateTime` i zastosuj ten sam niestandardowy format. Excel automatycznie wyświetli erę.

**Czy to działa w starszych wersjach Excela?**  
Token `[ja-JP-Era]` jest obsługiwany od Excela 2010 wzwyż. Aspose.Cells emuluje to zachowanie, więc skoroszyt wyświetla się poprawnie nawet w starszych wersjach Excela, które nie mają natywnej obsługi er.

## Podsumowanie

Teraz wiesz, jak **create Excel workbook**, **set cell value** z ciągiem japońskiej ery, **apply custom format** i **read date cell**, aby uzyskać `DateTime`. Ten wzorzec zapewnia solidne **excel date parsing** bez ręcznej obsługi ciągów, czyniąc Twój kod automatyzacji w C# zarówno zwięzłym, jak i niezawodnym.

Następnie odkryj powiązane tematy, takie jak **formatting multiple date columns**, **working with other cultural calendars** lub **exporting the workbook to PDF**. Każde rozszerzenie opiera się na tych samych zasadach, więc możesz dostosować rozwiązanie do szerokiego zakresu scenariuszy lokalizacyjnych. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które budują na technikach przedstawionych w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Create Excel Workbook in C# – Apply Custom Number Format](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/)
- [Create Excel Workbook with Custom Format – C# Guide](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-custom-format-c-guide/)
- [Excel Automation with Aspose.Cells .NET: Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}