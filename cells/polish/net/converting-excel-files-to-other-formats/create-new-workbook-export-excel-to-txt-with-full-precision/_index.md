---
category: general
date: 2026-03-18
description: Utwórz nowy skoroszyt i wyeksportuj Excel do TXT, zachowując precyzję
  numeryczną. Dowiedz się, jak zapisać arkusz jako txt i efektywnie konwertować arkusz
  na txt.
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: pl
og_description: Utwórz nowy skoroszyt i wyeksportuj Excel do TXT z precyzją. Ten samouczek
  pokazuje, jak zapisać arkusz jako txt oraz jak przekonwertować arkusz na txt przy
  użyciu C#.
og_title: Utwórz nowy skoroszyt – Przewodnik eksportu Excela do TXT
tags:
- Aspose.Cells
- C#
- Excel automation
title: Utwórz nowy skoroszyt – Eksportuj Excel do TXT z pełną precyzją
url: /pl/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz nowy skoroszyt – Eksportuj Excel do TXT z pełną precyzją

Kiedykolwiek potrzebowałeś **create new workbook** w C#, aby po prostu wyeksportować dane do pliku tekstowego? Być może pobierasz raport ze starszego systemu, a narzędzie downstream akceptuje jedynie plik `.txt`. Dobra wiadomość? Nie musisz poświęcać precyzji liczbowej i z pewnością nie musisz ręcznie tworzyć ciągów CSV.

W tym przewodniku przejdziemy przez cały proces **export excel to txt**, omawiając wszystko od inicjalizacji skoroszytu po zachowanie zer końcowych podczas **save worksheet as txt**. Po zakończeniu będziesz mieć gotowy fragment kodu, który możesz wkleić do dowolnego projektu .NET — bez dodatkowych narzędzi.

## Czego będziesz potrzebować

- **ASP.NET/ .NET 6+** (kod działa również na .NET Framework 4.6+)
- **Aspose.Cells for .NET** – biblioteka, która udostępnia klasy `Workbook`, `Worksheet` i `TxtSaveOptions`. Możesz ją pobrać z NuGet za pomocą `Install-Package Aspose.Cells`.
- Podstawowa znajomość C# (jeśli czujesz się komfortowo z instrukcjami `using`, jesteś gotowy).

To wszystko — bez interfejsu Excel, bez obiektów COM i zdecydowanie bez ręcznego łączenia ciągów.

---

## Krok 1: Inicjalizacja nowego skoroszytu (Primary Keyword)

Pierwszą rzeczą, którą musisz zrobić, jest **create new workbook**. Traktuj skoroszyt jako czyste płótno, na którym później wkleisz liczby, tekst lub formuły.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();                 // <‑‑ creates new workbook
            Worksheet worksheet = workbook.Worksheets[0];       // first sheet (index 0)
