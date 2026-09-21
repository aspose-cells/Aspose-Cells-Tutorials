---
category: general
date: 2026-02-28
description: Dowiedz się, jak ustawić format daty w Excelu, odczytać datę i czas w
  Excelu, wyodrębnić datę z Excela oraz obliczyć formuły skoroszytu przy użyciu Aspose.Cells
  w C#. Pełny, gotowy do uruchomienia przykład.
draft: false
keywords:
- set excel date format
- read excel datetime
- extract date from excel
- calculate workbook formulas
- get datetime cell
language: pl
og_description: Opanuj ustawianie formatu dat w Excelu, odczytywanie dat i czasu w
  Excelu, wyodrębnianie dat oraz obliczanie formuł w skoroszycie z pełnym przykładem
  w C#.
og_title: Ustaw format daty w Excelu w C# – Kompletny przewodnik krok po kroku
tags:
- Aspose.Cells
- C#
- Excel automation
title: Ustaw format daty w Excelu w C# – Kompletny przewodnik krok po kroku
url: /pl/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ustaw format daty w Excel – Kompletny przewodnik C#

Czy kiedykolwiek miałeś problem z **ustawieniem formatu daty w Excel** podczas generowania arkuszy kalkulacyjnych w locie? Nie jesteś sam. Wielu programistów napotyka na problem, gdy komórka wyświetla surowy ciąg znaków zamiast prawidłowej daty, szczególnie w przypadku japońskich dat epokowych lub niestandardowych ciągów lokalizacyjnych.  

W tym samouczku przeprowadzimy Cię przez rzeczywisty przykład, który **ustawia format daty w Excel**, następnie **odczytuje datę i czas w Excel**, **wyodrębnia datę z Excel**, a nawet **oblicza formuły skoroszytu**, abyś w końcu mógł **pobrać wartości komórek daty i czasu** jako natywne obiekty .NET `DateTime`. Bez zewnętrznych odwołań, tylko samodzielny, gotowy do uruchomienia fragment kodu, który możesz wkleić do Visual Studio i od razu zobaczyć działający.

## Czego będziesz potrzebować

- **Aspose.Cells for .NET** (dowolna aktualna wersja; użyte tutaj API działa z 23.x i nowszymi)  
- .NET 6 lub nowszy (kod kompiluje się także z .NET Framework 4.6+)  
- Podstawowa znajomość składni C# – jeśli potrafisz napisać `Console.WriteLine`, jesteś w porządku.

To wszystko. Nie potrzebujesz dodatkowych pakietów NuGet poza Aspose.Cells, nie jest wymagana instalacja Excel.

## Jak ustawić format daty w Excel w C#  

Pierwszą rzeczą, którą robimy, jest poinformowanie Excela, że komórka zawiera datę, a nie tylko tekst. Aspose.Cells udostępnia wbudowane ID formatu liczbowego (`14`), które odpowiada krótkim wzorcom daty bieżącej lokalizacji.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Step 2: Write a Japanese era date string into cell A1
        sheet.Cells["A1"].PutValue("Reiwa 2-04-01");

        // Step 3: Apply the standard date number format (ID 14) to A1
        // This tells Excel to treat the cell as a date.
        sheet.Cells["A1"].Style.Number = 14;

        // Step 4: Force Excel to recalculate formulas so the value is parsed
        workbook.CalculateFormula();

        // Step 5: Retrieve the parsed value as a .NET DateTime
        DateTime parsedDate = sheet.Cells["A1"].GetDateTime();

        // Step 6: Show the result – should be 2020‑04‑01
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
    }
}
```

> **Wskazówka:** Wywołanie `CalculateFormula()` jest kluczowe. Bez niego komórka nadal zawiera surowy ciąg znaków, a `GetDateTime()` zgłosi wyjątek. Ta linia zmusza Aspose.Cells do uruchomienia swojego wewnętrznego parsera, efektywnie **obliczając formuły skoroszytu** dla nas.

Wynik, który zobaczysz po uruchomieniu programu, to:

```
Parsed DateTime: 2020-04-01
```

To potwierdza, że pomyślnie **ustawiliśmy format daty w Excel**, i udało nam się **pobrać komórkę daty i czasu** jako prawidłowy obiekt `DateTime`.

## Odczytywanie wartości daty i czasu z Excel  

Teraz, gdy data jest poprawnie zapisana, możesz się zastanawiać, jak ją później pobrać, być może z istniejącego pliku. Ta sama metoda `GetDateTime()` działa na każdej komórce, która już ma format daty.

```csharp
// Assuming 'sheet' is already loaded from an existing workbook
DateTime existingDate = sheet.Cells["B5"].GetDateTime();
Console.WriteLine($"Cell B5 contains: {existingDate:d}");
```

Jeśli komórka nie jest sformatowana jako data, `GetDateTime()` zwraca `DateTime.MinValue`. Dlatego zawsze najpierw **ustawiamy format daty w Excel**.

## Wyodrębnianie daty z komórek Excel  

Czasami komórka zawiera pełny znacznik czasu (data + czas), ale potrzebujesz tylko części daty. Możesz odciąć komponent czasu, używając `.Date` na zwróconym `DateTime`.

```csharp
DateTime fullStamp = sheet.Cells["C3"].GetDateTime(); // e.g., 2023-07-15 14:30:00
DateTime onlyDate = fullStamp.Date;                  // 2023-07-15 00:00:00
Console.WriteLine($"Date only: {onlyDate:yyyy-MM-dd}");
```

To podejście działa niezależnie od podstawowego formatu liczbowego w Excel, pod warunkiem że komórka jest rozpoznana jako data.

## Obliczanie formuł skoroszytu  

Co jeśli data jest wynikiem formuły, takiej jak `=TODAY()` lub `=DATE(2022,5,10)`? Aspose.Cells oceni formułę po wywołaniu `CalculateFormula()`. Po tym komórka zachowuje się dokładnie tak, jak ręcznie wprowadzona data.

```csharp
sheet.Cells["D2"].Formula = "=TODAY()";
workbook.CalculateFormula(); // Re‑evaluate the sheet
DateTime today = sheet.Cells["D2"].GetDateTime();
Console.WriteLine($"Today is: {today:yyyy-MM-dd}");
```

Zauważ, że nie musieliśmy zmieniać stylu komórki; Excel już traktuje wyniki formuł jako daty, gdy formuła zwraca liczbę seryjną, która mapuje na datę.

## Pobieranie komórki daty i czasu z istniejącego skoroszytu  

Łącząc wszystko razem, oto zwarta procedura, którą możesz wkleić do dowolnego projektu, aby otworzyć plik Excel, zapewnić prawidłową interpretację wszystkich komórek dat i zwrócić listę obiektów `DateTime`.

```csharp
using System.Collections.Generic;
using Aspose.Cells;

