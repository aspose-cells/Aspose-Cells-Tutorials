---
category: general
date: 2026-06-08
description: Twórz skoroszyt Excel w C# krok po kroku i ucz się, jak używać funkcji expand
  w Excelu do dynamicznych zakresów. Idealne dla programistów .NET.
draft: false
keywords:
- create excel workbook c#
- use expand function in excel
language: pl
og_description: Utwórz skoroszyt Excel w C# z przejrzystym przykładem i odkryj, jak
  używać funkcji EXPAND w Excelu do generowania dynamicznych tablic.
og_title: Tworzenie skoroszytu Excel w C# – Kompletny przewodnik programistyczny
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  headline: Create Excel Workbook C# – Full Guide with Expand Function
  type: TechArticle
- description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  name: Create Excel Workbook C# – Full Guide with Expand Function
  steps:
  - name: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
    text: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
  - name: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
    text: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
  - name: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
    text: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
  - name: '**Creates an Excel workbook C#** using Aspose.Cells.'
    text: '**Creates an Excel workbook C#** using Aspose.Cells.'
  - name: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
    text: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
  - name: Adds a cotangent formula (`COT(PI()/4)`).
    text: Adds a cotangent formula (`COT(PI()/4)`).
  - name: Saves the file and optionally auto‑fits columns.
    text: Saves the file and optionally auto‑fits columns.
  type: HowTo
- questions:
  - answer: Absolutely. Aspose.Cells targets .NET Standard 2.0, which is compatible
      with both .NET Core and the classic Framework.
    question: Does this work with .NET Framework 4.8?
  - answer: Use `ws.Protect(ProtectionType.All, "yourPassword");` before saving.
    question: What if I need to protect the sheet?
  - answer: 'Yes—`workbook.Save(stream, SaveFormat.Xlsx);` is handy for web APIs that
      return the file as a download. --- ## TL;DR We built a **complete C# console
      app** that: 1. **Creates an Excel workbook C#** using Aspose.Cells. 2. **Uses
      the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5 block.'
    question: Can I write the workbook directly to a `MemoryStream`?
  type: FAQPage
tags:
- csharp
- excel
- aspose-cells
- .net
title: Tworzenie skoroszytu Excel w C# – Pełny przewodnik z funkcją Expand
url: /pl/net/excel-workbook/create-excel-workbook-c-full-guide-with-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz skoroszyt Excel C# – Pełny przewodnik z funkcją Expand

Zastanawiałeś się kiedyś, jak **utworzyć Excel workbook C#** bez walki z COM interop lub kombinowania z XML? Nie jesteś jedyny. W wielu projektach .NET musimy wygenerować arkusz kalkulacyjny, wypełnić go formułami i przekazać go użytkownikom nietechnicznym. Dobra wiadomość? Dzięki nowoczesnej bibliotece takiej jak **Aspose.Cells** cały proces to bułka z masłem.

W tym samouczku przeprowadzimy Cię przez kompletny, działający przykład, który **tworzy Excel workbook C#**, wstawia kilka formuł — w tym jak **używać funkcji EXPAND w Excel** — i zapisuje plik, abyś mógł od razu otworzyć go w Excelu. Po zakończeniu będziesz wiedział nie tylko *co* wpisać, ale *dlaczego* każda linia ma znaczenie, i będziesz miał szablon, który możesz skopiować do dowolnego projektu.

## Wymagania wstępne

- .NET 6 SDK (lub dowolna nowsza wersja .NET) zainstalowany.
- IDE kompatybilne z NuGet (Visual Studio, VS Code, Rider itp.).
- Pakiet NuGet **Aspose.Cells** – dostarcza klasy `Workbook` i `Worksheet` używane w kodzie.
- Podstawowa znajomość C#; nie jest wymagana znajomość Excela.

Masz wszystko? Świetnie — zaczynamy.

## Krok 1: Konfiguracja projektu i dodanie Aspose.Cells

Najpierw utwórz aplikację konsolową i dodaj bibliotekę.

