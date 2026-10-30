---
category: general
date: 2026-07-03
description: Jak używać SEQUENCE w C#, aby generować rosnące liczby w Excelu. Dowiedz
  się, jak tworzyć skoroszyt Excel w C# oraz ASP.NET i tworzyć plik Excel kilkoma
  liniami kodu.
draft: false
keywords:
- how to use sequence
- create excel workbook c#
- asp.net create excel file
- generate incremental numbers excel
language: pl
og_description: Jak używać SEQUENCE w C#, aby generować kolejne liczby w Excelu. Przewodnik
  krok po kroku, jak stworzyć skoroszyt Excel w C# oraz ASP.NET i wygenerować plik
  Excel.
og_title: Jak używać SEQUENCE w C# – Tworzenie skoroszytu Excel
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  headline: How to Use SEQUENCE in C# – Create Excel Workbook
  type: TechArticle
- description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  name: How to Use SEQUENCE in C# – Create Excel Workbook
  steps:
  - name: Why Use SEQUENCE Instead of a Loop?
    text: '- **Performance** – Excel does the math on its own engine, which is highly
      optimized. - **Maintainability** – The formula is self‑documenting; anyone opening
      the sheet instantly knows the intent. - **Dynamic resizing** – Change the `rows`
      argument and the spill range expands automatically.'
  - name: Pro Tip
    text: 'If you need the workbook in memory (e.g., to send it over a web API), use
      a `MemoryStream`:'
  - name: What If the Client Uses an Older Excel Version?
    text: 'Dynamic arrays (including `SEQUENCE`) were introduced in Excel 365/2019.
      If you need backward compatibility, fall back to a manual fill:'
  type: HowTo
- questions:
  - answer: No. `SEQUENCE` is a non‑iterative function; a simple `CalculateFormula()`
      call is enough.
    question: Do I need to enable iterative calculation?
  - answer: 'Change the second argument: `=SEQUENCE(1,5,10,2)` spills across B1:F1.'
    question: What if I want a horizontal spill?
  - answer: Absolutely. For example, `=INDEX(A:A, SEQUENCE(5,1,10,2))` can pull rows
      from another column.
    question: Can I combine SEQUENCE with other functions?
  - answer: The file size impact of a formula is negligible. Only when you start populating
      millions of cells manually does size become an issue.
    question: Is the workbook size a concern?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- ASP.NET
title: Jak używać SEQUENCE w C# – Tworzenie skoroszytu Excel
url: /pl/net/formulas-functions/how-to-use-sequence-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać SEQUENCE w C# – Tworzenie skoroszytu Excel

Zastanawiałeś się kiedyś **jak używać SEQUENCE**, aby wyświetlić listę liczb w arkuszu Excel z C#? Nie jesteś jedyny. Niezależnie od tego, czy tworzysz pulpit nawigacyjny raportów, zasilasz siatkę danych, czy po prostu potrzebujesz szybkiego sposobu generowania identyfikatorów, opanowanie tej sztuczki oszczędza ci ręczne pisanie pętli.

W tym samouczku **utworzymy skoroszyt Excel w C#**, wstawimy formułę dynamicznej tablicy `SEQUENCE` do komórki A1 i uzyskamy ładną kolumnę liczb rosnących. Pokażemy także, jak udostępnić ten plik z kontrolera ASP.NET — tak, **ASP.NET create Excel file** jest również omówione. Po zakończeniu będziesz w stanie **generować liczby rosnące w stylu Excel** jedną linią kodu.

## Czego będziesz potrzebować

- .NET 6+ (kod działa również na .NET Framework 4.6+)  
- Pakiet NuGet **Aspose.Cells for .NET** (lub dowolna biblioteka udostępniająca obiekty `Workbook`/`Worksheet`)  
- Podstawowy projekt ASP.NET Core lub MVC, jeśli chcesz wypróbować część pobierania przez sieć  

To wszystko. Nie potrzebujesz dodatkowego COM interop, ani instalacji Office.

---

## Jak używać SEQUENCE do generowania liczb rosnących

Funkcja Excel `SEQUENCE(rows, [columns], [start], [step])` zwraca zakres **spill**. W naszym przypadku chcemy 5 wierszy, 1 kolumnę, start od 10, krok 2. Formuła wygląda tak:

```excel
=SEQUENCE(5,1,10,2)
```

Gdy Excel ją oceni, komórki A1:A5 będą zawierały **10, 12, 14, 16, 18**. Najlepsze jest to, że nie musimy pisać żadnych pętli w C# — formuła wykonuje całą ciężką pracę.

Poniżej znajduje się kompletny fragment C#, który tworzy skoroszyt, wstawia formułę, wymusza obliczenia i zapisuje plik.

```csharp
using Aspose.Cells;
using System.IO;

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 2️⃣ Grab the first worksheet (Aspose creates one by default)
Worksheet sheet = workbook.Worksheets[0];

// 3️⃣ Insert the SEQUENCE formula – this will spill a 5‑row column starting at 10, step 2
sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";

// 4️⃣ Force calculation so the spilled range is materialized
workbook.CalculateFormula();

// 5️⃣ Save to disk (you can change the path as needed)
workbook.Save("DynamicArray.xlsx");
```

**Oczekiwany wynik** – otwórz *DynamicArray.xlsx* i zobaczysz:

| A |
|---|
| 10 |
| 12 |
| 14 |
| 16 |
| 18 |

To cała historia **how to use sequence** w C#. Proste, prawda? Ale przyjrzyjmy się nieco głębiej.

### Dlaczego używać SEQUENCE zamiast pętli?

