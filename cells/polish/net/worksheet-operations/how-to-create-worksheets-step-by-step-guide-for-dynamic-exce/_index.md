---
category: general
date: 2026-03-21
description: Dowiedz się, jak tworzyć arkusze, generować pliki Excel z dynamicznymi
  nazwami arkuszy oraz zapisywać skoroszyt jako XLSX przy użyciu Aspose.Cells w C#.
draft: false
keywords:
- how to create worksheets
- save workbook as xlsx
- generate excel sheets
- dynamic worksheet names
- process master sheet
language: pl
og_description: Jak tworzyć arkusze w Excelu przy użyciu Aspose.Cells, generować arkusze
  Excel z dynamicznymi nazwami arkuszy i zapisywać skoroszyt jako XLSX.
og_title: Jak tworzyć arkusze – Kompletny samouczek C#
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak tworzyć arkusze kalkulacyjne – Przewodnik krok po kroku po dynamicznym
  generowaniu Excela
url: /pl/net/worksheet-operations/how-to-create-worksheets-step-by-step-guide-for-dynamic-exce/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak tworzyć arkusze – Kompletny tutorial C#

Zastanawiałeś się kiedyś **jak tworzyć arkusze** „w locie”, bez ręcznego otwierania Excela za każdym razem? Nie jesteś sam. Wielu programistów napotyka problem, gdy muszą **generować arkusze Excel** z źródeł danych i chcą, aby każdy arkusz miał znaczącą, dynamiczną nazwę. Dobra wiadomość? Dzięki Aspose.Cells możesz zautomatyzować cały proces, **przetworzyć arkusz główny** i w końcu **zapisać skoroszyt jako XLSX** w kilku linijkach kodu.

W tym tutorialu przejdziemy przez scenariusz z życia wzięty: zaczniemy od pustego skoroszytu, wstawimy token smart‑marker, który mówi Aspose, które arkusze szczegółowe utworzyć, skonfigurujemy wzorzec nazewnictwa, aby każdy arkusz otrzymał unikalną nazwę, i w końcu zapisujemy wynik na dysku. Po zakończeniu będziesz mieć gotowy do uruchomienia program w C#, który tworzy arkusze, generuje arkusze Excel z dynamicznymi nazwami arkuszy i zapisuje skoroszyt jako XLSX — bez interakcji z UI.

> **Wymagania wstępne**  
> • .NET 6+ (lub .NET Framework 4.6+).  
> • Aspose.Cells for .NET (bezpłatna wersja próbna wystarczy do tego demo).  
> • Podstawowa znajomość C# — nie są potrzebne zaawansowane triki z Excel Interop.

---

## Przegląd tego, co zbudujemy

- **Arkusz główny** zawierający placeholder smart‑marker (`«DetailSheetNewName:Dept»`).  
- **SmartMarkerProcessor**, który odczytuje źródło danych (np. `DataTable`) i tworzy nowy arkusz dla każdego działu.  
- **Dynamiczne nazwy arkuszy** według wzorca `Dept_{0}`, gdzie `{0}` zostaje zastąpione nazwą działu.  
- **Końcowy plik XLSX** zapisany w wybranym folderze.

To wszystko. Proste, a jednocześnie wystarczająco potężne dla faktur, raportów czy każdego wielokartkowego wyjścia Excel.

---

![Diagram pokazujący, jak arkusz główny jest przetwarzany w celu wygenerowania wielu dynamicznych arkuszy](/images/how-to-create-worksheets-diagram.png "Diagram tworzenia arkuszy")

*Alt text: ilustracja pokazująca, jak tworzyć arkusze z dynamicznymi nazwami arkuszy przy użyciu Aspose.Cells.*

---

## Krok 1: Konfiguracja projektu i dodanie Aspose.Cells

### Dlaczego to ważne
Zanim jakikolwiek kod zostanie skompilowany, kompilator musi wiedzieć, gdzie znajdują się klasy `Workbook`, `Worksheet` i `SmartMarkerProcessor`. Dodanie pakietu NuGet zapewnia najnowsze, w pełni funkcjonalne API.

```csharp
// Install via CLI
// dotnet add package Aspose.Cells

using Aspose.Cells;
using System.Data;
```

> **Porada:** Jeśli używasz Visual Studio, kliknij prawym przyciskiem myszy projekt → *Manage NuGet Packages* → wyszukaj *Aspose.Cells* i zainstaluj najnowszą stabilną wersję.

---

## Krok 2: Utworzenie nowego skoroszytu i arkusza głównego

