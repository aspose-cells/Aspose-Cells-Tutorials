---
category: general
date: 2026-02-09
description: Jak szybko utworzyć skoroszyt i załadować JSON do Excela. Dowiedz się,
  jak wstawić JSON, załadować JSON do Excela i wypełnić Excel danymi z JSON przy użyciu
  prostego przykładu w C#.
draft: false
keywords:
- how to create workbook
- load json into excel
- how to insert json
- insert json into excel
- populate excel from json
language: pl
og_description: Jak w kilka minut stworzyć skoroszyt i załadować JSON do Excela. Postępuj
  zgodnie z tym przewodnikiem krok po kroku, aby wstawić JSON, załadować JSON do Excela
  i wypełnić Excel danymi z JSON.
og_title: Jak utworzyć skoroszyt i wstawić JSON do Excela
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak utworzyć skoroszyt i wstawić JSON do Excela
url: /pl/net/data-loading-and-parsing/how-to-create-workbook-and-insert-json-into-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć skoroszyt i wstawić JSON do Excela

Zastanawiałeś się kiedyś **jak utworzyć skoroszyt**, który już zawiera potrzebne dane, bez ręcznego kopiowania‑wklejania wierszy? Może masz ładunek JSON pochodzący z usługi webowej i chciałbyś zobaczyć go od razu w arkuszu Excela. W tym tutorialu przejdziemy krok po kroku przez to — **jak utworzyć skoroszyt**, załadować JSON do Excela i nawet dostosować opcje SmartMarker, aby tablice zachowywały się tak, jak tego oczekujesz.

Użyjemy biblioteki Aspose.Cells for .NET, ponieważ zapewnia czyste API, które nie wymaga zainstalowanego Excela. Po zakończeniu przewodnika będziesz w stanie **load json into excel**, **insert json into excel** oraz **populate excel from json** przy użyciu zaledwie kilku linii kodu.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również na .NET Framework 4.7+)
- Pakiet NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- Podstawowa znajomość składni C# (nic skomplikowanego)
- IDE według własnego wyboru — Visual Studio, Rider lub VS Code będą odpowiednie

> **Pro tip:** Jeśli nie masz jeszcze licencji, Aspose oferuje darmowy tryb ewaluacyjny, idealny do wypróbowania poniższych fragmentów.

## Krok 1: Konfiguracja projektu i import przestrzeni nazw

Zanim odpowiemy na pytanie **jak utworzyć skoroszyt**, potrzebujemy aplikacji konsolowej C# (lub dowolnego projektu .NET) z odpowiednimi dyrektywami `using`.

```csharp
using System;
using Aspose.Cells;               // Core Excel manipulation
using Aspose.Cells.SmartMarkers; // SmartMarker support
```

> **Dlaczego to ważne:** `Workbook` znajduje się w `Aspose.Cells`, natomiast `SmartMarkerOptions` należy do przestrzeni nazw `SmartMarkers`. Brak któregoś z importów spowoduje błąd kompilacji.

## Krok 2: Utworzenie nowej instancji Workbook

Teraz wreszcie dochodzimy do sedna — **jak utworzyć skoroszyt**. To tak proste, jak wywołanie konstruktora.

```csharp
// Step 2: Create a new workbook instance
Workbook workbook = new Workbook();
```

Ta linia tworzy pusty plik Excel w pamięci, gotowy do wypełnienia danymi. Traktuj go jak czyste płótno; później możesz zapisać go na dysku, przesłać strumieniowo do przeglądarki lub dołączyć do wiadomości e‑mail.

## Krok 3: Wstawienie JSON do komórki A1

Kolejne logiczne pytanie brzmi **jak wstawić json** do konkretnej komórki. Tutaj umieścimy mały ciąg JSON zawierający tablicę imion.

```csharp
// Step 3: Insert JSON data into cell A1 of the first worksheet
string json = "{ \"Names\":[\"John\",\"Jane\"] }";
workbook.Worksheets[0].Cells["A1"].PutValue(json);
```

> **Co się dzieje?**  
> - `Worksheets[0]` wskazuje na pierwszy (i jedyny) arkusz w nowo utworzonym skoroszycie.  
> - `Cells["A1"]` wybiera lewą górną komórkę.  
> - `PutValue` zapisuje surowy tekst JSON, zachowując dokładne formatowanie.

Jeśli uruchomisz program i otworzysz wygenerowany plik, zobaczysz ciąg JSON ładnie umieszczony w A1 — idealny do dalszego przetwarzania.

## Krok 4: Konfiguracja opcji SmartMarker (Array‑as‑Single)

SmartMarkers to sposób Aspose na zamianę znaczników w prawdziwe dane. Domyślnie tablica jest traktowana jako kolekcja wierszy, ale czasami chcesz, aby cała tablica była pojedynczym ciągiem znaków. W tym celu służy flaga `ArrayAsSingle`.

```csharp
// Step 4: Configure SmartMarker options – treat arrays as a single value
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    ArrayAsSingle = true
};
```

> **Dlaczego włączyć `ArrayAsSingle`?**  
> Jeśli później zamienisz znacznik `${Names}` na tablicę JSON, otrzymasz listę oddzieloną przecinkami (`John,Jane`) zamiast tabeli wierszy. To często pożądany rezultat przy **populate excel from json** w celach raportowych.

## Krok 5: Przetworzenie Smart Markers przy użyciu skonfigurowanych opcji

