---
category: general
date: 2026-03-30
description: Naucz się formatować datę w formacie ISO, odczytując wartości daty i
  czasu z Excela oraz wyodrębniając dane daty i czasu z Excela przy użyciu Aspose.Cells
  w C#.
draft: false
keywords:
- format date iso
- read excel datetime
- extract datetime excel
- Aspose.Cells date parsing
- Japanese era dates
language: pl
og_description: formatowanie daty ISO z danych Excel przy użyciu Aspose.Cells. Ten
  przewodnik pokazuje, jak odczytać daty i godziny z Excela, wyodrębnić ich wartości
  oraz wyświetlić daty w formacie ISO.
og_title: Formatowanie daty ISO z Excela – krok po kroku tutorial C#
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: formatowanie daty ISO z Excela – Kompletny przewodnik C#
url: /pl/net/excel-custom-number-date-formatting/format-date-iso-from-excel-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# formatowanie daty iso z Excela – Kompletny przewodnik C#

Czy kiedykolwiek potrzebowałeś **format date iso** przy wyciąganiu dat z arkusza Excel? Być może operujesz na japońskich datach ery, albo po prostu chcesz czysty ciąg `yyyy‑MM‑dd` do ładunku API. W tym samouczku zobaczysz dokładnie, jak **read Excel datetime** komórki, **extract datetime Excel** wartości i przekształcić je do formatu ISO‑8601 — bez zgadywania.

Przejdziemy przez rzeczywisty przykład wykorzystujący Aspose.Cells, wyjaśnimy, dlaczego każda linia ma znaczenie, i pokażemy ostateczny wynik, który możesz skopiować‑wkleić do swojego projektu. Po zakończeniu będziesz w stanie obsłużyć dziwaczne ciągi ery, takie jak „令和3年5月1日”, i wygenerować standardową datę ISO, gotową do baz danych, JSON lub gdziekolwiek jej potrzebujesz.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również z .NET Framework)
- Aspose.Cells dla .NET (bezpłatna wersja próbna lub licencjonowana)
- Podstawowa znajomość C# i koncepcji Excela
- Visual Studio lub dowolny edytor C#, który lubisz

Żadne dodatkowe pakiety NuGet nie są wymagane poza Aspose.Cells, więc konfiguracja jest dość prosta.

---

## Krok 1: Utwórz skoroszyt i skieruj się do pierwszego arkusza

Pierwszą rzeczą, którą robisz, jest utworzenie nowego obiektu `Workbook`. Daje to pamięciową reprezentację pliku Excel, którą możesz następnie manipulować lub odczytywać.

```csharp
using Aspose.Cells;
using System.Globalization;

// Step 1: Initialize a new workbook and grab the first worksheet
Workbook workbook = new Workbook();                 // creates an empty .xlsx
Worksheet worksheet = workbook.Worksheets[0];      // the default sheet is "Sheet1"
```

*Dlaczego to ważne:*  
Tworzenie skoroszytu programowo pozwala uniknąć pracy z fizycznymi plikami podczas testów. Zapewnia również, że odwołanie do arkusza jest zawsze prawidłowe — bez niespodziewanych null‑reference później, gdy próbujesz **read Excel datetime** wartości.

---

## Krok 2: Wpisz ciąg daty japońskiej ery do komórki

Naszym celem jest pokazanie parsowania daty nie‑gregoriańskiej. Umieścimy ciąg ery bezpośrednio w komórce **A1**.

```csharp
// Step 2: Insert a Japanese era date string into cell A1
worksheet.Cells["A1"].PutValue("令和3年5月1日");
```

*Wskazówka:* Jeśli pobierasz dane z istniejącego skoroszytu, pominiesz wywołanie `PutValue` i po prostu odwołasz się do komórki, która już zawiera datę. Kluczowe jest, aby komórka zawierała **string**, który reprezentuje datę w japońskim kalendarzu lunarnym.

---

## Krok 3: Skonfiguruj kulturę rozumiejącą japoński kalendarz lunarny

Klasa `CultureInfo` w .NET pozwala określić, jak daty mają być interpretowane. Zamieniając domyślny kalendarz gregoriański na `JapaneseLunisolarCalendar`, dostarczasz parserowi potrzebny kontekst.

```csharp
// Step 3: Set up a culture using the Japanese lunisolar calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();
```

*Dlaczego to robimy:*  
Gdybyś próbował sparsować „令和3年5月1日” przy użyciu domyślnej kultury, .NET wyrzuci `FormatException`. Wstawienie kalendarza lunarskiego informuje środowisko dokładnie, jak zamapować „令和3年” (3. rok ery Reiwa) na rok gregoriański 2021.

---

## Krok 4: Sparsuj wartość komórki jako `DateTime` przy użyciu skonfigurowanej kultury

Teraz następuje serce operacji — przekształcenie tego ciągu ery w prawidłowy obiekt `DateTime`. Aspose.Cells udostępnia wygodny przeciążony `GetDateTime`, który przyjmuje `CultureInfo`.

```csharp
// Step 4: Retrieve the cell value as a DateTime, respecting the Japanese culture
DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);
```

