---
category: general
date: 2026-02-14
description: 'Zautomatyzuj generowanie faktur za pomocą SmartMarker: dowiedz się,
  jak powielać arkusze, nadawać im dynamiczne nazwy i opanować dynamiczne nazewnictwo
  arkuszy w kilka minut.'
draft: false
keywords:
- automate invoice generation
- how to name worksheets
- how to repeat worksheet
- dynamic worksheet naming
language: pl
og_description: Zautomatyzuj generowanie faktur za pomocą SmartMarker. Ten przewodnik
  pokazuje, jak powielać arkusze, nadawać im dynamiczne nazwy i opanować dynamiczne
  nazewnictwo arkuszy.
og_title: Automatyzacja generowania faktur – dynamiczne nazewnictwo arkuszy i powtarzanie
tags:
- C#
- SmartMarker
- Excel Automation
title: Automatyzacja generowania faktur – dynamiczne nazewnictwo arkuszy i powtarzanie
  w C#
url: /pl/net/smart-markers-dynamic-data/automate-invoice-generation-dynamic-worksheet-naming-repeati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Automatyzacja generowania faktur – dynamiczne nazewnictwo arkuszy i powielanie w C#

Zastanawiałeś się kiedyś, jak **zautomatyzować generowanie faktur** bez ręcznego kopiowania arkuszy dla każdego zamówienia? Nie jesteś sam. Wielu programistów napotyka problem, gdy potrzebny jest oddzielny arkusz dla każdej faktury, a jednocześnie nazwa arkusza ma odzwierciedlać numer zamówienia. W tym samouczku rozwiążemy ten problem, wykorzystując `SmartMarkerProcessor` z SmartMarker i pokażemy, **jak dynamicznie nazwać arkusze**, a także **jak powielać arkusz** dla każdego rekordu. Po zakończeniu będziesz mieć gotowy do uruchomienia przykład w C#, który tworzy skoroszyt, w którym każda faktura znajduje się na własnej, ładnie nazwanej karcie.

Przejdziemy przez każdy krok — od pobierania zamówień ze źródła danych po konfigurację `SmartMarkerOptions` dla dynamicznego nazewnictwa arkuszy. Nie potrzebujesz zewnętrznej dokumentacji; wszystko, co jest potrzebne, znajduje się tutaj. Wystarczy podstawowa znajomość C# oraz odniesienie do biblioteki Aspose.Cells (lub dowolnego silnika kompatybilnego ze SmartMarker).

---

## Co zbudujesz

- Pobierzesz kolekcję obiektów zamówień.
- Skonfigurujesz SmartMarker, aby **powielał arkusz** dla każdego zamówienia.
- Zastosujesz **dynamiczne nazewnictwo arkuszy** przy użyciu placeholdera `{OrderId}`.
- Wygenerujesz plik Excel, w którym każda karta ma nazwę `Invoice_12345`, `Invoice_67890` itd.
- Zweryfikujesz wynik, otwierając skoroszyt.

---

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod kompiluje się również z .NET 5+).
- Aspose.Cells for .NET (lub dowolna biblioteka implementująca SmartMarker). Zainstaluj przez NuGet:

```bash
dotnet add package Aspose.Cells
```

- Podstawowa klasa `Order` (możesz ją zastąpić własnym DTO).

---

## Krok 1: Utworzenie projektu i modelu

