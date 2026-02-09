---
category: general
date: 2026-02-09
description: Utwórz nowy skoroszyt Excel i dowiedz się, jak bez wysiłku kopiować tabele
  przestawne. Ten przewodnik pokazuje, jak zduplikować tabelę przestawną i zapisać
  skoroszyt jako nowy.
draft: false
keywords:
- create new excel workbook
- how to copy pivot
- duplicate pivot table
- save workbook as new
- how to copy worksheet
language: pl
og_description: Utwórz nowy skoroszyt Excel w C# i natychmiast skopiuj tabelę przestawną.
  Dowiedz się, jak zduplikować tabelę przestawną i zapisać skoroszyt jako nowy, z
  pełnym przykładem kodu.
og_title: Utwórz nowy skoroszyt Excel – kopiowanie tabel przestawnych krok po kroku
tags:
- excel
- csharp
- aspose.cells
- automation
title: Utwórz nowy skoroszyt Excel – kopiuj i duplikuj tabelę przestawną
url: /pl/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz nowy skoroszyt Excel – kopiowanie i duplikowanie tabeli przestawnej

Czy kiedykolwiek potrzebowałeś **create new Excel workbook**, które przenosi złożoną tabelę przestawną z istniejącego pliku? Nie jesteś jedyny — wielu programistów napotyka ten problem przy automatyzacji pipeline'ów raportowych. Dobrą wiadomością jest to, że przy kilku linijkach C# i bibliotece Aspose.Cells możesz **how to copy pivot** szybko, **duplicate pivot table**, i **save workbook as new** bez ręcznego otwierania Excela.

W tym przewodniku przeprowadzimy Cię przez cały proces, od wczytania źródłowego skoroszytu po zapisanie zduplikowanej wersji. Na końcu będziesz mieć gotowy do uruchomienia fragment kodu, który możesz wkleić do dowolnego projektu .NET. Bez zbędnych ozdobników, tylko praktyczne rozwiązanie, które możesz przetestować już dziś.

## Co obejmuje ten tutorial

* **Prerequisites** – .NET 6+ (lub .NET Framework 4.6+), Visual Studio oraz pakiet NuGet Aspose.Cells for .NET.
* Krok po kroku kod, który **creates new Excel workbook**, kopiuje tabelę przestawną i zapisuje wynik na dysku.
* Wyjaśnienia **dlaczego** każda linijka ma znaczenie, nie tylko **co** robi.
* Wskazówki dotyczące obsługi przypadków brzegowych, takich jak ukryte arkusze czy duże zakresy danych.
* Krótkie spojrzenie na **how to copy worksheet**, jeśli kiedykolwiek będziesz potrzebował całego arkusza zamiast samej tabeli przestawnej.

Gotowy? Zanurzmy się.

![ilustracja tworzenia nowego skoroszytu Excel](image.png "Diagram przedstawiający źródłowy skoroszyt, kopiowanie tabeli przestawnej i docelowy skoroszyt")

## Krok 1: Przygotuj projekt i zainstaluj Aspose.Cells

Zanim będziemy mogli **create new Excel workbook**, potrzebujemy projektu, który odwołuje się do właściwej biblioteki.

```csharp
// Install the Aspose.Cells package via NuGet:
//   dotnet add package Aspose.Cells
using Aspose.Cells;   // Provides Workbook, Worksheet, Range, etc.
using System;        // For basic .NET types
```

*Dlaczego to jest ważne:* Aspose.Cells działa w pełni w pamięci, więc nigdy nie musisz uruchamiać Excela na serwerze. Zachowuje także informacje o pamięci podręcznej tabeli przestawnej, co jest niezbędne do prawdziwego **duplicate pivot table**.

> **Pro tip:** Jeśli tworzysz aplikację pod .NET Core, upewnij się, że identyfikator środowiska uruchomieniowego (RID) projektu odpowiada platformie, na którą będziesz wdrażać; w przeciwnym razie możesz napotkać błędy ładowania natywnych bibliotek.

## Krok 2: Wczytaj źródłowy skoroszyt zawierający tabelę przestawną

Teraz **how to copy pivot** z istniejącego pliku. Źródłowy skoroszyt może znajdować się gdziekolwiek na dysku, w strumieniu lub nawet w tablicy bajtów.

```csharp
// Step 2: Load the source workbook that contains the pivot table
string sourcePath = @"C:\Reports\source.xlsx";
Workbook sourceWorkbook = new Workbook(sourcePath);

// Grab the first worksheet (adjust the index if your pivot lives elsewhere)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that encloses the pivot table – A1:D20 in this example
Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");
```

*Dlaczego wybieramy zakres:* Tabela przestawna znajduje się w zwykłym zakresie komórek, ale ma także ukryte dane pamięci podręcznej powiązane z arkuszem. Kopiując zakres **including the pivot**, Aspose.Cells zapewnia, że pamięć podręczna podróżuje razem z nim, dając Ci funkcjonalny **duplicate pivot table** w pliku docelowym.

## Krok 3: Utwórz nowy skoroszyt Excel, aby przyjąć skopiowane dane

Tutaj faktycznie **create new Excel workbook**, który będzie przechowywał zduplikowaną tabelę przestawną.

```csharp
// Step 3: Create a fresh workbook (empty) for the destination
Workbook destinationWorkbook = new Workbook(); // Starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

// Destination starts at A1 – you could offset if you need space for other data
Range destinationRange = destinationSheet.Cells.CreateRange("A1");
```