- **Performance** – Excel wykonuje obliczenia własnym silnikiem, który jest wysoce zoptymalizowany.
- **Maintainability** – Formuła jest samo‑opisująca; każdy otwierający arkusz od razu rozumie intencję.
- **Dynamic resizing** – Zmiana argumentu `rows` powoduje automatyczne rozszerzenie zakresu spill.

---

## Tworzenie skoroszytu Excel w C# – krok po kroku

Jeśli jesteś nowy w **create excel workbook c#**, poniższa lista kontrolna pomoże ci uniknąć typowych pułapek.

1. **Dodaj pakiet Aspose.Cells**  
   ```bash
   dotnet add package Aspose.Cells
   ```
   (Możesz również użyć ClosedXML lub EPPlus, ale przedstawione API odpowiada powyższemu kodowi.)

2. **Ustaw licencję** (opcjonalnie w wersji próbnej).  
   ```csharp
   var license = new Aspose.Cells.License();
   license.SetLicense("Aspose.Total.NET.lic");
   ```

3. **Zainicjuj `Workbook`** – to daje ci nowy, pusty skoroszyt.

4. **Odwołaj się do arkusza** – `workbook.Worksheets[0]` to domyślny arkusz o nazwie *Sheet1*.

5. **Zastosuj formułę SEQUENCE** – jak pokazano wcześniej.

6. **Oblicz** – `workbook.CalculateFormula()` wymusza spill; w przeciwnym razie plik zawierałby tylko formułę.

7. **Zapisz** – możesz zapisać na dysk, do `MemoryStream`, lub bezpośrednio w odpowiedzi HTTP.

### Porada

Jeśli potrzebujesz skoroszytu w pamięci (np. aby wysłać go przez API webowe), użyj `MemoryStream`:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
byte[] excelBytes = ms.ToArray(); // ready to return or attach
```

---

## ASP.NET Create Excel File – strumieniowanie do przeglądarki

Teraz, gdy znamy **create excel workbook c#**, zintegrować to z kontrolerem ASP.NET Core, aby użytkownicy mogli pobrać plik w locie.

```csharp
using Aspose.Cells;
using Microsoft.AspNetCore.Mvc;
using System.IO;

[Route("api/[controller]")]
public class ExcelController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult Download()
    {
        // 1️⃣ Build the workbook (same steps as before)
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";
        workbook.CalculateFormula();

        // 2️⃣ Save to a memory stream
        using var ms = new MemoryStream();
        workbook.Save(ms, SaveFormat.Xlsx);
        ms.Position = 0; // reset stream position

        // 3️⃣ Return the file as a download
        const string fileName = "DynamicArray.xlsx";
        return File(ms, 
                    "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", 
                    fileName);
    }
}
```

Gdy użytkownik wejdzie pod `/api/excel/download`, przeglądarka wyświetli okno pobierania *DynamicArray.xlsx*. Plik już zawiera kolumnę **generated incremental numbers excel** dzięki formule `SEQUENCE`.

### Co jeśli klient używa starszej wersji Excel?

Dynamiczne tablice (w tym `SEQUENCE`) zostały wprowadzone w Excel 365/2019. Jeśli potrzebna jest kompatybilność wsteczna, użyj ręcznego wypełniania:

```csharp
// Alternative for older Excel: write numbers directly
for (int i = 0; i < 5; i++)
{
    sheet.Cells[i, 0].PutValue(10 + i * 2); // column 0 = A
}
```

Ten fragment pokazuje klasyczne podejście **generate incremental numbers excel** bez korzystania z nowej funkcji.

---

## Częste pytania i przypadki brzegowe

- **Czy muszę włączać iteracyjne obliczenia?**  
  Nie. `SEQUENCE` jest funkcją nie‑iteracyjną; wystarczy proste wywołanie `CalculateFormula()`.

- **Co zrobić, jeśli chcę poziomy spill?**  
  Zmień drugi argument: `=SEQUENCE(1,5,10,2)` rozlewa się wzdłuż B1:F1.

- **Czy mogę łączyć SEQUENCE z innymi funkcjami?**  
  Oczywiście. Na przykład, `=INDEX(A:A, SEQUENCE(5,1,10,2))` może pobierać wiersze z innej kolumny.

- **Czy rozmiar skoroszytu jest problemem?**  
  Wpływ formuły na rozmiar pliku jest znikomy. Dopiero gdy zaczynasz ręcznie wypełniać miliony komórek, rozmiar staje się istotny.

---

## Podsumowanie

Przeszliśmy przez **how to use sequence** w C#, aby **create excel workbook c#**, udostępniliśmy ten skoroszyt przez **ASP.NET create excel file**, i pokazaliśmy czysty sposób **generate incremental numbers excel** bez pisania pętli. Najważniejsze: pozwól silnikowi dynamicznych tablic Excela liczyć, a kodowi .NET skupić się na orkiestracji.

Śmiało eksperymentuj — zamień argumenty `rows`, `start` lub `step`, rozlej poziomo, lub połącz formułę z `IF` lub `FILTER` dla bardziej zaawansowanych raportów. Gdy będziesz gotowy, spróbuj połączyć wiele arkuszy lub wyeksportować skoroszyt jako CSV dla systemów downstream.

Masz własny pomysł, którym chcesz się podzielić? Dodaj komentarz poniżej lub napisz do mnie na GitHubie. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [How to Create and Save Excel Files with Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [How to Create and Style Excel Workbooks Using Aspose.Cells for .NET (2023 Guide)](/cells/english/net/formatting/create-style-excel-workbooks-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}