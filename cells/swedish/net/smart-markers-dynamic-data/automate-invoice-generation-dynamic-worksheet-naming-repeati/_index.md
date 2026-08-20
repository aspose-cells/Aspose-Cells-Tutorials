---
category: general
date: 2026-02-14
description: 'Automatisera fakturagenerering med SmartMarker: lär dig hur du upprepar
  kalkylblad, namnger dem dynamiskt och behärskar dynamisk namngivning av kalkylblad
  på några minuter.'
draft: false
keywords:
- automate invoice generation
- how to name worksheets
- how to repeat worksheet
- dynamic worksheet naming
language: sv
og_description: Automatisera fakturagenerering med SmartMarker. Denna guide visar
  hur du upprepar kalkylblad, namnger dem dynamiskt och behärskar dynamisk namngivning
  av kalkylblad.
og_title: Automatisera fakturagenerering – Dynamisk namngivning av kalkylblad och
  upprepning
tags:
- C#
- SmartMarker
- Excel Automation
title: Automatisera fakturagenerering – Dynamisk namngeivning av kalkylblad och upprepning
  i C#
url: /sv/net/smart-markers-dynamic-data/automate-invoice-generation-dynamic-worksheet-naming-repeati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Automatisera fakturagenerering – Dynamisk bladnamngivning & upprepning i C#

Har du någonsin undrat hur man **automatiserar fakturagenerering** utan att manuellt kopiera blad för varje beställning? Du är inte ensam. Många utvecklare stöter på problem när de behöver ett separat arbetsblad per faktura men också vill att bladnamnet ska spegla beställningsnumret. I den här handledningen löser vi problemet med SmartMarker’s `SmartMarkerProcessor` och visar dig **hur man namnger arbetsblad** dynamiskt samtidigt som vi täcker **hur man upprepar ett arbetsblad** för varje post. I slutet har du ett färdigt C#‑exempel som producerar en arbetsbok där varje faktura finns på sitt eget, snyggt namngivna flik.

Vi går igenom varje steg—från att hämta beställningar från en datakälla till att konfigurera `SmartMarkerOptions` för dynamisk bladnamngivning. Inga externa dokument behövs; allt du behöver finns här. Lite förkunskap om C# och en referens till Aspose.Cells‑biblioteket (eller någon SmartMarker‑kompatibel motor) räcker.

---

## Vad du kommer att bygga

- Hämta en samling order‑objekt.
- Konfigurera SmartMarker för att **upprepa ett arbetsblad** för varje order.
- Applicera **dynamisk bladnamngivning** med `{OrderId}`‑platshållaren.
- Generera en Excel‑fil där varje flik heter `Invoice_12345`, `Invoice_67890`, osv.
- Verifiera resultatet genom att öppna arbetsboken.

---

## Förutsättningar

- .NET 6.0 eller senare (koden kompileras även med .NET 5+).
- Aspose.Cells för .NET (eller något bibliotek som implementerar SmartMarker). Installera via NuGet:

```bash
dotnet add package Aspose.Cells
```

- En grundläggande `Order`‑klass (du kan ersätta den med din egen DTO).

---

## Steg 1: Ställ in projektet och modellen

Först, skapa en ny konsolapp och definiera datamodellen som representerar en order.

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

> **Proffstips:** Håll modellen lättviktig för demonstrationen; du kan alltid berika den senare med radposter, skattedetaljer osv.

---

## Steg 2: Förbered Excel‑mallen

SmartMarker arbetar mot en mallarbetsbok. Skapa en fil som heter `InvoiceTemplate.xlsx` med ett enda arbetsblad som heter `InvoiceTemplate`. I cell **A1** placera en SmartMarker‑platshållare som:

```
{{OrderId}} – {{Customer}} – {{Date}} – ${{Total}}
```

Du kan formatera cellerna på vilket sätt du vill—fet rubrik, valutformat osv. Spara filen i projektets rotmapp.

> **Varför en mall?** Den separerar layout från kod, så att formgivare kan justera utseendet utan att röra logiken.

---

## Steg 3: Konfigurera SmartMarker‑alternativ – Upprepa & namnge arbetsblad

Nu kommer vi att instruera SmartMarker att *upprepa* mallarbetsbladet för varje order och att ge varje kopia ett namn som inkluderar order‑ID. Detta är kärnan i **dynamisk bladnamngivning**.

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

### Så fungerar det

