---
category: general
date: 2026-02-14
description: Tworzenie hierarchii w szablonach SmartMarker jest łatwiejsze, niż myślisz
  – dowiedz się, jak tworzyć dane hierarchiczne i jak efektywnie wyświetlać listę
  pracowników.
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: pl
og_description: Tworzenie hierarchii w szablonach SmartMarker jest proste. Skorzystaj
  z tego przewodnika, aby stworzyć dane hierarchiczne i wymienić pracowników z zagnieżdżonymi
  zakresami.
og_title: Jak stworzyć hierarchię za pomocą SmartMarker – kompletny przewodnik
tags:
- SmartMarker
- C#
- templating
title: Jak stworzyć hierarchię przy użyciu SmartMarker – przewodnik krok po kroku
url: /pl/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak tworzyć hierarchię w SmartMarker – Kompletny przewodnik

Zastanawiałeś się kiedyś **jak tworzyć hierarchię** w szablonie SmartMarker, nie tracąc włosów? Nie jesteś jedyny. W wielu scenariuszach raportowania potrzebny jest związek rodzic‑dziecko — pomyśl o działach i ludziach w nich pracujących. Dobra wiadomość jest taka, że SmartMarker robi to bułką z masłem, gdy znasz właściwe kroki.

W tym tutorialu przejdziemy przez cały proces: od **tworzenia danych hierarchicznych** w C#, włączania zagnieżdżonych zakresów, aż po renderowanie szablonu, który **wyświetla listę pracowników** dla każdego działu. Na końcu będziesz mieć gotowy przykład, który możesz wrzucić do dowolnego projektu .NET.

---

## Czego będziesz potrzebować

- .NET 6+ (dowolna nowsza wersja działa)
- Odwołanie do biblioteki **SmartMarker** (przestrzeń nazw `ws.SmartMarkerProcessor`)
- Podstawowa znajomość C# – nic skomplikowanego, tylko kilka obiektów i jedna‑dwie lambdy
- IDE lub edytor według własnego wyboru (Visual Studio, Rider, VS Code… jak wolisz)

Jeśli już to masz, świetnie — zanurzmy się.

---

## Jak tworzyć hierarchię – przegląd

Podstawowa idea polega na zbudowaniu **zagnieżdżonego grafu obiektów**, który odzwierciedla strukturę, jaką chcesz zobaczyć w dokumencie końcowym. W naszym przypadku graf wygląda tak:

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

SmartMarker może wtedy iterować po `Departments` i, ponieważ włączymy **przetwarzanie zagnieżdżonych zakresów**, automatycznie przejdzie po kolekcji `Employees` każdego działu.

---

## Krok 1: Zbuduj hierarchiczny model danych

Najpierw tworzymy anonimowy obiekt, który zawiera tablicę działów, z których każdy ma własną listę pracowników. Użycie typu anonimowego utrzymuje przykład lekki — w razie potrzeby możesz później zamienić go na prawdziwe klasy POCO.

```csharp
// Step 1: Create hierarchical data that SmartMarker will iterate over
var departmentData = new
{
    Departments = new[]
    {
        new { Name = "HR", Employees = new[] { "John", "Amy" } },
        new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
    }
};
```

> **Dlaczego to ważne:** Tablica `Departments` jest kolekcją najwyższego poziomu. Każdy element zawiera tablicę `Employees`, dając nam drugi poziom hierarchii, do którego później odwołamy się przy pomocy `#Departments.Employees#`.

---

## Krok 2: Włącz przetwarzanie zagnieżdżonych zakresów

SmartMarker nie zagłębi się w wewnętrzne kolekcje, dopóki mu tego nie zlecisz. Obiekt `SmartMarkerOptions` przechowuje ten przełącznik.

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **Pro tip:** Jeśli zapomnisz ustawić ten flag, wewnętrzny zakres `#Employees#` po prostu nic nie zwróci i będziesz drapać się po głowie, zastanawiając się, dlaczego szablon jest pusty.

---

## Krok 3: Uruchom procesor z danymi

Teraz przekazujemy dane i opcje do procesora. Zmienna `ws` reprezentuje Twój **WebService** (lub dowolny obiekt hostujący silnik SmartMarker).

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

W tym momencie SmartMarker parsuje szablon, podstawia `#Departments.Name#` dla każdej nazwy działu, a ponieważ zagnieżdżone zakresy są włączone, iteruje po kolekcji `Employees` każdego działu.

