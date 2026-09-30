---
category: general
date: 2026-02-14
description: 'Automatizujte generování faktur pomocí SmartMarker: naučte se opakovat
  listy, pojmenovávat je dynamicky a ovládněte dynamické pojmenovávání listů během
  několika minut.'
draft: false
keywords:
- automate invoice generation
- how to name worksheets
- how to repeat worksheet
- dynamic worksheet naming
language: cs
og_description: Automatizujte generování faktur pomocí SmartMarkeru. Tento průvodce
  ukazuje, jak opakovat listy, pojmenovávat je dynamicky a ovládat dynamické pojmenování
  listů.
og_title: Automatizujte generování faktur – dynamické pojmenování listů a opakování
tags:
- C#
- SmartMarker
- Excel Automation
title: Automatizace generování faktur – Dynamické pojmenování listů a opakování v
  C#
url: /cs/net/smart-markers-dynamic-data/automate-invoice-generation-dynamic-worksheet-naming-repeati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Automatizace generování faktur – Dynamické pojmenování listů a opakování v C#

Už jste se někdy zamýšleli, jak **automatizovat generování faktur** bez ručního kopírování listů pro každou objednávku? Nejste v tom sami. Mnoho vývojářů narazí na problém, když potřebují samostatný list pro každou fakturu, ale zároveň chtějí, aby název listu odrážel číslo objednávky. V tomto tutoriálu vyřešíme tento problém pomocí `SmartMarkerProcessor` ze SmartMarker a ukážeme vám **jak dynamicky pojmenovávat listy** a zároveň pokryjeme **jak opakovat list** pro každý záznam. Na konci budete mít připravený C# příklad, který vytvoří sešit, kde každá faktura má svůj vlastní, pěkně pojmenovaný list.

Provedeme vás každým krokem – od načtení objednávek z datového zdroje po konfiguraci `SmartMarkerOptions` pro dynamické pojmenování listů. Nepotřebujete žádnou externí dokumentaci; vše, co potřebujete, je zde. Stačí základní znalost C# a reference na knihovnu Aspose.Cells (nebo jakýkoli engine kompatibilní se SmartMarker).

---

## Co vytvoříte

- Načíst kolekci objektů objednávek.
- Nastavit SmartMarker tak, aby **opakoval list** pro každou objednávku.
- Použít **dynamické pojmenování listů** pomocí zástupného symbolu `{OrderId}`.
- Vygenerovat soubor Excel, kde je každý list pojmenován `Invoice_12345`, `Invoice_67890` atd.
- Ověřit výstup otevřením sešitu.

## Předpoklady

- .NET 6.0 nebo novější (kód se také kompiluje s .NET 5+).
- Aspose.Cells pro .NET (nebo jakákoli knihovna implementující SmartMarker). Nainstalujte přes NuGet:

```bash
dotnet add package Aspose.Cells
```

- Základní třída `Order` (můžete ji nahradit vlastním DTO).

## Krok 1: Nastavení projektu a modelu

Nejprve vytvořte novou konzolovou aplikaci a definujte datový model, který představuje objednávku.

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

> **Tip:** Udržujte model pro demonstraci jednoduchý; můžete jej později rozšířit o položky, daňové detaily atd.

## Krok 2: Připravte Excel šablonu

SmartMarker pracuje s šablonovým sešitem. Vytvořte soubor s názvem `InvoiceTemplate.xlsx` s jediným listem pojmenovaným `InvoiceTemplate`. Do buňky **A1** vložte SmartMarker zástupný symbol, například:

```
{{OrderId}} – {{Customer}} – {{Date}} – ${{Total}}
```

Buňky můžete formátovat podle libosti – tučné záhlaví, formát měny atd. Uložte soubor do kořenové složky projektu.

> **Proč šablona?** Odděluje rozvržení od kódu, umožňuje designérům upravit vzhled bez zásahu do logiky.

## Krok 3: Konfigurace SmartMarker možností – Opakování a pojmenování listů

Nyní řekneme SmartMarkeru, aby *opakoval* šablonový list pro každou objednávku a aby každé kopii dal název obsahující ID objednávky. Toto je jádro **dynamického pojmenování listů**.

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

### Jak to funguje

