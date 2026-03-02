---
category: general
date: 2026-03-01
description: Jak szybko utworzyć skoroszyt w C# — naucz się zapisywać wartość do komórki,
  ustawiać format liczbowy komórki i formatować liczbę w komórce w prostych krokach.
draft: false
keywords:
- how to create workbook
- write value to cell
- format cell number
- set cell number format
- how to write cell
language: pl
og_description: Jak utworzyć skoroszyt w C#? Ten przewodnik pokazuje, jak zapisać
  wartość do komórki, ustawić format liczbowy komórki oraz sformatować liczbę w komórce
  w zaledwie kilku linijkach kodu.
og_title: Jak utworzyć skoroszyt w C# – zapisz wartość i sformatuj liczbę
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Jak utworzyć skoroszyt w C# – zapisywanie wartości i formatowanie liczb
url: /pl/net/excel-workbook/how-to-create-workbook-in-c-write-value-format-number/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć skoroszyt w C# – zapisywanie wartości i formatowanie liczb

Tworzenie skoroszytu w C# to powszechne zadanie, gdy trzeba generować pliki Excel „w locie”. W tym przewodniku pokażemy, jak zapisać wartość w komórce i sformatować liczbę, aby końcowy arkusz wyglądał profesjonalnie.

Jeśli kiedykolwiek patrzyłeś na pusty arkusz i zastanawiałeś się, dlaczego liczby wyświetlają zbyt wiele miejsc po przecinku, nie jesteś sam. Omówimy wszystko – od inicjalizacji obiektu skoroszytu po ustawienie własnego formatu liczbowego, a także podpowiemy kilka wskazówek dotyczących przypadków brzegowych, które mogą się pojawić później.

## Czego się nauczysz

- **Zainicjalizujesz** nową instancję `Workbook`.  
- **Zapiszesz wartość w komórce** przy użyciu metody `PutValue`.  
- **Ustawisz format liczbowy komórki** za pomocą obiektu `Style`, uzyskując czyste wyświetlanie z dwoma cyframi po przecinku.  
- Zweryfikujesz wynik, odczytując komórkę ponownie lub otwierając plik w Excelu.  

Nie są wymagane żadne zewnętrzne biblioteki poza standardowym Aspose.Cells (lub podobnym API), a kod działa na .NET 6+ bez dodatkowej konfiguracji.

---

## Jak utworzyć skoroszyt – inicjalizacja obiektu

Na początek potrzebujesz obiektu skoroszytu, który będzie przechowywał arkusze. Pomyśl o `Workbook` jako o całym pliku Excel, a każdy `Worksheet` to pojedyncza karta.

```csharp
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

*Dlaczego to ważne:* Tworzenie skoroszytu alokuje wewnętrzne struktury, które później będą przechowywać wiersze, kolumny i formatowanie. Bez tego obiektu nie ma gdzie zapisać wartości w komórce.

> **Porada:** Jeśli zamierzasz pracować z istniejącym plikiem, zamień `new Workbook()` na `new Workbook("template.xlsx")`, aby wczytać szablon i zachować jego style.

## Zapisz wartość w komórce

Mając już skoroszyt, wrzućmy liczbę do komórki **A1** pierwszego arkusza.

```csharp
// Step 2: Access cell A1 in the first worksheet
Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

// Step 3: Insert a numeric value into the cell
cellA1.PutValue(123.456789);
```

*Dlaczego używamy `PutValue`*: Metoda ta automatycznie wykrywa typ danych, więc nie musisz ręcznie rzutować ani konwertować. Szanuje także istniejący styl komórki, co jest przydatne, gdy później **ustawisz format liczbowy komórki**.

### Szybka kontrola

Jeśli odczytasz komórkę ponownie, zobaczysz surową wartość:

```csharp
double raw = cellA1.DoubleValue; // raw == 123.456789
```

To liczba przed zastosowaniem jakiegokolwiek formatowania.

## Ustaw format liczbowy komórki

Wyświetlanie surowego `double` z wieloma miejscami po przecinku nie zawsze jest przyjazne dla użytkownika. Ograniczmy je do dwóch cyfr znaczących.

```csharp
// Step 4: Apply a style that formats the number with two significant digits
cellA1.SetStyle(new Style() { Number = 2 });
```

Właściwość `Number` odpowiada wbudowanym identyfikatorom formatów liczbowych Excela. `2` oznacza „Liczba z dwoma miejscami po przecinku”. Jeśli potrzebujesz innego formatu – np. waluty lub daty – użyj innego ID lub własnego ciągu formatowania.

### Alternatywa: własny ciąg formatowania

```csharp
Style customStyle = workbook.CreateStyle();
customStyle.Custom = "#,##0.00"; // forces two decimals with thousand separator
cellA1.SetStyle(customStyle);
```

*Dlaczego wybrać własny styl?* Daje pełną kontrolę, szczególnie gdy wbudowane ID nie obejmują Twoich ustawień regionalnych.

## Zweryfikuj wynik (opcjonalnie, ale zalecane)

Po zastosowaniu stylu możesz zapisać skoroszyt i otworzyć go w Excelu, aby potwierdzić wygląd.

```csharp
// Save the workbook to a file
workbook.Save("FormattedWorkbook.xlsx");

