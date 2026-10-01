---
category: general
date: 2026-10-01
description: Dowiedz się, jak w C# tworzyć skoroszyt Excel, zastosować własny format
  liczbowy, ustawić liczbę miejsc dziesiętnych w komórce i zapisać skoroszyt jako
  XLSX w pełnym przewodniku krok po kroku.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: pl
lastmod: 2026-10-01
og_description: Utwórz skoroszyt Excel w C# z niestandardowym formatem liczbowym,
  ustaw liczbę miejsc dziesiętnych w komórce i zapisz skoroszyt jako XLSX. Skorzystaj
  z tego pełnego przewodnika, aby uzyskać precyzyjny wynik liczbowy.
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: Tworzenie skoroszytu Excel w C# – niestandardowy format liczb i eksport
  do XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  headline: How to create Excel workbook C# with custom number formatting
  type: TechArticle
- description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  name: How to create Excel workbook C# with custom number formatting
  steps:
  - name: Run the program (`dotnet run`).
    text: Run the program (`dotnet run`).
  - name: Open `SigDigits.xlsx`.
    text: Open `SigDigits.xlsx`.
  - name: Confirm that **A1** reads `123.5`.
    text: Confirm that **A1** reads `123.5`.
  - name: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
    text: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Jak utworzyć skoroszyt Excel w C# z niestandardowym formatowaniem liczb
url: /pl/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć skoroszyt Excel w C# z własnym formatowaniem liczb

Jeśli potrzebujesz **utworzyć skoroszyt Excel w C#**, który wyświetla liczby dokładnie tak, jak chcesz, ten przewodnik pokaże Ci, jak to zrobić w kilku prostych krokach. Nauczysz się zastosować własny format liczbowy, ustawić liczbę miejsc dziesiętnych w komórce i w końcu **zapisać skoroszyt jako xlsx** do dalszego wykorzystania.

Praca z danymi liczbowymi często wymaga równowagi między precyzją a czytelnością. Po zakończeniu tego samouczka będziesz mieć wielokrotnego użytku wzorzec, który ogranicza wyświetlane cyfry do określonej liczby cyfr znaczących, zachowując jednocześnie oryginalną wartość w pliku. Nie są wymagane żadne zewnętrzne skrypty — wystarczy C# i biblioteka Aspose.Cells.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