- **`RepeatWorksheet = true`** talar om för motorn att duplicera källbladet för varje element i `orders`‑samlingen. Detta uppfyller kravet **hur man upprepar ett arbetsblad**.
- **`RepeatWorksheetName = "Invoice_{OrderId}"`** är en mallsträng där `{OrderId}` är en platshållare som SmartMarker ersätter med det aktuella order‑ID:t. Det är svaret på **hur man namnger arbetsblad** och **dynamisk bladnamngivning**.
- Processorn sammanslår varje orders fält (`{{OrderId}}`, `{{Customer}}`, osv.) i det duplicerade bladet och skapar en fullständigt ifylld faktura.

---

## Steg 4: Kör applikationen och verifiera resultatet

Kompilera och kör konsolappen:

```bash
dotnet run
```

Du bör se framgångsmeddelandet i konsolen. Öppna `GeneratedInvoices.xlsx` och du hittar tre flikar:

- **Invoice_1001**
- **Invoice_1002**
- **Invoice_1003**

Varje blad innehåller orderdata som ersatts i platshållarna. Layouten du designade i mallen bevaras, vilket visar att **automatisera fakturagenerering** fungerar från början till slut.

### Förväntad skärmbild (alt‑text för SEO)

![exempel på automatiserad fakturagenerering som visar tre dynamiskt namngivna arbetsblad](/images/invoice-automation.png)

> *Bildens alt‑text inkluderar huvudnyckelordet för att uppfylla SEO.*

---

## Steg 5: Kantfall och vanliga variationer

### Vad händer om ett OrderId innehåller otillåtna tecken?

Excel‑bladnamn får inte innehålla `\ / ? * [ ] :`. Om dina ID:n kan innehålla dessa, rensa dem:

```csharp
RepeatWorksheetName = "Invoice_{SanitizedOrderId}"
```

Lägg till en beräknad egenskap i `Order`:

```csharp
public string SanitizedOrderId => OrderId.ToString().Replace("/", "-").Replace("\\", "-");
```

### Behöver du behålla det ursprungliga mallbladet?

Ställ in `smartMarkerOptions.RemoveTemplate = false;` (standard är `true`). Detta lämnar den ursprungliga `InvoiceTemplate` orörd som referens.

### Vill du gruppera fakturor per kund?

Du kan nästla **upprepningsgrupper**. Först upprepa per kund, sedan per order inom varje kunds arbetsblad. Syntaxen blir lite mer invecklad, men principen är densamma—använd `RepeatWorksheet` och ett namnmönster som speglar hierarkin.

---

## Fullständigt fungerande exempel (All kod på ett ställe)

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

Kopiera‑klistra in detta i `Program.cs`, placera `InvoiceTemplate.xlsx` bredvid den, så är du redo att köra.

---

## Vanliga frågor

**Q: Fungerar detta tillvägagångssätt med stora datamängder (tusentals fakturor)?**  
A: Ja. SmartMarker strömmar data effektivt, men håll ett öga på minnesanvändningen. Om du når gränser, överväg att bearbeta i batcher och skriva varje batch till en separat arbetsbok.

**Q: Kan jag lägga till en logotyp på varje faktura automatiskt?**  
A: Absolut. Placera logotypbilden på mallbladet. Eftersom bladet dupliceras visas logotypen på varje genererad faktura utan extra kod.

**Q: Vad händer om jag behöver skydda arbetsbladen?**  
A: Efter bearbetning, loopa igenom `wb.Worksheets` och anropa `ws.Protect(Password, ProtectionType.All)`.

---

## Slutsats

Vi har just **automatiserat fakturagenerering** genom att utnyttja SmartMarker’s upprepnings‑funktion för arbetsblad och ett smart namnmönster. Handledningen täckte **hur man namnger arbetsblad**, demonstrerade **hur man upprepar ett arbetsblad** för varje order, och visade **dynamisk bladnamngivning** som håller din arbetsbok organiserad och sökbar.

Från att hämta data, skapa en mall, konfigurera `SmartMarkerOptions`, till att hantera kantfall, har du nu en komplett, körbar lösning. Nästa steg kan vara att lägga till radposttabeller, applicera villkorlig formatering eller exportera samma data till PDF för en fullt automatiserad faktureringspipeline.

Redo att ta nästa steg? Utforska relaterade ämnen som “massexport till Excel med Aspose.Cells”, “PDF‑konvertering av arbetsblad” eller “skicka genererade fakturor via e‑post direkt från C#”. Himlen är gränsen—lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}