---
category: general
date: 2026-03-25
description: Jak tworzyć szablon przy użyciu Smart Markers oraz nauczyć się powtarzać
  wiersze, wiązać dane, generować raport i tworzyć szablon bez wysiłku.
draft: false
keywords:
- how to write template
- how to repeat rows
- how to bind data
- how to generate report
- how to create template
language: pl
og_description: Jak napisać szablon przy użyciu Smart Markers. Dowiedz się, jak powielać
  wiersze, wiązać dane, generować raport i tworzyć szablon w C#.
og_title: Jak napisać szablon z inteligentnymi znacznikami – pełny przewodnik
tags:
- Aspose.Cells
- C#
- SmartMarkers
title: Jak napisać szablon z inteligentnymi znacznikami – przewodnik krok po kroku
url: /pl/net/smart-markers-dynamic-data/how-to-write-template-with-smart-markers-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak napisać szablon z użyciem Smart Markers – Pełny poradnik  

Zastanawiałeś się kiedyś **jak napisać szablon**, który automatycznie rozszerza się w zależności od twoich danych? Nie jesteś sam — wielu programistów napotyka trudności, gdy potrzebują dynamicznego raportu Excel, ale nie wiedzą, której funkcji API użyć. Dobra wiadomość? Dzięki Aspose.Cells Smart Markers możesz stworzyć szablon w jednej komórce, powiązać dane hierarchiczne i pozwolić bibliotece powielać wiersze za Ciebie. W tym przewodniku omówimy także **jak powielać wiersze**, **jak powiązać dane** oraz **jak generować raport** bez ręcznego iterowania po arkuszach.

Pod koniec tego poradnika będziesz mieć kompletny, działający przykład, który pokazuje **jak stworzyć szablon** dla scenariuszy master‑detail, plus wskazówki dotyczące przypadków brzegowych i trików wydajnościowych. Nie potrzebujesz zewnętrznych dokumentów — wszystko, czego potrzebujesz, znajduje się tutaj.

---

## Co zbudujesz

Wygenerujemy skoroszyt Excel, który wyświetla zamówienia (master) i ich pozycje (detail). Szablon znajduje się w komórce **A1**, a Smart Markers rozszerzy go do ładnie sformatowanej tabeli. Końcowy arkusz będzie wyglądał tak:

```
Order1
   A
   B
Order2
   C
```

To klasyczny scenariusz „**jak generować raport**”, a kod działa z .NET 6+ i Aspose.Cells 23.x (lub nowszym).

---

## Wymagania wstępne

- .NET 6 SDK (lub dowolna aktualna wersja .NET)  
- Visual Studio 2022 lub VS Code  
- Aspose.Cells dla .NET (instalacja przez NuGet: `Install-Package Aspose.Cells`)  

Jeśli masz te elementy, jesteś gotowy do startu.

---

## Krok 1: Skonfiguruj projekt i dodaj Aspose.Cells  

```csharp
// Create a new console app (run this in a terminal)
// dotnet new console -n SmartMarkerDemo
// cd SmartMarkerDemo
// dotnet add package Aspose.Cells
```

```csharp
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new workbook with a single worksheet
            var workbook = new Workbook();
            var worksheet = workbook.Worksheets[0];
```

*Dlaczego to ważne*: Rozpoczęcie od nowego `Workbook` zapewnia czyste płótno. Obiekt `Worksheet` to miejsce, w którym umieścimy nasz szablon.

---

## Krok 2: Napisz szablon Smart Marker  

Szablon używa `${Master.Name}` dla tytułu zamówienia oraz `${Detail:Repeat}` do iteracji po każdej pozycji.

```csharp
            // Step 2: Define a Smart Marker template that repeats detail rows for each master record
            string smartMarkerTemplate = @"${Master.Name}
${Detail:Repeat}
   ${Detail.Item}
${/Detail}";
            
            // Write the template into cell A1
            worksheet.Cells["A1"].PutValue(smartMarkerTemplate);
```

> **Pro tip**: Trzymaj szablon w jednej komórce; Smart Markers automatycznie rozszerzy go na wiersze.  

