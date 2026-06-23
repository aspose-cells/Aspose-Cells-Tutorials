---
category: general
date: 2026-02-15
description: Jak utworzyć skoroszyt, przekonwertować ciąg znaków na datę i sformatować
  komórkę jako datę przy użyciu Aspose.Cells. Dowiedz się, jak ustawić format liczbowy
  komórki i łatwo odczytać datę w Excelu.
draft: false
keywords:
- how to create workbook
- convert string to date
- format cell as date
- set cell number format
- read excel date
language: pl
og_description: Jak utworzyć skoroszyt, przekonwertować ciąg znaków na datę i sformatować
  komórkę jako datę. Kompletny przewodnik krok po kroku dotyczący odczytywania dat
  w Excelu.
og_title: Jak utworzyć skoroszyt i przekonwertować ciąg znaków na datę w C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Jak utworzyć skoroszyt i przekonwertować ciąg znaków na datę w C#
url: /pl/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć skoroszyt i konwertować ciąg znaków na datę w C#

Zastanawiałeś się kiedyś **jak utworzyć skoroszyt**, który zamienia zwykły tekst taki jak `"R3-04-01"` na prawdziwą wartość `DateTime`? Nie jesteś jedyny — wielu programistów napotyka ten problem przy pobieraniu danych ze starszych systemów lub danych wprowadzanych przez użytkownika. Dobra wiadomość? Kilka linii C# i Aspose.Cells pozwoli Ci to zrobić w mig, bez ręcznego parsowania.

W tym samouczku przejdziemy przez cały proces: tworzenie skoroszytu, wstawianie ciągu daty, zastosowanie odpowiedniego **formatu komórki jako daty**, wymuszenie na silniku **ustawienia formatu liczbowego komórki**, a na koniec **odczytanie daty z Excela** jako `DateTime`. Po zakończeniu będziesz mieć działający fragment kodu, który możesz wkleić do dowolnego projektu .NET.

## Wymagania wstępne

- .NET 6+ (lub .NET Framework 4.7.2+)
- **Aspose.Cells for .NET** pakiet NuGet (`Install-Package Aspose.Cells`)
- Podstawowa znajomość składni C#
- IDE, takie jak Visual Studio lub VS Code (dowolne)

Nie wymagana jest dodatkowa konfiguracja — Aspose.Cells zajmuje się całą ciężką pracą wewnętrznie.

## Krok 1: Jak utworzyć skoroszyt – inicjalizacja pliku Excel

Najpierw potrzebujemy nowego obiektu skoroszytu. Pomyśl o nim jak o czystej notesie, w którym każdy arkusz jest stroną.

```csharp
using Aspose.Cells;

 // Step 1: Create a new workbook
 var workbook = new Workbook();          // Empty workbook with one default sheet
```

*Dlaczego to ważne:* Utworzenie skoroszytu daje nam kontener na komórki, style i formuły. Bez niego nie ma gdzie umieścić ciągu daty.

## Krok 2: Konwersja ciągu na datę – wstawienie surowego tekstu

Teraz wstawiamy surowy ciąg daty do komórki **A1** pierwszego arkusza. Ciąg używa własnego formatu (`R3-04-01`), którego Excel nie rozpoznaje od razu.

```csharp
 // Step 2: Insert a date string into cell A1 of the first worksheet
 var targetCell = workbook.Worksheets[0].Cells["A1"];
 targetCell.PutValue("R3-04-01");        // Raw text, not yet a date
```

*Dlaczego to robimy:* `PutValue` zapisuje dosłowny tekst. Gdybyśmy spróbowali ustawić `DateTime` bezpośrednio, własny format zostałby utracony. Trzymanie go jako tekst pozwala nam później zastosować **ustawienie formatu liczbowego komórki**, które mówi Excelowi, jak go interpretować.

## Krok 3: Formatuj komórkę jako datę – zastosuj styl numer 14

Wbudowany w Excel styl daty 14 odpowiada `mm-dd-yy`. Przypisując ten styl, informujemy silnik: „Traktuj zawartość tej komórki jako datę.”

```csharp
 // Step 3: Apply a date number format (style number 14) to the cell
 targetCell.SetStyle(new Style { Number = 14 });
```

*Co się dzieje w tle:* Właściwość `Number` mapuje na wewnętrzne identyfikatory formatów liczbowych Excela. Gdy skoroszyt przelicza się ponownie, Excel spróbuje przekształcić tekst w datę seryjną przy użyciu podanego formatu.

## Krok 4: Ustaw format liczbowy komórki – wymuś przeliczenie

Excel nie przekształci magicznie tekstu, dopóki nie poprosimy go o ocenę formuł (lub, w tym przypadku, reinterpretację komórki). Wywołanie `CalculateFormula` uruchamia tę konwersję.