Najpierw utwórz nową aplikację konsolową i zdefiniuj model danych reprezentujący zamówienie.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    // Simple POCO representing an order – replace fields as needed
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }
    }

    class Program
    {
        static void Main()
        {
            // Retrieve orders (in real life this could be a DB call)
            var orders = GetOrders();

            // The rest of the tutorial continues here...
        }

        // Mock method – in production pull from EF Core, Dapper, etc.
        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

> **Pro tip:** Trzymaj model lekki na potrzeby demonstracji; zawsze możesz później dodać pozycje zamówienia, szczegóły podatkowe itp.

---

## Krok 2: Przygotowanie szablonu Excel

SmartMarker działa na bazie szablonu skoroszytu. Utwórz plik o nazwie `InvoiceTemplate.xlsx` z jednym arkuszem nazwanym `InvoiceTemplate`. W komórce **A1** umieść placeholder SmartMarker, np.:

```
{{OrderId}} – {{Customer}} – {{Date}} – ${{Total}}
```

Możesz sformatować komórki dowolnie — pogrubione nagłówki, formatowanie walutowe itp. Zapisz plik w katalogu głównym projektu.

> **Dlaczego szablon?** Oddziela układ od kodu, pozwalając projektantom modyfikować wygląd bez ingerencji w logikę.

---

## Krok 3: Konfiguracja opcji SmartMarker – powielanie i nazewnictwo arkuszy

Teraz poinstruujemy SmartMarker, aby *powielał* szablonowy arkusz dla każdego zamówienia i nadawał każdej kopii nazwę zawierającą identyfikator zamówienia. To jest sedno **dynamicznego nazewnictwa arkuszy**.

```csharp
// Inside Main() after retrieving orders
// Load the template workbook
Workbook wb = new Workbook("InvoiceTemplate.xlsx");

// Set up SmartMarker options
var smartMarkerOptions = new SmartMarkerOptions
{
    // Instructs SmartMarker to create a new worksheet per data item
    RepeatWorksheet = true,

    // Naming pattern – {OrderId} will be replaced with the actual value
    RepeatWorksheetName = "Invoice_{OrderId}"
};

// Run the processor
wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

// Save the result
string outputPath = "GeneratedInvoices.xlsx";
wb.Save(outputPath);

Console.WriteLine($"✅ Invoices generated: {outputPath}");
```

### Jak to działa

- **`RepeatWorksheet = true`** mówi silnikowi, aby duplikował arkusz źródłowy dla każdego elementu w kolekcji `orders`. To spełnia wymaganie **jak powielać arkusz**.
- **`RepeatWorksheetName = "Invoice_{OrderId}"`** to szablonowa nazwa, w której `{OrderId}` jest placeholderem, który SmartMarker zastępuje bieżącym identyfikatorem zamówienia. To odpowiedź na **jak nazwać arkusze** oraz **dynamiczne nazewnictwo arkuszy**.
- Procesor scala pola każdego zamówienia (`{{OrderId}}`, `{{Customer}}` itp.) z duplikowanym arkuszem, tworząc w pełni wypełnioną fakturę.

---

## Krok 4: Uruchomienie aplikacji i weryfikacja wyniku

Skompiluj i uruchom aplikację konsolową:

```bash
dotnet run
```

Powinieneś zobaczyć komunikat o sukcesie w konsoli. Otwórz `GeneratedInvoices.xlsx` i znajdziesz trzy karty:

- **Invoice_1001**
- **Invoice_1002**
- **Invoice_1003**

Każdy arkusz zawiera dane zamówienia wstawione w miejsce placeholderów. Układ zaprojektowany w szablonie jest zachowany, co dowodzi, że **automatyzacja generowania faktur** działa od początku do końca.

### Oczekiwany zrzut ekranu (tekst alternatywny dla SEO)

![przykład automatyzacji generowania faktur pokazujący trzy dynamicznie nazwane arkusze](/images/invoice-automation.png)

> *Tekst alternatywny obrazu zawiera główne słowo kluczowe, aby spełnić wymagania SEO.*

---

## Krok 5: Przypadki brzegowe i typowe wariacje

### Co zrobić, gdy OrderId zawiera niedozwolone znaki?

Nazwy arkuszy w Excelu nie mogą zawierać `\ / ? * [ ] :`. Jeśli Twoje identyfikatory mogą je zawierać, oczyść je:

```csharp
RepeatWorksheetName = "Invoice_{SanitizedOrderId}"
```

Dodaj właściwość obliczaną do klasy `Order`:

```csharp
public string SanitizedOrderId => OrderId.ToString().Replace("/", "-").Replace("\\", "-");
```

### Czy trzeba zachować oryginalny arkusz szablonu?

Ustaw `smartMarkerOptions.RemoveTemplate = false;` (domyślnie `true`). Dzięki temu oryginalny `InvoiceTemplate` pozostanie niezmieniony jako odniesienie.

### Czy można grupować faktury według klienta?

Możesz zagnieździć **grupy powielania**. Najpierw powielaj według klienta, a potem zamówienia w obrębie każdego arkusza klienta. Składnia staje się nieco bardziej złożona, ale zasada pozostaje ta sama — użyj `RepeatWorksheet` i wzoru nazwy odzwierciedlającego hierarchię.

---

## Pełny działający przykład (wszystkie kody w jednym miejscu)

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }

        // Helper for safe sheet names
        public string SanitizedOrderId => OrderId.ToString();
    }

    class Program
    {
        static void Main()
        {
            var orders = GetOrders();

            // Load template
            Workbook wb = new Workbook("InvoiceTemplate.xlsx");

            // Configure SmartMarker for repeating and naming worksheets
            var smartMarkerOptions = new SmartMarkerOptions
            {
                RepeatWorksheet = true,
                RepeatWorksheetName = "Invoice_{OrderId}" // dynamic worksheet naming
                // RemoveTemplate = true; // default behavior
            };

            // Process the data
            wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

            // Save the final workbook
            string outputPath = "GeneratedInvoices.xlsx";
            wb.Save(outputPath);

            Console.WriteLine($"✅ Invoices generated: {outputPath}");
        }

        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

Skopiuj‑wklej to do `Program.cs`, umieść `InvoiceTemplate.xlsx` obok i jesteś gotowy do działania.

---

## Najczęściej zadawane pytania

**P: Czy to rozwiązanie działa przy dużych zestawach danych (tysiące faktur)?**  
O: Tak. SmartMarker strumieniuje dane efektywnie, ale monitoruj zużycie pamięci. Jeśli napotkasz limity, rozważ przetwarzanie w partiach i zapisywanie każdej partii do osobnego skoroszytu.

**P: Czy mogę automatycznie dodać logo do każdej faktury?**  
O: Oczywiście. Umieść obraz logo w szablonie arkusza. Ponieważ arkusz jest duplikowany, logo pojawi się w każdej wygenerowanej fakturze bez dodatkowego kodu.

**P: Co zrobić, jeśli muszę zabezpieczyć arkusze?**  
O: Po przetworzeniu przeiteruj `wb.Worksheets` i wywołaj `ws.Protect(Password, ProtectionType.All)`.

---

## Podsumowanie

Właśnie **zautomatyzowaliśmy generowanie faktur**, wykorzystując funkcję powielania arkuszy SmartMarker oraz sprytny wzorzec nazewnictwa. Samouczek obejmował **jak nazwać arkusze**, pokazał **jak powielać arkusz** dla każdego zamówienia oraz zaprezentował **dynamiczne nazewnictwo arkuszy**, które utrzymuje Twój skoroszyt przejrzysty i łatwy do przeszukiwania.  

Od pobierania danych, przez przygotowanie szablonu, konfigurację `SmartMarkerOptions`, po obsługę przypadków brzegowych — masz teraz kompletną, gotową do uruchomienia implementację. Następnie spróbuj dodać tabele pozycji, zastosować formatowanie warunkowe lub wyeksportować te same dane do PDF, aby uzyskać w pełni zautomatyzowany proces rozliczeniowy.

Gotowy na kolejny poziom? Zapoznaj się z powiązanymi tematami, takimi jak „masowy eksport Excel z Aspose.Cells”, „konwersja arkuszy do PDF” czy „wysyłanie wygenerowanych faktur e‑mailem bezpośrednio z C#”. Nie ma granic — powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}