*Jak to rozwiązuje problem*: Umieszczając blok powtarzania bezpośrednio w komórce, unikasz ręcznego wstawiania wierszy — Aspose zajmuje się tym za Ciebie.

---

## Krok 3: Zbuduj dane hierarchiczne pasujące do szablonu  

Nasze dane muszą odzwierciedlać strukturę szablonu: kolekcja `Master`, z której każda zawiera tablicę `Detail`.

```csharp
            // Step 3: Create hierarchical data matching the template structure
            var orderData = new
            {
                Master = new[]
                {
                    new
                    {
                        Name = "Order1",
                        Detail = new[]
                        {
                            new { Item = "A" },
                            new { Item = "B" }
                        }
                    },
                    new
                    {
                        Name = "Order2",
                        Detail = new[]
                        {
                            new { Item = "C" }
                        }
                    }
                }
            };
```

*Dlaczego wiążemy dane w ten sposób*: Smart Markers używają wiązania w stylu refleksji, więc nazwy właściwości muszą dokładnie odpowiadać placeholderom. To jest sedno **jak powiązać dane** dla dynamicznych raportów.

---

## Krok 4: Przetwórz szablon — pozwól Smart Markers wykonać ciężką pracę  

```csharp
            // Step 4: Process the Smart Markers – the template will be expanded using the data above
            worksheet.SmartMarkerProcessor.Process(orderData);
```

Po przetworzeniu arkusz będzie zawierał rozszerzone wiersze. Bez pętli, bez ręcznego zapisywania komórek.

---

## Krok 5: Zapisz skoroszyt  

```csharp
            // Save the result to an XLSX file
            workbook.Save("SmartMarkerReport.xlsx", SaveFormat.Xlsx);
            System.Console.WriteLine("Report generated: SmartMarkerReport.xlsx");
        }
    }
}
```

Otwórz wygenerowany plik i zobaczysz układ master‑detail dokładnie taki, jak opisano wcześniej. To **jak generować raport** jedną linią kodu przetwarzającego.

---

## Przegląd wizualny  

![Raport Excel wygenerowany przez Smart Markers – jak napisać szablon](/images/smart-marker-report.png "jak napisać szablon")

*Alt text*: "jak napisać szablon" — zrzut ekranu finalnego pliku Excel pokazujący powtarzające się wiersze dla każdego zamówienia.

---

## Szczegółowo: Dlaczego Smart Markers to przełom  

### Jak powielać wiersze bez pętli  

Tradycyjna automatyzacja Excel zmusza do obliczania ostatniego wiersza, wstawiania nowych wierszy i kopiowania stylów — wszystkie te czynności są podatne na błędy. Smart Markers zastępują to deklaratywnym blokiem `${Detail:Repeat}`. Silnik parsuje blok, klonuje wiersz dla każdego elementu w kolekcji i wstawia wartości. To podejście jest **jak powielać wiersze** efektywnie.

### Powiązanie złożonych obiektów  

Możesz powiązać zagnieżdżone obiekty, kolekcje lub nawet DataTables. Dopóki nazwy właściwości się zgadzają, procesor przejdzie po grafie obiektów. To istota **jak powiązać dane**: przekazujesz procesorowi zwykły obiekt CLR (lub anonimowy typ, jak w naszym przykładzie) i pozwalasz mu automatycznie mapować.

### Generowanie różnych formatów  

Choć nasz przykład zapisuje do XLSX, możesz zamienić `SaveFormat.Pdf` lub `SaveFormat.Csv` jedną linią zmiany. To szybka ścieżka do **jak generować raport** w wielu formatach bez modyfikacji szablonu.

### Ponowne użycie szablonu  

Jeśli potrzebujesz **jak stworzyć szablon** dla innych arkuszy, po prostu skopiuj zawartość komórki do innego arkusza lub przechowuj ją w zasobie string. To samo wywołanie procesora działa wszędzie, co sprawia, że kod jest DRY i łatwy w utrzymaniu.

---