### Co robimy
Zaczynamy od czystego skoroszytu, a następnie pobieramy pierwszy arkusz (indeks 0). Ten arkusz będzie pełnił rolę **arkusza głównego**, w którym znajduje się token smart‑marker.

```csharp
// Step 1: Create a new workbook and get the first worksheet (master sheet)
Workbook workbook = new Workbook();
Worksheet masterSheet = workbook.Worksheets[0];

// Optional: give the master sheet a friendly name
masterSheet.Name = "Master";
```

Klasa `Workbook` jest kontenerem dla wszystkich arkuszy. Domyślnie tworzy jeden arkusz o nazwie *Sheet1*; zmiana nazwy na „Master” ułatwia późniejszą nawigację w pliku.

---

## Krok 3: Wstawienie tokenu smart‑marker dla nazw arkuszy szczegółowych

### Dlaczego używać smart‑markera?
Smart markery pozwalają Aspose.Cells zastępować placeholdery danymi w czasie wykonywania. Token `«DetailSheetNewName:Dept»` mówi procesorowi: *„Kiedy zobaczysz to, utwórz nowy arkusz szczegółowy dla każdego wiersza w kolumnie `Dept`.”*

```csharp
// Step 2: Place a smart‑marker token that will be replaced with detail sheet names
masterSheet.Cells["A1"].PutValue("«DetailSheetNewName:Dept»");
```

Token możesz umieścić w dowolnym miejscu; wybraliśmy **A1** dla przejrzystości. Gdy procesor zostanie uruchomiony, zamieni token na rzeczywistą nazwę działu i wygeneruje odpowiadający arkusz.

---

## Krok 4: Przygotowanie źródła danych

### Jak dane napędzają tworzenie arkuszy
Aspose.Cells współpracuje z dowolnym źródłem danych typu `IEnumerable`. W tym demo użyjemy `DataTable` z jedną kolumną o nazwie `Dept`.

```csharp
// Sample data source: list of departments
DataTable dataSource = new DataTable();
dataSource.Columns.Add("Dept", typeof(string));

// Populate with example rows
dataSource.Rows.Add("Finance");
dataSource.Rows.Add("HR");
dataSource.Rows.Add("IT");
dataSource.Rows.Add("Marketing");
```

> **Co jeśli masz więcej kolumn?**  
> Procesor zignoruje dodatkowe kolumny, chyba że odwołasz się do nich w kolejnych smart markerach. Dzięki temu generowanie arkuszy pozostaje lekkie.

---

## Krok 5: Konfiguracja SmartMarkerProcessor i wzorca nazewnictwa

### Dynamiczne nazwy arkuszy w praktyce
Chcemy, aby każdy nowy arkusz miał nazwę `Dept_Finance`, `Dept_HR` itd. Opcja `DetailSheetNewName` pozwala zdefiniować wzorzec, w którym `{0}` zostaje podstawione rzeczywistą nazwą działu.

```csharp
// Step 3: Initialise the SmartMarker processor and set the naming pattern for generated sheets
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
processor.Options.DetailSheetNewName = "Dept_{0}";   // Aspose adds an index if needed
```

Jeśli dział pojawi się dwukrotnie, Aspose automatycznie doda przyrostek liczbowy (np. `Dept_Finance_1`), aby uniknąć duplikatów nazw arkuszy.

---

## Krok 6: Przetworzenie arkusza głównego w celu wygenerowania arkuszy szczegółowych

### Sedno **process master sheet**
Wywołanie `Process` wykonuje najcięższą pracę: skanuje arkusz główny w poszukiwaniu smart markerów, tworzy nowe arkusze, kopiuje układ arkusza głównego i wypełnia je danymi z wiersza.

```csharp
// Step 4: Process the master sheet using the data source to create detail sheets
processor.Process(masterSheet, dataSource);
```

Po tym wywołaniu skoroszyt zawiera jeden arkusz główny oraz cztery arkusze szczegółowe — każdy nazwany zgodnie z naszym wzorcem i wypełniony nazwą działu w komórce A1.

---

## Krok 7: Zapis skoroszytu jako XLSX

### Ostatni krok — **save workbook as XLSX**
Teraz, gdy arkusze istnieją, zapisujemy plik na dysku. Możesz wybrać dowolną ścieżkę; upewnij się tylko, że katalog istnieje.

