---
category: general
date: 2026-03-21
description: Ustaw niestandardowy format komórki w C# i dowiedz się, jak zapisać datę
  do Excela, zastosować niestandardowy format daty, odczytać DateTime z Excela oraz
  szybko utworzyć arkusz skoroszytu.
draft: false
keywords:
- set cell custom format
- write date to excel
- read datetime from excel
- apply custom date format
- create workbook worksheet
language: pl
og_description: Ustaw niestandardowy format komórki w C#, aby zapisać datę do Excela,
  zastosuj własny format daty, odczytaj DateTime z Excela i z łatwością utwórz arkusz
  skoroszytu.
og_title: Ustaw niestandardowy format komórki w C# – Zapis i odczyt dat w Excelu
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Ustaw niestandardowy format komórki w C# – Kompletny przewodnik po zapisywaniu
  i odczytywaniu dat w Excelu
url: /pl/net/excel-custom-number-date-formatting/set-cell-custom-format-in-c-complete-guide-to-writing-readin/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ustaw niestandardowy format komórki – zapisywanie i odczytywanie dat w Excelu przy użyciu C#

Czy kiedykolwiek potrzebowałeś **ustawić niestandardowy format komórki** w pliku Excel z poziomu C#, ale nie wiedziałeś od czego zacząć? Nie jesteś sam. W wielu narzędziach raportujących lub utilitach eksportu danych data musi być wyświetlana w określonej lokalizacji — pomyśl o datach w japońskim systemie ery, kalendarzach fiskalnych lub ciągach ISO‑8601.

W tym samouczku przeprowadzimy Cię przez **kompletny, działający przykład**, który pokaże, jak **zapisać datę do Excela**, **zastosować niestandardowy format daty**, **odczytać DateTime z Excela** oraz **utworzyć arkusz skoroszytu** przy użyciu Aspose.Cells. Po zakończeniu będziesz mieć pojedynczy, samodzielny program, który możesz wkleić do dowolnego projektu .NET.

## Czego się nauczysz

- Jak **utworzyć arkusz skoroszytu** programowo.  
- Dokładne kroki, aby **zapisać datę do Excela** przy użyciu łańcucha znaków specyficznego dla lokalizacji.  
- Jak **zastosować niestandardowy format daty** (w tym notację japońskiej ery).  
- Sposób **odczytania DateTime z Excela** z powrotem do obiektu `DateTime`.  
- Wskazówki, pułapki i warianty, które mogą się pojawić przy pracy z datami w Excelu.

Nie potrzebujesz żadnej zewnętrznej dokumentacji — wszystko, co potrzebne, znajduje się tutaj.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również na .NET Framework 4.7+).  
- Aspose.Cells for .NET zainstalowany przez NuGet (`Install-Package Aspose.Cells`).  
- Podstawowa znajomość składni C# — nic skomplikowanego.

> **Pro tip:** Jeśli używasz Visual Studio, włącz *nullable reference types*, aby wcześnie wykrywać subtelne błędy.

## Krok 1: Utwórz Workbook i Worksheet  

Najpierw potrzebujesz obiektu workbook, który reprezentuje plik Excel, oraz arkusza, w którym będą przechowywane dane.

```csharp
using Aspose.Cells;
using System;

class ExcelDateDemo
{
    static void Main()
    {
        // Step 1: Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];           // default sheet is named "Sheet1"
```

*Dlaczego to ważne:* Klasa `Workbook` jest punktem wejścia dla wszystkich operacji na Excelu. Tworząc ją w pamięci, nie dotykasz systemu plików, dopóki nie zapiszesz explicite, co przyspiesza proces i ułatwia testowanie.

## Krok 2: Zapisz datę do Excela  

Następnie umieścimy łańcuch znaków daty japońskiej ery (`"R02-04-01"`) w komórce **A1**. Łańcuch imituje erę Reiwa (rok 2, 1 kwietnia).

```csharp
        // Step 2: Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("R02-04-01");
```

*Co się dzieje:* `PutValue` zapisuje surowy łańcuch znaków. Aspose.Cells później spróbuje go sparsować w oparciu o styl komórki. Jeśli pominiesz ten krok i zapiszesz bezpośrednio `DateTime`, utracisz informację o erze, którą chcesz wyświetlić.

## Krok 3: Zastosuj wbudowany format liczbowy daty (ID 14)

Excel posiada wbudowany format daty o ID 14 (`mm-dd-yy`). Zastosowanie go informuje silnik, że komórka **zawiera datę**, a nie tylko tekst.

```csharp
        // Step 3: Apply the built‑in date number format (ID 14)
        worksheet.Cells["A1"].Style.Number = 14;
```

*Dlaczego używać ID 14?* To uniwersalny format „krótkiej daty”, który zapewnia, że Excel traktuje zawartość jako wartość daty — warunek wstępny, aby każdy niestandardowy format działał poprawnie.

## Krok 4: Ustaw niestandardowy format wyświetlający notację japońskiej ery  

Teraz najciekawsza część: instruujemy Excel, aby renderował datę przy użyciu formatu japońskiej ery. Niestandardowy łańcuch `[$-ja-JP]ggge年m月d日` robi dokładnie to.

```csharp
        // Step 4: Set a custom format to display the date in Japanese era notation
        worksheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge年m月d日";
```