## Częste pytania i przypadki brzegowe  

| Pytanie | Odpowiedź |
|----------|--------|
| *Co jeśli master nie ma wierszy szczegółowych?* | Blok `${Detail:Repeat}` zostanie pominięty, pozostawiając tylko nazwę mastera. Nie zostaną utworzone puste wiersze. |
| *Czy mogę stylizować powtarzane wiersze?* | Tak — zastosuj formatowanie do wiersza szablonu (czcionka, obramowania itp.) przed przetworzeniem. Styl zostanie skopiowany do każdego wygenerowanego wiersza. |
| *Czy muszę zwolnić zasoby workbook?* | `Workbook` implementuje `IDisposable`. Owiń go w blok `using` w kodzie produkcyjnym, ale w krótkiej demonstracji konsolowej jest to opcjonalne. |
| *Jak duże mogą być dane?* | Smart Markers są efektywne pamięciowo, ale bardzo duże kolekcje (setki tysięcy) mogą wymagać stronicowania lub strumieniowania. |
| *Czy mogę użyć pliku JSON zamiast obiektu?* | Oczywiście — zdeserializuj JSON do POCO pasującego do szablonu, a następnie przekaż go do `Process`. |

---

## Pełny działający przykład (gotowy do kopiowania i wklejania)

```csharp
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize workbook
            var workbook = new Workbook();
            var worksheet = workbook.Worksheets[0];

            // Define template
            string smartMarkerTemplate = @"${Master.Name}
${Detail:Repeat}
   ${Detail.Item}
${/Detail}";

            worksheet.Cells["A1"].PutValue(smartMarkerTemplate);

            // Prepare data
            var orderData = new
            {
                Master = new[]
                {
                    new
                    {
                        Name = "Order1",
                        Detail = new[]
                        {
                            new { Item = "A" },
                            new { Item = "B" }
                        }
                    },
                    new
                    {
                        Name = "Order2",
                        Detail = new[]
                        {
                            new { Item = "C" }
                        }
                    }
                }
            };

            // Process template
            worksheet.SmartMarkerProcessor.Process(orderData);

            // Save file
            workbook.Save("SmartMarkerReport.xlsx", SaveFormat.Xlsx);
            System.Console.WriteLine("Report generated: SmartMarkerReport.xlsx");
        }
    }
}
```

Uruchom program (`dotnet run`) i otwórz *SmartMarkerReport.xlsx* — zobaczysz wiersze master‑detail ładnie ułożone.

---

## Podsumowanie  

Odpowiedzieliśmy na **jak napisać szablon** przy użyciu Aspose.Cells Smart Markers, pokazaliśmy **jak powielać wiersze**, przedstawiliśmy **jak powiązać dane** z obiektami hierarchicznymi oraz zilustrowaliśmy **jak generować raport** w formacie XLSX (lub innym obsługiwanym formacie). Ten sam wzorzec pozwala **jak stworzyć szablon** dla faktur, inwentaryzacji lub dowolnego układu master‑detail, jaki możesz sobie wyobrazić.

---

## Co dalej?  

- **Stylizuj wynik**: zastosuj style komórek do wiersza szablonu przed przetworzeniem.  
- **Eksportuj do PDF**: zmień `SaveFormat.Xlsx` na `SaveFormat.Pdf`, aby uzyskać raport do druku.  
- **Dynamiczne nagłówki**: dodaj placeholdery `${Headers}`, aby generować tytuły kolumn w locie.  
- **Wiele arkuszy**: powtórz proces na dodatkowych arkuszach dla raportów wielosekcyjnych.  

Śmiało eksperymentuj — zamień źródło danych, dodaj więcej zagnieżdżonych poziomów lub połącz z formułami. Elastyczność Smart Markers oznacza, że spędzasz mniej czasu na kodowaniu pętli, a więcej na dostarczaniu wartości.

*Miłego kodowania! Jeśli napotkasz problemy, zostaw komentarz poniżej lub napisz do mnie na Stack Overflow z tagiem `aspose-cells`. Kontynuujmy dyskusję.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}