---
category: general
date: 2026-03-18
description: Dowiedz się, jak zastosować naprzemienne kolory wierszy w arkuszu przy
  użyciu C#. Zawiera ustawianie koloru tła wiersza, dodawanie jasnożółtego tła oraz
  naprzemienne kolorowanie wierszy.
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: pl
og_description: Zastosuj naprzemienne kolory wierszy w C#, aby poprawić czytelność.
  Ten przewodnik pokazuje, jak ustawić kolor tła wiersza, dodać jasnożółte tło i kolorować
  wiersze naprzemiennie.
og_title: Zastosuj naprzemienne kolory wierszy w C# – Kompletny poradnik
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: Zastosuj naprzemienne kolory wierszy w C# – Przewodnik krok po kroku
url: /pl/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zastosuj Naprzemienne Kolory Wierszy w C# – Kompletny Poradnik

Kiedykolwiek potrzebowałeś **zastosować naprzemienne kolory wierszy** w arkuszu opartym na danych, ale nie wiedziałeś od czego zacząć? Nie jesteś sam — większość programistów napotyka ten problem przy pierwszej próbie uczynienia tabel bardziej przyjaznymi dla oka. Dobra wiadomość? W kilku linijkach C# możesz **ustawić kolor tła wiersza**, dodać **jasnożółte tło**, i uzyskać wypolerowaną siatkę, która od razu poprawia czytelność.

W tym poradniku przejdziemy krok po kroku przez cały proces, od pobrania `DataTable` do pamięci po stylizowanie każdego wiersza delikatną żółto‑białą paską. Po zakończeniu będziesz mógł **kolorować wiersze naprzemiennie** z pewnością, a także zobaczysz kilka przydatnych wariantów, gdy potrzebne będą inne odcienie lub dynamiczne motywy.

## Co będzie potrzebne

Zanim zaczniemy, upewnij się, że masz pod ręką:

- Projekt .NET targetujący .NET 6 lub nowszy (kod działa również na .NET Framework 4.7+).  
- Bibliotekę arkuszy kalkulacyjnych obsługującą obiekty stylu – w przykładzie użyto ogólnego API `Workbook`/`Worksheet`, które odzwierciedla biblioteki takie jak **Aspose.Cells**, **GemBox.Spreadsheet** lub **ClosedXML**.  
- Źródło `DataTable` – może pochodzić z zapytania do bazy danych, importu CSV lub dowolnej kolekcji w pamięci.  

Nie potrzebujesz dodatkowych pakietów NuGet poza samą biblioteką arkuszy. Jeśli używasz Aspose.Cells, przestrzeń nazw to `Aspose.Cells`; dla ClosedXML to `ClosedXML.Excel`. Zamień wywołania `CreateStyle` i `ImportDataTable` odpowiednio.

## Krok 1: Pobranie danych źródłowych jako DataTable

Najpierw – pobierz dane, które chcesz wyświetlić. W rzeczywistych aplikacjach zazwyczaj oznacza to połączenie z bazą danych, ale dla przejrzystości stworzymy metodę pomocniczą `GetData()`, która zwraca wypełniony `DataTable`.

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **Dlaczego to ważne:** `DataTable` definiuje wiersze i kolumny, które później otrzymają naprzemienne cieniowanie. Jeśli tabela jest pusta, nie ma czego stylizować, więc zawsze sprawdzaj, czy `Rows.Count` > 0 przed kontynuacją.

### Wskazówka
Jeśli pobierasz dane z Entity Framework, możesz użyć `DataTable.Load(reader)` po wykonaniu `SqlCommand`. To utrzymuje kod schludnym i unika ręcznych definicji kolumn.

## Krok 2: Alokacja tablicy przechowującej styl dla każdego wiersza

Następnie potrzebujemy kontenera o rozmiarze równym liczbie wierszy. Większość API arkuszy pozwala przekazać tablicę stylów do metody importu, więc utworzymy `Style[]` o dokładnie takiej liczbie elementów, jak liczba wierszy.

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **Wyjaśnienie:** Pre‑alokując tablicę, unikamy tworzenia nowego obiektu stylu przy każdej iteracji, co może przynieść korzyść wydajnościową przy tysiącach wierszy.

## Krok 3: Zastosowanie naprzemiennych kolorów wierszy (Jasny żółty / Biały)