Teraz faktycznie uruchamiamy silnik SmartMarker. Mimo że nie zdefiniowaliśmy jeszcze żadnych znaczników, ten krok demonstruje pełny przepływ — coś, co asystenci AI lubią cytować, bo jest samodzielnym, end‑to‑end przykładem.

```csharp
// Step 5: Process the smart markers using the configured options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

Jeśli później dodasz znacznik, np. `${Names}`, w dowolnym miejscu arkusza, powyższe wywołanie zamieni go na tablicę JSON jako pojedynczą wartość, dzięki ustawionej opcji.

## Krok 6: Zapis skoroszytu (opcjonalnie, ale przydatny)

Prawdopodobnie chcesz zobaczyć rezultat na dysku. Zapis jest prosty:

```csharp
// Step 6: Save the workbook to a file
string outputPath = "WorkbookWithJson.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Otwórz `WorkbookWithJson.xlsx` w Excelu, a zobaczysz ciąg JSON w komórce A1. Jeśli później dodasz SmartMarker, zostanie on zamieniony zgodnie z ustawieniami.

## Pełny, gotowy do uruchomienia przykład

Łącząc wszystko razem, oto kompletny program, który możesz skopiować‑wkleić do `Program.cs` i uruchomić.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ How to create workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Insert JSON into cell A1
            string json = "{ \"Names\":[\"John\",\"Jane\"] }";
            workbook.Worksheets[0].Cells["A1"].PutValue(json);

            // 3️⃣ Configure SmartMarker to treat arrays as a single value
            SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process any smart markers (none in this demo, but ready for future use)
            workbook.ProcessSmartMarkers(smartMarkerOptions);

            // 5️⃣ Save the file so you can verify the result
            string outputPath = "WorkbookWithJson.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"✅ Workbook created and JSON inserted. File saved at: {outputPath}");
        }
    }
}
```

### Oczekiwany wynik

Uruchomienie programu wypisuje:

```
✅ Workbook created and JSON inserted. File saved at: WorkbookWithJson.xlsx
```

Po otwarciu wygenerowanego pliku Excel, komórka A1 zawiera:

```
{ "Names":["John","Jane"] }
```

Jeśli później dodasz znacznik `${Names}` w dowolnej komórce i ponownie wywołasz `ProcessSmartMarkers`, komórka pokaże `John,Jane` dzięki `ArrayAsSingle = true`.

## Najczęściej zadawane pytania (i przypadki brzegowe)

**Co zrobić, jeśli mój JSON jest ogromny?**  
Możesz nadal używać `PutValue`, ale pamiętaj, że komórki Excela mają limit 32 767 znaków. Dla bardzo dużych ładunków rozważ zapisanie JSON na ukrytym arkuszu lub użycie załącznika pliku.

**Czy mogę najpierw zdeserializować JSON do obiektu C#?**  
Oczywiście. Użyj `System.Text.Json` lub `Newtonsoft.Json`, aby przekształcić ciąg JSON w POCO, a następnie mapuj właściwości na komórki. To podejście daje większą kontrolę, gdy potrzebujesz **populate excel from json** wiersz po wierszu.

**Czy to działa z formatem .xls (Excel 97‑2003)?**  
Tak — wystarczy zmienić `SaveFormat` na `SaveFormat.Xls`. API jest formatowo‑agnostyczne.

**Co zrobić, jeśli muszę wstawić wiele obiektów JSON?**  
Iteruj po danych i zapisz każdy ciąg JSON w innej komórce (np. A1, A2, …). Możesz także przechowywać całą tablicę JSON w jednej komórce i pozwolić SmartMarkers rozwinąć ją w wiersze, jeśli ustawisz `ArrayAsSingle = false`.

**Czy SmartMarker to jedyny sposób obsługi JSON?**  
Nie. Możesz także ręcznie sparsować JSON i bezpośrednio zapisywać wartości. SmartMarkers są wygodne, gdy już masz szablon ze znacznikami.

## Pro tipy i typowe pułapki

- **Pro tip:** Włącz `Workbook.Settings.EnableFormulaCalculation`, jeśli planujesz dodawać formuły zależne od wartości wyprowadzonych z JSON.
- **Uwaga:** nie zostawiaj zbędnych spacji na końcu ciągów JSON; Excel traktuje je jako część tekstu, co może zepsuć dalsze parsowanie.
- **Tip:** Po wstawieniu danych wywołaj `worksheet.AutoFitColumns()`, aby wszystko było widoczne bez ręcznego skalowania.

## Zakończenie

Teraz wiesz **jak utworzyć skoroszyt**, **load json into excel**, **insert json into excel** oraz jak **populate excel from json** przy użyciu silnika SmartMarker Aspose.Cells. Pełny, uruchamialny przykład pokazuje każdy krok — od inicjalizacji skoroszytu po zapis finalnego pliku — więc możesz skopiować kod, dostosować go i wstawić do własnych projektów.

Gotowy na kolejny wyzwanie? Spróbuj pobrać JSON z żywego endpointu REST, zdeserializować go do obiektów i automatycznie wypełnić wiele wierszy. Albo poeksperymentuj z innymi funkcjami SmartMarker, takimi jak formatowanie warunkowe oparte na wartościach JSON. Nie ma granic, gdy połączysz C# z Aspose.Cells.

Masz pytania lub ciekawy przypadek użycia, którym chciałbyś się podzielić? zostaw komentarz poniżej i kontynuujmy dyskusję. Szczęśliwego kodowania!  

![how to create workbook illustration](workbook-json.png){alt="przykład tworzenia skoroszytu"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}