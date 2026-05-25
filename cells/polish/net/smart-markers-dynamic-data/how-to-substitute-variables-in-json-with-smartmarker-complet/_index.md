---
category: general
date: 2026-03-29
description: Jak podmienić zmienne w JSON przy użyciu SmartMarker – naucz się używać
  wyrażenia if, stosować logikę warunkową, mnożyć wartości i generować JSON bez wysiłku.
draft: false
keywords:
- how to substitute variables
- use if expression
- how to apply conditional
- how to multiply values
- how to generate json
language: pl
og_description: Jak podmienić zmienne w JSON przy użyciu SmartMarker. Dowiedz się,
  jak używać wyrażenia if, stosować logikę warunkową, mnożyć wartości i generować
  JSON w kilka minut.
og_title: Jak podmienić zmienne w JSON za pomocą SmartMarker – krok po kroku
tags:
- C#
- SmartMarker
- JSON templating
title: Jak zastąpić zmienne w JSON przy użyciu SmartMarker – kompletny przewodnik
url: /pl/net/smart-markers-dynamic-data/how-to-substitute-variables-in-json-with-smartmarker-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak podmienić zmienne w JSON przy użyciu SmartMarker – Kompletny przewodnik

Zastanawiałeś się kiedyś **jak podmienić zmienne** wewnątrz ładunku JSON bez pisania własnego parsera? Nie jesteś sam. W wielu scenariuszach integracji — myśl o fakturach, silnikach wyceny czy dynamicznych plikach konfiguracyjnych — musisz wstrzyknąć wartości w czasie wykonywania, zastosować proste warunki i być może wykonać szybkie mnożenie. Ten samouczek pokaże Ci dokładnie **jak podmienić zmienne** przy użyciu biblioteki SmartMarker, zachowując JSON czysty i czytelny.

Przejdziemy przez praktyczny przykład, który obejmuje **użycie wyrażenia if**, **jak zastosować warunek**, **jak mnożyć wartości** oraz **jak generować json** w locie. Na koniec będziesz mieć gotowy fragment C#, który możesz wkleić do dowolnego projektu .NET.

## Czego się nauczysz

- Skonfigurujesz `SmartMarkerOptions`, aby przechowywać wielokrotnie używane zmienne.  
- Napiszesz szablon JSON zawierający wyrażenie `if` dla logiki warunkowej.  
- Pomnożysz wartość przez zmienną wewnątrz szablonu.  
- Przetworzysz szablon przy użyciu `SmartMarkerProcessor` i otrzymasz końcowy ciąg JSON.  
- Rozwiążesz typowe problemy, takie jak brakujące zmienne czy niepoprawne wyrażenia.

Bez zewnętrznych usług, bez ciężkich zależności — tylko czysty C# i pakiet NuGet SmartMarker.

---

## Jak podmienić zmienne – przegląd krok po kroku

Poniżej znajduje się wysokopoziomowy schemat przepływu. Wyobraź sobie go jako potok, w którym surowy szablon JSON wchodzi po lewej, silnik SmartMarker wykonuje swoją magię, a w pełni wyrenderowany JSON wychodzi po prawej.

