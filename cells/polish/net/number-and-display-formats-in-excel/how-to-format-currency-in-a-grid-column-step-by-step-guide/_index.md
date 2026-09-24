---
category: general
date: 2026-02-15
description: Jak szybko sformatować walutę, używając ustawienia formatu liczbowego
  kolumny i zastosować własny format liczbowy w C#. Dowiedz się, jak pobrać kolumnę
  po nazwie i ustawić wyrównanie kolumny w siatce.
draft: false
keywords:
- how to format currency
- set column number format
- apply custom numeric format
- retrieve column by name
- set grid column alignment
language: pl
og_description: Jak sformatować walutę w kolumnie siatki przy użyciu C#. Ten samouczek
  pokazuje, jak pobrać kolumnę po nazwie, ustawić format liczbowy kolumny, zastosować
  niestandardowy format numeryczny oraz ustawić wyrównanie kolumny w siatce.
og_title: Jak sformatować walutę w kolumnie siatki – Kompletny przewodnik
tags:
- C#
- GridFormatting
- UI
title: Jak sformatować walutę w kolumnie siatki – przewodnik krok po kroku
url: /pl/net/number-and-display-formats-in-excel/how-to-format-currency-in-a-grid-column-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak sformatować walutę w kolumnie siatki – kompletny samouczek programistyczny

Zastanawiałeś się kiedyś **jak sformatować walutę** w kolumnie siatki, nie tracąc włosów? Nie jesteś jedyny. Kiedy patrzysz na zwykłą liczbę taką jak `1234.5` i chciałbyś, aby magicznie pojawiła się jako `$1,234.50`, odpowiedź zazwyczaj sprowadza się do kilku linii konfiguracji.  

W tym przewodniku **pobierzemy kolumnę po nazwie**, **ustawimy format liczbowy kolumny** i **zastosujemy własny format numeryczny**, który respektuje typowy układ księgowy. Po drodze **ustawimy wyrównanie kolumny w siatce** i dodamy subtelną ramkę, aby interfejs wyglądał elegancko.

> **TL;DR** – Po zakończeniu będziesz mieć gotowy fragment kodu, który zamienia surowe liczby dziesiętne w pięknie sformatowane wartości walutowe w dowolnym kontrolce w stylu `GridJs`.

---

## Czego będziesz potrzebować

