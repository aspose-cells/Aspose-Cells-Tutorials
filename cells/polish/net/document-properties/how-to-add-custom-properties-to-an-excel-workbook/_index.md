---
category: general
date: 2026-10-01
description: Dowiedz się, jak dodać własne właściwości do skoroszytu Excel przy użyciu
  Aspose.Cells. Ten przewodnik pokazuje również, jak dodać identyfikator projektu
  i odczytać własne właściwości.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom properties
- how to add custom
- excel custom properties
- add project id
- read custom properties
language: pl
lastmod: 2026-10-01
og_description: Dodaj niestandardowe właściwości do skoroszytu Excel przy użyciu Aspose.Cells.
  Skorzystaj z tego pełnego samouczka, aby dodać identyfikator projektu, ustawić informacje
  o recenzencie oraz odczytać niestandardowe właściwości programowo.
og_image_alt: Screenshot of an Excel worksheet displaying custom properties added
  via Aspose.Cells
og_title: Dodaj własne właściwości do skoroszytu Excel – przewodnik krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  headline: How to add custom properties to an Excel workbook
  type: TechArticle
- description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  name: How to add custom properties to an Excel workbook
  steps:
  - name: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
    text: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
  - name: Go to **File → Info → Properties → Advanced Properties**.
    text: Go to **File → Info → Properties → Advanced Properties**.
  - name: Select the **Custom** tab.
    text: Select the **Custom** tab.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak dodać niestandardowe właściwości do skoroszytu Excel
url: /pl/net/document-properties/how-to-add-custom-properties-to-an-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak dodać własne właściwości do skoroszytu Excel

Jeśli potrzebujesz **dodać własne właściwości** do skoroszytu Excel, ten przewodnik pokaże Ci dokładnie, jak to zrobić przy użyciu Aspose.Cells for .NET. Dowiesz się również, jak dodać identyfikator projektu, ustawić nazwę recenzenta oraz później **odczytać własne właściwości** z pliku.

Praca z własnymi metadanymi pozwala osadzić informacje specyficzne dla biznesu bezpośrednio w arkuszu kalkulacyjnym, co ułatwia śledzenie właściciela, wersji lub dowolnego innego kontekstu bez konieczności utrzymywania osobnej bazy danych. Poniższe kroki obejmują kompletny przepływ pracy od tworzenia skoroszytu po zachowanie nowych właściwości.

## Wymagania wstępne

* .NET 6.0 lub nowszy zainstalowany  
* Ważna licencja Aspose.Cells for .NET (lub wersja próbna)  
* Visual Studio 2022 (lub dowolne IDE C#)  

Nie są wymagane dodatkowe pakiety NuGet poza `Aspose.Cells`.

## Krok 1: Konfiguracja projektu i importowanie przestrzeni nazw

Utwórz nową aplikację konsolową i dodaj odwołanie do Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // The rest of the code lives here
        }
    }
}
```

Przestrzeń nazw `Aspose.Cells` zawiera klasy `Workbook`, `Worksheet` oraz `CustomPropertyCollection`, których będziemy używać.

## Krok 2: Załaduj istniejący skoroszyt (lub utwórz nowy)

Możesz rozpocząć od istniejącego pliku `.xlsb` lub wygenerować nowy skoroszyt. Poniższy przykład ładuje plik o nazwie **Data.xlsb** znajdujący się w folderze o nazwie `YOUR_DIRECTORY`.

```csharp
// Load the existing workbook
var workbookPath = @"YOUR_DIRECTORY\Data.xlsb";
var workbook = new Workbook(workbookPath);
```

Jeśli plik nie istnieje, zamień kod na `new Workbook();`, aby utworzyć pusty skoroszyt.

## Krok 3: Dodaj własne właściwości do pierwszego arkusza

Główną operacją jest **dodanie własnych właściwości** do arkusza. Aspose.Cells przechowuje własne właściwości w kolekcji zachowującej się jak słownik.

```csharp
// Get the first worksheet (index 0)
var worksheet = workbook.Worksheets[0];

// Add a numeric ProjectId property
worksheet.CustomProperties.Add("ProjectId", 12345);

// Add a string Reviewer property
worksheet.CustomProperties.Add("Reviewer", "John Doe");

// Optional: add a DateTime property for the creation timestamp
worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);
```

Używamy `CustomProperties.Add` zamiast `CustomProperties["Name"] = value`, ponieważ metoda `Add` tworzy wpis, jeśli nie istnieje, i zapewnia, że przechowywany jest prawidłowy typ danych. Takie podejście zapobiega przypadkowym niezgodnościom typów, które mogłyby powodować błędy w czasie wykonywania podczas późniejszego odczytu wartości.

## Krok 4: Zapisz skoroszyt z nowymi właściwościami

Po wstrzyknięciu metadanych zapisz zmiany do nowego pliku, aby oryginał pozostał niezmieniony.

```csharp
// Save the workbook with the custom properties
var outputPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

W tym momencie plik Excel zawiera zdefiniowane przez Ciebie własne metadane. Możesz zweryfikować właściwości, korzystając z kroków w następnym rozdziale.

## Krok 5: Odczytaj własne właściwości ze skoroszytu

Odczytywanie **własnych właściwości Excel** odbywa się według tego samego wzorca kolekcji. Ten fragment kodu pokazuje, jak pobrać wartości, które właśnie zapisaliśmy.

```csharp
// Load the workbook that contains custom properties
var loadedWorkbook = new Workbook(outputPath);
var loadedWorksheet = loadedWorkbook.Worksheets[0];
var props = loadedWorksheet.CustomProperties;

// Retrieve each property safely
int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

Console.WriteLine($"ProjectId: {projectId}");
Console.WriteLine($"Reviewer: {reviewer}");
Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
```