* .NET 6.0 SDK lub nowszy zainstalowany  
* Visual Studio 2022 (lub dowolne IDE dla C#)  
* Pakiet NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`) – ta biblioteka dostarcza klasy `Workbook`, `Worksheet` i `ExportTableOptions` używane w przykładach.  

Te wymagania są minimalne; ten sam kod działa w .NET Core, .NET Framework i nawet w Azure Functions.

## Krok 1: Utwórz skoroszyt Excel w C# – inicjalizacja pliku

Pierwszą operacją jest utworzenie nowego obiektu `Workbook`. Obiekt ten reprezentuje cały plik Excel w pamięci i automatycznie zawiera domyślny arkusz.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // creates an empty .xlsx container
            Worksheet sheet = workbook.Worksheets[0];         // reference to the default sheet
```

**Dlaczego to ważne:**  
Utworzenie skoroszytu na początku daje czyste płótno. Domyślny arkusz (`Worksheets[0]`) jest gotowy do wprowadzania danych, więc nie musisz dodawać nowego arkusza, chyba że Twój scenariusz wymaga wielu zakładek.

## Krok 2: Zapisz wartość liczbową w komórce

Teraz wstaw przykładową liczbę do komórki **A1**. Wartość, której używamy (`123.456789`), zawiera więcej miejsc dziesiętnych niż ostatecznie chcemy wyświetlać, co pozwala nam później pokazać zaokrąglanie.

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**Wskazówka:** `PutValue` automatycznie wykrywa typ danych, więc nie musisz konwertować liczby na ciąg znaków.

## Krok 3: Zastosuj własny format liczbowy – ogranicz widoczne miejsca dziesiętne

Aby kontrolować, jak Excel wyświetla liczbę, tworzymy obiekt `Style` z **własnym formatem liczbowym**. Wzorzec `"0.######"` mówi Excelowi, aby wyświetlał do sześciu miejsc dziesiętnych, pomijając końcowe zera.

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**Jak to działa:**  
Ciąg formatu podąża za składnią własnych formatów Excela. `0` wymusza cyfrę, natomiast `#` wyświetla cyfrę tylko wtedy, gdy jest znacząca. Łącząc je, uzyskasz elastyczne wyświetlanie, które nadal zachowuje pierwotną precyzję.

## Krok 4: Ustaw liczbę miejsc dziesiętnych w komórce – przy użyciu ExportTableOptions

Jeśli musisz **ustawić liczbę miejsc dziesiętnych w komórce** dla eksportowanych danych (np. przy konwersji do DataTable), Aspose.Cells pozwala określić liczbę **cyfr znaczących**. Ten krok zapewnia, że eksportowany CSV lub DataTable respektuje te same zasady zaokrąglania, które zastosowano w skoroszycie.

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**Dlaczego używać `SignificantDigits`?**  
W przeciwieństwie do stałej liczby miejsc po przecinku, cyfry znaczące zachowują skalę liczby, ograniczając jednocześnie precyzję, co często jest oczekiwane przez analityków przy podsumowywaniu danych.

## Krok 5: Eksportuj dane arkusza i **zapisz skoroszyt jako xlsx**

Na koniec wyeksportuj dane (jeśli potrzebujesz DataTable) i zapisz skoroszyt na dysku. Wywołanie `ExportDataTable` respektuje skonfigurowane `ExportTableOptions`, a `workbook.Save` zapisuje standardowy plik XLSX.

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**Oczekiwany rezultat:**  
Po otwarciu *SigDigits.xlsx* w Excelu, komórka **A1** pokazuje `123.5`. Wartość bazowa pozostaje `123.456789`, ale wyświetlana liczba respektuje regułę 4‑cyfrową znaczącą. Jeśli wyeksportujesz arkusz do DataTable, wartość w tabeli również zostanie zaokrąglona do `123.5`.

---

## Zastosuj własny format liczbowy do dodatkowych komórek

Jeśli potrzebujesz sformatować zakres, a nie pojedynczą komórkę, użyj ponownie obiektu `Style`:

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**Pro tip:** Ponowne użycie obiektu stylu zmniejsza zużycie pamięci i zapewnia spójne formatowanie w całym arkuszu.

## Jak formatować liczby w Excelu przy użyciu C# – typowe warianty

| Scenariusz | Ciąg formatu | Wynik |
|------------|--------------|-------|
| Stałe dwa miejsca po przecinku | `"0.00"` | `123.46` |
| Waluta (US) | `"$#,##0.00"` | `$123.46` |
| Procent z jednym miejscem | `"0.0%"` | `12,346.0%` |
| Notacja naukowa | `"0.00E+00"` | `1.23E+02` |

Wybierz wzorzec, który pasuje do Twoich wymagań raportowych. Wszystkie wzorce są kompatybilne z właściwością `Style.Custom` pokazanej wcześniej.

## Ustaw liczbę miejsc dziesiętnych dynamicznie na podstawie danych wejściowych użytkownika

Czasami wymagana precyzja nie jest znana w czasie kompilacji. Możesz zbudować ciąg formatu w czasie wykonywania:

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**Przypadek brzegowy:** Jeśli `decimals` wynosi zero, format staje się `"0"` (wyświetlanie jako liczba całkowita). Zawsze waliduj dane wejściowe użytkownika, aby uniknąć niepoprawnych ciągów formatu.

## Zapisz skoroszyt jako XLSX – najlepsze praktyki

* **Używaj ścieżek bezwzględnych** przy zapisie do znanego katalogu (`Path.Combine(Environment.CurrentDirectory, "output.xlsx")`).  
* **Zwolnij zasoby** (`Dispose`) obiektu `Workbook`, jeśli otaczasz go instrukcją `using`, aby szybko zwolnić niezarządzane zasoby:

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **Kompatybilność wersji:** Aspose.Cells zapisuje pliki zgodne z Excel 2010‑2023, więc użytkownicy końcowi nie napotkają problemów z formatem.

---

## Pełny działający przykład

Poniżej znajduje się kompletny program, który możesz skopiować, wkleić i od razu uruchomić. Zawiera wszystkie niezbędne dyrektywy `using`, komentarze i obsługę błędów.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Create workbook and get the first worksheet
                Workbook workbook = new Workbook();
                Worksheet sheet = workbook.Worksheets[0];

                // 2️⃣ Write a high‑precision number to A1
                sheet.Cells[0, 0].PutValue(123.456789);

                // 3️⃣ Apply a custom number format (up to 6 decimals)
                Style customStyle = workbook.CreateStyle();
                customStyle.Custom = "0.######";
                sheet.Cells[0, 0].SetStyle(customStyle);

                // 4️⃣ Configure export options for 4 significant digits
                ExportTableOptions exportOptions = new ExportTableOptions
                {
                    SignificantDigits = 4
                };

                // 5️⃣ Export data (optional) and save the workbook as XLSX
                sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
                string outputPath = Path.Combine(Environment.CurrentDirectory, "SigDigits.xlsx");
                workbook.Save(outputPath);

                Console.WriteLine($"Workbook saved successfully at: {outputPath}");
                Console.WriteLine("Cell A1 displays: " + sheet.Cells["A1"].StringValue);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error creating workbook: {ex.Message}");
            }
        }
    }
}
```

**Kroki weryfikacji**

1. Uruchom program (`dotnet run`).  
2. Otwórz `SigDigits.xlsx`.  
3. Potwierdź, że **A1** wyświetla `123.5`.  
4. Jeśli otworzysz XML pliku (`.xlsx` jest archiwum zip), zobaczysz własny format `"0.######"` zapisany w atrybucie `s` elementu `<c>`.

---

## Podsumowanie

W tym samouczku nauczyłeś się, jak **utworzyć skoroszyt Excel w C#**, **zastosować własny format liczbowy**, **ustawić liczbę miejsc dziesiętnych w komórce** i **zapisać skoroszyt jako xlsx** przy użyciu Aspose.Cells. Rozwiązanie demonstruje zarówno wizualne formatowanie w Excelu, jak i zaokrąglanie przy eksporcie danych poprzez `ExportTableOptions`.  

Od tego momentu możesz:

* Rozszerzyć podejście na całe zakresy lub tabele.  
* Łączyć wiele stylów (czcionki, obramowania) przy użyciu `StyleFlag`.  
* Automatyzować generowanie raportów, iterując po źródłach danych i stosując tę samą logikę formatowania.  

Śmiało eksperymentuj z różnymi ciągami formatu, liczbą miejsc dziesiętnych lub opcjami eksportu, aby dopasować je do swoich specyficznych potrzeb raportowych. Powodzenia w kodowaniu!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne przykłady kodu oraz szczegółowe wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Create Excel Workbook C# – Step‑by‑Step Guide with Conditional Formatting](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}