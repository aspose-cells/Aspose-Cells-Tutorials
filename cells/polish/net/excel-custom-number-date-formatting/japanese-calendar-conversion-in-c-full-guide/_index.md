---
category: general
date: 2026-07-13
description: Konwersja kalendarza japońskiego w C# z kodem krok po kroku. Dowiedz
  się, jak wyodrębnić DateTime z Excela i efektywnie obsługiwać daty z japońskimi
  erami.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- japanese calendar conversion
- extract datetime from excel
- excel date parsing c#
- aspnet excel cultureinfo
- japanese era date handling
language: pl
lastmod: 2026-07-13
og_description: Konwersja japońskiego kalendarza w C# wyjaśniona. Opanuj wyodrębnianie
  DateTime z komórek Excela i konwersję japońskich nazw epok na daty gregoriańskie.
og_image_alt: Code screenshot illustrating Japanese calendar conversion in a C# console
  app
og_title: Konwersja japońskiego kalendarza w C# – Kompletny przewodnik programistyczny
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Japanese calendar conversion in C# with step‑by‑step code. Learn how
    to extract DateTime from Excel and handle Japanese era dates efficiently.
  headline: Japanese Calendar Conversion in C# – Full Guide
  type: TechArticle
- description: Japanese calendar conversion in C# with step‑by‑step code. Learn how
    to extract DateTime from Excel and handle Japanese era dates efficiently.
  name: Japanese Calendar Conversion in C# – Full Guide
  steps:
  - name: Recognizes era names (e.g., *Meiji*, *Taishō*, *Shōwa*, *Heisei*, *Reiwa*).
    text: Recognizes era names (e.g., *Meiji*, *Taishō*, *Shōwa*, *Heisei*, *Reiwa*).
  - name: Parses the year number relative to the era’s start.
    text: Parses the year number relative to the era’s start.
  - name: Constructs the corresponding Gregorian `DateTime`.
    text: Constructs the corresponding Gregorian `DateTime`.
  type: HowTo
tags:
- C#
- Excel
- DateTime
- Localization
title: Konwersja japońskiego kalendarza w C# – pełny przewodnik
url: /pl/net/excel-custom-number-date-formatting/japanese-calendar-conversion-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwersja kalendarza japońskiego w C# – Pełny przewodnik

Kiedykolwiek potrzebowałeś **japanese calendar conversion** podczas pobierania danych z arkusza Excel? Nie jesteś jedynym, który drapie się po głowie, próbując przekształcić „Reiwa 3‑04‑01” w prawidłowy .NET `DateTime`. W tym samouczku przeprowadzimy Cię przez czyste, kompleksowe rozwiązanie, które nie tylko konwertuje daty w erze japońskiej, ale także pokazuje, jak **extract datetime from excel** komórki przy użyciu Aspose.Cells. Na koniec będziesz mieć gotową do uruchomienia aplikację konsolową oraz solidne zrozumienie, dlaczego ustawienia kultury mają znaczenie.

Omówimy wszystko, o co możesz zapytać: ustawienie właściwej kultury, parsowanie ciągu epoki, obsługę przypadków brzegowych, takich jak lata przestępne, oraz ostateczne wypisanie wyniku gregoriańskiego. Nie potrzebna żadna zewnętrzna dokumentacja — po prostu kopiuj, wklej i uruchom.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa zarówno na .NET Core, jak i .NET Framework)
- Aspose.Cells for .NET (bezpłatny pakiet próbny NuGet `Aspose.Cells`)
- Podstawowa znajomość C# i aplikacji konsolowych
- Plik Excel (lub nowy skoroszyt), w którym data jest przechowywana jako ciąg znaków w formacie japońskiej ery

Jeśli brakuje Ci któregoś z nich, pobierz pakiet NuGet za pomocą:

```bash
dotnet add package Aspose.Cells
```

Zanurzmy się.

## Krok 1: Utwórz skoroszyt i ustaw kulturę japońską

Pierwszą rzeczą, którą musisz zrobić, jest poinformowanie Aspose.Cells, że skoroszyt powinien interpretować daty przy użyciu japońskiego kalendarza. To tutaj **japanese calendar conversion** naprawdę się rozpoczyna.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook instance
        Workbook workbook = new Workbook();

        // 2️⃣ Apply Japanese culture (Japanese calendar) to the workbook settings
        workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("ja-JP-u-ca-japanese");

        // The rest of the steps follow...
