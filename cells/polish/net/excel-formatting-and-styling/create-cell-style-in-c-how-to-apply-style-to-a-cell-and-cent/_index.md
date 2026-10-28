---
category: general
date: 2026-02-21
description: Szybko twórz styl komórki w C#. Dowiedz się, jak zastosować styl do komórki,
  wyśrodkować tekst w komórce, ustawić wyrównanie komórki i opanować formatowanie
  komórek.
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: pl
og_description: Utwórz styl komórki w C# i dowiedz się, jak zastosować styl do komórki,
  wyśrodkować tekst w komórce oraz ustawić wyrównanie komórki, korzystając z przejrzystego,
  krok po kroku przewodnika.
og_title: Utwórz styl komórki w C# – Zastosuj styl do komórki i wyśrodkuj tekst
tags:
- C#
- Aspose.Cells
- Excel automation
title: Utwórz styl komórki w C# – Jak zastosować styl do komórki i wyśrodkować tekst
url: /pl/net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie stylu komórki w C# – Kompletny przewodnik po stosowaniu stylów i wyśrodkowywaniu tekstu

Czy kiedykolwiek potrzebowałeś **create cell style** w arkuszu Excel, ale nie wiedziałeś, od czego zacząć? Nie jesteś sam. W wielu projektach automatyzacji możliwość **apply style to cell** obiektów jest różnicą między nijaką tabelą a dopracowanym raportem.  

W tym tutorialu przeprowadzimy Cię przez pełny, działający przykład, który pokaże, **how to center text** wewnątrz komórki, ustawi wyrównanie i doda cienką obramowanie — wszystko w zaledwie kilku linijkach C#. Po zakończeniu dokładnie zrozumiesz, dlaczego każdy element ma znaczenie i jak go dostosować do własnych scenariuszy.

## Co wyniesiesz z tego tutorialu

- Jasne zrozumienie przepływu **create cell style** przy użyciu Aspose.Cells (lub dowolnej podobnej biblioteki).  
- Dokładny kod, który możesz skopiować i wkleić do aplikacji konsolowej, aby **apply style to cell**.  
- Wgląd w **center text in cell**, **set cell alignment** oraz obsługę przypadków brzegowych, takich jak scalone komórki czy własne formaty liczb.  
- Porady dotyczące rozszerzania stylu — różne czcionki, kolory tła lub formatowanie warunkowe.  

