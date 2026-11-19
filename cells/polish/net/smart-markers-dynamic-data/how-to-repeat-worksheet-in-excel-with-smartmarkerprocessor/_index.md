---
category: general
date: 2026-11-19
description: Jak powielać arkusz podczas wypełniania Excela danymi z tablicy. Dowiedz
  się, jak w kilku krokach generować wiele arkuszy i wypełniać arkusz z listy.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: pl
lastmod: 2026-11-19
og_description: Jak powtarzać arkusz przy użyciu SmartMarkerProcessor. Postępuj zgodnie
  z tym przewodnikiem, aby wypełnić Excel danymi z tablicy, generować wiele arkuszy
  i wypełniać arkusz z listy.
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: Jak powielać arkusz w Excelu – przewodnik krok po kroku
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: Jak powtarzać arkusz w Excelu za pomocą SmartMarkerProcessor
url: /pl/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak powielać arkusz w Excelu przy użyciu SmartMarkerProcessor

Jeśli potrzebujesz **jak powielać arkusz** podczas generowania raportów Excel, ten przewodnik pokaże Ci kompletną, działającą rozwiązanie. Po zakończeniu tutorialu będziesz w stanie **wypełnić Excel danymi z tablicy**, **generować wiele arkuszy**, oraz **wypełnić arkusz z listy** przy użyciu biblioteki SmartMarkerProcessor.

Powielanie arkusza jest częstym wymogiem, gdy każdy dział, region lub okres czasu potrzebuje własnej zakładki. Poniższy przykład demonstruje dokładne kroki, wyjaśnia, dlaczego każde ustawienie ma znaczenie, oraz omawia przypadki brzegowe, takie jak puste listy lub niestandardowe nazewnictwo.

## Wymagania wstępne

- .NET 6.0 lub nowszy zainstalowany
- Odwołanie do pakietu NuGet **GroupDocs.Viewer** (lub równoważnego), który zawiera `SmartMarkerProcessor`
- Szablon skoroszytu Excel (`.xlsx`) z markerem takim jak `${repeat:Dept}` umieszczonym w wierszu, który chcesz powielać
- Podstawowa znajomość C# i LINQ (opcjonalna, ale pomocna)

Nie są wymagane dodatkowe biblioteki zewnętrzne.

## Krok 1: Utwórz instancję SmartMarkerProcessor

Procesor koordynuje zamianę markerów i duplikację arkuszy. Utworzenie go bez argumentów używa domyślnych opcji.

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

Wczesne utworzenie procesora pozwala skonfigurować globalne opcje przed zastosowaniem jakichkolwiek danych. To podstawa do **jak powielać arkusz** prawidłowo.

## Krok 2: Włącz powielanie arkusza

Domyślnie procesor zamienia markery tylko w bieżącym arkuszu. Ustawienie `RepeatWorksheet` na `true` informuje silnik, aby sklonował cały arkusz dla każdego elementu w kolekcji danych.

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

Włączenie tej opcji jest kluczem do **generowania wielu arkuszy** — procesor utworzy nową zakładkę dla każdego elementu w tablicy `Dept` i zachowa oryginalne formatowanie.

## Krok 3: Przygotuj źródło danych jako tablicę lub listę

SmartMarkerProcessor działa z dowolnym enumerable, ale użycie tablicy jasno określa zamiar, gdy chcesz **wypełnić arkusz z listy**. Tutaj tworzymy anonimowy obiekt, który zawiera właściwość `Dept` przechowującą tablicę stringów.

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

Jeśli już masz `List<string>`, możesz ją przekazać bezpośrednio; procesor potraktuje ją tak samo. Ważne jest, aby nazwa właściwości (`Dept`) odpowiadała markerowi `${repeat:Dept}` w szablonie.

## Krok 4: Załaduj szablon arkusza

Zakładając, że masz `ExcelPackage` (z EPPlus) lub obiekt `Workbook`, pobierz arkusz, który chcesz powielać. Zmienna `ws` reprezentuje ten arkusz.

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

Jeśli wolisz inną bibliotekę (np. ClosedXML), zasada pozostaje taka sama: uzyskaj obiekt arkusza, który implementuje wymaganą interfejs.

## Krok 5: Przetwórz arkusz przy użyciu danych

Teraz zastosuj dane do szablonu. Procesor klonuje arkusz dla każdego działu, zamienia marker `${repeat:Dept}` na rzeczywistą nazwę działu i pozostawia resztę arkusza niezmienioną.

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

Po zakończeniu `Process`, `ws` staje się pierwszym z kilku arkuszy — po jednym na dział. Nazwa oryginalnego arkusza jest zachowana, natomiast duplikaty otrzymują kolejno rosnące przyrostki (np. „Sheet1 (1)”, „Sheet1 (2)”). Możesz je później przemianować, jeśli potrzebujesz własnego schematu nazewnictwa.