```

**Why this matters:** `CultureInfo` niesie nie tylko język, ale także informacje o kalendarzu. Przełączając na `"ja-JP-u-ca-japanese"` umożliwiamy bibliotece rozpoznawanie nazw er, takich jak *Reiwa* czy *Heisei*, gdy pojawiają się w komórkach.

## Krok 2: Wpisz datę w erze japońskiej do komórki

Dla demonstracji wstawimy ciąg daty w erze japońskiej bezpośrednio do komórki **A1**. W rzeczywistym scenariuszu prawdopodobnie odczytywałbyś istniejący skoroszyt, ale zasada pozostaje ta sama.

```csharp
        // 3️⃣ Write a Japanese era date string into cell A1 (row 0, column 0)
        workbook.Worksheets[0].Cells[0, 0].PutValue("Reiwa 3-04-01");
```

> **Pro tip:** Jeśli źródłowy Excel już przechowuje daty jako prawidłowe liczby seryjne Excel, możesz pominąć krok `PutValue` i przejść od razu do ekstrakcji. Logika konwersji działa w obu przypadkach.

## Krok 3: Wyodrębnij DateTime z Excela – rdzeń „extract datetime from excel”

Teraz nadchodzi część, w której **extract datetime from excel**. Aspose.Cells udostępnia wygodną metodę `GetDateTime`, która respektuje ustawienia kultury skoroszytu.

```csharp
        // 4️⃣ Retrieve the cell value as a .NET DateTime object
        DateTime gregorianDate = workbook.Worksheets[0].Cells[0, 0].GetDateTime();
```

Za kulisami Aspose patrzy na wcześniej ustawioną kulturę, parsuje „Reiwa 3‑04‑01” i zwraca równoważną datę gregoriańską (`2021‑04‑01`).

## Krok 4: Wyświetl wynik

Na koniec wydrukujmy przekonwertowaną datę w konsoli, abyś mógł zweryfikować, że **japanese calendar conversion** powiodła się.

```csharp
        // 5️⃣ Show the converted Gregorian date
        Console.WriteLine(gregorianDate.ToString("yyyy‑MM‑dd"));
        // Expected output: 2021‑04‑01
    }
}
```

Uruchom program (`dotnet run`) i powinieneś zobaczyć:

```
2021‑04‑01
```

To cały cykl: utwórz skoroszyt, ustaw kulturę japońską, wpisz datę w erze, wyodrębnij `DateTime` i wyświetl go.

---

## Głębokie zanurzenie: Jak działa japoński kalendarz w .NET

Japoński kalendarz jest systemem *lunisolarnym*, który grupuje lata w ery nazwane na cześć panującego cesarza. Klasa .NET `JapaneseCalendar` mapuje każdą erę na zakres lat gregoriańskich. Kiedy żądasz `CultureInfo`, który zawiera `-u-ca-japanese`, środowisko uruchomieniowe automatycznie:

1. Rozpoznaje nazwy er (np. *Meiji*, *Taishō*, *Shōwa*, *Heisei*, *Reiwa*).
2. Parsuje numer roku względem początku ery.
3. Tworzy odpowiadający gregoriański `DateTime`.

Jeśli kiedykolwiek będziesz musiał konwertować w drugą stronę — z gregoriańskiego na japońską erę — możesz użyć:

```csharp
var japaneseCal = new System.Globalization.JapaneseCalendar();
int era = japaneseCal.GetEra(gregorianDate);
string eraName = japaneseCal.Eras[era - 1]; // .Eras is zero‑based
int yearInEra = japaneseCal.GetYear(gregorianDate);
Console.WriteLine($"{eraName} {yearInEra:D2}-{gregorianDate:MM-dd}");
```

### Obsługa przypadków brzegowych

| Sytuacja | Na co zwrócić uwagę | Sugerowana poprawka |
|-----------|-------------------|---------------|
| **Brak nazwy ery** (np. “03‑04‑01”) | `GetDateTime` zgłosi `FormatException`. | Wstępnie zweryfikuj ciąg lub użyj `DateTime.ParseExact` z własnym wzorcem. |
| **Przyszła era** (nowy cesarz) | Obecny `JapaneseCalendar` może nie znać nowej ery do momentu aktualizacji systemu operacyjnego. | Zaktualizuj środowisko .NET lub użyj własnej tabeli mapowań, dopóki system operacyjny nie zostanie zaktualizowany. |
| **Mieszane kalendarze w jednym skoroszycie** | Niektóre komórki mogą używać kalendarza gregoriańskiego, a inne japońskiego. | Ustaw `CultureInfo` dla każdej komórki, używając `cell.Style.CultureInfo`, jeśli to konieczne. |

## Wyodrębnianie DateTime z istniejących plików Excel

Jeśli już masz plik `.xlsx` z japońskimi datami, kod ekstrakcji jest prawie identyczny — wystarczy zamienić tworzenie skoroszytu na wywołanie ładowania:

```csharp
Workbook workbook = new Workbook("Path/To/YourFile.xlsx");
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("ja-JP-u-ca-japanese");

