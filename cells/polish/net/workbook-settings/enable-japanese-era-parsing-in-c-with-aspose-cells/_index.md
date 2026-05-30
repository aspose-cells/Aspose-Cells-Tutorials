---
category: general
date: 2026-05-30
description: Włącz parsowanie japońskich er w C# przy użyciu Aspose.Cells. Dowiedz
  się, jak ustawić kulturę skoroszytu, parsować daty w erze oraz obsługiwać japoński
  kalendarz w arkuszach Excel.
draft: false
keywords:
- enable japanese era parsing
- Aspose.Cells Japanese era
- set workbook culture
- parse era dates
- c# excel date parsing
language: pl
og_description: Włącz parsowanie japońskich er w C# z Aspose.Cells. Ten przewodnik
  pokazuje, jak ustawić kulturę skoroszytu, włączyć obsługę er oraz pracować z japońskimi
  datami.
og_title: Włączanie parsowania japońskich er w C# – Kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Enable Japanese era parsing in C# using Aspose.Cells. Learn to set
    workbook culture, parse era dates, and handle Japanese calendar in Excel worksheets.
  headline: Enable Japanese Era Parsing in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Włącz parsowanie japońskich er w C# z Aspose.Cells
url: /pl/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Włącz parsowanie japońskich er w C# z Aspose.Cells

Czy kiedykolwiek musiałeś **włączyć parsowanie japońskich er** przy generowaniu plików Excel dla japońskiego klienta? Nie jesteś jedyny — wielu programistów napotyka problem, gdy w danych pojawia się tradycyjny japoński kalendarz (令和, 平成 itp.). Dobrą wiadomością jest to, że Aspose.Cells sprawia, że rozpoznawanie tych dat er i przekształcanie ich w standardowe wartości gregoriańskie jest dziecinnie proste.

W tym samouczku przeprowadzimy Cię przez dokładne kroki, aby **włączyć parsowanie japońskich er** przy użyciu Aspose.Cells, ustawić kulturę skoroszytu na japońską i wstawić datę sformatowaną jako era do komórki. Po zakończeniu będziesz mieć działający fragment C#, który parsuje „令和3年5月1日” do prawidłowego obiektu daty `2021‑05‑01`. Nie potrzebujesz zewnętrznej dokumentacji — po prostu skopiuj, wklej i uruchom.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa z .NET Core, .NET Framework i .NET 5+)
- Aspose.Cells for .NET (pakiet NuGet `Aspose.Cells`)
- Podstawowa znajomość C# — jeśli potrafisz napisać `Console.WriteLine`, jesteś gotowy
- IDE według własnego wyboru (Visual Studio, VS Code, Rider…)

> **Wskazówka:** Utrzymuj swoją wersję Aspose.Cells aktualną; wersja 24.10+ zawiera najnowsze definicje japońskich er.

## Dlaczego włączyć parsowanie japońskich er?

Japońskie kalendarze używają er powiązanych z panowaniami cesarskimi. Dla większości nowoczesnych aplikacji będziesz chciał przechowywać daty w znanym formacie gregoriańskim, ale dane źródłowe mogą nadal przychodzić jako „令和3年5月1日”. Jeśli pominiesz **włączenie parsowania japońskich er**, ciąg zostanie potraktowany jako zwykły tekst, co zepsuje obliczenia, sortowanie i wykresy. Włączając obsługę er, Aspose.Cells automatycznie konwertuje te ciągi na prawidłowe wartości `DateTime`, zachowując zarówno czytelność dla japońskich użytkowników, jak i poprawność numeryczną dla dalszego przetwarzania.

## Krok 1: Ustaw kulturę skoroszytu na japoński

Pierwszą rzeczą, którą musisz zrobić, jest poinformowanie Aspose.Cells, że domyślna lokalizacja skoroszytu to japoński (`ja-JP`). Dzięki temu wszelkie parsowanie zależne od kultury (w tym nazwy er) będzie odbywać się zgodnie z japońskimi zasadami.

```csharp
using Aspose.Cells;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Set the workbook culture to Japanese (ja-JP)
        workbook.Settings.Culture = new CultureInfo("ja-JP");
```

> **Dlaczego to ma znaczenie:** Obiekt `CultureInfo` kontroluje formaty liczb, separatory dat i, co najważniejsze dla nas, system kalendarzowy używany przy parsowaniu ciągów.

## Krok 2: Włącz parsowanie japońskich er

Teraz, gdy kultura jest ustawiona, musisz przełączyć przełącznik, który mówi Aspose.Cells, aby rozpoznawał daty er. To jest sedno **włączenia parsowania japońskich er**.

```csharp
        // Enable parsing of Japanese era dates (令和, 平成, 昭和, etc.)
        workbook.Settings.UseJapaneseEra = true;
```

> **Typowy błąd:** Zapomnienie tego flagi powoduje, że „令和3年5月1日” pozostaje dosłownym ciągiem znaków. Po włączeniu Aspose.Cells automatycznie mapuje erę na właściwy rok gregoriański.

## Krok 3: Wstaw datę sformatowaną jako era do komórki

Po przygotowaniu kultury i obsługi er, wstawienie japońskiego ciągu era jest proste. Biblioteka go sparsuje i zapisze prawdziwą wartość `DateTime`.