static List<DateTime> ExtractAllDates(string filePath)
{
    Workbook wb = new Workbook(filePath);
    Worksheet ws = wb.Worksheets[0];
    wb.CalculateFormula(); // Make sure formulas are evaluated

    var dates = new List<DateTime>();
    foreach (Cell cell in ws.Cells)
    {
        // Check if the cell has a date number format (ID 14‑22 are common date formats)
        if (cell.GetStyle().Number >= 14 && cell.GetStyle().Number <= 22)
        {
            dates.Add(cell.GetDateTime());
        }
    }
    return dates;
}
```

Uruchomienie `ExtractAllDates("Sample.xlsx")` zwróci wszystkie daty, które zostały **ustawione format daty w Excel** poprawnie w pierwszym arkuszu.

## Typowe pułapki i jak ich unikać  

| Problem | Dlaczego się pojawia | Rozwiązanie |
|-------|----------------|-----|
| `GetDateTime()` throws `ArgumentException` | Komórka nie jest rozpoznana jako data (brak formatu liczbowego) | Zastosuj `Style.Number = 14` **przed** wywołaniem `CalculateFormula()` |
| Date appears as `1900‑01‑00` | Numer seryjny 0 w Excel jest interpretowany jako epoka | Upewnij się, że komórka faktycznie zawiera prawidłowy numer seryjny (>0) |
| Japanese era strings don’t parse | Aspose.Cells parsuje ciągi epokowe dopiero po `CalculateFormula()` | Zachowaj surowy ciąg, ustaw format daty, a następnie wywołaj `CalculateFormula()` |
| Time zone shifts | `DateTime` jest przechowywany bez informacji o strefie, ale aplikacja może wyświetlać w innej lokalizacji | Użyj `DateTimeKind.Utc` lub dokonaj jawnej konwersji w razie potrzeby |

## Obraz – Podsumowanie wizualne  

![przykład ustawienia formatu daty w Excel](excel-date-format.png "przykład ustawienia formatu daty w Excel")

Diagram ilustruje przepływ: **zapisz ciąg → zastosuj format liczbowy → przelicz → pobierz DateTime**.

## Podsumowanie  

Omówiliśmy wszystko, co potrzebne, aby **ustawić format daty w Excel**, **odczytać datę i czas z Excel**, **wyodrębnić datę z Excel**, **obliczyć formuły skoroszytu**, a w końcu **pobrać wartości komórek daty i czasu** jako natywne obiekty .NET. Pełny, gotowy do uruchomienia kod jest gotowy do kopiowania i wklejania, a wyjaśnienia dostarczają „dlaczego” każdego kroku, dzięki czemu możesz dostosować wzorzec do bardziej złożonych scenariuszy.

### Co dalej?

- **Masowy import/eksport:** Użyj pomocnika `ExtractAllDates`, aby przetwarzać wsadowo duże raporty.  
- **Niestandardowe formaty dat:** Zastąp `Style.Number = 14` przez `Style.Custom = "yyyy/mm/dd"` dla formatowania niezależnego od lokalizacji.  
- **Daty uwzględniające strefę czasową:** Połącz `DateTimeOffset` z numerami seryjnymi Excela dla aplikacji globalnych.

Śmiało eksperymentuj, dodawaj formatowanie warunkowe lub wprowadzaj daty do bazy danych. Jeśli napotkasz jakiekolwiek problemy, zostaw komentarz — miłego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}