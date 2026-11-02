---
category: general
date: 2026-03-29
description: Dowiedz się, jak wyeksportować tabele Excel do zwykłego tekstu, zapisać
  ciąg znaków do pliku oraz przekonwertować tabelę Excel na CSV lub TXT przy użyciu
  C#. Zawiera pełny kod i wskazówki.
draft: false
keywords:
- how to export excel
- write string to file
- convert excel table
- export table as csv
- save txt file c#
language: pl
og_description: Jak wyeksportować tabele Excel do plików tekstowych w C#. Pobierz
  pełne rozwiązanie, kod oraz najlepsze praktyki konwertowania tabel Excel i zapisywania
  plików TXT.
og_title: Jak eksportować dane z Excela – Kompletny samouczek C#
tags:
- C#
- Excel
- File I/O
title: Jak eksportować dane z Excela – przewodnik krok po kroku w C#
url: /pl/net/excel-data-export-retrieval/how-to-export-excel-data-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyeksportować dane z Excela – Kompletny przewodnik C#

Zastanawiałeś się kiedyś **jak wyeksportować dane z Excela** bez ręcznego otwierania arkusza? Może potrzebujesz zrzucić tabelę do prostego pliku tekstowego dla starszego systemu, albo chcesz szybki eksport CSV dla potoków analizy danych. W tym samouczku przeprowadzimy Cię przez praktyczne, kompleksowe rozwiązanie, które **zapisuje ciąg znaków do pliku** i pokaże dokładnie, jak **przekształcić tabelę Excel** na format tekstowy z delimitacją przy użyciu C#.

Omówimy wszystko, od wczytania skoroszytu, wybrania właściwej tabeli, skonfigurowania opcji eksportu, po ostateczne zapisanie wyniku jako plik `.txt`. Po zakończeniu będziesz w stanie **wyeksportować tabelę jako CSV** (lub dowolny wybrany separator) oraz zobaczysz kilka przydatnych sztuczek dla projektów **saving txt file C#**. Nie są potrzebne zewnętrzne narzędzia — wystarczy kilka pakietów NuGet i odrobina kodu.

---

## Czego będziesz potrzebować

- **.NET 6.0+** (lub .NET Framework 4.7.2, jeśli wolisz klasyczny)
- **Syncfusion.XlsIO** pakiet NuGet (klasa `ExportTableOptions` znajduje się tutaj)
- Podstawowe IDE C# (Visual Studio, VS Code, Rider — dowolne)
- Skoroszyt Excel zawierający przynajmniej jedną tabelę (w przykładzie użyjemy `ws.Tables[0]`)

> Pro tip: Jeśli nie masz jeszcze biblioteki Syncfusion, uruchom  
> `dotnet add package Syncfusion.XlsIO.Net.Core` z wiersza poleceń.

---

## Krok 1 – Otwórz skoroszyt i pobierz pierwszą tabelę  

Pierwszą rzeczą jest wczytanie pliku Excel i uzyskanie odniesienia do arkusza, który zawiera tabelę. Ten krok jest kluczowy, ponieważ operacja **convert excel table** działa na obiekcie `ITable`, a nie na surowych zakresach komórek.

```csharp
using Syncfusion.XlsIO;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        // Load the workbook (replace with your actual file path)
        using (ExcelEngine excelEngine = new ExcelEngine())
        {
            IApplication application = excelEngine.Excel;
            application.DefaultVersion = ExcelVersion.Xlsx;

            // Open the file
            FileStream stream = new FileStream(@"C:\Data\Sample.xlsx", FileMode.Open, FileAccess.Read);
            IWorkbook workbook = application.Workbooks.Open(stream);
            IWorksheet ws = workbook.Worksheets[0];   // First worksheet
```

*Dlaczego to ważne:* Otwieranie skoroszytu przy użyciu `using` zapewnia zwolnienie wszystkich niezarządzanych zasobów, zapobiegając problemom z blokadą pliku później, gdy próbujesz **write string to file**.