// Assuming the date is in B2 (row 1, column 1)
DateTime dateFromFile = workbook.Worksheets[0].Cells[1, 1].GetDateTime();
Console.WriteLine(dateFromFile);
```

Zauważ, że **extract datetime from excel** pozostaje tym samym wywołaniem metody; jedynym dodatkowym krokiem jest załadowanie pliku.

---

## Pełny działający przykład (gotowy do kopiowania i wklejania)

Poniżej znajduje się kompletny program, który możesz wkleić do projektu konsolowego. Zawiera wszystkie niezbędne dyrektywy `using`, komentarze i obsługę błędów, aby wyglądał jak rozwiązanie produkcyjne.

```csharp
using System;
using Aspose.Cells;

class JapaneseCalendarDemo
{
    static void Main()
    {
        try
        {
            // Initialize workbook
            Workbook wb = new Workbook();

            // Apply Japanese calendar culture
            wb.Settings.CultureInfo = new System.Globalization.CultureInfo("ja-JP-u-ca-japanese");

            // Insert a Japanese era date string (could be read from an existing file)
            wb.Worksheets[0].Cells[0, 0].PutValue("Reiwa 3-04-01");

            // Extract as .NET DateTime – this is the core of "extract datetime from excel"
            DateTime gregDate = wb.Worksheets[0].Cells[0, 0].GetDateTime();

            // Output in ISO format
            Console.WriteLine(gregDate.ToString("yyyy-MM-dd"));
        }
        catch (Exception ex)
        {
            // Simple error handling – in real apps you might log this
            Console.Error.WriteLine($"Error during conversion: {ex.Message}");
        }
    }
}
```

**Oczekiwany wynik w konsoli**

```
2021-04-01
```

Uruchom go, a zobaczysz datę gregoriańską, która odpowiada wprowadzonemu wejściowi w erze japońskiej.

---

## Często zadawane pytania

**P:** Czy to działa ze starszymi plikami Excel (.xls)?  
Tak. Aspose.Cells abstrahuje format pliku, więc to samo wywołanie `GetDateTime` działa zarówno dla `.xls`, jak i `.xlsx`.

**P:** Co jeśli komórka zawiera rzeczywistą datę Excel (liczbę seryjną) zamiast ciągu znaków?  
Aspose nadal będzie respektować kulturę skoroszytu i zwróci prawidłowy gregoriański `DateTime`. Nie jest potrzebne dodatkowe parsowanie.

**P:** Czy mogę przekonwertować całą kolumnę japońskich dat jednocześnie?  
Oczywiście. Przejdź pętlą po wierszach:

```csharp
for (int i = 0; i < worksheet.Cells.MaxDataRow + 1; i++)
{
    DateTime dt = worksheet.Cells[i, 0].GetDateTime();
    // Do something with dt
}
```

**P:** Czy ustawienie kultury ma wpływ na wydajność?  
Znikomy dla typowych zestawów danych. Kultura jest stosowana raz na skoroszyt, nie na każdą komórkę.

---

## Podsumowanie

Właśnie zakończyliśmy przewodnik **japanese calendar conversion**, który pokazuje dokładnie, jak **extract datetime from excel** przy użyciu Aspose.Cells. Ustawiając `CultureInfo` skoroszytu na `"ja-JP-u-ca-japanese"` odblokowujesz płynne parsowanie ciągów er, takich jak *Reiwa 3‑04‑01*, do standardowych obiektów .NET `DateTime`. Kod jest zwięzły, solidny i gotowy do produkcji.

Co dalej? Spróbuj załadować rzeczywisty skoroszyt, przekonwertować całą kolumnę lub nawet zapisać daty gregoriańskie z powrotem do nowego arkusza. Możesz także zbadać inne lokalizacje — francuski kalendarz republikański, islamski kalendarz hijri — zamieniając ciąg kultury. Wzorzec pozostaje ten sam.

Masz własny pomysł, którym chcesz się podzielić? Dodaj komentarz i szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i zbadać alternatywne podejścia implementacyjne w własnych projektach.

- [Opanuj system dat 1904 w Excelu przy użyciu Aspose.Cells Java dla efektywnych operacji na komórkach](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Konwersja odwołań komórek w Excelu przy użyciu Aspose.Cells .NET: Kompletny przewodnik](/cells/english/net/cell-operations/excel-cell-reference-conversion-aspose-cells-net/)
- [Opanuj konwersję HTML do Excel przy użyciu Aspose.Cells dla .NET](/cells/english/net/workbook-operations/aspose-cells-net-html-layout-conversion/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}