```csharp
        // Grab the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Insert a Japanese era date string into cell A1
        // The string "令和3年5月1日" becomes 2021‑05‑01 internally
        sheet.Cells["A1"].PutValue("令和3年5月1日");

        // Save the workbook to verify the result
        workbook.Save("JapaneseEraDemo.xlsx");
    }
}
```

### Oczekiwany wynik

- **Komórka A1** w wygenerowanym pliku `JapaneseEraDemo.xlsx` wyświetli **2021‑05‑01** (lub zlokalizowany japoński format daty, jeśli otworzysz go w Excelu z japońską lokalizacją).
- Wartość podstawowa jest prawdziwym `DateTime`, więc możesz ją bezpiecznie używać w formułach, tabelach przestawnych lub dalszych obliczeniach C#.

## Krok 4: Zweryfikuj sparsowaną datę programowo (opcjonalnie)

Jeśli chcesz podwójnie sprawdzić, że parsowanie powiodło się przed zapisaniem, możesz odczytać komórkę ponownie:

```csharp
        // Retrieve the value as a DateTime
        DateTime parsedDate = sheet.Cells["A1"].GetDateTime();

        Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
        // Output: Parsed date: 2021-05-01
```

Ten mały krok weryfikacyjny jest przydatny w testach jednostkowych lub przy przetwarzaniu plików Excel dostarczonych przez użytkowników.

## Przypadki brzegowe i warianty

| Scenariusz | Co zrobić |
|------------|-----------|
| **Wiele er w jednym skoroszycie** | Utrzymaj `UseJapaneseEra = true`; Aspose.Cells rozpozna wszystkie obsługiwane ery (令和, 平成, 昭和, 大正, 明治). |
| **Mieszane ciągi gregoriańskie i erowe** | Parser automatycznie rozróżnia; ciągi gregoriańskie pozostają niezmienione. |
| **Wymagania dotyczące niestandardowego kalendarza** | Możesz nadal ustawić `Workbook.Settings.Calendar` na konkretną instancję `Calendar`, jeśli potrzebujesz większej kontroli. |
| **Starsze wersje .NET** | Ten sam kod działa na .NET Framework 4.6+; wystarczy zapewnić dostępność konstruktora `System.Globalization.CultureInfo`. |

## Praktyczne wskazówki dla projektów rzeczywistych

- **Cache'uj obiekt CultureInfo** jeśli tworzysz wiele skoroszytów w pętli; wielokrotne tworzenie go zwiększa narzut.
- **Waliduj dane wejściowe** przed wywołaniem `PutValue`; nieprawidłowe ciągi erowe spowodują wyrzucenie wyjątku.
- **Wyłącz parsowanie er** (`UseJapaneseEra = false`), gdy masz pewność, że dane nigdy nie zawierają dat erowych — może to nieco poprawić wydajność.
- **Użyj `Workbook.SaveOptions`** aby kontrolować format wyjściowy (XLSX, XLS, CSV) przy zachowaniu sparsowanej daty.

## Pełny działający przykład (gotowy do kopiowania‑wklejania)

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class EnableJapaneseEraParsingDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Set workbook culture to Japanese (ja-JP)
        workbook.Settings.Culture = new CultureInfo("ja-JP");

        // 3️⃣ Enable Japanese era parsing
        workbook.Settings.UseJapaneseEra = true;

        // 4️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 5️⃣ Insert an era‑formatted date
        sheet.Cells["A1"].PutValue("令和3年5月1日");

        // Optional: read back the parsed value
        DateTime dt = sheet.Cells["A1"].GetDateTime();
        Console.WriteLine($"Parsed date: {dt:yyyy-MM-dd}");

        // Save the workbook
        workbook.Save("EnableJapaneseEraParsing.xlsx");
    }
}
```

Uruchom program, otwórz wygenerowany plik i zobaczysz **2021‑05‑01** w komórce A1 — dowód, że pomyślnie **włączyliśmy parsowanie japońskich er**.

## Zakończenie

Właśnie pokazaliśmy, jak **włączyć parsowanie japońskich er** w C# przy użyciu Aspose.Cells, ustawić kulturę skoroszytu i płynnie przekształcić daty er, takie jak „令和3年5月1日”, na standardowe wartości gregoriańskie. Kroki są minimalne, kod jest samodzielny, a rezultat działa bezbłędnie w Excelu.

Gotowy na kolejny wyzwanie? Spróbuj połączyć **ustawienie kultury skoroszytu** z formatowaniem liczb w jenach, lub wygeneruj raport wieloarkuszowy, który miesza daty gregoriańskie i erowe. Masz już solidne podstawy, aby radzić sobie z wszelkimi niuansami japońskiego kalendarza w swoich projektach automatyzacji Excel w .NET.

---

*Jeśli ten przewodnik okazał się pomocny, rozważ nadanie gwiazdki repozytorium Aspose.Cells na GitHubie lub podzielenie się własnymi wskazówkami w komentarzach. Szczęśliwego kodowania!*

## Co warto się nauczyć dalej?

- [Ładuj skoroszyty Excel z datami specyficznymi dla kultury przy użyciu Aspose.Cells dla .NET](/cells/english/net/formatting/load-workbook-culture-specific-dates-aspose-cells-net/)
- [Jak ustawić język w plikach Excel przy użyciu Aspose.Cells .NET dla wsparcia wielojęzycznego](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [Ładuj daty specyficzne dla kultury w skoroszycie Aspose Cells Net](/cells/chinese/net/formatting/load-workbook-culture-specific-dates-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}