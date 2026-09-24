---
category: general
date: 2026-02-21
description: Eksportuj dane do Excela, ładując szablon Excela i używając Smart Markers
  do generowania raportu Excel z tablicy. Dowiedz się, jak szybko wypełnić szablon
  Excela.
draft: false
keywords:
- export data to excel
- populate excel template
- load excel template
- generate excel report
- create excel from array
language: pl
og_description: Eksportuj dane do Excela przy użyciu szablonu SmartMarker. Ten przewodnik
  pokazuje, jak załadować szablon Excela, utworzyć plik Excel z tablicy oraz wygenerować
  raport Excel.
og_title: Eksport danych do Excela – wypełnij szablon z tablicy
tags:
- C#
- Excel Automation
- Smart Markers
title: 'Eksport danych do Excela: wypełnianie szablonu z tablicy w C#'
url: /pl/net/smart-markers-dynamic-data/export-data-to-excel-populate-a-template-from-an-array-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eksport danych do Excela: wypełnianie szablonu z tablicy w C#

Czy kiedykolwiek potrzebowałeś **eksportować dane do Excela**, ale nie wiedziałeś, jak zamienić zwykłą tablicę w ładnie sformatowany skoroszyt? Nie jesteś sam — większość programistów napotyka ten problem, gdy po raz pierwszy próbuje udostępnić dane osobom nietechnicznym. Dobrą wiadomością jest to, że kilka linii C# pozwala **załadować szablon Excela**, dodać swoje dane i natychmiast **wygenerować raport Excel**, który wygląda profesjonalnie.

W tym samouczku przeprowadzimy Cię przez kompletny, działający przykład, który **wypełnia szablon Excela** przy użyciu Aspose.Cells Smart Markers. Po zakończeniu będziesz w stanie **tworzyć Excel z tablicy** obiektów, zapisać wynik i otworzyć plik, aby zobaczyć wypełnione wiersze. Brak brakujących elementów, tylko samodzielne rozwiązanie, które możesz skopiować‑wkleić do swojego projektu.

## Czego się nauczysz

- Jak **załadować szablon Excela**, który już zawiera znaczniki Smart Marker, takie jak `${OrderId}` i `${OrderItems:ItemName}`.  
- Jak ustrukturyzować źródło danych, aby SmartMarkerProcessor mógł iterować po kolekcjach.  
- Jak **wypełnić szablon Excela** zagnieżdżoną tablicą i uzyskać gotowy plik **generujący raport Excel**.  
- Porady dotyczące obsługi przypadków brzegowych, takich jak puste kolekcje lub duże zestawy danych.  

**Wymagania wstępne**: .NET 6+ (lub .NET Framework 4.6+) oraz pakiet NuGet Aspose.Cells for .NET. Jeśli już używasz Visual Studio, po prostu dodaj pakiet przez Menedżera NuGet — nie wymaga dodatkowej konfiguracji.

