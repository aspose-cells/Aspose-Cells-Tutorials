---
category: general
date: 2026-02-23
description: Jak utworzyć skoroszyt przy użyciu Aspose.Cells i dodać znaczniki za
  pomocą tablicy JSON. Dowiedz się, jak dodawać znaczniki, używać tablicy JSON oraz
  inteligentnych znaczników Aspose.Cells w kilka minut.
draft: false
keywords:
- how to create workbook
- how to add markers
- use json array
- smart markers aspose.cells
language: pl
og_description: Jak utworzyć skoroszyt przy użyciu Aspose.Cells, dodać znaczniki i
  użyć tablicy JSON. Ten przewodnik krok po kroku pokaże Ci wszystko, czego potrzebujesz.
og_title: Jak utworzyć skoroszyt z inteligentnymi znacznikami – Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Jak utworzyć skoroszyt z inteligentnymi znacznikami – przewodnik Aspose.Cells
url: /pl/net/smart-markers-dynamic-data/how-to-create-workbook-with-smart-markers-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć skoroszyt z inteligentnymi znacznikami – przewodnik Aspose.Cells

Zastanawiałeś się kiedyś, **jak utworzyć skoroszyt**, który automatycznie wypełnia dane z źródła JSON? Nie jesteś jedyny – programiści ciągle pytają, jak dodać znaczniki pobierające wartości z tablic, szczególnie przy pracy z Aspose.Cells. Dobra wiadomość? To całkiem proste, gdy zrozumiesz koncepcję inteligentnych znaczników. W tym samouczku przejdziemy przez tworzenie skoroszytu, dodawanie znaczników, użycie tablicy JSON oraz konfigurowanie inteligentnych znaczników w Aspose.Cells, abyś mógł generować pliki Excel w locie.

Omówimy wszystko, co musisz wiedzieć: inicjalizację skoroszytu, budowanie `MarkerCollection`, podawanie tablicy JSON, przełączanie flagi „ArrayAsSingle” oraz ostateczne zastosowanie znaczników. Po zakończeniu będziesz mieć w pełni działający program w C#, który tworzy plik Excel z wartościami **A**, **B** i **C** wstawionymi automatycznie. Bez zewnętrznych usług, tylko czysta magia Aspose.Cells.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa także z .NET Framework 4.6+)
- Pakiet NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- Podstawowa znajomość składni C# (jeśli dopiero zaczynasz, fragmenty kodu są obficie skomentowane)
- Visual Studio lub dowolne inne IDE

Jeśli już to masz, świetnie – przejdźmy do rzeczy.

## Krok 1: Jak utworzyć skoroszyt (Zainicjalizuj plik Excel)

Pierwszą rzeczą, której potrzebujesz, jest pusty obiekt workbook. Traktuj go jak czyste płótno, które Aspose.Cells później pomaluje danymi.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // reference to the default sheet
```

> **Dlaczego to ważne:** `Workbook` jest punktem wejścia dla każdej operacji w Excelu. Bez niego nie możesz dołączyć inteligentnych znaczników ani zapisać pliku. Utworzenie skoroszytu jako pierwszego zapewnia czyste środowisko dla kolejnych kroków.

## Krok 2: Jak dodać znaczniki – Zainicjalizuj kolekcję znaczników

Inteligentne znaczniki znajdują się wewnątrz `MarkerCollection`. To w tej kolekcji definiujesz miejsca wstawienia (znaczniki) oraz dane, które je zastąpią.

```csharp
        // Step 2: Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();
```

> **Porada:** Możesz używać tej samej `MarkerCollection` dla wielu arkuszy, ale trzymanie jednej kolekcji na arkusz ułatwia debugowanie.

## Krok 3: Użyj tablicy JSON – Dodaj znacznik z danymi JSON

Teraz faktycznie dodajemy znacznik. Symbol `{SmartMarker}` zostanie zastąpiony tablicą JSON, którą podamy. JSON musi być sformatowany jako ciąg znaków tablicy, np. `["A","B","C"]`.

```csharp
        // Step 3: Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");
```

> **Wyjaśnienie:** Metoda `Add` przyjmuje dwa argumenty: tekst znacznika oraz źródło danych. Tutaj źródłem danych jest tablica JSON, którą Aspose.Cells potrafi automatycznie sparsować. To jest sedno **use json array** z inteligentnymi znacznikami.

## Krok 4: Skonfiguruj znacznik – Traktuj tablicę jako pojedynczą wartość

Domyślnie Aspose.Cells rozwija tablicę JSON do osobnych wierszy. Jeśli chcesz, aby cała tablica była traktowana jako jedna wartość komórki (przydatne przy listach rozwijanych lub łańcuchach znaków), ustaw flagę `ArrayAsSingle`.

```csharp
        // Step 4: Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;
```

> **Kiedy używać:** Jeśli potrzebujesz, aby tablica pojawiła się w jednej komórce (np. `"A,B,C"`), włącz tę flagę. W przeciwnym razie Aspose.Cells zapisze każdy element w osobnym wierszu.

## Krok 5: Dołącz znaczniki do arkusza i zastosuj je

Na koniec podłącz kolekcję znaczników do arkusza i powiedz Aspose.Cells, aby zamienił symbole na rzeczywiste dane.

```csharp
        // Step 5: Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Optional: write the placeholder into a cell so you can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook to disk
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

