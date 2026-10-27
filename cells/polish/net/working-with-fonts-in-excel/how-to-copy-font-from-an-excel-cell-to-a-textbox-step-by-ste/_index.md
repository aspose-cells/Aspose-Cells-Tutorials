---
category: general
date: 2026-02-15
description: jak skopiować czcionkę i zastosować styl komórki w C# przy użyciu prostego
  przykładu. Dowiedz się, jak uzyskać styl komórki i używać formatowania komórek,
  aby ustawić rozmiar czcionki w polu tekstowym.
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: pl
og_description: jak skopiować czcionkę z komórki arkusza i zastosować styl komórki
  do pola tekstowego. Ten przewodnik pokazuje, jak uzyskać styl komórki, używać formatowania
  komórki i ustawić rozmiar czcionki pola tekstowego.
og_title: Jak skopiować czcionkę z komórki Excel – kompletny samouczek C#
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: Jak skopiować czcionkę z komórki Excel do pola tekstowego – przewodnik krok
  po kroku
url: /pl/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak skopiować czcionkę z komórki Excel do TextBox – kompletny samouczek C#

Kiedykolwiek potrzebowałeś **skopiować czcionkę** z komórki arkusza i sprawić, by pole tekstowe w interfejsie wyglądało dokładnie tak samo? Nie jesteś jedyny. W wielu narzędziach raportujących lub własnych pulpitach nawigacyjnych znajdziesz się w sytuacji, w której pobierasz dane z Excela i starasz się zachować wierność wizualną — rodzinę czcionki, rozmiar i kolor — nienaruszoną.  

Dobra wiadomość jest taka, że przy użyciu kilku linijek C# możesz **pobrać styl komórki**, odczytać jej właściwości czcionki i **zastosować styl komórki** do dowolnego kontrolki tekstowej. W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który pokazuje, jak **używać formatowania komórek** i nawet **ustawiać rozmiar czcionki w textboxie** programowo.

---

## Czego się nauczysz

- Jak pobrać obiekt `TextBox` z komponentu siatki (`gridJs` w naszym przykładzie)
- Jak odczytać rodzinę czcionki, rozmiar i kolor z konkretnej komórki Excel (`B2`)
- Jak skopiować te atrybuty czcionki do pola tekstowego, aby UI odzwierciedlało arkusz
- Typowe pułapki (np. konwersja koloru) oraz kilka **pro tipów**, które utrzymają Twój kod w dobrej formie
- Gotowy fragment kodu, który możesz wkleić do aplikacji konsolowej lub projektu WinForms

**Wymagania wstępne**  
Powinieneś mieć:

1. .NET 6+ (lub .NET Framework 4.8) zainstalowany  
2. Pakiet NuGet EPPlus (do obsługi Excela)  
3. Kontrolkę siatki, która udostępnia słownik `TextBoxes` (przykład używa fikcyjnego `gridJs`, ale pomysł działa z dowolną biblioteką UI)

Teraz, zabierzmy się do pracy.

---

## Krok 1: Konfiguracja projektu i załadowanie arkusza

Najpierw utwórz nowy projekt konsolowy lub WinForms i dodaj EPPlus:

```bash
dotnet add package EPPlus --version 6.*
```

Następnie wczytaj skoroszyt i pobierz komórkę, której styl chcesz skopiować.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**Dlaczego to ważne:** EPPlus daje bezpośredni dostęp do obiektu `Style`, który zawiera podobiekt `Font`. Stamtąd możesz odczytać `Name`, `Size` i `Color`. To jest sedno operacji **pobierania stylu komórki**.

---

## Krok 2: Pobranie docelowego TextBoxa z siatki

Zakładając, że Twoja siatka UI (`gridJs`) przechowuje pola tekstowe w słowniku kluczowanym nazwą kolumny, możesz pobrać potrzebny element w następujący sposób:

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

Jeśli używasz WinForms, `notesTextBox` może być kontrolką `TextBox`; w WPF może to być element `TextBox`, a w siatce opartej na sieci może to być obiekt interfejsu JavaScript. Najważniejsze, że masz referencję, którą możesz manipulować.

---

## Krok 3: Przeniesienie rodziny czcionki

Teraz, gdy mamy zarówno styl źródłowy, jak i kontrolkę docelową, skopiuj rodzinę czcionki.

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**Pro tip:** Nie wszystkie frameworki UI udostępniają właściwość `FontFamily`, która przyjmuje zwykły ciąg znaków. W WinForms ustawiłbyś `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);`. Dostosuj odpowiednio.

---

## Krok 4: Przeniesienie rozmiaru czcionki

Rozmiar czcionki jest przechowywany jako `float` w EPPlus. Zastosuj go bezpośrednio:

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

Jeśli Twoja kontrolka używa punktów (co większość robi), możesz przypisać wartość bez konwersji. W siatkach opartych na CSS może być konieczne dopisanie `"pt"`.

