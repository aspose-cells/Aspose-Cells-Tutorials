---
category: general
date: 2026-10-10
description: Dowiedz się, jak usunąć cały wiersz w skoroszycie Excel przy użyciu C#.
  Ten przewodnik krok po kroku obejmuje także, jak usunąć wiersz według indeksu i
  usunąć wiersz według indeksu przy użyciu Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete entire row
- how to delete row
- remove row by index
- delete row excel
- delete row c#
language: pl
lastmod: 2026-10-10
og_description: Usuń cały wiersz w skoroszycie Excel przy użyciu C#. Skorzystaj z
  tego przewodnika, aby dowiedzieć się, jak usuwać wiersz po indeksie, usuwać wiersz
  po indeksie oraz bezpiecznie zapisać plik.
og_image_alt: Screenshot of an Excel worksheet before and after deleting an entire
  row with C# code
og_title: Usuwanie całego wiersza w Excelu przy użyciu C# – kompletny przewodnik programistyczny
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to delete entire row in an Excel workbook with C#. This step‑by‑step
    guide also covers how to delete row by index and remove row by index using Aspose.Cells.
  headline: How to delete entire row in an Excel file using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Jak usunąć cały wiersz w pliku Excel przy użyciu C#
url: /pl/net/row-and-column-management/how-to-delete-entire-row-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Usuń cały wiersz w pliku Excel przy użyciu C#

Jeśli potrzebujesz **usunąć cały wiersz** w skoroszycie Excel, ten przewodnik pokaże Ci dokładnie, jak to zrobić w C#. Niezależnie od tego, czy czyszczysz zaimportowane dane, czy tworzysz narzędzie raportujące, poniższe kroki pozwolą usunąć wiersz według jego indeksu i zapisać wynik bez utraty pozostałych danych.

Zobaczysz także, jak to samo podejście odpowiada na pytanie **how to delete row** według indeksu, jak **remove row by index**, oraz dlaczego działa w scenariuszach **delete row excel** w C#.

## Wymagania wstępne

Przed rozpoczęciem upewnij się, że masz:

* .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.6+)
* Biblioteka **Aspose.Cells for .NET** (dostępna przez NuGet: `Install-Package Aspose.Cells`)
* Podstawowa znajomość projektów konsolowych lub desktopowych w C#

Nie są wymagane dodatkowe komponenty Excel interop ani COM, co sprawia, że rozwiązanie jest lekkie i bezpieczne dla wykonania po stronie serwera.

## Krok 1: Konfiguracja projektu i import przestrzeni nazw

