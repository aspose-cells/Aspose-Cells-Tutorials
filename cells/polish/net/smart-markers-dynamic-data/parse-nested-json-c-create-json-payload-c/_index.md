---
category: general
date: 2026-02-15
description: Parsuj zagnieżdżony JSON w C# przy użyciu SmartMarkers i dowiedz się,
  jak tworzyć ładunek JSON w C# dla złożonych zamówień. Przewodnik krok po kroku z
  pełnym kodem i wyjaśnieniami.
draft: false
keywords:
- parse nested json c#
- create json payload c#
language: pl
og_description: Natychmiast parsuj zagnieżdżone JSON w C#. Dowiedz się, jak tworzyć
  ładunek JSON w C# i przetwarzać go za pomocą SmartMarkers w pełnym, gotowym do uruchomienia
  przykładzie.
og_title: Parsowanie zagnieżdżonego JSON w C# – Tworzenie ładunku JSON w C#
tags:
- json
- csharp
- smartmarkers
title: Parsowanie zagnieżdżonego JSON w C# – Tworzenie ładunku JSON w C#
url: /pl/net/smart-markers-dynamic-data/parse-nested-json-c-create-json-payload-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Parsowanie zagnieżdżonego JSON w C# – Tworzenie ładunku JSON w C#

Kiedykolwiek potrzebowałeś **parse nested JSON C#**, ale nie wiedziałeś, od czego zacząć? Nie jesteś sam — wielu programistów napotyka trudności, gdy ich dane zawierają tablice wewnątrz obiektów. Dobrą wiadomością jest to, że kilkoma liniami kodu możesz zarówno **create JSON payload C#**, jak i pozwolić SmartMarkers przejść przez zagnieżdżoną strukturę za Ciebie.

W tym samouczku zbudujemy ciąg JSON reprezentujący zamówienia z pozycjami, włączymy procesor SmartMarkers, aby rozumiał zagnieżdżone zakresy, i w końcu zweryfikujemy, że dane zostały poprawnie sparsowane. Na końcu będziesz mieć samodzielny, gotowy do skopiowania program, który możesz dostosować do dowolnego hierarchicznego JSON, z którym się spotkasz.

## Czego będziesz potrzebować  

- .NET 6 lub nowszy (kod kompiluje się również z .NET Core 3.1)  
- Odwołanie do biblioteki SmartMarkers (lub dowolnego podobnego procesora obsługującego zagnieżdżone zakresy)  
- Podstawowa znajomość C# — nic egzotycznego, tylko standardowe instrukcje `using` i metoda `Main`  

To wszystko. Nie potrzebujesz dodatkowych pakietów NuGet poza biblioteką markerów i nie wymaga to zewnętrznych usług.

## Krok 1: Tworzenie ładunku JSON w C# — Budowanie danych  

Najpierw tworzymy ciąg JSON, który zawiera tablicę zamówień, a każde zamówienie posiada własną tablicę `Lines`. Traktuj to jako miniaturowy migawkę zarządzania zamówieniami.

```csharp
using System;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // STEP 1 – Define the JSON payload with nested arrays
            // -------------------------------------------------
            string ordersJson = @"{
                ""Orders"": [
                    {
                        ""Id"": 1,
                        ""Lines"": [
                            { ""Prod"": ""A"" },
                            { ""Prod"": ""B"" }
                        ]
                    },
                    {
                        ""Id"": 2,
                        ""Lines"": [
                            { ""Prod"": ""C"" }
                        ]
                    }
                ]
            }";

            // The rest of the steps follow…
```

Dlaczego tworzyć ładunek jako dosłowny ciąg znaków? Zachowuje on podziały wierszy i pozwala zobaczyć strukturę na pierwszy rzut oka — przydatne podczas debugowania zagnieżdżonego JSON.

> **Pro tip:** Jeśli Twój JSON pochodzi z bazy danych lub API, możesz zamienić literał na `File.ReadAllText` lub żądanie sieciowe — nic w tym samouczku nie zależy od źródła.

## Krok 2: Włączenie zagnieżdżonych zakresów za pomocą SmartMarkerOptions  

SmartMarkers potrzebuje małego impulsu, aby zrozumieć, że tablica może zawierać inną tablicę. Właśnie to robi `EnableNestedRanges`.

```csharp
            // -------------------------------------------------
            // STEP 2 – Configure SmartMarker options for nesting
            // -------------------------------------------------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                EnableNestedRanges = true   // <-- crucial for Orders → Lines
            };
```

Ustawienie `EnableNestedRanges` na `true` informuje procesor, aby traktował każdą kolekcję `Lines` jako podzakres swojego nadrzędnego zakresu `Orders`. Bez tego flagi wewnętrzna pętla byłaby pomijana i widziałbyś tylko obiekty najwyższego poziomu.

## Krok 3: Przetwarzanie JSON za pomocą SmartMarkersProcessor  