> **Prerequisite:** Visual Studio 2022 (lub dowolne IDE C#) oraz pakiet NuGet Aspose.Cells for .NET. Nie są wymagane inne zależności.

---

## Krok 1: Skonfiguruj projekt i zaimportuj przestrzenie nazw

Zanim będziemy mogli **create cell style**, potrzebujemy projektu, który odwołuje się do biblioteki Excel.

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*Dlaczego to ważne:* Importowanie `Aspose.Cells` daje dostęp do klas `Workbook`, `Worksheet`, `Style` i `Border`. Jeśli używasz innej biblioteki (np. EPPlus), nazwy klas się zmienią, ale koncepcja pozostaje taka sama.

---

## Krok 2: Utwórz skoroszyt i pobierz pierwszą komórkę

Teraz **create cell style** poprzez najpierw uzyskanie referencji do komórki, którą chcemy sformatować.

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

Zauważ, że użyliśmy `Cell` zamiast ogólnego `var` — jawne typowanie czyni kod czytelniejszym dla nowicjuszy. Wywołanie `PutValue` zapisuje ciąg znaków, aby później można było zobaczyć efekt stylu.

---

## Krok 3: Zdefiniuj styl – wyśrodkuj tekst, dodaj cienką obramowanie

Oto serce operacji **create cell style**. Ustawimy wyrównanie poziome, cienką obramowanie i kilka opcjonalnych udogodnień.

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*Dlaczego to robimy:*  
- **HorizontalAlignment** i **VerticalAlignment** razem odpowiadają na pytanie „**how to center text** in a cell?”.  
- Dodanie wszystkich czterech krawędzi zapewnia, że komórka wygląda jak zamknięta etykieta, co jest przydatne przy nagłówkach.  
- Kolor tła nie jest wymagany, ale pokazuje, jak później można rozszerzyć styl.

---

## Krok 4: Zastosuj zdefiniowany styl do wybranej komórki

Teraz, gdy styl istnieje, **apply style to cell** jedną metodą.

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

I to wszystko — Aspose.Cells zajmuje się kopiowaniem stylu do wewnętrznej kolekcji stylów komórki. Jeśli potrzebujesz takiego samego formatowania w zakresie, możesz użyć `ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });`.

---

## Krok 5: Zapisz skoroszyt i zweryfikuj wynik

Szybki zapis pozwala otworzyć plik w Excelu i potwierdzić, że tekst jest naprawdę wyśrodkowany, a obramowanie widoczne.

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*Oczekiwany wynik:* Po otwarciu **StyledCell.xlsx**, komórka **A1** zawiera „Hello, styled world!” wyśrodkowane zarówno poziomo, jak i pionowo, otoczone cienką szarą obramowaniem i ustawione na jasnoszare tło.

---

## Typowe warianty i przypadki brzegowe

### 1. Wyśrodkowanie tekstu w scalonym obszarze

Jeśli scalasz komórki **A1:C1** i nadal chcesz, aby tekst był wyśrodkowany, musisz zastosować styl do komórki w lewym‑górnym rogu **po** scaleniu:

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. Użycie formatu liczbowego

Czasami trzeba **set cell alignment** *i* wyświetlić liczby w określonym formacie:

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

Wyrównanie pozostaje wyśrodkowane, a liczba wyświetla się jako `12,345.68`.

### 3. Efektywne ponowne użycie stylów

Tworzenie nowego `Style` dla każdej komórki może obniżać wydajność. Zamiast tego utwórz jeden obiekt stylu i używaj go wielokrotnie w wielu komórkach lub zakresach. Klasa `StyleFlag` pozwala zastosować tylko te części, które Cię interesują, oszczędzając pamięć.

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

---

## Pro tipy i pułapki, na które warto zwrócić uwagę

- **Nie zapominaj o wyrównaniu pionowym** — wyśrodkowanie tylko poziome często wygląda nieestetycznie, zwłaszcza przy wyższych wierszach.  
- **Typy obramowań**: `CellBorderType.Thin` sprawdza się w większości raportów, ale możesz przełączyć na `Medium` lub `Dashed`, aby uzyskać hierarchię wizualną.  
- **Obsługa kolorów**: Przy .NET Core używaj `System.Drawing.Color` z pakietu `System.Drawing.Common`; w przeciwnym razie napotkasz błąd w czasie wykonywania.  
- **Format zapisu**: Jeśli potrzebna jest kompatybilność ze starszymi wersjami Excela, zmień `SaveFormat.Xlsx` na `SaveFormat.Xls`.

---

![Przykład tworzenia stylu komórki](https://example.com/images/create-cell-style.png "Tworzenie stylu komórki w C#")

*Alt text: zrzut ekranu pokazujący komórkę z wyśrodkowanym tekstem i cienką obramowaniem utworzony w tutorialu create cell style.*

---

## Pełny działający przykład (gotowy do kopiowania i wklejenia)

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

Uruchom ten program, otwórz **StyledCell.xlsx**, a zobaczysz dokładnie taki wynik, jaki opisano wcześniej. Śmiało zmieniaj tekst, styl obramowania lub kolor tła, aby dopasować je do własnej identyfikacji wizualnej.

---

## Zakończenie

Właśnie **created cell style** od podstaw, **applied style to cell**, i pokazaliśmy **how to center text** zarówno poziomo, jak i pionowo. Opanowując te elementy, możesz teraz formatować nagłówki, podkreślać sumy lub budować całe szablony raportów, nie opuszczając C#.  

Jeśli chcesz iść dalej, wypróbuj:

- **Zastosowanie tego samego stylu do całego wiersza** (`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`).  
- **Dodanie formatowania warunkowego**, aby zmieniało tło w zależności od wartości komórki.  
- **Eksport do PDF** przy zachowaniu stylu.

Pamiętaj, że stylowanie to nie tylko estetyka, ale i czytelność. Eksperymentuj, iteruj i wkrótce Twoje arkusze będą wyglądały tak profesjonalnie, jak Twój kod.

*Miłego kodowania!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}