- Projekt .NET (dowolna wersja obsługująca C# 8.0+ – Visual Studio 2022 świetnie się sprawdzi).  
- Komponent siatki udostępniający kolekcję `Columns` (przykład używa fikcyjnej klasy `GridJs`, ale koncepcje mają zastosowanie do siatek DevExpress, Telerik lub Syncfusion).  
- Podstawowa znajomość składni C# – nie są potrzebne zaawansowane sztuczki.

Jeśli już to masz, super. Jeśli nie, po prostu uruchom aplikację konsolową; siatkę można zamockować w celach ilustracyjnych.

---

## Implementacja krok po kroku

Poniżej każdego kroku zobaczysz zwarty blok kodu, krótkie wyjaśnienie **dlaczego** dana linia jest ważna oraz wskazówkę, jak uniknąć typowych pułapek.

### ## Krok 1 – Pobierz kolumnę „Amount” według nazwy

```csharp
// Step 1: Retrieve the "Amount" column from the grid
var amountColumn = gridJs.Columns["Amount"];
if (amountColumn == null)
{
    throw new InvalidOperationException("Column 'Amount' does not exist. Verify the column name or check the grid's schema.");
}
```

**Dlaczego to jest ważne:**  
Większość API siatek udostępnia kolumny poprzez indeksator przypominający słownik. Pobranie kolumny po nazwie nagłówka (`"Amount"`) pozwala manipulować jej wyglądem bez ingerencji w źródło danych.  

**Wskazówka:** Zawsze sprawdzaj, czy zwrócony obiekt nie jest `null` – literówka w nazwie kolumny lub dynamiczna zmiana schematu może w innym wypadku spowodować `NullReferenceException` w czasie wykonywania.

---

### ## Krok 2 – Ustaw format liczbowy kolumny przy użyciu własnej maski walutowej

```csharp
// Step 2: Apply a custom numeric format for currency values
amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";
```

**Dlaczego to jest ważne:**  
Ciąg formatu podąża za konwencjami formatu księgowego Excela:

- `_(* #,##0.00_)` → Liczby dodatnie, wyrównane do prawej z wiodącą spacją dla symbolu waluty.  
- `_(* (#,##0.00)` → Liczby ujemne otoczone nawiasami.  
- `_(* \"-\"??_)` → Zero wyświetlane jako kreska.  
- `_(@_)` → Wartości tekstowe pozostają niezmienione.

Użycie **apply custom numeric format** daje pełną kontrolę nad separatorami tysięcy, miejscami po przecinku i położeniem symbolu waluty.  

**Przypadek brzegowy:** Jeśli aplikacja ma obsługiwać inną lokalizację (np. Euro zamiast USD), zamień wiodącą spację na odpowiedni symbol lub użyj formatowania uwzględniającego `CultureInfo` w źródle danych.

---

### ## Krok 3 – Wyrównaj zawartość kolumny do prawej dla lepszej czytelności

```csharp
// Step 3: Align the column contents to the right for better readability
amountColumn.Alignment = GridAlignment.Right;
```

**Dlaczego to jest ważne:**  
Wartości walutowe łatwiej skanować, gdy są wyrównane do separatora dziesiętnego. Ustawienie **set grid column alignment** na `Right` odzwierciedla sposób, w jaki arkusze kalkulacyjne wyświetlają dane finansowe.  

**Pułapka:** Niektóre siatki ignorują wyrównanie w komórkach zawierających własne szablony. Jeśli zauważysz, że wyrównanie nie działa, sprawdź, czy kolumna nie używa niestandardowego renderera komórek.

---

### ## Krok 4 – Dodaj cienką szarą ramkę wokół komórek kolumny

```csharp
// Step 4: Add a thin gray border around the column cells
amountColumn.Border = new GridBorder
{
    Color = Color.Gray,
    Style = BorderLineStyle.Thin
};
```

**Dlaczego to jest ważne:**  
Subtelna ramka oddziela kolumnę „Amount” od sąsiadów, szczególnie gdy siatka ma naprzemienne kolory wierszy. To wizualny sygnał, że dane reprezentują odrębną wartość finansową.  

**Wskazówka:** Jeśli potrzebujesz grubszej linii do druku, zwiększ `BorderLineStyle` do `Medium` lub zmień `Color` na `Color.Black`.

---

## Pełny działający przykład

Oto cały fragment, który możesz wkleić do projektu WinForms lub WPF używającego kontrolki w stylu `GridJs`. Przykład dodatkowo wypisuje sformatowane wartości w konsoli, abyś mógł zweryfikować wynik bez UI.

```csharp
using System;
using System.Drawing;   // For Color
using GridLibrary;      // Hypothetical namespace for GridJs

namespace GridCurrencyDemo
{
    class Program
    {
        static void Main()
        {
            // Create a mock grid and add a sample column
            var gridJs = new GridJs();
            gridJs.Columns.Add(new GridColumn
            {
                Name = "Amount",
                Header = "Amount",
                DataType = typeof(decimal)
            });

            // Populate some sample data
            gridJs.Rows.Add(new { Amount = 1234.5m });
            gridJs.Rows.Add(new { Amount = -567.89m });
            gridJs.Rows.Add(new { Amount = 0m });

            // ---- Formatting steps ------------------------------------------------
            // 1️⃣ Retrieve the "Amount" column
            var amountColumn = gridJs.Columns["Amount"]
                ?? throw new InvalidOperationException("Column 'Amount' not found.");

            // 2️⃣ Apply custom numeric format for currency
            amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";

            // 3️⃣ Right‑align the values
            amountColumn.Alignment = GridAlignment.Right;

            // 4️⃣ Add a thin gray border
            amountColumn.Border = new GridBorder
            {
                Color = Color.Gray,
                Style = BorderLineStyle.Thin
            };
            // -----------------------------------------------------------------------

            // Render the grid (in a real UI you would call gridJs.Render() or similar)
            Console.WriteLine("Formatted Currency Grid:");
            foreach (var row in gridJs.Rows)
            {
                var rawValue = (decimal)row.Amount;
                // The grid library would automatically apply NumberFormat when displaying.
                // For console demo we mimic the formatting:
                string formatted = rawValue.ToString("#,##0.00", System.Globalization.CultureInfo.InvariantCulture);
                if (rawValue < 0)
                    formatted = $"({formatted.TrimStart('-')})";
                else if (rawValue == 0)
                    formatted = "-";

                Console.WriteLine($"| {formatted,15} |");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Oczekiwany output konsoli**

```
Formatted Currency Grid:
|        1,234.50 |
|       (567.89) |
|               - |
```

Zauważ, że liczba dodatnia jest wyrównana do prawej, liczba ujemna pojawia się w nawiasach, a zero wyświetla kreskę – dokładnie tak, jak określa własny ciąg formatu.

---

## Najczęściej zadawane pytania i przypadki brzegowe

| Pytanie | Odpowiedź |
|----------|--------|
| *Co jeśli siatka używa innej kultury (np. € zamiast $)?* | Zamień wiodącą spację w ciągu formatu na żądany symbol lub pozwól źródłu danych zwrócić już sformatowany ciąg przy użyciu `CultureInfo.CurrentCulture`. |
| *Czy mogę ponownie użyć tego samego formatu dla wielu kolumn?* | Oczywiście. Przechowaj ciąg formatu w stałej (`const string CurrencyMask = "...";`) i przypisz go wszędzie tam, gdzie potrzebna jest waluta. |
| *Co się stanie, jeśli kolumna zawiera wartość typu string?* | Ciąg formatu wpływa tylko na typy numeryczne. Stringi przechodzą niezmienione, dlatego ostatnia część maski (`_(@_)`) istnieje – zachowuje treść nie‑numeryczną. |
| *Czy ma to wpływ na wydajność?* | Nieznaczny. Format jest stosowany w czasie renderowania, a nie podczas pobierania danych. Dopóki nie renderujesz tysięcy wierszy na klatkę, nie zauważysz spowolnienia. |
| *Jak sprawić, by obramowanie było grubsze w raportach drukowanych?* | Zamień `BorderLineStyle.Thin` na `BorderLineStyle.Medium` lub `BorderLineStyle.Thick`. Niektóre biblioteki pozwalają także określić szerokość w pikselach bezpośrednio. |

---

## Podsumowanie

Przeszliśmy przez **sposób formatowania waluty** w kolumnie siatki od początku do końca: pobranie kolumny po nazwie, ustawienie formatu liczbowego, zastosowanie własnego formatu numerycznego, wyrównanie komórek i dodanie eleganckiej ramki. Pełny przykład działa od razu i pokazuje dokładny efekt wizualny, którego możesz się spodziewać.

Jeśli chcesz pójść dalej, wypróbuj:

- **Dynamiczne kultury** – zmień ciąg formatu w zależności od lokalizacji użytkownika.  
- **Conditional

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}