Indeksator `CustomPropertyCollection` zwraca obiekt `CustomProperty`; dostęp do jego właściwości `Value` daje przechowywane dane w ich pierwotnym typie. Sprawdzenie pod kątem `null` przed rzutowaniem zapobiega `NullReferenceException`, jeśli właściwość nie istnieje.

### Oczekiwany wynik w konsoli

```
ProjectId: 12345
Reviewer: John Doe
CreatedOn (UTC): 2026-10-01 12:34:56Z
```

Znacznik czasu odzwierciedli dokładny moment, w którym wywołałeś `Add` w kroku 3.

## Porada: Aktualizacja istniejącej własnej właściwości

Jeśli później potrzebujesz **dodać własne** informacje (na przykład zmienić recenzenta), użyj settera `CustomPropertyCollection`:

```csharp
// Change the reviewer name
if (props["Reviewer"] != null)
{
    props["Reviewer"].Value = "Jane Smith";
}
else
{
    // Property does not exist; add it
    props.Add("Reviewer", "Jane Smith");
}
```

Ten wzorzec zapewnia, że właściwość zostanie zaktualizowana lub utworzona, co jest przydatne w iteracyjnych przepływach pracy, takich jak automatyczne generowanie raportów.

## Krok 6: Zweryfikuj właściwości w Excelu (opcjonalnie)

Możesz również zobaczyć własne właściwości bezpośrednio w Excelu:

1. Otwórz zapisany plik `DataWithProps.xlsb` w Microsoft Excel.  
2. Przejdź do **Plik → Informacje → Właściwości → Właściwości zaawansowane**.  
3. Wybierz zakładkę **Własne**.  

Zobaczysz wpisy `ProjectId`, `Reviewer` i `CreatedOn` wraz z ich odpowiednimi wartościami.

## Pełny działający przykład

Poniżej znajduje się kompletny, samodzielny program, który łączy wszystkie poprzednie fragmenty kodu. Skopiuj go do `Program.cs` i uruchom; konsola wyświetli pobrane wartości.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // Paths (adjust to your environment)
            var sourcePath = @"YOUR_DIRECTORY\Data.xlsb";
            var resultPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";

            // Load or create workbook
            var workbook = new Workbook(sourcePath);
            var worksheet = workbook.Worksheets[0];

            // Add custom properties
            worksheet.CustomProperties.Add("ProjectId", 12345);
            worksheet.CustomProperties.Add("Reviewer", "John Doe");
            worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);

            // Save the workbook
            workbook.Save(resultPath);
            Console.WriteLine($"Saved workbook with custom properties to {resultPath}");

            // Load the saved workbook to read properties
            var loadedWorkbook = new Workbook(resultPath);
            var loadedWorksheet = loadedWorkbook.Worksheets[0];
            var props = loadedWorksheet.CustomProperties;

            // Read properties
            int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
            string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
            DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

            Console.WriteLine($"ProjectId: {projectId}");
            Console.WriteLine($"Reviewer: {reviewer}");
            Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
        }
    }
}
```

Uruchomienie tego programu generuje wyjście w konsoli pokazane wcześniej i tworzy `DataWithProps.xlsb` zawierający osadzone metadane.

## Częste pytania i przypadki brzegowe

| Pytanie | Odpowiedź |
|---|---|
| **Czy mogę przechowywać typy nie‑pierwotne?** | Aspose.Cells obsługuje `string`, `int`, `double`, `DateTime` i `bool`. W przypadku złożonych obiektów najpierw należy je zserializować do JSON lub XML i przechowywać jako ciąg znaków. |
| **Co jeśli skoroszyt jest zabezpieczony hasłem?** | Otwórz skoroszyt z hasłem (`new Workbook(path, password)`) przed dostępem do `CustomProperties`. Właściwości pozostają dostępne po odszyfrowaniu. |
| **Czy własne właściwości przetrwają konwersję formatu?** | Podczas zapisywania do innego formatu (np. `.xlsx`) Aspose.Cells zachowuje własne właściwości, o ile docelowy format je obsługuje. |
| **Jak usunąć własną właściwość?** | Użyj `worksheet.CustomProperties.Remove("PropertyName");`. Usuwa to wpis z kolekcji. |

## Kolejne kroki

Teraz, gdy wiesz, jak **dodawać własne właściwości**, możesz zgłębić powiązane tematy, takie jak:

* **excel custom properties** dla wersjonowania dokumentów  
* **read custom properties** z wielu arkuszy w jednym skoroszycie  
* Korzystanie z **Aspose.Cells** do tworzenia tabel przestawnych odwołujących się do własnych metadanych  
* Eksportowanie skoroszytu do PDF przy zachowaniu własnych właściwości  

Eksperymentuj z różnymi typami danych, łącz własne właściwości z komentarzami komórek lub integruj metadane w większym systemie zarządzania dokumentami.

---

**Gotowy, aby zautomatyzować raportowanie w Excelu?** Dodaj powyższy kod do swojego projektu, dostosuj nazwy właściwości do potrzeb biznesowych i będziesz mieć samowyjaśniający się arkusz gotowy do dalszego przetwarzania.

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Utwórz skoroszyt Excel – Dodaj własne właściwości i zapisz jako XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [Jak uzyskać dostęp do własnych właściwości dokumentu w Excelu przy użyciu Aspose.Cells for .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [Opanuj własne właściwości Excel przy użyciu Aspose.Cells .NET dla zaawansowanego zarządzania danymi](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}