```

> **Dlaczego to ważne:** Tworzenie instancji `Workbook` bez ładowania pliku daje czystą kartę. Następnie możesz programowo dodawać dane, co jest idealne w scenariuszach **convert worksheet to txt**, gdy nie masz istniejącego pliku `.xlsx`.

## Krok 2: Wypełnianie komórek — zachowaj zera końcowe

Częstym pułapką przy zapisywaniu liczb do tekstu jest utrata zer końcowych (`123.45000` staje się `123.45`). Jeśli systemy downstream polegają na polach o stałej szerokości, taka utrata może zepsuć wszystko.

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **Wskazówka:** `PutValue` automatycznie określa typ danych. Jeśli potrzebujesz łańcucha wyglądającego jak liczba, użyj `PutValue("123.45000")`.

## Krok 3: Konfiguracja opcji zapisu TXT — zachowanie precyzji liczbowej

Tutaj dzieje się magia. Przełączając `PreserveNumericPrecision`, instruujesz Aspose.Cells, aby zapisał dokładnie wprowadzoną wartość, włącznie z nieistotnymi zerami końcowymi.

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **Dlaczego to włączyć?** Gdy **save excel as txt**, domyślne zachowanie usuwa niepotrzebne miejsca po przecinku. Ustawienie `PreserveNumericPrecision = true` zapewnia, że wynik odzwierciedla wyświetlaną wartość komórki, co jest kluczowe dla raportów finansowych lub danych naukowych.

## Krok 4: Zapisz arkusz jako TXT — ostateczny eksport

Teraz faktycznie **save worksheet as txt**. Możesz wskazać dowolną ścieżkę, do której masz uprawnienia zapisu; w przykładzie używany jest względny folder o nazwie `output`.

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **Oczekiwany wynik** (`num-preserve.txt`):

```
123.45000
```

Zauważ, że zera końcowe są zachowane — dokładnie tak, jak prosiłeś.

## Krok 5: Weryfikacja wyniku — szybka kontrola poprawności

Po uruchomieniu programu otwórz `num-preserve.txt` w dowolnym edytorze tekstu. Powinieneś zobaczyć jedną linię `123.45000`. Jeśli zamiast tego zobaczysz `123.45`, sprawdź ponownie, czy `PreserveNumericPrecision` jest ustawione na `true` oraz czy używasz najnowszej wersji Aspose.Cells (v23.10+).

## Typowe warianty i przypadki brzegowe

### Eksportowanie wielu komórek lub zakresów

Jeśli musisz **export excel to txt** dla całego zakresu, po prostu wypełnij więcej komórek przed zapisem:

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

Aspose domyślnie zapisze każdą komórkę w nowej linii. Możesz także zmienić separator (tabulator, przecinek) za pomocą `txtSaveOptions.Separator`.

### Konwersja arkusza do TXT z różnymi kodowaniami

Czasami systemy downstream wymagają UTF‑8 BOM lub ASCII. Dostosuj kodowanie w ten sposób:

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### Obsługa dużych skoroszytów

Podczas pracy z ogromnymi arkuszami (setki tysięcy wierszy) rozważ strumieniowanie wyniku:

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

## Porady i pułapki

- **Nie zapomnij utworzyć katalogu wyjściowego** przed wywołaniem `Save`, w przeciwnym razie otrzymasz `DirectoryNotFoundException`.
- **Uważaj na lokalne separatory dziesiętne**. Jeśli Twoje środowisko używa przecinków (`1,23`), ustaw `txtSaveOptions.DecimalSeparator = '.'`, aby wymusić kropkę.
- **Kompatybilność wersji**: Flaga `PreserveNumericPrecision` została wprowadzona w Aspose.Cells 20.6. Jeśli używasz starszej wersji, flaga nie będzie dostępna i będziesz musiał sformatować komórkę jako tekst przed zapisem.

![Przykład tworzenia nowego skoroszytu](excel-to-txt.png "Utwórz nowy skoroszyt")

*Tekst alternatywny obrazu: "Utwórz nowy skoroszyt i wyeksportuj Excel do TXT z zachowaną precyzją liczbową"*

## Podsumowanie – co omówiliśmy

- **Create new workbook** przy użyciu Aspose.Cells.
- Wypełnij komórkę liczbą zawierającą zera końcowe.
- Ustaw `TxtSaveOptions.PreserveNumericPrecision = true`, aby **save excel as txt** bez utraty precyzji.
- Zapisz plik na dysku, weryfikując, że wynik odpowiada pierwotnej wartości.

To pełny przepływ **convert worksheet to txt** w mniej niż 50 liniach C#.

## Kolejne kroki i powiązane tematy

Teraz, gdy możesz **export excel to txt** z doskonałą precyzją, możesz chcieć zbadać:

- **Eksportowanie do CSV** z niestandardowymi separatorami (`TxtSaveOptions.Separator`).
- **Zapisywanie w innych formatach tekstowych** takich jak TSV (`SaveFormat.TabDelimited`).
- **Przetwarzanie wsadowe** wielu skoroszytów w folderze przy użyciu `Directory.GetFiles`.
- **Integracja z Azure Functions** w celu konwersji na żądanie w chmurze.

Każdy z nich opiera się na tym samym schemacie `Workbook` → `Worksheet` → `TxtSaveOptions`, więc poczujesz się jak w domu.

### Ostatnia myśl

Jeśli podążałeś za instrukcją, teraz wiesz dokładnie, jak **create new workbook**, wypełnić go i **save worksheet as txt**, zachowując każdy potrzebny znak dziesiętny. To mały fragment kodu, ale rozwiązuje zaskakująco powszechny problem, gdy starsze pipeline’y wymagają wejść w formacie tekstowym.

Wypróbuj go, dostosuj opcje i niech dane płyną dokładnie tak, jak potrzebujesz. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}