- **`RepeatWorksheet = true`** říká enginu, aby duplikoval zdrojový list pro každý prvek v kolekci `orders`. Tím se splňuje požadavek **jak opakovat list**.
- **`RepeatWorksheetName = "Invoice_{OrderId}"`** je šablonový řetězec, kde `{OrderId}` je zástupný symbol, který SmartMarker nahradí aktuálním ID objednávky. To je odpověď na **jak pojmenovat listy** a **dynamické pojmenování listů**.
- Procesor sloučí pole každé objednávky (`{{OrderId}}`, `{{Customer}}` atd.) do duplikovaného listu a vytvoří plně vyplněnou fakturu.

## Krok 4: Spusťte aplikaci a ověřte výstup

Kompilujte a spusťte konzolovou aplikaci:

```bash
dotnet run
```

V konzoli by se měla zobrazit zpráva o úspěchu. Otevřete `GeneratedInvoices.xlsx` a najdete tři listy:

- **Invoice_1001**
- **Invoice_1002**
- **Invoice_1003**

Každý list obsahuje data objednávky dosazená do zástupných symbolů. Rozvržení, které jste navrhli v šabloně, je zachováno, což dokazuje, že **automatizace generování faktur** funguje od začátku do konce.

### Očekávaný snímek obrazovky (alt text pro SEO)

![příklad automatizace generování faktur ukazující tři dynamicky pojmenované listy](/images/invoice-automation.png)

> *Alt text obrázku obsahuje hlavní klíčové slovo pro SEO.*

## Krok 5: Okrajové případy a běžné varianty

### Co když OrderId obsahuje nelegální znaky?

Excel názvy listů nemohou obsahovat `\ / ? * [ ] :`. Pokud vaše ID mohou tyto znaky obsahovat, očistěte je:

```csharp
RepeatWorksheetName = "Invoice_{SanitizedOrderId}"
```

Přidejte vypočítanou vlastnost do `Order`:

```csharp
public string SanitizedOrderId => OrderId.ToString().Replace("/", "-").Replace("\\", "-");
```

### Potřebujete zachovat původní šablonový list?

Nastavte `smartMarkerOptions.RemoveTemplate = false;` (výchozí hodnota je `true`). Tím zůstane původní `InvoiceTemplate` nedotčený jako reference.

### Chcete seskupit faktury podle zákazníka?

Můžete vnořit **opakující se skupiny**. Nejprve opakujte podle zákazníka a poté podle objednávek v rámci každého listu zákazníka. Syntaxe je trochu složitější, ale princip zůstává stejný – použijte `RepeatWorksheet` a pojmenovací vzor, který odráží hierarchii.

## Kompletní funkční příklad (všechen kód na jednom místě)

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

Zkopírujte a vložte tento kód do `Program.cs`, umístěte `InvoiceTemplate.xlsx` vedle něj a můžete spustit.

## Často kladené otázky

**Q: Funguje tento přístup s velkými datovými sadami (tisíce faktur)?**  
A: Ano. SmartMarker streamuje data efektivně, ale sledujte využití paměti. Pokud narazíte na limity, zvažte zpracování po dávkách a zápis každé dávky do samostatného sešitu.

**Q: Můžu automaticky přidat logo ke každé faktuře?**  
A: Rozhodně. Umístěte obrázek loga na šablonový list. Protože se list duplikuje, logo se objeví na každé vygenerované faktuře bez dalšího kódu.

**Q: Co když potřebuji chránit listy?**  
A: Po zpracování projděte `wb.Worksheets` a zavolejte `ws.Protect(Password, ProtectionType.All)`.

## Závěr

Právě jsme **automatizovali generování faktur** využitím funkce opakování listů SmartMarkeru a chytrého pojmenovacího vzoru. Tutoriál pokryl **jak pojmenovat listy**, předvedl **jak opakovat list** pro každou objednávku a ukázal **dynamické pojmenování listů**, které udržuje váš sešit přehledný a snadno prohledávatelný.  

Od načtení dat, nastavení šablony, konfigurace `SmartMarkerOptions` až po řešení okrajových případů máte nyní kompletní, spustitelný řešení. Dále můžete přidat tabulky položek, aplikovat podmíněné formátování nebo exportovat stejná data do PDF pro plně automatizovaný fakturační proces.

Jste připraveni posunout se dál? Prozkoumejte související témata jako „hromadný export do Excelu s Aspose.Cells“, „konverze listů do PDF“ nebo „odesílání vygenerovaných faktur e-mailem přímo z C#“. Možnosti jsou neomezené – šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}