// Or, for quick verification in code:
string displayed = cellA1.StringValue; // "123.46"
Console.WriteLine($"Displayed value: {displayed}");
```

Powinieneś zobaczyć **123,46** w komórce A1 – dokładnie dwa miejsca po przecinku, dzięki ustawionemu formatowi.

---

### Pełny działający przykład

Łącząc wszystko w całość, oto samodzielny program, który możesz skopiować i wkleić do aplikacji konsolowej.

```csharp
using System;
using Aspose.Cells;   // Ensure you have the Aspose.Cells NuGet package

class Program
{
    static void Main()
    {
        // Initialize the workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet and cell A1
        Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

        // Write a numeric value
        cellA1.PutValue(123.456789);

        // Apply a two‑decimal number format
        cellA1.SetStyle(new Style() { Number = 2 });

        // Save to disk (optional)
        workbook.Save("FormattedWorkbook.xlsx");

        // Output the displayed text for verification
        Console.WriteLine($"Cell A1 shows: {cellA1.StringValue}");
    }
}
```

**Oczekiwany wynik po uruchomieniu programu:**

```
Cell A1 shows: 123.46
```

Otwórz `FormattedWorkbook.xlsx` w Excelu i zobaczysz tę samą sformatowaną wartość.

---

## Typowe warianty i przypadki brzegowe

### 1. Różne formaty liczbowe

| Cel | ID formatu | Fragment kodu |
|------|------------|----------------|
| Waluta (dwa miejsca po przecinku) | 5 | `cellA1.SetStyle(new Style() { Number = 5 });` |
| Procent (bez miejsc po przecinku) | 10 | `cellA1.SetStyle(new Style() { Number = 10 });` |
| Notacja naukowa | 11 | `cellA1.SetStyle(new Style() { Number = 11 });` |

Jeśli żadne wbudowane ID nie pasuje, użyj własnego ciągu formatowania, jak pokazano wcześniej.

### 2. Separatory dziesiętne zależne od kultury

Niektóre locale używają przecinków jako separatorów dziesiętnych. Możesz wymusić format uwzględniający kulturę:

```csharp
Style cultureStyle = workbook.CreateStyle();
cultureStyle.Custom = "#,##0.00"; // works for most European locales
cellA1.SetStyle(cultureStyle);
```

### 3. Zapis tekstu zamiast liczb

Gdy potrzebujesz **zapisać tekst w komórce**, po prostu przekaż łańcuch znaków do `PutValue`:

```csharp
cellA1.PutValue("Total Revenue");
```

Format liczbowy nie jest wymagany, ale nadal możesz zastosować styl czcionki.

### 4. Duże zestawy danych

Jeśli wypełniasz tysiące wierszy, wstawianie wsadowe (`Cells.ImportArray`) jest szybsze niż iteracyjne wywoływanie `PutValue`. Podejście do formatowania pozostaje takie samo; wystarczy zastosować styl do zakresu:

```csharp
Range range = workbook.Worksheets[0].Cells.CreateRange("B2:B1001");
range.ApplyStyle(new Style() { Number = 2 });
```

---

## Najczęściej zadawane pytania

**P: Czy to działa z .NET Core?**  
O: Zdecydowanie. Aspose.Cells obsługuje .NET Standard 2.0 i nowsze, więc możesz celować w .NET 5, .NET 6 lub .NET 7 bez zmian.

**P: Co zrobić, jeśli potrzebuję więcej niż dwóch miejsc po przecinku?**  
O: Zmień właściwość `Number` na odpowiednie wbudowane ID (np. `3` dla trzech miejsc po przecinku) lub dostosuj własny ciąg formatowania (`"#,##0.000"`).

**P: Czy mogę zastosować format do całej kolumny jednocześnie?**  
O: Tak. Użyj `Cells["A:A"]`, aby pobrać całą kolumnę, a następnie `SetStyle`.

---

## Podsumowanie

Teraz wiesz, **jak utworzyć obiekt skoroszytu** w C#, **zapisać wartość w komórce** i **ustawić format liczbowy komórki**, aby liczby wyświetlały się dokładnie tak, jak chcesz. Opanowując te podstawy, będziesz w stanie generować profesjonalnie wyglądające raporty Excel, faktury lub eksporty danych przy minimalnym wysiłku.

Następnie możesz zgłębić **formatowanie liczb** dla dat, procentów lub formatowanie warunkowe – każdy z tych tematów opiera się na tych samych zasadach, które omówiliśmy. Zagłęb się w dokumentację Aspose.Cells, aby poznać bardziej zaawansowane opcje stylizacji, lub spróbuj połączyć wiele arkuszy w jednym skoroszycie, aby uzyskać bogatsze raporty.

Miłego kodowania, i pamiętaj: dobrze sformatowany arkusz kalkulacyjny to po prostu

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}