### Oczekiwany wynik

Po otwarciu wygenerowanego skoroszytu powinieneś zobaczyć:

- **Sheet1** – oryginalny szablon (często pusty lub używany jako główny)
- **Sheet1 (1)** – wypełniony „HR”
- **Sheet1 (2)** – wypełniony „IT”
- **Sheet1 (3)** – wypełniony „Finance”

Każdy arkusz zawiera ten sam układ, ale z nazwą działu podmienioną w miejscu, gdzie występował `${repeat:Dept}`.

## Obsługa przypadków brzegowych

### Puste lub nullowe tablice

Jeśli `Dept` jest null lub pusty, procesor nie utworzy dodatkowych arkuszy. Aby uniknąć całkowicie pustego skoroszytu, możesz dodać zabezpieczenie:

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### Niestandardowe nazwy arkuszy

Domyślny schemat nazewnictwa może nie pasować do wszystkich wymagań raportowych. Po przetworzeniu, przemianuj każdy arkusz w pętli:

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### Wypełnianie dodatkowych kolumn

Jeśli potrzebujesz **wypełnić Excel danymi z tablicy** poza pojedynczym markerem, rozszerz obiekt danych:

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

Następnie dostosuj markery w szablonie do `${repeat:Dept.Name}` i `${repeat:Dept.Headcount}`. Procesor powieli wiersz dla każdego działu i wypełni obie kolumny.

## Pełny działający przykład

Poniżej znajduje się samodzielna aplikacja konsolowa, która demonstruje cały przepływ od ładowania szablonu po zapis końcowego skoroszytu.

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**Wyjaśnienie kluczowych sekcji**

- **Utworzenie procesora** – ustanawia silnik, który będzie interpretował markery.
- **Opcja RepeatWorksheet** – aktywuje podstawową funkcję, która odpowiada na pytanie *jak powielać arkusz*.
- **Źródło danych** – używa tablicy (`new[]`) aby spełnić **wypełnić Excel danymi z tablicy**.
- **Ładowanie szablonu** – pokazuje typowy sposób uzyskania obiektu arkusza.
- **Przetwarzanie** – wykonuje duplikację i wstawianie danych w jednym wywołaniu.
- **Renamowanie** – pokazuje, jak zamienić ogólne nazwy „(1)”, „(2)” na znaczące tytuły, typowy wymóg po **generowaniu wielu arkuszy**.

Uruchomienie tego programu generuje `Result.xlsx` z trzema zakładkami specyficznymi dla działów, każda wypełniona danymi z tablicy.

## Częste pułapki i wskazówki profesjonalne

- **Pisownia markera** – marker musi dokładnie odpowiadać nazwie właściwości (`${repeat:Dept}`). Błąd literowy uniemożliwia powielanie.
- **Indeks arkusza** – po przetworzeniu oryginalny arkusz pozostaje na indeksie 0; wygenerowane arkusze następują kolejno. Nieprawidłowe indeksowanie może spowodować przemianowanie niewłaściwej zakładki.
- **Duże zestawy danych** – generowanie setek arkuszy może znacznie zwiększyć rozmiar pliku. Rozważ podział raportów lub użycie jednego arkusza z sekcjami grupowanymi, jeśli wydajność stanie się problemem.
- **Bezpieczeństwo wątków** – `SmartMarkerProcessor` nie jest bezpieczny wątkowo. Utwórz osobną instancję na wątek, jeśli przetwarzasz wiele skoroszytów równocześnie.

## Zakończenie

Teraz wiesz, **jak powielać arkusz** w Excelu przy użyciu SmartMarkerProcessor, jak **wypełnić Excel danymi z tablicy**, jak **generować wiele arkuszy**, oraz jak **wypełnić arkusz z listy** efektywnie. Pełny przykład łączy wszystkie koncepcje, a opcjonalny krok przemianowy pozwala uzyskać czyste, przyjazne dla użytkownika nazwy zakładek.

Następnie możesz zbadać:

- Użycie **wypełnić arkusz z listy** z złożonymi obiektami (zagnieżdżone kolekcje)
- Stosowanie formatowania warunkowego po duplikacji arkusza
- Eksportowanie wygenerowanego skoroszytu do PDF lub CSV w celu dalszego wykorzystania

Śmiało dostosuj kod do własnych scenariuszy raportowych i ciesz się automatyzacją skoroszytów Excel z pewnością!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak powielać arkusze – Kompletny przewodnik po automatyzacji Excel](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [Utwórz arkusz na element – Jak powielać arkusz w C#](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [Jak rozwinąć tablicę w Excelu i wypełnić szablon](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}