*Co się dzieje w tle:*  
`GetDateTime` odczytuje surowy ciąg, stosuje reguły kalendarza dostarczonej kultury i zwraca `DateTime`, który reprezentuje tę samą chwilę w kalendarzu gregoriańskim. To jest moment, w którym **extract datetime Excel** dane w formie, z którą możesz pracować w .NET.

---

## Krok 5: Wyświetl sparsowaną datę w formacie ISO 8601

Na koniec formatujemy `DateTime` jako ciąg ISO — `yyyy‑MM‑dd` — który jest powszechnie akceptowany przez API, bazy danych i frameworki front‑end.

```csharp
// Step 5: Print the date in ISO format (e.g., 2021-05-01)
Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // Output: 2021-05-01
```

*Dlaczego ISO?*  
ISO 8601 eliminuje niejednoznaczność. „05/01/2021” może oznaczać 1 maja lub 5 stycznia w zależności od ustawień regionalnych. `2021-05-01` jest całkowicie jasne, dlatego **format date iso** w prawie każdym scenariuszu integracji.

---

## Pełny działający przykład

Poniżej znajduje się kompletny, gotowy do uruchomienia program. Skopiuj go do projektu aplikacji konsolowej, dodaj odwołanie do Aspose.Cells i naciśnij **F5**.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and select the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // 3️⃣ Set up Japanese lunisolar culture
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();

        // 4️⃣ Parse the cell value as DateTime using the culture
        DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);

        // 5️⃣ Output the date in ISO format
        Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // 2021-05-01
    }
}
```

**Oczekiwany wynik**

```
2021-05-01
```

Uruchom go raz, a zobaczysz datę w formacie ISO wydrukowaną w konsoli. To cały potok od **read Excel datetime** do **format date iso**.

---

## Obsługa typowych przypadków brzegowych

### 1. Komórki zawierające rzeczywiste liczby dat w Excelu

Czasami Excel przechowuje daty jako liczby seryjne (np. `44204`). W takim przypadku nie potrzebujesz kultury; po prostu wywołaj `GetDateTime()` bez parametrów:

```csharp
DateTime serialDate = worksheet.Cells["B2"].GetDateTime(); // B2 holds a numeric date
Console.WriteLine(serialDate.ToString("yyyy-MM-dd"));
```

### 2. Puste lub nieprawidłowe komórki

Jeśli komórka jest pusta lub zawiera nieparsowalny ciąg, `GetDateTime` wyrzuci wyjątek. Owiń wywołanie w `try/catch` lub najpierw sprawdź `IsDateTime`:

```csharp
if (worksheet.Cells["C3"].Type == CellValueType.IsDateTime)
{
    DateTime safeDate = worksheet.Cells["C3"].GetDateTime();
    Console.WriteLine(safeDate.ToString("yyyy-MM-dd"));
}
else
{
    Console.WriteLine("Cell C3 does not contain a valid date.");
}
```

### 3. Różne formaty ery

Inne japońskie ery (Heisei, Showa) podążają za tym samym schematem. Ten sam `JapaneseLunisolarCalendar` obsłuży je automatycznie, więc nie potrzebujesz dodatkowej logiki — po prostu podaj ciąg.

---

## Porady i pułapki

- **Wydajność:** Podczas przetwarzania dużych arkuszy, ponownie używaj jednej instancji `CultureInfo` zamiast tworzyć nową w pętli.
- **Bezpieczeństwo wątków:** Obiekty `CultureInfo` są tylko do odczytu po ustawieniu kalendarza, więc można je bezpiecznie udostępniać między wątkami.
- **Licencjonowanie Aspose.Cells:** Jeśli używasz wersji próbnej, pamiętaj, że niektóre funkcje mogą być ograniczone po wygaśnięciu okresu próbnego. Parsowanie dat pokazane tutaj działa zarówno w trybie próbnym, jak i licencjonowanym.
- **Strefy czasowe:** `DateTime`, który otrzymujesz, jest **nieokreślony** (brak strefy czasowej). Jeśli potrzebujesz UTC, wywołaj `DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc)` lub skonwertuj przy użyciu `TimeZoneInfo`.

---

## Zakończenie

Omówiliśmy wszystko, co potrzebne, aby **format date iso** z skoroszytu Excel przy użyciu C#. Zaczynając od surowego ciągu japońskiej ery, **read Excel datetime**, ustawiliśmy odpowiednią kulturę, **extract datetime excel** dane i w końcu wyprowadziliśmy czysty ciąg ISO‑8601. Podejście działa dla każdej reprezentacji daty, jaką Excel może Ci przedstawić, niezależnie czy to liczba seryjna, ciąg zależny od ustawień regionalnych, czy tradycyjny format ery.

Kolejne kroki? Spróbuj przeiterować całą kolumnę dat, zapisać wyniki ISO z powrotem do nowego arkusza lub wprowadzić je bezpośrednio do ładunku JSON dla usługi webowej. Jeśli jesteś ciekawy innych systemów kalendarzowych (hebrajski, islamski), Aspose.Cells i `CultureInfo` w .NET ułatwiają takie eksperymenty.

Masz pytania lub trudny format daty, którego nie możesz rozgryźć? zostaw komentarz poniżej i szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}