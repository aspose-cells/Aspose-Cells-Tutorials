---
category: general
date: 2026-03-25
description: Skapa en ny arbetsbok i C# och lär dig hur du använder EXPAND, beräknar
  cotangens och sparar arbetsboken till fil med steg‑för‑steg‑kod.
draft: false
keywords:
- create new workbook
- save workbook to file
- how to use expand
- how to calculate cotangent
- how to save excel
language: sv
og_description: Skapa en ny arbetsbok i C# och se omedelbart hur du använder EXPAND,
  beräknar cotangens och sparar arbetsboken till en fil.
og_title: Skapa ny arbetsbok i C# – Komplett programmeringsguide
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Skapa ny arbetsbok i C# – Komplett programmeringsguide
url: /sv/net/workbook-operations/create-new-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa ny arbetsbok i C# – Komplett programmeringsguide

Har du någonsin behövt **skapa ny arbetsbok** i C# men varit osäker på var du ska börja? Du är inte ensam. Oavsett om du automatiserar en rapporteringspipeline eller bara leker med Excel‑formler i kod, är förmågan att skapa en arbetsbok, lägga in formler som `EXPAND` eller `COT`, och sedan **spara arbetsbok till fil** en grundläggande färdighet för alla .NET‑utvecklare.

I den här handledningen går vi igenom ett verkligt exempel som gör just det: vi instansierar en ny arbetsbok, använder `EXPAND`‑funktionen för att omvandla en statisk array till en dynamisk kolumn, beräknar en kotangens med `COT`‑funktionen och slutligen **sparar arbetsbok till fil** som en `.xlsx`. När du är klar har du ett färdigt kodexempel, förstår *varför* varje anrop är viktigt och ser några praktiska varianter för kantfall.

> **Proffstips:** All kod nedan fungerar med den senaste versionen av Aspose.Cells för .NET (från och med mars 2026). Om du använder en äldre version är API‑ytan i stort sett densamma, men dubbelkolla namnrymd‑importerna.

## Vad du behöver

- .NET 6.0 eller senare (exemplet riktar sig mot .NET 6, men .NET 5 fungerar också)  
- Aspose.Cells för .NET installerat via NuGet (`Install-Package Aspose.Cells`)  
- En grundläggande kunskap i C# (du klarar det)  

Det är allt—inga extra DLL‑filer, ingen COM‑interop och definitivt ingen Excel‑installation på maskinen. Är du redo? Då kör vi.