```csharp
 // Step 4: Recalculate any formulas so the cell value is interpreted as a date
 workbook.CalculateFormula();
```

*Wskazówka:* Jeśli pracujesz z wieloma komórkami, możesz wywołać `CalculateFormula` raz po zakończeniu wszystkich formatowań — to oszczędza kilka milisekund.

## Krok 5: Odczytaj datę z Excela – pobierz wartość DateTime

Na koniec wyciągamy reprezentację `DateTime` z komórki. Aspose.Cells udostępnia ją poprzez `DateTimeValue`.

```csharp
 // Step 5: Retrieve the DateTime representation and display it
 Console.WriteLine(targetCell.DateTimeValue);
```

**Oczekiwany wynik (zakładając domyślny kalendarz gregoriański):**

```
2023-04-01 00:00:00
```

Zauważ, że prefiks `"R3-"` jest pomijany, ponieważ parser dat w Excelu skupia się na części numerycznej, gdy styl jest datą. Jeśli Twoje ciągi zawierają inne prefiksy, może być konieczne ich wstępne przetworzenie, ale dla wielu starszych formatów to podejście działa doskonale.

## Pełny działający przykład

Łącząc wszystko razem, oto kompletny, gotowy do uruchomienia program:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook
        var workbook = new Workbook();

        // Step 2: Insert a date string into cell A1 of the first worksheet
        var targetCell = workbook.Worksheets[0].Cells["A1"];
        targetCell.PutValue("R3-04-01");

        // Step 3: Apply a date number format (style number 14) to the cell
        targetCell.SetStyle(new Style { Number = 14 });

        // Step 4: Recalculate any formulas so the cell value is interpreted as a date
        workbook.CalculateFormula();

        // Step 5: Retrieve the DateTime representation and display it
        Console.WriteLine(targetCell.DateTimeValue);
    }
}
```

Zapisz to jako `Program.cs`, przywróć pakiet Aspose.Cells i uruchom `dotnet run`. Powinieneś zobaczyć sformatowany `DateTime` wypisany w konsoli.

## Typowe warianty i przypadki brzegowe

### Różne ciągi dat

Jeśli Twoje dane źródłowe wyglądają jak `"2023/04/01"` lub `"01‑Apr‑2023"`, nadal możesz korzystać z tego samego przepływu pracy — wystarczy zmienić właściwość **Number** na format pasujący do wzorca (np. `Number = 15` dla `d-mmm-yy`).  

### Formaty specyficzne dla lokalizacji

Excel respektuje ustawienia regionalne skoroszytu. Aby wymusić parsowanie w stylu US, ustaw kulturę skoroszytu:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");
```

### Gdy ciąg nie jest rozpoznany

Czasami Excel nie potrafi wywnioskować daty (np. `"R3-13-40"`). W takich przypadkach należy wstępnie przetworzyć ciąg:

```csharp
string raw = "R3-04-01";
string cleaned = raw.Replace("R3-", "");   // Remove the prefix
targetCell.PutValue(cleaned);
```

Następnie zastosuj ten sam format liczbowy.

## Porady i pułapki

- **Porada:** Użyj `StyleFlag`, aby zmodyfikować tylko format liczbowy, pozostawiając inne atrybuty stylu nietknięte.  
  ```csharp
  var style = targetCell.GetStyle();
  style.Number = 14;
  var flag = new StyleFlag { Number = true };
  targetCell.SetStyle(style, flag);
  ```
- **Uwaga:** Nadpisywanie istniejących stylów w komórce, która już ma obramowania lub czcionki. Podejście z `StyleFlag` zapobiega temu.
- **Uwaga dotycząca wydajności:** Jeśli przetwarzasz tysiące wierszy, wywołuj `CalculateFormula` jednorazowo po zakończeniu wszystkich aktualizacji; wywoływanie go dla każdego wiersza wprowadza niepotrzebny narzut.

## Zakończenie

Teraz wiesz **jak utworzyć skoroszyt**, **konwertować ciąg na datę**, **formatować komórkę jako datę**, **ustawiać format liczbowy komórki**, a na koniec **odczytać datę z Excela** jako `DateTime`. Wzorzec jest prosty: wstaw surowy tekst, zastosuj styl daty, wymuś przeliczenie, a następnie odczytaj wartość.

Od tego momentu możesz rozszerzyć logikę na całe kolumny, importować dane CSV lub nawet generować raporty, które automatycznie przetwarzają starsze ciągi dat na prawidłowe daty w Excelu.

Gotowy, aby podnieść poziom? Spróbuj zastosować własny format liczbowy (`Number = 22`), aby wyświetlać daty jako `yyyy-mm-dd`, lub zapoznaj się z narzędziami `DateTimeConversion` w Aspose.Cells dla bardziej złożonych scenariuszy.

Szczęśliwego kodowania! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}