Teraz przekazujemy ciąg JSON oraz opcje do procesora. Wywołanie jest synchroniczne i nie zwraca nic — SmartMarkers zapisuje wyniki w wewnętrznym kontekście, który możesz później pobrać.

```csharp
            // -------------------------------------------------
            // STEP 3 – Run the processor on the JSON payload
            // -------------------------------------------------
            ws.SmartMarkersProcessor.Process(ordersJson, options);
```

Jeśli używasz innej biblioteki, zamień `ws.SmartMarkersProcessor.Process` na odpowiednią nazwę metody; zasada pozostaje ta sama — przekaż JSON i konfigurację, która włącza obsługę zagnieżdżonych struktur.

## Krok 4: Weryfikacja sparsowanego wyniku  

Po przetworzeniu zazwyczaj chcesz potwierdzić, że każde zamówienie i jego pozycje zostały odwiedzone. Poniżej znajduje się prosty sposób na wypisanie danych z powrotem do konsoli przy użyciu hipotetycznej metody `GetProcessedData` (zastąp ją rzeczywistym dostępem w Twojej bibliotece).

```csharp
            // -------------------------------------------------
            // STEP 4 – Output the parsed structure (demo purpose)
            // -------------------------------------------------
            var result = ws.SmartMarkersProcessor.GetProcessedData(); // pseudo‑code
            Console.WriteLine("=== Parsed Orders ===");
            foreach (var order in result.Orders)
            {
                Console.WriteLine($"Order Id: {order.Id}");
                foreach (var line in order.Lines)
                {
                    Console.WriteLine($"  - Product: {line.Prod}");
                }
            }
        }
    }
}
```

**Oczekiwany wynik w konsoli**

```
=== Parsed Orders ===
Order Id: 1
  - Product: A
  - Product: B
Order Id: 2
  - Product: C
```

Widząc odtworzoną hierarchię, potwierdzasz, że **parse nested json c#** działało zgodnie z zamierzeniami.

## Krok 5: Przypadki brzegowe i typowe pułapki  

### Puste kolekcje  
Jeśli zamówienie nie ma `Lines`, procesor i tak utworzy pusty zakres. Upewnij się, że Twój dalszy kod potrafi obsłużyć pustą listę bez rzucania `NullReferenceException`.

### Głęboko zagnieżdżone struktury  
`EnableNestedRanges` działa od razu dla zagnieżdżenia dwupoziomowego. Dla trzech lub więcej poziomów może być konieczne ustawienie `MaxNestedDepth` (jeśli biblioteka go udostępnia) lub rekurencyjne wywoływanie procesora na każdym pod‑obiekcie.

### Znaki specjalne  
Ciągi JSON zawierające cudzysłowy, ukośniki lub Unicode wymagają odpowiedniego escapowania. Użycie dosłownego ciągu (`@""`) jak w naszym przykładzie omija większość problemów, ale jeśli tworzysz JSON programowo, pozwól `System.Text.Json.JsonSerializer` zająć się escapowaniem.

### Wydajność  
Parsowanie dużych ładunków (megabajty) może być intensywne pod względem pamięci. Rozważ strumieniowanie JSON przy użyciu `Utf8JsonReader` i przekazywanie fragmentów do procesora, jeśli napotkasz wąskie gardła wydajności.

## Przegląd wizualny  

![Diagram illustrating how parse nested json c# flows through SmartMarkers processing](parse-nested-json-csharp-diagram.png "parse nested json c# diagram")

Obrazek pokazuje przebieg od surowego JSON → SmartMarkerOptions → Processor → Sparowany model obiektowy.

## Podsumowanie  

Przeszliśmy przez kompletny przykład **parse nested json c#**, od **create json payload c#** po weryfikację zagnieżdżonych danych po przetworzeniu. Najważniejsze wnioski to:

1. Zbuduj dobrze ustrukturyzowany ciąg JSON odzwierciedlający Twoje obiekty domenowe.  
2. Włącz `EnableNestedRanges` (lub jego odpowiednik), aby parser respektował wewnętrzne tablice.  
3. Uruchom procesor i sprawdź wynik, aby upewnić się, że każdy poziom został odwiedzony.  

## Co dalej?  

- **Dynamic payloads:** Zastąp sztywno zakodowany ciąg obiektami serializowanymi przy użyciu `System.Text.Json`.  
- **Custom markers:** Rozszerz SmartMarkers o własne znaczniki, aby wstawiać wyliczone pola do każdej pozycji.  
- **Error handling:** Otocz wywołanie `Process` blokiem try/catch i loguj szczegóły `SmartMarkerException` w celu rozwiązywania problemów.  

Śmiało eksperymentuj — zamień tablicę `Orders` na klientów, faktury lub dowolne hierarchiczne dane, które musisz **parse nested json c#**. Wzorzec pozostaje ten sam.

Miłego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}