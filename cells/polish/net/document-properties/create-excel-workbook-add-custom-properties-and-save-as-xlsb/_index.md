---
category: general
date: 2026-03-22
description: Utwórz skoroszyt Excel, dodaj własne właściwości, ustaw nazwę arkusza
  i zapisz jako plik binarny XLSB przy użyciu C#.
draft: false
keywords:
- create excel workbook
- add custom properties
- save as xlsb
- set worksheet name
- write binary excel file
language: pl
og_description: Utwórz skoroszyt Excel, dodaj własne właściwości, ustaw nazwę arkusza
  i zapisz jako plik binarny XLSB przy użyciu C#.
og_title: Utwórz skoroszyt Excel – Dodaj własne właściwości i zapisz jako XLSB
tags:
- C#
- Aspose.Cells
- Excel automation
title: Utwórz skoroszyt Excel – Dodaj własne właściwości i zapisz jako XLSB
url: /pl/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz skoroszyt Excel – Dodaj własne właściwości i zapisz jako XLSB

Czy kiedykolwiek potrzebowałeś **utworzyć skoroszyt Excel** programowo, ale także zachować pewne metadane? Być może tworzysz silnik raportujący, który oznacza każdy plik identyfikatorem raportu, nazwą autora lub numerem wersji. W takim wypadku nauka, jak **dodać własne właściwości** podczas **ustawiania nazwy arkusza** i w końcu **zapisać jako XLSB**, zaoszczędzi Ci wiele ręcznego przetwarzania.

W tym samouczku przeprowadzimy Cię przez kompletny, działający przykład, który dokładnie pokazuje, jak **zapisować binarny plik Excel** przy użyciu C#. Zobaczysz, dlaczego format XLSB jest właściwym wyborem do przenoszenia własnych właściwości, jak unikać najczęstszych pułapek oraz co zrobić, gdy potrzebujesz obsługi starszych wersji Excela.

---

## Czego będziesz potrzebować

- **.NET 6+** (lub .NET Framework 4.6+). Kod działa na każdym nowoczesnym środowisku uruchomieniowym.
- **Aspose.Cells for .NET** (bezpłatna wersja próbna lub licencjonowana). Dostarcza klasy `Workbook`, `Worksheet` i `CustomProperties` używane poniżej.
- IDE, z którym czujesz się komfortowo – Visual Studio, Rider lub nawet VS Code będą odpowiednie.
- Uprawnienia do zapisu w folderze, w którym zostanie zapisany wygenerowany plik.

Nie są wymagane żadne inne biblioteki firm trzecich.

## Krok 1: Zainstaluj Aspose.Cells

Na początek dodaj pakiet NuGet Aspose.Cells do swojego projektu:

```bash
dotnet add package Aspose.Cells
```

> **Wskazówka:** Jeśli pracujesz na serwerze CI, przechowuj klucz licencyjny w zmiennej środowiskowej i wczytuj go w czasie działania – zapobiega to pojawieniu się znaku wodnego „evaluation” w Twoim wyniku.

## Krok 2: Utwórz skoroszyt Excel – przegląd

Pierwszym rzeczywistym działaniem jest **utworzenie skoroszytu Excel**. Ten obiekt reprezentuje cały plik w pamięci i daje dostęp do arkuszy, stylów oraz własnych właściwości.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2.1: Instantiate a new workbook (empty by default)
            Workbook workbook = new Workbook();

            // The rest of the steps follow...
```

Dlaczego tworzyć nowy `Workbook` zamiast wczytywać szablon? Pusty skoroszyt zapewnia brak ukrytych stylów czy pozostawionych własnych właściwości, co jest szczególnie ważne, gdy zamierzasz **zapisować binarny plik Excel** dla systemów downstream oczekujących czystego stanu.

## Krok 3: Ustaw nazwę arkusza (i dlaczego ma to znaczenie)

Arkusze w Excelu domyślnie noszą nazwy „Sheet1”, „Sheet2” itd. Nadanie arkuszowi znaczącej nazwy ułatwia przetwarzanie downstream — takim jak Power Query czy makra VBA — i sprawia, że jest bardziej czytelny.

```csharp
            // Step 3.1: Grab the first worksheet (index 0) and rename it
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data"; // clear, concise, and self‑describing
```

Jeśli spróbujesz przypisać zduplikowaną nazwę, Aspose.Cells zgłosi `ArgumentException`. Dla bezpieczeństwa możesz sprawdzić `Worksheets.Exists("Data")` przed zmianą nazwy.

## Krok 4: Dodaj własne właściwości

Własne właściwości są przechowywane w wewnętrznym XML skoroszytu i podróżują wraz z plikiem niezależnie od formatu. Są idealne do osadzania takich elementów jak `ReportId` czy `GeneratedBy`.

```csharp
            // Step 4.1: Add a numeric property
            workbook.CustomProperties.Add("ReportId", 12345);

            // Step 4.2: Add a string property
            workbook.CustomProperties.Add("GeneratedBy", "MyApp");