---

## Krok 5: Przeniesienie koloru czcionki

Konwersja koloru jest najtrudniejszą częścią, ponieważ EPPlus przechowuje kolory jako liczby całkowite ARGB, podczas gdy wiele frameworków UI oczekuje `System.Drawing.Color` lub ciągu szesnastkowego CSS.

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **Dlaczego to działa:** `GetColor()` rozwiązuje kolory oparte na temacie i zwraca konkretny `System.Drawing.Color`. Jeśli komórka używa domyślnego koloru (brak wyraźnego ustawienia), domyślnie ustawiamy czarny, aby uniknąć wyjątków null reference.

---

## Pełny działający przykład

Łącząc wszystko razem, oto minimalna aplikacja konsolowa, która odczytuje plik Excel, wyciąga czcionkę z **B2** i stosuje ją do przykładowego pola tekstowego.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**Oczekiwany wynik (zakładając, że B2 używa Arial, 12 pt, niebieski):**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

Uruchom program, otwórz swój interfejs i zobaczysz, że pole tekstowe „Notes” teraz odzwierciedla dokładny styl czcionki komórki **B2**. Bez ręcznego dopasowywania.

---

## Najczęściej zadawane pytania i przypadki brzegowe

### Co zrobić, gdy komórka używa koloru tematu zamiast explicite określonej wartości RGB?

`GetColor()` w EPPlus automatycznie rozwiązuje kolory tematyczne do konkretnego `System.Drawing.Color`. Jednak jeśli używasz starszej biblioteki, która zwraca jedynie indeks tematu, będziesz musiał samodzielnie zamapować ten indeks na paletę kolorów.

### Czy mogę skopiować inne atrybuty stylu (np. pogrubienie, kursywę)?

Oczywiście. Obiekt `ExcelStyle.Font` udostępnia także `Bold`, `Italic`, `Underline` i `Strike`. Po prostu ustaw odpowiednie właściwości na swojej kontrolce UI:

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### Co zrobić, gdy kontrolka siatki nie udostępnia właściwości `FontColor`?

Większość nowoczesnych frameworków UI tak, ale jeśli Twoja akceptuje jedynie ciąg CSS, skonwertuj `Color` na format szesnastkowy:

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### Jak obsłużyć wiele komórek jednocześnie?

Iteruj po żądanym zakresie, pobieraj styl każdej komórki i stosuj go do odpowiadającego pola tekstowego. Pamiętaj, aby buforować obiekty stylu przy przetwarzaniu wielu wierszy, aby uniknąć spadków wydajności.

---

## Pro tipy i typowe pułapki

- **Cache'uj ExcelPackage** – otwieranie i zamykanie pliku dla każdej komórki jest kosztowne. Wczytaj skoroszyt raz, a potem używaj ponownie obiektu `ExcelWorksheet`.
- **Uważaj na null w kolorach** – komórka dziedzicząca domyślny kolor zwraca `null`. Zawsze podawaj wartość domyślną (czarny lub domyślny kolor kontrolki).
- **Zwróć uwagę na skalowanie DPI** – przy docelowych monitorach wysokiej rozdzielczości rozmiary czcionek mogą wydawać się nieco większe. W razie potrzeby dostosuj je przy użyciu `Graphics.DpiX`.
- **Bezpieczeństwo wątkowe** – EPPlus nie jest wątkowo‑bezpieczny. Jeśli przetwarzasz wiele arkuszy równolegle, utwórz osobny `ExcelPackage` dla każdego wątku.

---

## Zakończenie

Teraz wiesz **jak skopiować czcionkę** z komórki Excel i **zastosować styl komórki** do dowolnej kontrolki tekstowej przy użyciu C#. Pobierając `Style` komórki, wyciągając jej właściwości `Font` i przypisując je elementowi UI, zachowujesz spójność wizualną bez ręcznego kopiowania.  

Kompletne rozwiązanie – wczytanie skoroszytu, pobranie stylu komórki oraz ustawienie rodziny czcionki, rozmiaru i koloru w textboxie – obejmuje rdzeń **używania formatowania komórek** i pokazuje, jak **ustawiać rozmiar czcionki w textboxie** prawidłowo.  

Następnie spróbuj rozszerzyć przykład o kopiowanie kolorów tła, obramowań lub nawet całych treści komórek. Jeśli pracujesz z biblioteką siatki danych, która obsługuje bogate renderowanie komórek, możesz teraz przekazać jej dokładnie te same informacje stylu, które pobrałeś z Excela, utrzymując UI i raporty w idealnej synchronizacji.

Masz więcej pytań? zostaw komentarz lub zagłęb się w powiązane tematy, takie jak „dynamiczne powiązanie Excel‑UI” i „konwersja kolorów świadoma tematu”. Szczęśliwego kodowania!

---

![how to copy font example](placeholder-image.jpg "how to copy font from Excel cell to TextBox")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}