---
category: general
date: 2026-08-11
description: Utwórz plik Excel programowo w C# przy użyciu Aspose.Cells. Przetwórz
  japońską datę w erze, zapisz ją w komórce i zapisz skoroszyt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel file programmatically
- datetime.parseexact custom format
- write date to excel cell
- how to save excel file c#
language: pl
lastmod: 2026-08-11
og_description: Twórz plik Excel programowo w C# przy użyciu Aspose.Cells. Dowiedz
  się, jak parsować japońską datę z erą za pomocą niestandardowego formatu DateTime.ParseExact,
  zapisać datę w komórce Excela i efektywnie zapisać skoroszyt.
og_image_alt: Screenshot of an Excel workbook with a parsed Japanese era date in cell
  A1
og_title: Utwórz plik Excel programowo w C# – pełny poradnik
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel file programmatically in C# using Aspose.Cells. Parse
    a Japanese era date, write it to a cell, and save the workbook.
  headline: Create excel file programmatically in C# – tutorial
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- DateTime parsing
title: Tworzenie pliku Excel programowo w C# – poradnik
url: /pl/net/excel-file-handling/create-excel-file-programmatically-in-c-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie pliku Excel programowo w C# – samouczek

Jeśli potrzebujesz **tworzyć plik Excel programowo**, możesz to zrobić w kilku linijkach kodu C#. Ten przewodnik pokazuje, jak wygenerować skoroszyt Excel przy użyciu Aspose.Cells, sparsować japońską datę epoki przy użyciu **niestandardowego formatu DateTime.ParseExact**, zapisać tę datę w komórce arkusza oraz ostatecznie **zapisać plik Excel w stylu C#**. Po zakończeniu będziesz mieć gotowy do użycia plik *.xlsx*, który zawiera prawidłowo skonwertowaną datę gregoriańską.

Nauczysz się, jak:

* Zainicjować skoroszyt bez szablonu.  
* Przekształcić ciąg znaków oparty na erze, np. `"R3/04/01"`, na `DateTime`.  
* Wstawić wartość `DateTime` do określonej komórki (`A1`).  
* Zachować skoroszyt na dysku przy użyciu pojedynczego wywołania `Save`.

Nie są wymagane dodatkowe biblioteki poza Aspose.Cells i podstawową biblioteką klas .NET.

---

## Wymagania wstępne

Przed rozpoczęciem upewnij się, że masz:

* **.NET 6.0** lub nowszy zainstalowany (kod działa również z .NET Framework 4.6+).  
* Ważną licencję **Aspose.Cells** lub darmową wersję ewaluacyjną.  
* Podstawową znajomość składni C# oraz Visual Studio (lub dowolnego preferowanego IDE).

---

## Tworzenie pliku Excel programowo – inicjalizacja skoroszytu

Pierwszym krokiem jest utworzenie pustego obiektu skoroszytu. Aspose.Cells udostępnia klasę `Workbook`, która reprezentuje cały plik Excel w pamięci.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();               // creates an empty .xlsx structure
        var worksheet = workbook.Worksheets[0];      // the default first sheet is named "Sheet1"
```

**Dlaczego to ważne:**  
Tworzenie skoroszytu programowo eliminuje potrzebę fizycznego pliku szablonu, co zmniejsza rozmiar wdrożenia i pozwala generować pliki w locie dla raportów, faktur lub eksportu danych.

---

## Użycie niestandardowego formatu DateTime.ParseExact dla japońskich dat epokowych

Ciągi dat zawierające japońskie symbole epok (np. `"R"` dla Reiwa) nie mogą być parsowane domyślnym `DateTime.Parse`. Musisz podać **niestandardowy format** oraz japońską kulturę rozpoznającą oznaczenie ery.

```csharp
        // Step 2: Define the era‑based date string (Reiwa 3, April 1)
        string eraDate = "R3/04/01";

        // Step 3: Create a CultureInfo that knows Japanese eras
        var japaneseCulture = new CultureInfo("ja-JP");

        // Step 4: Parse the era date using a custom format string
        //   "g"  = era designator (R, H, etc.)
        //   "yy" = two‑digit year within the era
        //   "MM" = month (01‑12)
        //   "dd" = day of month (01‑31)
        DateTime parsedDate = DateTime.ParseExact(
            eraDate,
            "ggy/MM/dd",
            japaneseCulture,
            DateTimeStyles.None);
```

**Dlaczego to ważne:**  
`DateTime.ParseExact` gwarantuje, że wejście pasuje do określonego wzorca, zapobiegając niejednoznacznościom zależnym od ustawień regionalnych. Wzorzec `"ggy/MM/dd"` instruuje .NET, aby traktował pierwszy znak jako erę (`g`), po którym następuje dwucyfrowy rok (`yy`), miesiąc i dzień. Użycie `japaneseCulture` zapewnia prawidłową interpretację symboli ery, co skutkuje datą gregoriańską `DateTime` (`2021‑04‑01` w przykładzie).

---

## Zapis daty do komórki Excel przy użyciu Aspose.Cells

Teraz, gdy masz instancję `DateTime`, możesz umieścić ją w dowolnej komórce arkusza. Aspose.Cells automatycznie formatuje komórkę zgodnie z domyślnym stylem daty skoroszytu.

```csharp
        // Step 5: Write the DateTime value into cell A1
        worksheet.Cells["A1"].PutValue(parsedDate);

        // Optional: Apply a custom number format if you want a specific display
        worksheet.Cells["A1"].Style.Number = 14; // 14 = "m/d/yyyy" in Excel