Teraz serce sprawy: **zastosować naprzemienne kolory wierszy**. Przejdziemy po każdym wierszu, utworzymy nową instancję stylu z workbooka i ustawimy tło w zależności od indeksu wiersza. Parzyste wiersze otrzymają jasny żółty wypełnienie, nieparzyste pozostaną białe.

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### Dlaczego to działa
- **`rowIndex % 2 == 0`** sprawdza, czy wiersz jest parzysty.  
- **`Color.LightYellow`** daje delikatny, nieinwazyjny odcień idealny dla tabel danych.  
- **`BackgroundType.Solid`** zapewnia, że wypełnienie obejmuje całą komórkę, osiągając efekt **set row background color**.  

Możesz zamienić `Color.LightYellow` na dowolny inny odcień (np. `Color.LightCyan`), jeśli wolisz inny wygląd. Ta sama logika pozwala także **color rows alternately** na podstawie innych kryteriów, takich jak flagi statusu.

## Krok 4: Import DataTable do arkusza z przygotowanymi stylami

Na koniec wprowadzamy wszystko do arkusza. Większość bibliotek udostępnia przeciążenie `ImportDataTable`, które przyjmuje tablicę stylów. Flaga `true` mówi API, aby zapisało nagłówki kolumn, a współrzędne `0, 0` rozpoczynają wstawianie od komórki w lewym‑górnym rogu.

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **Rezultat:** Arkusz wyświetla dane z czystym **alternating row shading** – jasny żółty w parzystych wierszach, biały w nieparzystych. Użytkownicy mogą przeglądać siatkę bez konieczności „skakania” wzrokiem.

### Oczekiwany wynik
Jeśli otworzysz wygenerowany arkusz, zobaczysz coś takiego:

| ID | Name      | Quantity |
|----|-----------|----------|
| **1** | Apple      | 50       |
| **2** | Banana     | 30       |
| **3** | Cherry     | 20       |
| **4** | Date       | 15       |

Wiersze 1, 3, 5… mają **jasnożółte tło**, natomiast wiersze 2, 4, 6… pozostają **białe**. Wiersz nagłówka (wiersz 0) dziedziczy domyślny styl, chyba że dostosujesz go osobno.

## Opcjonalne warianty i przypadki brzegowe

### 1. Użycie innej palety kolorów
Jeśli jasny żółty nie pasuje do Twojej identyfikacji wizualnej, po prostu zamień `Color.LightYellow` na inny `System.Drawing.Color`. Dla motywu niebiesko‑szarego możesz użyć:

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. Dynamiczne cieniowanie w zależności od danych
Czasem chcesz podświetlić wiersze spełniające warunek (np. niski stan magazynowy). Połącz sprawdzenie modulo z własnym testem:

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. Stosowanie stylów tylko w wybranych kolumnach
Jeśli potrzebujesz **set row background color** tylko w niektórych kolumnach, utwórz osobny styl dla każdej kolumny i przypisz go po imporcie, używając API zakresu komórek arkusza.

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. Wskazówka wydajnościowa dla dużych tabel
Przy > 10 000 wierszy rozważ ponowne użycie jednego obiektu stylu dla każdego koloru zamiast tworzenia nowego przy każdym wierszu. Tablica będzie wtedy przechowywać odwołania do dwóch współdzielonych stylów, co znacząco zmniejsza zużycie pamięci.

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## Pełny działający przykład

Poniżej znajduje się samodzielny program, który możesz wkleić do aplikacji konsolowej. Używa fikcyjnego API `Workbook`/`Worksheet`; zamień typy na te z wybranej biblioteki.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**Wynik:** Plik o nazwie `AlternatingRows.xlsx`, w którym każdy wiersz naprzemiennie ma wypełnienie jasnym żółtym i białe, co ułatwia czytanie tabeli.

## Najczęściej zadawane pytania

**P: Czy to podejście działa z formatowaniem warunkowym w stylu Excel?**  
O: Tak. Jeśli Twoja biblioteka obsługuje reguły warunkowe, możesz przenieść tę samą logikę do reguły sprawdzającej `MOD(ROW(),2)=0`. Metoda oparta na kodzie, przedstawiona tutaj, jest bardziej przenośna między bibliotekami, które nie mają wbudowanego formatowania warunkowego.

**P: Co zrobić, jeśli muszę **color rows alternately** w tabeli PDF zamiast arkusza Excel?**  
O: Większość generatorów tabel PDF (np. iTextSharp, PdfSharp) pozwala ustawić `BackgroundColor` dla każdego wiersza. Ta sama kalkulacja modulo ma zastosowanie—

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}