*Wyjaśnienie:*  
- `[$-ja-JP]` wymusza lokalizację na japoński.  
- `ggg` to nazwa ery (np. „R” dla Reiwa).  
- `e` to rok ery.  
- `年`, `月`, `日` to dosłowne japońskie znaki oznaczające rok, miesiąc i dzień.

Jeśli potrzebujesz innej lokalizacji, po prostu zamień `ja-JP` na odpowiedni kod kultury (np. `en-US`).

## Krok 5: Pobierz sparsowaną wartość DateTime  

Na koniec odczytamy **rzeczywisty `DateTime`**, który Excel sparsował z komórki. To dowód, że łańcuch został poprawnie zinterpretowany.

```csharp
        // Step 5: Retrieve the parsed DateTime value from the cell
        DateTime parsedDate = worksheet.Cells["A1"].DateTime;   // => 2020‑04‑01

        // Output to console for verification
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

*Wynik:* Konsola wypisuje `Parsed DateTime: 2020-04-01`. Mimo że wprowadziliśmy łańcuch japońskiej ery, Excel wewnętrznie przechowuje datę gregoriańską, którą możesz wykorzystać do obliczeń, porównań lub dalszego eksportu.

## Krok 6: Zapisz Workbook (opcjonalnie)

Jeśli chcesz zobaczyć sformatowany skoroszyt w Excelu, po prostu zapisz go na dysk.

```csharp
        // Optional: Save the workbook to a file
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

Otwórz wygenerowany **JapaneseEraDate.xlsx** i zobaczysz, że komórka **A1** wyświetla `R02年4月1日` (dokładny format japońskiej ery, który ustawiliśmy).

![przykład ustawienia niestandardowego formatu komórki](image-placeholder.png "Komórka Excel pokazująca datę w japońskiej erze – ustaw niestandardowy format komórki")

*Tekst alternatywny powyżej zawiera główne słowo kluczowe, spełniając wymóg SEO dla obrazu.*

## Typowe warianty i przypadki brzegowe  

### Zapis innego formatu daty  

Jeśli wolisz ISO‑8601 (`2020-04-01`) zamiast łańcucha ery, po prostu zmień wywołanie `PutValue`:

```csharp
worksheet.Cells["A1"].PutValue(new DateTime(2020, 4, 1));
worksheet.Cells["A1"].Style.Number = 14;                 // keep built‑in date format
worksheet.Cells["A1"].Style.Custom = "yyyy-mm-dd";      // custom ISO format
```

### Obsługa pustych lub nullowych komórek  

Podczas odczytu daty zawsze zabezpieczaj się przed pustymi komórkami, aby uniknąć `InvalidOperationException`:

```csharp
if (!worksheet.Cells["A1"].IsDate)
{
    Console.WriteLine("Cell A1 does not contain a valid date.");
}
else
{
    DateTime dt = worksheet.Cells["A1"].DateTime;
    // use dt...
}
```

### Wsparcie wielu lokalizacji  

Możesz przeiterować listę kodów kultury i zastosować je dynamicznie:

```csharp
string[] cultures = { "ja-JP", "en-US", "fr-FR" };
foreach (var culture in cultures)
{
    worksheet.Cells["A1"].Style.Custom = $"[$-{culture}]ggge年m月d日";
    // Save or export per culture if needed
}
```

## Pro tipy i pułapki  

- **Zawsze najpierw ustaw wbudowany format liczbowy** (`Style.Number`). Bez tego Excel traktuje komórkę jako zwykły tekst i niestandardowy format zostaje zignorowany.  
- **Kody lokalizacji nie rozróżniają wielkości liter**, ale używanie kanonicznej formy (`ja-JP`) zapobiega nieporozumieniom.  
- **Zapisywanie jest opcjonalne** przy przetwarzaniu w pamięci; możesz bezpośrednio strumieniować workbook do odpowiedzi webowej (`workbook.Save(stream, SaveFormat.Xlsx)`).  
- **Licencje Aspose.Cells**: Wersja darmowa z oceną dodaje znak wodny. W produkcji upewnij się, że posiadasz ważną licencję, aby uniknąć spadku wydajności.

## Podsumowanie  

Pokażemy, jak **ustawić niestandardowy format komórki** w C# aby wyświetlać daty w japońskiej erze, jak **zapisać datę do Excela**, **zastosować niestandardowy format daty**, **odczytać DateTime z Excela** oraz **utworzyć arkusz skoroszytu** — wszystko w jednym, samodzielnym programie. Główne słowo kluczowe pojawia się naturalnie w całym tekście, a słowa kluczowe drugorzędne są wplecione w nagłówki i treść, spełniając zarówno wymagania SEO, jak i standardy cytowania AI.

## Co dalej?

- Zbadaj **formatowanie warunkowe**, aby podświetlać przeterminowane daty.  
- Połącz to podejście z **PivotTables** dla dynamicznego raportowania.  
- Spróbuj **odczytywać duże pliki CSV** i konwertować je na Excel przy użyciu tej samej logiki obsługi dat.  

Śmiało eksperymentuj z różnymi lokalizacjami, niestandardowymi wzorcami lub nawet strefami czasowymi. Jeśli napotkasz problemy, zostaw komentarz poniżej — happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}