```

**Dlaczego to ważne:**  
Użycie `PutValue` pozwala Aspose.Cells wywnioskować typ komórki (data, liczba, tekst) z podanego typu .NET. To podejście jest bezpieczniejsze niż zapisywanie sformatowanego ciągu, ponieważ Excel zachowuje semantykę daty — umożliwiając późniejsze sortowanie, filtrowanie lub wykonywanie obliczeń na kolumnie.

---

## Jak zapisać plik Excel w C# – finalizacja skoroszytu

Ostatnim krokiem jest zapisanie skoroszytu znajdującego się w pamięci do fizycznego pliku. Aspose.Cells obsługuje wiele formatów; tutaj używamy nowoczesnego formatu `.xlsx`.

```csharp
        // Step 6: Save the workbook to the desired location
        string outputPath = @"C:\Temp\JapaneseEra.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Dlaczego to ważne:**  
Wywołanie `Save` z `SaveFormat.Xlsx` zapisuje zgodny ze standardem plik Office Open XML, który może być otwarty w Excel, LibreOffice lub dowolnym przeglądarce obsługującej ten format. Metoda obsługuje również całą kompresję i pakowanie, więc nie musisz samodzielnie zarządzać strumieniami zip.

---

## Oczekiwany wynik

Po uruchomieniu programu:

| Komórka | Wartość (wyświetlana) | Typ bazowy |
|---------|-----------------------|------------|
| A1      | 4/1/2021              | Data (DateTime) |

Plik `JapaneseEra.xlsx` będzie zawierał jedną arkusz o nazwie **Sheet1** z datą gregoriańską `2021‑04‑01` w komórce **A1**. Excel potraktuje tę komórkę jako datę, umożliwiając dalsze obliczenia, np. `=A1+30`, aby dodać 30 dni.

---

## Typowe warianty i przypadki brzegowe

| Sytuacja | Rozwiązanie |
|----------|-------------|
| **Inna era** (np. Heisei `H30/12/31`) | Zmień ciąg wejściowy; ten sam wzorzec `"ggy/MM/dd"` działa, ponieważ japoński `CultureInfo` zna wszystkie ery. |
| **Cztero‑cyfrowy rok** (np. `"R2023/04/01"`) | Użyj `"ggyyyy/MM/dd"` jako ciągu formatu. |
| **Brak symbolu ery** | Podaj format awaryjny, np. `"yyyy/MM/dd"` i spróbuj `DateTime.TryParseExact` z wieloma wzorcami. |
| **Nieprawidłowa data** (np. `"R3/13/01"`) | Umieść `ParseExact` w bloku `try/catch` lub użyj `DateTime.TryParseExact`, aby obsłużyć niepowodzenia parsowania w sposób łagodny. |

**Wskazówka:** Zawsze waliduj sparsowany `DateTime` przed zapisaniem go do arkusza, szczególnie gdy dane źródłowe pochodzą od użytkownika lub z plików zewnętrznych.

---

## Podsumowanie

* Utworzyłeś **plik Excel programowo** przy użyciu Aspose.Cells.  
* Zparsowałeś japoński ciąg epoki przy użyciu **niestandardowego formatu DateTime.ParseExact**.  
* Zapisano **datę do komórki Excel** przy użyciu `PutValue`.  
* Nauczyłeś się **jak zapisać plik Excel w C#** przy użyciu jednego wywołania `Save`.

Te cztery kroki tworzą wielokrotnego użytku wzorzec dla każdego scenariusza, w którym trzeba zaimportować kulturowo specyficzne daty do raportów Excel.

---

## Kolejne kroki

* Zbadaj **stylizację komórek** (czcionki, kolory, obramowania), aby Twoje raporty wyglądały profesjonalnie.  
* Użyj **Workbook.Save** w innych formatach (`Csv`, `Pdf`), aby eksportować dane dla różnych odbiorców.  
* Połącz tę technikę z **masowym wstawianiem danych** (`Cells.ImportDataTable`) dla dużych importów.  

Śmiało eksperymentuj z różnymi symbolami ery, niestandardowymi formatami liczb lub wieloma arkuszami. Ta sama podstawowa logika — utwórz, sparsuj, zapisz, zapisz — ma zastosowanie we wszystkich zadaniach automatyzacji Excel w C#.

---

## Co powinieneś się nauczyć dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z krok po kroku wyjaśnieniami, pomagając opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak utworzyć i zapisać skoroszyt Excel jako ODS przy użyciu Aspose.Cells dla .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Jak zapisać wybrane strony pliku Excel jako PDF przy użyciu Aspose.Cells dla .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)
- [Jak utworzyć i zapisać skoroszyt Excel jako SVG przy użyciu Aspose.Cells dla Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}