---

## Krok 2 – Skonfiguruj opcje eksportu (czysty tekst, bez nagłówków, separator średnikowy)  

Teraz informujemy Syncfusion, jak ma być serializowana tabela. `ExportTableOptions` pozwala przełączać włączenie nagłówków, wybrać separator oraz zdecydować, czy otrzymać ciąg znaków czy tablicę bajtów.

```csharp
            // Step 2: Configure export options – plain text, omit headers, ';' delimiter
            var exportOptions = new ExportTableOptions
            {
                ExportAsString = true,      // Returns a string we can write directly
                IncludeHeaders = false,     // Skip column headers if you don’t need them
                Delimiter = ";"             // Change to ',' for classic CSV
            };
```

*Dlaczego to ważne:* Ustawienie `IncludeHeaders = false` często odpowiada oczekiwaniom systemów downstream, które już znają kolejność kolumn. Zmiana separatora to sposób, w jaki **export table as CSV** z niestandardowym separatorem.

---

## Krok 3 – Wyeksportuj tabelę do ciągu znaków  

Mając gotowe opcje, wywołujemy `ExportToString`. Ta metoda pobiera całą tabelę (wraz ze wszystkimi wierszami) i zwraca pojedynczy ciąg znaków gotowy do zapisu w pliku.

```csharp
            // Step 3: Export the first table to a string using the configured options
            ITable firstTable = ws.Tables[0];               // Access the first table
            string tableText = firstTable.ExportToString(exportOptions);
```

*Dlaczego to ważne:* Wywołanie `ExportToString` wykonuje ciężką pracę konwersji siatki Excel do formatu z delimitacją. Respektuje ustawiony `Delimiter`, więc otrzymujesz czysty wynik **export table as csv** bez dodatkowego przetwarzania.

---

## Krok 4 – Zapisz wyeksportowany tekst do pliku  

Na koniec zapisujemy ciąg znaków na dysku. `File.WriteAllText` to najprostszy sposób na **save txt file C#**; automatycznie tworzy plik, jeśli nie istnieje, i nadpisuje go w przeciwnym razie.

```csharp
            // Step 4: Write the exported text to a file
            string outputPath = @"C:\Data\ExportedTable.txt";
            File.WriteAllText(outputPath, tableText);
            System.Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

*Dlaczego to ważne:* Zapisując ciąg znaków bezpośrednio, unikasz dodatkowego kroku konwersji. Plik teraz zawiera wiersze takie jak `Value1;Value2;Value3`, gotowe dla dowolnego parsera downstream.

---

## Pełny działający przykład (wszystkie kroki w jednym miejscu)  

Poniżej znajduje się kompletny, gotowy do skopiowania program, który łączy wszystko, o czym rozmawialiśmy. Zawiera obsługę błędów i komentarze dla przejrzystości.

```csharp
using Syncfusion.XlsIO;
using System;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load workbook and get first worksheet
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication app = excelEngine.Excel;
                app.DefaultVersion = ExcelVersion.Xlsx;

                string sourcePath = @"C:\Data\Sample.xlsx";
                using (FileStream fs = new FileStream(sourcePath, FileMode.Open, FileAccess.Read))
                {
                    IWorkbook wb = app.Workbooks.Open(fs);
                    IWorksheet ws = wb.Worksheets[0]; // first sheet

                    // 2️⃣ Set export options (plain text, no headers, ';' delimiter)
                    var opts = new ExportTableOptions
                    {
                        ExportAsString = true,
                        IncludeHeaders = false,
                        Delimiter = ";"
                    };

                    // 3️⃣ Export the first table to a string
                    ITable table = ws.Tables[0];
                    string csvText = table.ExportToString(opts);

                    // 4️⃣ Save the string to a .txt file
                    string destPath = @"C:\Data\ExportedTable.txt";
                    File.WriteAllText(destPath, csvText);

                    Console.WriteLine($"✅ Export complete! File saved at: {destPath}");
                }
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