![Diagram showing how to substitute variables in JSON](https://example.com/images/smartmarker-flow.png "How to substitute variables in JSON")

*Tekst alternatywny obrazu: Diagram pokazujący, jak podmienić zmienne w JSON.*

---

## Krok 1: Zainstaluj i zaimportuj SmartMarker

Zanim zaczniesz, upewnij się, że pakiet SmartMarker jest dodany do Twojego projektu. Jeśli używasz .NET CLI, uruchom:

```bash
dotnet add package SmartMarker
```

Następnie dodaj niezbędne dyrektywy `using` na początku pliku C#:

```csharp
using SmartMarker;
using SmartMarker.Models;
using System;
```

> **Wskazówka:** Najnowsza wersja (stan na marzec 2026) to 2.4.1. Obsługuje .NET 6 i nowsze, ale działa także z .NET Framework 4.7.

---

## Krok 2: Utwórz opcje SmartMarker i zdefiniuj zmienne

Teraz stworzymy instancję `SmartMarkerOptions`, która będzie przechowywać wszystkie zmienne, które chcemy ponownie wykorzystać w szablonie. To właśnie tutaj odpowiadamy na pytanie **jak podmienić zmienne** — zmienne działają jako symbole zastępcze, które SmartMarker później zamieni.

```csharp
// Step 2: Create SmartMarker options to hold variables used in the template
var smartMarkerOptions = new SmartMarkerOptions();

// Define a variable (Rate) that we’ll reference later in the JSON expression
smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission rate
```

Dlaczego przechowujemy stawkę w `Variables`, a nie wpisujemy jej na stałe? Ponieważ możesz pobrać tę liczbę z bazy danych, pliku konfiguracyjnego lub wejścia użytkownika. Trzymanie jej w opcjach sprawia, że szablon jest wielokrotnego użytku i łatwy do testowania.

---

## Krok 3: Napisz szablon JSON z wyrażeniem `if`

Tutaj wkracza słowo kluczowe **use if expression**. SmartMarker pozwala osadzać logikę warunkową bezpośrednio w ciągu JSON. Składnia wygląda nieco jak nazwa właściwości, ale SmartMarker traktuje ją jako dyrektywę.

```csharp
// Step 3: Prepare the JSON data with a conditional field that uses the variable
string jsonTemplate = @"{
    ""Amount"": 1000,
    ""if(Amount>500)"": ""${Amount * Rate}""
}";
```

Zwróć uwagę na klucz `if(Amount>500)`. SmartMarker ocenia wyrażenie `Amount>500`; jeśli jest prawdziwe, odpowiadająca wartość (`${Amount * Rate}`) zostaje wstawiona do wyniku. Składnia `${...}` to silnik *podstawiania zmiennych* — tutaj **jak mnożyć wartości** (`Amount * Rate`) przed wstrzyknięciem wyniku.

---

## Krok 4: Przetwórz szablon i uzyskaj końcowy JSON

Mając gotowe opcje i szablon, przekazujemy wszystko procesorowi. Metoda `ProcessJson` parsuje szablon, stosuje warunek, wykonuje mnożenie i zwraca czysty ciąg JSON.

```csharp
// Step 4: Process the JSON with SmartMarker, applying the variable substitution
string resultJson = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(resultJson);
```

Uruchomienie fragmentu wypisuje:

```json
{
  "Amount": 1000,
  "Result": "80"
}
```

**Co się stało?**  
- `Amount` wynosi 1000, co spełnia warunek `Amount>500`.  
- SmartMarker ocenia `${Amount * Rate}` → `1000 * 0.08 = 80`.  
- Oryginalny warunkowy klucz (`if(Amount>500)`) zostaje zamieniony na czystą nazwę właściwości (`Result`). Domyślnie SmartMarker używa `"Result"`, ale możesz to zmienić (więcej niżej).

Jeśli zmienisz `Amount` na `400`, wynik będzie:

```json
{
  "Amount": 400
}
```

Blok warunkowy znika, ponieważ wyrażenie oceniło się jako `false`. To właśnie istota **jak zastosować warunek** w JSON.

---

## Krok 5: Dostosowanie nazwy właściwości wyjściowej (opcjonalnie)

Czasami nie chcesz używać ogólnego klucza `"Result"`. SmartMarker pozwala określić własną nazwę przy pomocy opcji `RenameIfExpression`:

```csharp
smartMarkerOptions.RenameIfExpression = "Discount";
string customResult = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(customResult);
```

Wynik:

```json
{
  "Amount": 1000,
  "Discount": "80"
}
```

Teraz wartość warunkowa jest zapisana pod bardziej znaczącą nazwą — idealną dla usług downstream, które oczekują konkretnego pola.

---

## Typowe pułapki i jak ich unikać

| Problem | Dlaczego się pojawia | Rozwiązanie |
|-------|----------------|-----|
| Variable not found | Odwołujesz się do zmiennej, której nie ma w `smartMarkerOptions.Variables`. | Sprawdź pisownię i upewnij się, że zmienna została dodana przed przetworzeniem. |
| Invalid `if` syntax | Brak nawiasów lub niepoprawny operator (`>`, `<`, `==`). | Trzymaj się dokładnego wzorca `if(<wyrażenie>)`; SmartMarker obsługuje tylko proste porównania liczbowe. |
| JSON becomes malformed | Przypadkowo pozostawiono przecinek po bloku warunkowym. | Pozwól SmartMarkerowi usunąć go; utrzymuj szablon w poprawnej składni. |
| Unexpected number format | Wynik pojawia się jako ciąg `"80"` zamiast liczby. | Rzutuj lub sparsuj później, albo użyj `${(Amount * Rate):N0}` dla formatowania liczbowego. |

---

## Pełny działający przykład (gotowy do kopiowania)

Poniżej znajduje się kompletny program, który możesz skompilować i uruchomić. Demonstruje **jak generować json** z dynamicznymi zmiennymi, warunkami i arytmetyką — wszystko w mniej niż 30 linijkach.

```csharp
using System;
using SmartMarker;
using SmartMarker.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Create SmartMarker options and define a reusable variable
        var smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission
        smartMarkerOptions.RenameIfExpression = "Discount"; // optional custom name

        // 2️⃣ JSON template with an if expression and multiplication
        string jsonTemplate = @"{
            ""Amount"": 1000,
            ""if(Amount>500)"": ""${Amount * Rate}""
        }";

        // 3️⃣ Process the template
        string output = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);

        // 4️⃣ Show the result
        Console.WriteLine("Generated JSON:");
        Console.WriteLine(output);
    }
}
```

**Oczekiwany wynik w konsoli**

```
Generated JSON:
{
  "Amount": 1000,
  "Discount": "80"
}
```

Śmiało zmieniaj `Amount`, aby przetestować gałąź warunkową, lub modyfikuj `Rate`, aby zobaczyć różne obliczenia rabatu.

---

## Rozszerzanie wzorca – kolejne scenariusze „Jak zrobić”

- **How to substitute variables** z pliku konfiguracyjnego: wczytaj `Dictionary<string, object>` z `appsettings.json` i przekaż go do `smartMarkerOptions.Variables`.  
- **How to use if expression** dla wielu warunków: łańcuchuj je tak: `"if(Amount>500 && CustomerType=='VIP')"` — SmartMarker obsługuje logiczne AND/OR.  
- **How to apply conditional** formatowanie: użyj `${Amount:0.00}` wewnątrz wyrażenia, aby kontrolować liczbę miejsc po przecinku.  
- **How to multiply values** z bardziej złożoną matematyką: `${(Amount - Discount) * TaxRate}` działa tak samo.  
- **How to generate json** dla zagnieżdżonych obiektów: umieść blok warunkowy wewnątrz innego obiektu JSON, a SmartMarker zachowa hierarchię.

---

## Zakończenie

Omówiliśmy **jak podmienić zmienne** w JSON przy użyciu SmartMarker, pokazaliśmy **use if expression** do warunkowego włączania, wyjaśniliśmy **jak zastosować warunek**, przedstawiliśmy **jak mnożyć wartości** w szablonie oraz zilustrowaliśmy **jak generować json** gotowy do dalszego przetwarzania. Podejście jest lekkie, nie wymaga zewnętrznego silnika szablonów i łatwo wpasowuje się w każdy kod C#.

Wypróbuj je — zmień zmienne, dodaj kolejne warunki lub opakuj całość w klasę pomocniczą do ponownego użycia w całym rozwiązaniu. Gdy potrzebujesz szybko wygenerować dynamiczny JSON, SmartMarker jest solidnym, gotowym do produkcji rozwiązaniem.

---

**Kolejne kroki**

- Zagłęb się w zaawansowane funkcje SmartMarker, takie jak pętle (`foreach`) i funkcje użytkownika.  
- Połącz tę technikę z endpointami ASP.NET Core, aby serwować dynamiczne API JSON.  
- Przejrzyj inne biblioteki szablonowe (np. Handlebars.NET) w celu porównania, szczególnie jeśli potrzebujesz bogatszej składni.

Masz pytania lub konkretny przypadek użycia, z którym się mierzysz? zostaw komentarz poniżej, a wspólnie znajdziemy rozwiązanie. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}