```bash
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

> **Wskazówka:** Jeśli pracujesz w sieci korporacyjnej, może być konieczne skonfigurowanie proxy dla NuGet. Pakiet Aspose.Cells jest lekki, więc instalacja kończy się w kilka sekund.

Teraz otwórz `Program.cs`. Zobaczysz domyślną metodę `Main` — zamień ją na szkielet poniżej.

```csharp
using System;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // All of our Excel logic will go here.
        }
    }
}
```

Linia `using Aspose.Cells;` wprowadza klasy arkusza kalkulacyjnego do zakresu. Jeśli ją pominiesz, kompilator zgłosi, że `Workbook` jest niezdefiniowany — czego później unikniemy.

## Krok 2: Utwórz Excel Workbook C# i uzyskaj dostęp do pierwszego arkusza

Po przygotowaniu projektu możemy w końcu **utworzyć Excel workbook C#**. Konstruktor `Workbook` daje nam nowy, pusty skoroszyt, a indeks `Worksheets[0]` zwraca domyślny arkusz (nazwany „Sheet1”).

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty .xlsx file in memory
Worksheet ws = workbook.Worksheets[0];            // reference to the first (default) sheet
```

Dlaczego pobieramy pierwszy arkusz explicite? Ponieważ wiele dalszych API (np. ustawianie formuł) wymaga obiektu `Worksheet`, a nie samego `Workbook`. To także sprawia, że kod jest czytelniejszy dla przyszłych czytelników.

## Krok 3: Użyj funkcji Expand w Excel, aby wypełnić dynamiczny zakres

Teraz przychodzi gwiazda programu: **używać funkcji EXPAND w Excel**. Funkcja `EXPAND` (dostępna od Excel 365) przyjmuje tablicę źródłową i rozszerza ją do żądanego rozmiaru. W naszym przykładzie zaczniemy od pionowej tablicy 3‑wierszowej generowanej przez `SEQUENCE(3)` i rozszerzymy ją do bloku 5 × 5.

```csharp
// Step 3: Insert the EXPAND formula into cell A1
ws.Cells["A1"].Formula = "EXPAND(SEQUENCE(3),5,5)";
```

Co się tak naprawdę dzieje?

1. `SEQUENCE(3)` generuje pionową tablicę `{1;2;3}`.
2. `EXPAND(...,5,5)` instruuje Excel, aby powiększyć tę tablicę do 5 wierszy i 5 kolumn.
3. Wynik to siatka 5 × 5, w której pierwsze trzy wiersze zawierają liczby 1‑3 powtarzane w kolumnach, a pozostałe dwa wiersze są puste.

Ponieważ zapisujemy formułę jako ciąg znaków, Excel ocenia ją *gdy plik jest otwierany*, a nie w czasie wykonywania. Oznacza to, że skoroszyt pozostaje lekki, a wszelkie zmiany w tablicy źródłowej będą automatycznie się rozprzestrzeniać.

> **Przypadek brzegowy:** Jeśli użytkownik otworzy skoroszyt w starszej wersji Excela, która nie obsługuje `EXPAND`, komórka wyświetli `#NAME?`. Aby się przed tym zabezpieczyć, możesz otoczyć formułę funkcją `IFERROR`, ale w nowoczesnych środowiskach można bezpiecznie polegać na tej funkcji.

## Krok 4: Dodaj formułę cotangensa dla pełni

Dodajmy kolejną formułę, aby pokazać, jak proste jest dodawanie wyrażeń matematycznych. Obliczymy cotangens π/4, który wynosi dokładnie `1`.

```csharp
// Step 4: Insert a cotangent calculation in cell B1
ws.Cells["B1"].Formula = "COT(PI()/4)";
```

Funkcja `COT` w Excel nie jest tak powszechnie używana jak `SIN` czy `COS`, ale jest idealna do przepływów pracy z trygonometrią. Po otwarciu skoroszytu komórka **B1** wyświetli `1`.

## Krok 5: Zapisz skoroszyt i zweryfikuj wynik

Cała ta praca byłaby bezcelowa, gdybyśmy nie zapisali pliku. Metoda `Save` zapisuje skoroszyt z pamięci na dysk. Wybierz folder, do którego masz prawo zapisu, i nadaj plikowi przyjazną nazwę.