> **Rezultat:** Po uruchomieniu programu, `SmartMarkerResult.xlsx` zawiera wartość **A** (lub całą tablicę, jeśli `ArrayAsSingle` jest ustawione na true) w komórce `A1`. Otwórz plik, aby to zweryfikować.

### Oczekiwany wynik

| A |
|---|
| A |   *(jeśli `ArrayAsSingle` jest false, pierwszy element wypełnia komórkę)*

Jeśli ustawisz `ArrayAsSingle = true`, komórka `A1` będzie zawierała ciąg `["A","B","C"]`.

## Krok 6: Jak dodać znaczniki – Scenariusze zaawansowane (Opcjonalnie)

Możesz się zastanawiać, *co jeśli potrzebuję więcej niż jednego znacznika?* Odpowiedź jest prosta: po prostu wywołaj ponownie `Add`.

```csharp
        smartMarkerCollection.Add("{SecondMarker}", "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]");
        // You can also control each marker individually:
        smartMarkerCollection["SecondMarker"] = false; // expand into rows
```

> **Dlaczego to działa:** Każdy znacznik działa niezależnie, więc możesz mieszać „array as single” i „expand into rows” w tym samym arkuszu. Ta elastyczność jest znakiem rozpoznawczym **smart markers aspose.cells**.

## Typowe pułapki i jak ich unikać

| Problem | Dlaczego się pojawia | Rozwiązanie |
|---------|----------------------|-------------|
| Znacznik nie został zamieniony | Brakujący lub błędny tekst placeholdera | Upewnij się, że komórka zawiera dokładny ciąg znacznika (`{SmartMarker}`) |
| JSON nie został sparsowany | Nieprawidłowa składnia JSON (brak cudzysłowów) | Użyj walidatora JSON lub podwójnie escapuj cudzysłowy w łańcuchach C# |
| Tablica rozwija się nieoczekiwanie | `ArrayAsSingle` pozostawione domyślnie `false` | Ustaw `["ArrayAsSingle"] = true` dla konkretnego znacznika |
| Skoroszyt zapisany pusty | `Apply()` nie wywołane przed `Save()` | Zawsze wywołuj `worksheet.SmartMarkers.Apply()` przed zapisem |

## Pełny działający przykład (Gotowy do skopiowania)

Poniżej znajduje się kompletny program, który możesz wkleić do aplikacji konsolowej. Nie są wymagane żadne dodatkowe pliki.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();

        // Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");

        // Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;

        // Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Place the marker in a cell so we can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

Uruchom program, otwórz `SmartMarkerResult.xlsx` i zobaczysz tablicę JSON (lub jej pierwszy element) ładnie umieszczony w komórce **A1**.

## Kolejne kroki: Rozszerzanie rozwiązania

Teraz, gdy wiesz **jak utworzyć skoroszyt**, **jak dodać znaczniki** i **jak używać tablicy JSON** z Aspose.Cells, rozważ następujące pomysły:

1. **Wiele arkuszy** – Przejdź pętlą po liście arkuszy i podłącz różne kolekcje znaczników do każdego z nich.
2. **Dynamiczny JSON** – Pobieraj JSON z API internetowego (`HttpClient`) i podawaj go bezpośrednio do `smartMarkerCollection.Add`.
3. **Stylizacja wyniku** – Po zastosowaniu znaczników, sformatuj komórki (czcionki, kolory), aby raport wyglądał profesjonalnie.
4. **Formaty eksportu** – Zapisz skoroszyt jako PDF, CSV lub HTML, zmieniając `workbook.Save("file.pdf")`.

Każdy z tych tematów naturalnie wykorzystuje **smart markers aspose.cells**, więc będziesz rozwijać te same podstawowe koncepcje, które właśnie poznałeś.

## Zakończenie

Przeszliśmy przez **jak utworzyć skoroszyt** od podstaw, **jak dodać znaczniki** oraz **jak używać tablicy JSON** z inteligentnymi znacznikami Aspose.Cells. Kompletny, gotowy do uruchomienia przykład demonstruje cały przepływ pracy, od inicjalizacji `Workbook` po zapis finalnego pliku. Dzięki przełączaniu flagi `ArrayAsSingle` zyskujesz precyzyjną kontrolę nad tym, jak dane JSON pojawiają się w Excelu, co czyni rozwiązanie elastycznym dla szerokiego zakresu scenariuszy raportowych.

Wypróbuj kod, zmodyfikuj JSON i eksperymentuj z dodatkowymi znacznikami. Gdy opanujesz te elementy budulcowe, generowanie zaawansowanych raportów Excel stanie się bułką z masłem. Masz pytania lub chcesz podzielić się ciekawym przypadkiem użycia? zostaw komentarz poniżej – powodzenia w kodowaniu! 

![Diagram pokazujący, jak utworzyć skoroszyt z inteligentnymi znacznikami w Aspose.Cells](https://example.com/images/create-workbook-smart-markers.png "jak utworzyć skoroszyt z inteligentnymi znacznikami Aspose.Cells")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}