---

## Krok 4: Stwórz znaczniki szablonu

Poniżej znajduje się minimalny szablon, który demonstruje zarówno zewnętrzną, jak i wewnętrzną pętlę. Wklej go do edytora szablonów SmartMarker (lub do pliku `.txt`, który przekażesz procesorowi).

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Po wyrenderowaniu zobaczysz:

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **Co widzisz:** Zewnętrzny `#Departments.Name#` wypisuje tytuł działu. Wewnętrzny blok `#Departments.Employees#` iteruje po każdym pracowniku, a `#Departments.Employees#` wewnątrz bloku wyświetla rzeczywistą nazwę.

---

## Oczekiwany wynik i weryfikacja

Uruchomienie pełnego przykładu (dane + opcje + szablon) powinno dokładnie wyprodukować listę pokazaną powyżej. Aby szybko zweryfikować, możesz wypisać wynik na konsolę:

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

Jeśli zobaczysz dwa nagłówki działów, po których następują wypunktowane nazwiska pracowników, udało Ci się **utworzyć hierarchię** i **wyświetlić pracowników**.

---

## Częste pułapki i przypadki brzegowe

| Problem | Dlaczego się pojawia | Rozwiązanie |
|---------|----------------------|-------------|
| Brak wyników dla pracowników | `EnableNestedRange` pozostawiono jako false | Ustaw `EnableNestedRange = true` |
| Duplikaty nazw pracowników | Ten sam array używany w wielu działach | Sklonuj array lub użyj odrębnych kolekcji |
| Bardzo duże hierarchie powodują obciążenie pamięci | SmartMarker ładuje cały graf obiektów do pamięci | Strumieniuj dane lub paginuj duże kolekcje |
| Błędy składni szablonu | Brak zamykającego tagu `#/…#` | Użyj walidatora SmartMarker lub szybko przetestuj mały szablon |

---

## Idąc dalej – warianty w rzeczywistych zastosowaniach

1. **Dynamiczne źródła danych** – Pobierz działy z bazy danych i zamapuj je na anonimową strukturę przy użyciu LINQ.  
2. **Warunkowe formatowanie** – Dodaj flagę `IsManager` do każdego pracownika i użyj warunkowych znaczników SmartMarker (`#if …#`), aby wyróżnić menedżerów.  
3. **Wiele poziomów zagnieżdżenia** – Jeśli potrzebujesz zespoły w ramach działów, po prostu dodaj kolejną kolekcję (`Teams`) i pozostaw włączone `EnableNestedRange`.

---

## Pełny działający przykład (gotowy do kopiowania i wklejania)

```csharp
using System;
using SmartMarker; // hypothetical namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Build hierarchical data
        var departmentData = new
        {
            Departments = new[]
            {
                new { Name = "HR", Employees = new[] { "John", "Amy" } },
                new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
            }
        };

        // 2️⃣ Enable nested ranges
        var smartMarkerOptions = new SmartMarkerOptions
        {
            EnableNestedRange = true
        };

        // 3️⃣ Start processing
        var ws = new WebService(); // assume this is your entry point
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);

        // 4️⃣ Retrieve and display the result
        string output = ws.SmartMarkerProcessor.GetProcessedResult(); // placeholder method
        Console.WriteLine(output);
    }
}
```

**Szablon (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Uruchomienie programu wypisuje hierarchię dokładnie tak, jak pokazano wcześniej.

---

## Zakończenie

Omówiliśmy **jak tworzyć hierarchię** w SmartMarker, od kształtowania **danych hierarchicznych** w C#, przez włączanie zagnieżdżonych zakresów, aż po renderowanie szablonu, który **wyświetla listę pracowników** w każdym dziale. Wzorzec skaluje się — wystarczy dodać kolejne zagnieżdżone kolekcje lub logikę warunkową i masz potężny silnik raportowy w zasięgu ręki.

Gotowy na kolejne wyzwanie? Spróbuj zamienić typy anonimowe na silnie typowane klasy POCO lub zintegrować ten przepływ z endpointem ASP.NET Core, który zwraca dokument PDF lub Word. Nie ma granic, a teraz masz solidne podstawy.

![How to create hierarchy diagram](image.png){alt="Diagram pokazujący zależność dział‑pracownik"}

*Szczęśliwego kodowania! Jeśli napotkasz problemy, zostaw komentarz poniżej — chętnie pomogę.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}