```csharp
// Step 5: Save the workbook to the output folder
string outputPath = @"./output.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Uruchom program:

```bash
dotnet run
```

Powinieneś zobaczyć komunikat w konsoli potwierdzający zapis. Otwórz `output.xlsx` w Excel, a zauważysz:

- Komórki **A1:E5** wypełnione rozszerzoną sekwencją (1,2,3 w pierwszych trzech wierszach, puste w wierszach 4‑5).
- Komórka **B1** wyświetlająca wartość `1` z formuły cotangensa.

To pełny cykl: **utworzyć excel workbook c#**, osadzić formuły i wygenerować użyteczny arkusz kalkulacyjny.

![Zrzut ekranu wygenerowanego skoroszytu Excel pokazujący rozszerzoną tablicę i wynik cotangensa](/images/create-excel-workbook-csharp.png "przykład create excel workbook c#")

*Tekst alternatywny obrazu: create excel workbook c# – widok wypełnionego arkusza.*

## Krok 6: Opcjonalnie – Auto‑Fit kolumn dla profesjonalnego wyglądu

Jeśli planujesz dystrybuować plik do użytkowników końcowych, szybkie auto‑fit sprawi, że będzie wyglądał profesjonalnie.

```csharp
// Optional: Auto‑fit all columns in the used range
ws.AutoFitColumns(0, ws.Cells.MaxColumn);
```

Ta linia przechodzi przez każdą kolumnę zawierającą dane i dostosowuje jej szerokość do najdłuższego wpisu. To mały detal, ale zapobiega niechcianemu przepełnieniu „…###”, gdy liczby są szersze niż domyślna szerokość kolumny.

## Krok 7: Podsumowanie i kolejne kroki

Gratulacje — właśnie opanowałeś, jak **utworzyć excel workbook c#** od podstaw i nauczyłeś się, jak **używać funkcji EXPAND w excel** do generowania dynamicznych tablic. Kod jest celowo minimalistyczny, abyś mógł go kopiować i wklejać w dowolnym projekcie, ale koncepcje skalują się:

- **Dynamiczne źródła danych:** Zamień `SEQUENCE(3)` na odwołanie do innego zakresu lub nazwanej tabeli.
- **Formatowanie warunkowe:** Użyj `ws.Cells["A1:E5"].Style`, aby dodać kolory w zależności od wartości.
- **Wykresy i grafika:** Aspose.Cells może osadzać wykresy, obrazy i nawet tabele przestawne.

Śmiało eksperymentuj — zamień wymiary `EXPAND`, wypróbuj `FILTER` lub `SORT`, lub łącz wiele formuł razem. Biblioteka radzi sobie ze wszystkim, bez konieczności bezpośredniego manipulowania formatem OpenXML.

---

### Najczęściej zadawane pytania

**P: Czy to działa z .NET Framework 4.8?**  
O: Zdecydowanie tak. Aspose.Cells jest skierowany do .NET Standard 2.0, co jest kompatybilne zarówno z .NET Core, jak i klasycznym Frameworkiem.

**P: Co zrobić, jeśli muszę zabezpieczyć arkusz?**  
O: Użyj `ws.Protect(ProtectionType.All, "yourPassword");` przed zapisem.

**P: Czy mogę zapisać skoroszyt bezpośrednio do `MemoryStream`?**  
O: Tak — `workbook.Save(stream, SaveFormat.Xlsx);` jest przydatne w API webowych, które zwracają plik jako pobranie.

## TL;DR

Zbudowaliśmy **kompletną aplikację konsolową C#**, która:

1. **Tworzy Excel workbook C#** przy użyciu Aspose.Cells.  
2. **Używa funkcji EXPAND w Excel** aby przekształcić tablicę 3‑wierszową w blok 5 × 5.  
3. Dodaje formułę cotangensa (`COT(PI()/4)`).  
4. Zapisuje plik i opcjonalnie automatycznie dopasowuje kolumny.

Masz teraz solidną bazę do każdego zadania automatyzacji, które wymaga generowania plików Excel z .NET. Szczęśliwego kodowania i niech Twoje arkusze zawsze będą wolne od błędów!

## Co warto nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z instrukcjami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak utworzyć zakresy nazwane o zasięgu skoroszytu w Excel przy użyciu Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [Jak tworzyć i używać zakresów Union w Excel z Aspose.Cells .NET (poradnik C#)](/cells/english/net/range-management/excel-union-range-aspose-cells-net/)
- [Utwórz skoroszyt Excel z wykresami przy użyciu Aspose.Cells .NET | przewodnik krok po kroku](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}