Utwórz nową aplikację konsolową (lub dodaj kod do istniejącego projektu) i dodaj wymagane dyrektywy `using`:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the tutorial code lives here.
        }
    }
}
```

*Dlaczego to ważne*: Importowanie `Aspose.Cells` daje dostęp do `Workbook`, `Worksheet` oraz metody `DeleteRows`, która wykonuje rzeczywiste usunięcie wiersza.

## Krok 2: Załaduj skoroszyt i wybierz arkusz

Musisz załadować plik źródłowy (`input.xlsx`) i uzyskać arkusz, który chcesz zmodyfikować. Pierwszy arkusz jest dostępny pod indeksem `0`.

```csharp
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Get the first worksheet (you can also use workbook.Worksheets["SheetName"])
Worksheet ws = workbook.Worksheets[0];
```

**Wskazówka**: Jeśli musisz pracować z konkretnym arkuszem, zamień indeks na nazwę arkusza: `workbook.Worksheets["Data"]`.

## Krok 3: Usuń cały wiersz według indeksu zerowego

Aspose.Cells używa indeksowania zerowego, więc pierwszy wiersz ma indeks `0`. Aby usunąć wiersz 5 (szósty widoczny wiersz), wywołaj `DeleteRows` z parametrem `DeleteOptions.DeleteEntireRow`.

```csharp
// Delete one row starting at index 5 (zero‑based) and remove the whole row
ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
```

*Wyjaśnienie*:

* `ws.Cells[5, 0]` wskazuje na pierwszą komórkę wiersza, który chcesz usunąć.  
* `DeleteRows(1, DeleteOptions.DeleteEntireRow)` instruuje Aspose.Cells, aby usunął **1** wiersz, a flaga `DeleteEntireRow` zapewnia, że **cały wiersz** znika, a wiersze poniżej przesuwają się w górę.

### Jak usunąć wiersz według indeksu w innych scenariuszach

* **Usuń wiele kolejnych wierszy** – zmień pierwszy argument na liczbę wierszy, które chcesz usunąć:

  ```csharp
  // Remove rows 5, 6 and 7 (three rows total)
  ws.Cells[5, 0].DeleteRows(3, DeleteOptions.DeleteEntireRow);
  ```

* **Usuń ostatni wiersz** – użyj `ws.Cells.MaxDataRow`, aby uzyskać indeks najniższego wypełnionego wiersza:

  ```csharp
  int lastRow = ws.Cells.MaxDataRow;
  ws.Cells[lastRow, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
  ```

Te fragmenty kodu odpowiadają wymaganiu **remove row by index**, jednocześnie utrzymując kod czytelnym.

## Krok 4: Zapisz skoroszyt po usunięciu wiersza

Po usunięciu zapisz zmodyfikowany skoroszyt z powrotem na dysk. Możesz nadpisać oryginalny plik lub utworzyć nowy.

```csharp
// Save the workbook to a new file (or overwrite the original)
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

Jeśli musisz zachować niezmieniony oryginalny plik, po prostu zmień ścieżkę wyjściową. Metoda `Save` obsługuje wiele formatów (`.xls`, `.csv`, `.pdf` itp.) – wystarczy zmienić rozszerzenie pliku.

## Pełny działający przykład

Łącząc wszystko razem, oto kompletny, gotowy do uruchomienia program:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Select the first worksheet
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Delete the entire row at index 5 (sixth visual row)
            ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);

            // 4️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Row deleted successfully. Output saved to output.xlsx");
        }
    }
}
```

**Oczekiwany wynik**: Po uruchomieniu programu, `output.xlsx` będzie zawierał wszystkie oryginalne wiersze oprócz tego, który zaczynał się od wizualnego wiersza 6. Wszystkie dane poniżej usuniętego wiersza przesuwają się automatycznie w górę, zachowując formuły i formatowanie.

## Typowe pułapki i jak ich uniknąć

| Problem | Dlaczego się pojawia | Rozwiązanie |
|---------|----------------------|-------------|
| **Index out of range** | Próba usunięcia wiersza o indeksie, który nie istnieje (np. `ws.Cells[1000,0]` w arkuszu z 200 wierszami) | Użyj `ws.Cells.MaxDataRow`, aby zweryfikować najwyższy prawidłowy indeks przed wywołaniem `DeleteRows`. |
| **Partial row deletion** | Pominięcie `DeleteOptions.DeleteEntireRow` powoduje, że usuwane są tylko zawartości komórek | Zawsze przekazuj `DeleteOptions.DeleteEntireRow`, gdy potrzebne jest usunięcie całego wiersza. |
| **Unexpected formula changes** | Usuwanie wierszy będących częścią zakresu formuły może zerwać odwołania | Przelicz formuły po usunięciu (`workbook.CalculateFormula()`), jeśli skoroszyt zależy od dynamicznych zakresów. |
| **Saving to a read‑only location** | Wywołanie `Save` rzuca wyjątek, jeśli folder jest chroniony | Upewnij się, że docelowy katalog jest zapisywalny lub uruchom program z odpowiednimi uprawnieniami. |

Rozwiązanie tych problemów sprawia, że rozwiązanie jest solidne w środowisku produkcyjnym i spełnia zapytania **delete row excel** oraz **delete row c#**.

## Zaawansowane: Usuwanie wierszy na podstawie warunku

Czasami trzeba usunąć wiersze spełniające określony warunek (np. wiersze, w których kolumna A jest pusta). Poniższa pętla demonstruje bezpieczny sposób skanowania od dołu do góry i usuwania pasujących wierszy:

```csharp
int lastRow = ws.Cells.MaxDataRow;
for (int row = lastRow; row >= 0; row--)
{
    // Check if column A (index 0) is empty
    if (ws.Cells[row, 0].StringValue == string.Empty)
    {
        ws.Cells[row, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
    }
}
workbook.Save("YOUR_DIRECTORY/cleaned.xlsx");
```

Skanowanie w górę zapobiega problemowi przesunięcia indeksów, który występuje przy usuwaniu wierszy podczas iteracji w przód.

## Podsumowanie

Teraz wiesz, jak **delete entire row** w skoroszycie Excel przy użyciu C#. Przewodnik obejmował:

* Ładowanie skoroszytu i wybór arkusza  
* Użycie `DeleteRows` z `DeleteOptions.DeleteEntireRow` do **how to delete row** według indeksu  
* Bezpieczne zapisywanie zmodyfikowanego pliku  
* Obsługa przypadków brzegowych, wskazówki wydajnościowe oraz przykład usuwania warunkowego  

Dzięki tej wiedzy możesz pewnie wdrożyć funkcjonalność **remove row by index**, automatyzować czyszczenie danych i integrować manipulację Excel w dowolnej aplikacji C#.

**Kolejne kroki**: zapoznaj się z innymi funkcjami Aspose.Cells, takimi jak wstawianie wierszy, kopiowanie zakresów czy konwertowanie skoroszytu do PDF — wszystkie opierają się na tych samych obiektach `Workbook` i `Worksheet`, które właśnie opanowałeś. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak usunąć wiersz Excel przy użyciu Aspose.Cells .NET: Kompletny przewodnik](/cells/english/net/worksheet-management/delete-excel-row-aspose-cells-net-tutorial/)
- [Aspose Cells Delete Rows – Ochrona wiersza nagłówka w Excel](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [Efektywne zarządzanie wierszami w Excel przy użyciu Aspose.Cells dla Java: Wstawianie i usuwanie wierszy](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}