```

> **Dlaczego używać własnych właściwości?**  
> • Są dostępne w panelu Excela „Plik → Informacje → Właściwości”.  
> • Kod, który konsumuje skoroszyt, może je odczytać bez skanowania zawartości komórek.  
> • Przetrwają konwersje formatów (XLSX ↔ XLSB), ponieważ są częścią metadanych pliku.

Możesz także przechowywać daty, wartości logiczne lub nawet binarne blob’y, ale zachowaj mały rozmiar danych — Excel nie jest bazą danych.

## Krok 5: Zapisz jako XLSB (zapis binarnego pliku Excel)

Format XLSB przechowuje dane w strukturze binarnej, co sprawia, że plik jest mniejszy i szybciej się otwiera. Co ważniejsze w tym samouczku, **własne właściwości są wbudowane w strumień binarny**, co zapewnia ich przenoszenie wraz z plikiem.

```csharp
            // Step 5.1: Define the output path
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "WithCustomProps.xlsb");

            // Step 5.2: Save the workbook as a binary XLSB file
            workbook.Save(outputPath, SaveFormat.Xlsb);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

### Oczekiwany wynik

Po uruchomieniu programu znajdziesz plik `WithCustomProps.xlsb` na pulpicie. Otwórz go w Excelu, przejdź do **Plik → Informacje → Właściwości** i zobaczysz `ReportId` oraz `GeneratedBy` wymienione w sekcji *Własne*.

## Krok 6: Przypadki brzegowe i typowe pytania

### Co zrobić, gdy docelowy folder jest tylko do odczytu?

Umieść wywołanie `Save` w bloku `try/catch` i przejdź do lokalizacji zapisywalnej przez użytkownika, takiej jak `%TEMP%`. Zapobiega to awarii aplikacji w przypadku błędów uprawnień.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsb);
}
catch (UnauthorizedAccessException)
{
    string fallback = Path.GetTempFileName().Replace(".tmp", ".xlsb");
    workbook.Save(fallback, SaveFormat.Xlsb);
    Console.WriteLine($"Saved to fallback location: {fallback}");
}
```

### Czy mogę **zapisować jako XLSX** i nadal zachować własne właściwości?

Tak — wystarczy zmienić `SaveFormat.Xlsb` na `SaveFormat.Xlsx`. Właściwości są przechowywane w tej samej części XML, więc przetrwają zmianę formatu. Jednak pliki XLSX są większe, ponieważ są spakowanym XML, podczas gdy XLSB zapewnia lepszą wydajność przy dużych zestawach danych.

### Jak odczytać własne właściwości później?

```csharp
Workbook loaded = new Workbook(outputPath);
foreach (CustomProperty prop in loaded.CustomProperties)
{
    Console.WriteLine($"{prop.Name} = {prop.Value}");
}
```

Ten fragment wypisuje każdą własną właściwość, co ułatwia usługom downstream weryfikację pochodzenia pliku.

## Pełny działający przykład

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do nowego projektu konsolowego. Nie brakuje żadnych elementów — wszystko od instrukcji `using` po końcowe `Console.WriteLine` jest zawarte.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook instance
            Workbook workbook = new Workbook();

            // 2️⃣ Access the first worksheet and give it a meaningful name
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data";

            // 3️⃣ Add custom properties (they travel with the file)
            workbook.CustomProperties.Add("ReportId", 12345);
            workbook.CustomProperties.Add("GeneratedBy", "MyApp");

            // 4️⃣ Define where to save the binary XLSB file
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "WithCustomProps.xlsb");

            // 5️⃣ Save the workbook as a binary XLSB file
            try
            {
                workbook.Save(outputPath, SaveFormat.Xlsb);
                Console.WriteLine($"✅ Workbook saved to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❌ Failed to save workbook: {ex.Message}");
            }
        }
    }
}
```

Uruchom program, otwórz powstały plik i zweryfikuj własne właściwości. To cały proces **utworzenia skoroszytu Excel**, **dodania własnych właściwości**, **ustawienia nazwy arkusza** i **zapisania jako xlsb** w jednym spójnym przebiegu.

## Zakończenie

Teraz wiesz dokładnie, jak **utworzyć skoroszyt Excel**, nadać jego arkuszowi wyraźną **nazwę arkusza**, osadzić przydatne metadane za pomocą **dodania własnych właściwości**, a na koniec **zapisać jako XLSB**, aby uzyskać kompaktowy, binarny plik Excel. Ten przepływ pracy jest niezawodny, działa na różnych wersjach .NET i dobrze się skalowuje, niezależnie od tego, czy generujesz jeden raport, czy tysiąc.

Co dalej? Spróbuj dodać tabelę danych do arkusza „Data”, poeksperymentuj z różnymi typami właściwości (daty, wartości logiczne) lub zmień wyjście na **zapis jako xlsb** dla ogromnych zestawów danych. Możesz także zbadać ochronę skoroszytu hasłem — Aspose.Cells umożliwia to w jednej linii kodu.

Śmiało zostaw komentarz, jeśli napotkasz problemy, lub podziel się, jak rozbudowałeś ten wzorzec w swoich projektach. Szczęśliwego kodowania!  

---  

![Zrzut ekranu tworzenia skoroszytu Excel](image.png){alt="Utwórz skoroszyt Excel z własnymi właściwościami"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}