> **Dlaczego świeży skoroszyt?** Rozpoczęcie od czystego stanu gwarantuje, że żadne pozostałe formatowanie ani ukryte obiekty nie zakłócą skopiowanej tabeli przestawnej. Dzięki temu wynikowy plik jest mniejszy, co jest przydatne przy automatycznych załącznikach e‑mail.

## Krok 4: Skopiuj zakres tabeli przestawnej do nowego skoroszytu

Teraz wykonujemy rzeczywistą operację **how to copy pivot**.

```csharp
// Step 4: Copy the range (including the pivot) from source to destination
sourceRange.Copy(destinationRange);
```

Ta pojedyncza linijka wykonuje najcięższą pracę:

* Wartości komórek, formuły i formatowanie są przenoszone.
* Pamięć podręczna tabeli przestawnej jest duplikowana, więc nowa tabela pozostaje w pełni funkcjonalna.
* Wszelkie względne odwołania wewnątrz tabeli przestawnej automatycznie dostosowują się do nowej lokalizacji.

### Obsługa przypadków brzegowych

* **Hidden worksheets:** Jeśli arkusz źródłowy jest ukryty, tabela przestawna i tak zostanie skopiowana poprawnie, ale możesz chcieć odkryć arkusz docelowy dla widoczności użytkownika:
  ```csharp
  destinationSheet.IsVisible = true;
  ```
* **Large data sets:** Dla zakresów większych niż kilka tysięcy wierszy rozważ użycie `CopyTo` z `CopyOptions`, aby strumieniować operację i zmniejszyć obciążenie pamięci.

## Krok 5: Zapisz docelowy skoroszyt jako nowy plik

Na koniec **save workbook as new** i zweryfikuj wynik.

```csharp
// Step 5: Save the destination workbook with the duplicated pivot table
string destPath = @"C:\Reports\copied.xlsx";
destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

// Quick verification – open the file manually or read a cell value
Console.WriteLine($"Workbook saved to {destPath}");
```

Jeśli otworzysz `copied.xlsx`, zobaczysz dokładną kopię oryginalnej tabeli przestawnej, gotową do dalszej manipulacji lub dystrybucji.

### Opcjonalnie: Jak skopiować arkusz zamiast samej tabeli przestawnej

Czasami potrzebny jest cały arkusz, nie tylko tabela przestawna. To samo API czyni to trywialnym:

```csharp
// Copy the whole worksheet (including all charts, tables, etc.)
sourceSheet.CopyTo(destinationWorkbook, 0); // Inserts at index 0
destinationWorkbook.Save(@"C:\Reports\full_copy.xlsx");
```

To spełnia zapytanie **how to copy worksheet** i może być przydatne, gdy musisz zachować dodatkowe ustawienia na poziomie arkusza.

## Pełny działający przykład

Łącząc wszystko razem, oto samodzielna aplikacja konsolowa, którą możesz skompilować i uruchomić:

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load source workbook
        string sourcePath = @"C:\Reports\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");

        // 2️⃣ Create destination workbook
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
        Range destinationRange = destinationSheet.Cells.CreateRange("A1");

        // 3️⃣ Copy the pivot (range)
        sourceRange.Copy(destinationRange);

        // 4️⃣ Save as new file
        string destPath = @"C:\Reports\copied.xlsx";
        destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Successfully created new Excel workbook with duplicated pivot table at {destPath}");
    }
}
```

**Expected output:** Konsola wyświetla komunikat o sukcesie, a `copied.xlsx` pojawia się w `C:\Reports` z funkcjonalną tabelą przestawną identyczną z tą w `source.xlsx`.

## Częste pytania i pułapki

* **Will formulas inside the pivot break?** Nie — ponieważ pamięć podręczna tabeli przestawnej podróżuje wraz z zakresem, wszystkie pola obliczeniowe pozostają nienaruszone.
* **What if the source pivot uses external data connections?** Te połączenia *nie* są kopiowane. Będziesz musiał je ponownie ustanowić w skoroszycie docelowym lub najpierw przekształcić tabelę przestawną w statyczną tabelę.
* **Can I copy multiple pivots at once?** Oczywiście — po prostu zdefiniuj większy zakres obejmujący wszystkie tabele przestawne lub iteruj po każdym obiekcie `PivotTable` w `sourceSheet.PivotTables` i kopiuj je indywidualnie.
* **Do I need to dispose of the `Workbook` objects?** Implementują one `IDisposable`, więc owinięcie ich w instrukcje `using` jest dobrą praktyką, szczególnie w usługach o wysokim natężeniu.

## Zakończenie

Teraz wiesz, **how to create new Excel workbook**, jak skopiować tabelę przestawną, **duplicate pivot table** oraz **save workbook as new** przy użyciu C# i Aspose.Cells. Kroki są proste: wczytaj, utwórz, skopiuj i zapisz. Dzięki opcjonalnemu fragmentowi **how to copy worksheet** masz także rozwiązanie awaryjne dla pełnego kopiowania arkusza.

Następnie możesz zgłębić:

* Dodawanie własnego formatowania do zduplikowanej tabeli przestawnej.
* Odświeżanie pamięci podręcznej tabeli przestawnej programowo po zmianach danych.
* Eksportowanie skoroszytu do PDF lub CSV dla systemów downstream.

Wypróbuj, dostosuj zakres i pozwól automatyzacji przejąć ciężką pracę w Twoim procesie raportowania. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}