![Screenshot showing how to create new workbook in C#](assets/create-new-workbook.png){alt="Skärmdump som visar hur man skapar en ny arbetsbok i C#"}

## Steg 1: Skapa en ny arbetsbok

Det första du måste göra är att instansiera `Workbook`‑klassen. Tänk på den som att öppna en tom Excel‑fil i minnet. Detta objekt innehåller en samling kalkylblad, stilar och allt annat du kommer att behöva senare.

```csharp
using Aspose.Cells;

class ExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();               // <-- creates an empty .xlsx structure
        Worksheet ws = workbook.Worksheets[0];            // default sheet is named "Sheet1"
```

Varför hämta det första kalkylbladet direkt? De flesta snabba exempel arbetar med ett enda blad, och åtkomsten `Worksheets[0]` är det snabbaste sättet att få en referens utan att loopa. Om du senare behöver flera blad kan du lägga till dem med `workbook.Worksheets.Add()`.

## Steg 2: Så här använder du EXPAND för att generera dynamiska områden

`EXPAND` är en nyare Excel‑funktion som tar en array och fyller ut den till en angiven storlek. I vår kod expanderar vi den bokstavliga arrayen `{1,2,3}` till en **5‑radig kolumn** med start i cell `A1`. Syntaxen i strängen är exakt vad du skulle skriva i Excel, så du kan kopiera‑klistra in den direkt i en cell senare om du vill.

```csharp
        // Step 2: Apply EXPAND to turn {1,2,3} into a 5‑row vertical range
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"; // rows=5, cols=1
```

### Vad händer under huven?

- `{1,2,3}` är en horisontell array‑literal.  
- Det andra argumentet (`5`) säger åt Excel att expandera arrayen till **5 rader**.  
- Det tredje argumentet (`1`) tvingar en **enda kolumn** som resultat.  

Om du utelämnar det tredje argumentet försöker Excel bevara den ursprungliga formen, vilket kan ge dig ett 5×3‑block istället för en enda kolumn. Det är ett vanligt fallgropp när du först experimenterar med `EXPAND`.

#### Variationer du kan behöva

| Önskad form | Formel­exempel |
|-------------|----------------|
| 3‑radigt, 2‑kolumners block | `=EXPAND({1,2,3},3,2)` |
| Endast fyll ner (samma kolumn) | `=EXPAND({10,20},10,1)` |
| Expandera till fler kolumner | `=EXPAND({5},5,4)` |

Känn dig fri att byta ut literalerna eller dimensionerna så att de matchar din datagenereringslogik.

## Steg 3: Så här beräknar du kotangens med COT‑funktionen

`COT`‑funktionen returnerar kotangensen för en vinkel uttryckt i radianer. I vårt exempel beräknar vi kotangensen för 45° (π/4 radianer). Resultatet, `1`, hamnar i cell `B1`.

```csharp
        // Step 3: Use COT to calculate cotangent of 45 degrees (π/4 radians)
        ws.Cells["B1"].Formula = "=COT(PI()/4)"; // PI() returns π, divided by 4 = 45°
```

### Varför använda COT istället för att beräkna manuellt?

Excel vet redan hur man hanterar den trigonometriska konverteringen, så du undviker flyttalsavrundningsfel som kan smyga sig in om du försöker `1 / TAN(angle)`. Dessutom blir formeln läsbar för alla som senare granskar kalkylbladet.

#### Kantfall: vinklar utanför 0‑360°

Om du matar in en vinkel som är större än `2*PI()` (eller en negativ), kommer Excel automatiskt att "wrap‑a" den, men resultatet kan bli oväntat. För att vara på den säkra sidan kan du normalisera vinkeln först:

```csharp
        // Normalize angle to 0‑2π range before applying COT
        ws.Cells["C1"].Formula = "=COT(MOD(PI()*3, 2*PI()))";
```

Detta kodstycke visar hur du kombinerar `MOD` med `COT` för robusta beräkningar.

## Steg 4: Så här sparar du arbetsbok till fil (Excel)

Nu när formlerna är på plats är sista steget att **spara arbetsbok till fil**. Du kan välja vilken sökväg du vill—se bara till att katalogen finns och att du har skrivrättigheter.

```csharp
        // Step 4 (optional): Save the workbook so you can inspect the results
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "output.xlsx");

        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Vad sparas egentligen?

När du öppnar `output.xlsx` i Excel ser du:

| A | B |
|---|---|
| 1 | 1 |
| 2 |   |
| 3 |   |
|   |   |
|   |   |

- Kolumn **A** innehåller den expanderade arrayen `{1,2,3}` följt av två tomma celler (eftersom vi begärde 5 rader).  
- Cell **B1** visar `1`, kotangensen för 45°.  

Om du uppdaterar arbetsboken (tryck `F9` eller aktivera automatisk beräkning) kommer Excel att utvärdera formlerna och visa resultaten. Aspose.Cells erbjuder också en `CalculateFormula`‑metod om du behöver värdena utan att öppna Excel:

```csharp
        workbook.CalculateFormula();
        double cotResult = ws.Cells["B1"].DoubleValue; // should be 1.0
```

## Vanliga frågor & fallgropar

| Fråga | Svar |
|-------|------|
| **Måste jag aktivera beräkning manuellt?** | Nej. Som standard sparar Aspose.Cells formler som de är; Excel beräknar dem vid öppning. Använd `workbook.CalculateFormula()` för förberäkning. |
| **Kan jag skriva formler till flera celler på en gång?** | Absolut. Använd `ws.Cells["D1:D5"].Formula = "=RAND()"` för att fylla ett område med slumpmässiga tal. |
| **Vad händer om mål‑mappen inte finns?** | Skapa den först: `Directory.CreateDirectory(Path.GetDirectoryName(outputPath));` |
| **Stöds `EXPAND` i äldre Excel‑versioner?** | `EXPAND` kom med Excel 365/2019. Om du behöver kompatibilitet med äldre filer, överväg `INDEX`/`SEQUENCE`‑kombinationer istället. |
| **Hur döljer jag formelvyn?** | Sätt `ws.Cells["A1"].FormulaHidden = true;` och skydda bladet om du inte vill att användare ska se den underliggande formeln. |

## Sammanfattning

Du vet nu **hur du skapar nya arbetsboks‑objekt** i C#, utnyttjar kraften i `EXPAND`‑funktionen för att generera dynamiska arrayer, beräknar en kotangens med `COT` och **sparar arbetsbok till fil** som ett prydligt Excel‑dokument. Det kompletta, körbara exemplet finns i kodsnuttarna ovan—kopiera det till en konsolapp, tryck `F5` och öppna den resulterande `output.xlsx` för att se magin.

### Vad blir nästa steg?

- **Utforska andra dynamiska array‑funktioner** som `SEQUENCE`, `FILTER` och `SORT`.  
- **Automatisera diagramskapande** med Aspose.Cells rika diagram‑API.  
- **Integrera med datakällor** (SQL, CSV) och mata in dessa värden i formler programatiskt.  
- **Lär dig spara Excel som PDF** eller andra format—perfekt för rapporteringspipelines.

Känn dig fri att experimentera: ändra arrayvärdena, justera vinkeln eller skriv resultatet till ett annat blad. Himlen är gränsen när du kombinerar C# med Excels moderna formelmotor.

Lycka till med kodningen, och må dina kalkylblad alltid beräkna korrekt!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}