```csharp
// Step 5: Save the resulting workbook to a file
string outputPath = @"C:\Temp\DetailSheets.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Otwierając `DetailSheets.xlsx`, zobaczysz:

| Nazwa arkusza | Zawartość komórki A1 |
|---------------|----------------------|
| Master        | «DetailSheetNewName:Dept» (bez zmian) |
| Dept_Finance  | Finance |
| Dept_HR       | HR |
| Dept_IT       | IT |
| Dept_Marketing| Marketing |

> **Przypadek brzegowy:** Jeśli docelowy folder nie istnieje, `Save` zgłosi `DirectoryNotFoundException`. Owiń wywołanie w blok try‑catch lub utwórz folder wcześniej.

---

## Pełny działający przykład

Łącząc wszystko razem, oto kompletny program, który możesz skopiować i wkleić do aplikacji konsolowej:

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelDynamicSheetsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and master sheet
            Workbook workbook = new Workbook();
            Worksheet masterSheet = workbook.Worksheets[0];
            masterSheet.Name = "Master";

            // 2️⃣ Insert smart‑marker token
            masterSheet.Cells["A1"].PutValue("«DetailSheetNewName:Dept»");

            // 3️⃣ Build data source (departments)
            DataTable dataSource = new DataTable();
            dataSource.Columns.Add("Dept", typeof(string));
            dataSource.Rows.Add("Finance");
            dataSource.Rows.Add("HR");
            dataSource.Rows.Add("IT");
            dataSource.Rows.Add("Marketing");

            // 4️⃣ Configure processor with dynamic naming
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
            processor.Options.DetailSheetNewName = "Dept_{0}";

            // 5️⃣ Process master sheet → generate detail sheets
            processor.Process(masterSheet, dataSource);

            // 6️⃣ Save as XLSX
            string outputPath = @"C:\Temp\DetailSheets.xlsx";
            try
            {
                workbook.Save(outputPath, SaveFormat.Xlsx);
                Console.WriteLine($"✅ Workbook saved to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❌ Failed to save workbook: {ex.Message}");
            }
        }
    }
}
```

Uruchom program, otwórz wygenerowany plik i zobacz dokładnie taki układ, jak opisano wcześniej. Bez ręcznego kopiowania, bez COM interop — po prostu czysty kod C#, który **generuje arkusze Excel** z **dynamicznymi nazwami arkuszy**.

---

## Częste pytania i pułapki

| Pytanie | Odpowiedź |
|----------|-----------|
| *Czy mogę użyć DataSet z wieloma tabelami?* | Tak. Przekaż odpowiednią tabelę do `Process` lub użyj słownika tabel. |
| *Co zrobić, jeśli potrzebuję więcej niż jednego smart‑markera na arkuszu głównym?* | Umieść dodatkowe tokeny, np. `«DetailSheetNewName:Region»` i skonfiguruj osobny wzorzec nazewnictwa w razie potrzeby. |
| *Czy arkusz główny pozostaje w pliku końcowym?* | Domyślnie tak. Jeśli go nie potrzebujesz, wywołaj `workbook.Worksheets.RemoveAt(0)` po przetworzeniu. |
| *Jak Aspose radzi sobie z bardzo dużymi zestawami danych?* | Strumieniuje dane efektywnie, ale możesz zwiększyć `MemorySetting`, jeśli napotkasz limity pamięci. |
| *Czy mogę eksportować do CSV zamiast XLSX?* | Oczywiście — użyj `workbook.Save("file.csv", SaveFormat.Csv)`. Logika tworzenia arkuszy pozostaje taka sama. |

---

## Kolejne kroki

Teraz, gdy wiesz **jak dynamicznie tworzyć arkusze**, możesz rozważyć:

- **Zapis skoroszytu jako XLSX** z ochroną hasłem (`workbook.Protect("pwd")`).  
- **Generowanie arkuszy Excel** z źródeł JSON lub XML przy użyciu `JsonDataSource` lub `XmlDataSource`.  
- **Stosowanie stylów** do każdego wygenerowanego arkusza (czcionki, kolory) za pomocą obiektów `Style`.  
- **Scalanie komórek** lub automatyczne wstawianie formuł dla raportów podsumowujących.

Każde z tych rozszerzeń opiera się na tym samym koncepcie **process master sheet**, więc przejście będzie płynne.

---

## Zakończenie

Omówiliśmy cały pipeline: od inicjalizacji skoroszytu, wstawienia smart‑markera, konfiguracji **dynamicznych nazw arkuszy**, przetworzenia arkusza głównego w celu **generowania arkuszy Excel**, aż po **zapis skoroszytu jako XLSX**. Przykład jest kompletny, gotowy do uruchomienia i demonstruje najlepsze praktyki pod kątem wydajności i utrzymania kodu.  

Wypróbuj go, zmodyfikuj wzorzec nazewnictwa, podaj prawdziwe dane biznesowe i zobacz, jak Twoja automatyzacja Excela nabiera tempa. Jeśli napotkasz problemy, zostaw komentarz poniżej — powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}