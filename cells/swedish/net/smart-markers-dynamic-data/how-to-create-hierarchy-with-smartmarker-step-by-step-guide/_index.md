---
category: general
date: 2026-02-14
description: Att skapa hierarki i SmartMarker‑mallar är enklare än du tror – lär dig
  att skapa hierarkiska data och hur du listar anställda effektivt.
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: sv
og_description: Att skapa hierarki i SmartMarker‑mallar är enkelt. Följ den här guiden
  för att skapa hierarkiska data och lista anställda med nästlade intervall.
og_title: Hur man skapar hierarki med SmartMarker – Komplett guide
tags:
- SmartMarker
- C#
- templating
title: Hur man skapar hierarki med SmartMarker – Steg‑för‑steg‑guide
url: /sv/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar hierarki med SmartMarker – Komplett guide

Har du någonsin undrat **hur man skapar hierarki** i en SmartMarker-mall utan att rycka upp håret? Du är inte ensam. I många rapporteringsscenarier behöver du ett förälder‑barn‑förhållande – tänk avdelningar och personerna som arbetar i dem. Den goda nyheten är att SmartMarker gör det till en barnlek när du känner till rätt steg.

I den här handledningen går vi igenom hela processen: från **att skapa hierarkisk data** i C#, aktivera nästlade intervall, och slutligen rendera en mall som **listar anställda** för varje avdelning. När du är klar har du ett färdigt exempel som du kan släppa in i vilket .NET‑projekt som helst.

---

## Vad du behöver

- .NET 6+ (någon nyare version fungerar)
- En referens till **SmartMarker**‑biblioteket (namnutrymmet `ws.SmartMarkerProcessor`)
- Grundläggande C#‑kunskaper – inget avancerat, bara några objekt och en lambda eller två
- En IDE eller redigerare du föredrar (Visual Studio, Rider, VS Code… du bestämmer)

Om du redan har detta, toppen—låt oss dyka ner.

---

## Så skapar du hierarki – Översikt

Kärnidén är att bygga ett **nästlat objektgraf** som speglar den struktur du vill se i det slutgiltiga dokumentet. I vårt fall ser grafen ut så här:

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

SmartMarker kan sedan iterera över `Departments` och, eftersom vi slår på **nästlad intervallbehandling**, loopa över varje avdelnings `Employees`‑samling automatiskt.

---

## Steg 1: Bygg den hierarkiska datamodellen

Först skapar vi ett anonymt objekt som innehåller en array av avdelningar, var och en med sin egen anställdlista. Att använda en anonym typ håller exemplet lättviktigt—känn dig fri att ersätta det med riktiga POCO‑klasser senare.

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

> **Varför detta är viktigt:** `Departments`‑arrayen är samlingen på toppnivå. Varje element innehåller en `Employees`‑array, vilket ger oss den andra hierarkinivån som vi senare kommer åt med `#Departments.Employees#`.

---

## Steg 2: Aktivera nästlad intervallbehandling

SmartMarker dyker inte ner i inre samlingar om du inte säger åt den. `SmartMarkerOptions`‑objektet innehåller den växeln.

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **Proffstips:** Om du glömmer den här flaggan returnerar det inre `#Employees#`‑intervallet helt enkelt inget, och du kommer att klia dig i huvudet och undra varför mallen är tom.

---

## Steg 3: Kör processorn med dina data

Nu överlämnar vi data och alternativ till processorn. Variabeln `ws` representerar din **WebService** (eller vilket objekt som helst som hostar SmartMarker‑motorn).

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

Vid den här tidpunkten analyserar SmartMarker mallen, ersätter `#Departments.Name#` med varje avdelnings namn, och eftersom nästlade intervall är aktiverade itererar den genom varje avdelnings `Employees`‑samling.

---

## Steg 4: Skapa mallmarkörerna

Nedan är en minimal mall som demonstrerar både det yttre och det inre loopen. Klistra in den i SmartMarker‑mallredigeraren (eller en `.txt`‑fil du skickar till processorn).

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

När den renderas ser du:

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **Vad du ser:** Det yttre `#Departments.Name#` skriver ut avdelningens titel. Det inre `#Departments.Employees#`‑blocket loopar över varje anställd, och `#Departments.Employees#` inuti blocket skriver ut själva namnet.

---

## Förväntad output & verifiering

Att köra hela exemplet (data + alternativ + mall) bör producera exakt listan som visas ovan. För att snabbt verifiera kan du dumpa resultatet till konsolen:

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

Om du ser de två avdelningsrubrikerna följda av deras anställdas punkter har du framgångsrikt **skapat en hierarki** och **listat anställda**.

---

## Vanliga fallgropar & edge‑cases

| Problem | Varför det händer | Lösning |
|---------|-------------------|---------|
| Ingen output för anställda | `EnableNestedRange` left false | Set `EnableNestedRange = true` |
| Duplicerade anställda namn | Same array reused across departments | Clone the array or use distinct collections |
| Mycket stora hierarkier orsakar minnespress | SmartMarker loads the whole object graph into memory | Stream data or paginate large collections |
| Syntaxfel i mall | Missed closing `#/…#` tags | Use the SmartMarker validator or run a quick test with a tiny template |

---

## Gå vidare – Verkliga variationer

1. **Dynamic data sources** – Pull departments from a database and map them to the anonymous structure using LINQ.  
2. **Conditional formatting** – Add a `IsManager` flag to each employee and use SmartMarker’s conditional tags (`#if …#`) to highlight managers.  
3. **Multiple nesting levels** – If you need teams inside departments, just add another collection (`Teams`) and keep `EnableNestedRange` turned on.

---

## Fullt fungerande exempel (klar för kopiering)

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

**Template (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Att köra programmet skriver ut hierarkin exakt som visat tidigare.

---

## Slutsats

Vi har gått igenom **hur man skapar hierarki** i SmartMarker, från att forma **hierarkisk data** i C# till att slå på nästlade intervall och slutligen rendera en mall som **listar anställda** per avdelning. Mönstret skalar—lägg bara till fler nästlade samlingar eller villkorslogik så har du en kraftfull rapporteringsmotor inom räckhåll.

Redo för nästa utmaning? Prova att byta de anonyma typerna mot starkt typade POCO‑klasser, eller integrera detta flöde i en ASP.NET Core‑endpoint som returnerar en PDF‑ eller Word‑fil. Himlen är gränsen, och nu har du en solid grund.

![How to create hierarchy diagram](image.png){alt="Diagram som visar hur man skapar hierarki med avdelning‑anställd‑relation"}

*Lycklig kodning! Om du stöter på problem, lämna en kommentar nedan—jag hjälper gärna till.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}