![Export data to Excel process diagram](https://example.com/export-data-diagram.png "Export data to Excel workflow")

## Eksport danych do Excela przy użyciu szablonu SmartMarker

Pierwszą rzeczą, której potrzebujemy, jest skoroszyt, który będzie szkieletą naszego raportu. Pomyśl o nim jak o dokumencie Word z polami scalania, z tą różnicą, że to plik Excel, a pola nazywają się **Smart Markers**.  

```csharp
// Step 1: Load the Excel template that contains Smart Markers (${OrderId}, ${OrderItems:ItemName})
var workbook = new Aspose.Cells.Workbook("YOUR_DIRECTORY/template.xlsx");
```

Dlaczego w ogóle ładować szablon? Ponieważ układ — szerokości kolumn, style nagłówków, formuły — nie musi być odtwarzany w kodzie. Projektujesz go raz w Excelu, umieszczasz znaczniki i pozwalasz bibliotece wykonać ciężką pracę.

## Załaduj szablon Excela i przygotuj środowisko

Zanim będziemy mogli cokolwiek przetworzyć, musimy odwołać się do przestrzeni nazw Aspose.Cells i upewnić się, że plik szablonu istnieje.  

```csharp
using Aspose.Cells;

// Verify template existence (optional but helpful)
if (!System.IO.File.Exists("YOUR_DIRECTORY/template.xlsx"))
{
    throw new System.IO.FileNotFoundException("Template file not found. Ensure the path is correct.");
}
```

> **Pro tip:** Przechowuj szablon w folderze `Resources` i ustaw właściwość pliku *Copy to Output Directory* na *Copy always*; w ten sposób ścieżka będzie działać zarówno w trakcie developmentu, jak i po publikacji.

## Przygotuj źródło danych (Utwórz Excel z tablicy)

Teraz nadchodzi część, w której **tworzymy Excel z tablicy**. SmartMarkerProcessor oczekuje obiektu enumerowalnego, więc prosty anonimowy typ działa bez problemu.  

```csharp
// Step 2: Prepare the data source – an array of orders, each with an ID and a list of item names
var orderData = new[]
{
    new
    {
        OrderId = 1,
        OrderItems = new[]
        {
            new { ItemName = "Pen" },
            new { ItemName = "Paper" }
        }
    },
    new
    {
        OrderId = 2,
        OrderItems = new[]
        {
            new { ItemName = "Notebook" },
            new { ItemName = "Marker" },
            new { ItemName = "Eraser" }
        }
    }
};
```

Zauważ zagnieżdżoną tablicę `OrderItems` — odzwierciedla ona znacznik `${OrderItems:ItemName}` w szablonie. Procesor powtórzy wiersz dla każdego elementu, automatycznie wypełniając kolumnę `ItemName`.

Jeśli już masz `List<Order>` lub DataTable, po prostu przekaż go do procesora; kluczowe jest, aby nazwy właściwości odpowiadały znacznikom.

## Przetwórz szablon, aby wypełnić Excela

Mając gotowy skoroszyt i dane, tworzymy instancję `SmartMarkerProcessor` i pozwalamy mu scalić dane.  

```csharp
// Step 3: Create a SmartMarkerProcessor for the loaded workbook
var processor = new Aspose.Cells.SmartMarkerProcessor(workbook);

// Step 4: Populate the template by processing the Smart Markers with the data source
processor.Process(orderData);
```

Dlaczego używać `SmartMarkerProcessor`? Jest szybszy niż ręczne zapisywanie komórka po komórce i respektuje funkcje Excela, takie jak formuły, scalone komórki i formatowanie warunkowe. Dodatkowo automatycznie rozszerza wiersze dla kolekcji — idealne w scenariuszach **wypełniania szablonu Excela**.

## Zapisz wygenerowany raport Excel

Na koniec zapisujemy wypełniony skoroszyt na dysk.  

```csharp
// Step 5: Save the populated workbook to a new file
string outputPath = "YOUR_DIRECTORY/output.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Excel report generated at: {outputPath}");
```

Po uruchomieniu programu otwórz `output.xlsx`. Powinieneś zobaczyć coś takiego:

| OrderId | ItemName |
|---------|----------|
| 1       | Pen      |
| 1       | Paper    |
| 2       | Notebook |
| 2       | Marker   |
| 2       | Eraser   |

To w pełni **wygenerowany raport Excel** zbudowany z tablicy w pamięci, bez konieczności pisania własnej logiki pętli.

## Obsługa przypadków brzegowych i typowe pułapki

- **Puste kolekcje** – Jeśli `OrderItems` jest pusty dla konkretnego zamówienia, Smart Markers po prostu pominą wiersz. Jeśli potrzebujesz wiersza zastępczego, dodaj warunkowy znacznik, np. `${OrderItems?ItemName:"(no items)"}`.  
- **Duże zestawy danych** – Przy tysiącach wierszy rozważ strumieniowanie wyjścia (`workbook.Save(outputPath, SaveFormat.Xlsx)` jest już zoptymalizowane, ale możesz także włączyć `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference`).  
- **Aktualizacje szablonu** – Gdy zmieniasz nazwy znaczników, zaktualizuj odpowiednio nazwy właściwości w anonimowym typie; w przeciwnym razie procesor po cichu zignoruje niezgodne pola.  
- **Formatowanie dat/liczb** – Format komórki w szablonie ma pierwszeństwo. Jeśli potrzebujesz formatowania specyficznego dla kultury, ustaw `NumberFormat` komórki przed przetworzeniem.

## Pełny działający przykład (Gotowy do kopiowania)

Poniżej znajduje się kompletny program, który możesz wkleić do aplikacji konsolowej. Zawiera wszystkie dyrektywy `using`, obsługę błędów i komentarze.

```csharp
using System;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load the Excel template that contains Smart Markers
            // -------------------------------------------------
            string templatePath = "YOUR_DIRECTORY/template.xlsx";
            if (!System.IO.File.Exists(templatePath))
            {
                Console.WriteLine("Template not found. Please place template.xlsx in the specified folder.");
                return;
            }

            var workbook = new Workbook(templatePath);

            // -------------------------------------------------
            // 2️⃣ Prepare the data source – create excel from array
            // -------------------------------------------------
            var orderData = new[]
            {
                new
                {
                    OrderId = 1,
                    OrderItems = new[]
                    {
                        new { ItemName = "Pen" },
                        new { ItemName = "Paper" }
                    }
                },
                new
                {
                    OrderId = 2,
                    OrderItems = new[]
                    {
                        new { ItemName = "Notebook" },
                        new { ItemName = "Marker" },
                        new { ItemName = "Eraser" }
                    }
                }
            };

            // -------------------------------------------------
            // 3️⃣ Process the template – populate excel template
            // -------------------------------------------------
            var processor = new SmartMarkerProcessor(workbook);
            processor.Process(orderData);

            // -------------------------------------------------
            // 4️⃣ Save the generated Excel report
            // -------------------------------------------------
            string outputPath = "YOUR_DIRECTORY/output.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"✅ Export data to Excel completed. File saved at: {outputPath}");
        }
    }
}
```

Uruchom program, otwórz `output.xlsx` i zobaczysz dane ładnie wypełnione. To wszystko — Twój **workflow eksportu danych do Excela** jest teraz w pełni zautomatyzowany.

## Podsumowanie

Właśnie przeszliśmy przez kompletną metodę **eksportu danych do Excela** przy użyciu wcześniej zaprojektowanego szablonu, prostej tablicy jako źródła danych oraz Aspose.Cells Smart Markers do automatycznego **wypełniania szablonu Excela**. W kilku krokach możesz **załadować szablon Excela**, przekształcić dowolną kolekcję w dopracowany **generowany raport Excel** i **tworzyć Excel z tablicy** bez pisania niskopoziomowego kodu komórek.

Co dalej? Spróbuj zamienić anonimowy typ na prawdziwą klasę `Order`, dodaj bardziej złożone znaczniki, np. `${OrderDate:MM/dd/yyyy}`, lub zintegrować tę logikę z Web API, które zwraca plik na żądanie. Ten sam wzorzec sprawdzi się przy fakturach, arkuszach inwentarzowych czy każdym innym tabelarycznym wyjściu, które musisz udostępnić.

Masz pytania lub trudny scenariusz? zostaw komentarz poniżej i powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}