**Oczekiwany wynik** (zawartość `ExportedTable.txt`):

```
John;Doe;35
Jane;Smith;28
Bob;Brown;42
```

Każdy wiersz odpowiada wierszowi z oryginalnej tabeli Excel, z wartościami oddzielonymi średnikami. Jeśli zmienisz `Delimiter = ","`, otrzymasz klasyczny plik CSV.

---

## Częste pytania i przypadki brzegowe  

### Co zrobić, jeśli mój skoroszyt ma wiele tabel?  
Możesz po prostu zmienić `ws.Tables[0]` na odpowiedni indeks lub przeiterować `ws.Tables`:

```csharp
foreach (var tbl in ws.Tables)
{
    string txt = tbl.ExportToString(opts);
    // Save each table to a separate file or concatenate as needed
}
```

### Jak włączyć nagłówki kolumn?  
Ustaw `IncludeHeaders = true` w `ExportTableOptions`. Jest to przydatne, gdy system downstream oczekuje wiersza nagłówka.

### Czy mogę eksportować do innego folderu dynamicznie?  
Oczywiście. Użyj `Path.Combine` z `Environment.GetFolderPath(Environment.SpecialFolder.Desktop)` lub dowolną ścieżką podaną przez użytkownika, aby uczynić rozwiązanie bardziej elastycznym.

### Co z dużymi plikami?  
W przypadku ogromnych tabel rozważ strumieniowanie wyjścia zamiast ładowania całego ciągu do pamięci:

```csharp
using (StreamWriter writer = new StreamWriter(outputPath))
{
    writer.Write(table.ExportToString(opts));
}
```

### Czy to działa na .NET Core?  
Tak — Syncfusion.XlsIO obsługuje .NET 5/6/7. Po prostu odwołaj się do odpowiedniego pakietu NuGet i jesteś gotowy.

---

## Pro tipy dla niezawodnych eksportów  

- **Zweryfikuj ścieżkę pliku** przed zapisem. Brakujący katalog spowoduje wyrzucenie `DirectoryNotFoundException`.  
- **Sprawdź `ExportAsString`** tylko wtedy, gdy tabela mieści się wygodnie w pamięci; w przeciwnym razie użyj `ExportToStream` dla ogromnych zestawów danych.  
- **Zwróć uwagę na kulturę**: jeśli Twoje dane zawierają przecinki jako separatory dziesiętne, wybierz średnik (`;`) lub tabulację (`\t`) jako separator, aby uniknąć błędów parsowania CSV.  
- **Zablokowanie wersji**: Syncfusion od czasu do czasu zmienia sygnatury API. Zablokuj wersję NuGet (`<PackageReference Include="Syncfusion.XlsIO.Net.Core" Version="21.2.0.44" />`), aby utrzymać powtarzalność kompilacji.

---

## Zakończenie  

W tym przewodniku pokazaliśmy **jak wyeksportować dane z Excela** do plików tekstowych przy użyciu C#. Ładując skoroszyt, konfigurując `ExportTableOptions`, eksportując tabelę do ciągu znaków i w końcu **zapisując ciąg do pliku**, masz teraz solidny wzorzec dla zadań **convert excel table**, **export table as csv** oraz **save txt file C#**.

Śmiało eksperymentuj — zmieniaj separator, włączaj nagłówki lub iteruj po wielu tabelach. To samo podejście sprawdza się przy generowaniu raportów CSV, przekazywaniu danych do starszych parserów lub po prostu archiwizowaniu zawartości arkuszy jako lekkich plików tekstowych.

Masz więcej scenariuszy, które chciałbyś rozwiązać? Może potrzebujesz **write string to file** asynchronicznie, albo chcesz na bieżąco spakować wynik. Sprawdź nasze kolejne samouczki o *asynchronicznym I/O plików w C#* i *pakowaniu plików w .NET*, aby utrzymać tempo.

Szczęśliwego kodowania! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}