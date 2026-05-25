---
category: general
date: 2026-02-15
description: Skapa en ny arbetsbok i C# och lär dig hur du lägger till en tabell,
  aktiverar filter och sparar arbetsboken som xlsx. Snabb, komplett guide för Excel‑automatisering.
draft: false
keywords:
- create new workbook
- save workbook as xlsx
- how to create workbook
- how to add table
- how to enable filter
language: sv
og_description: Skapa en ny arbetsbok i C# och lägg omedelbart till en tabell, slå
  på filter, och spara sedan arbetsboken som xlsx. Följ denna korta, praktiska handledning.
og_title: Skapa ny arbetsbok i C# – Komplett programmeringsguide
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Skapa ny arbetsbok i C# – Steg‑för‑steg‑guide
url: /sv/net/excel-workbook/create-new-workbook-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa ny arbetsbok i C# – Komplett programmeringsguide

Har du någonsin behövt **create new workbook** i C# men inte vetat vilka objekt du ska börja med? Du är inte ensam; många utvecklare fastnar när de automatiserar Excel‑filer. I den här handledningen går vi igenom hur du skapar en ny arbetsbok, infogar ett bord, slår på auto‑filter och slutligen **save workbook as xlsx** – allt med tydlig, körbar kod.

Vi svarar också på de vanliga frågorna “hur lägger man till ett bord” och “hur aktiverar man filter” som ofta dyker upp efter den första arbetsboks‑skapelsen. När du är klar har du ett självständigt exempel som du kan klistra in i vilket .NET‑projekt som helst, utan onödig extra kod.

## Förutsättningar och installation

Innan vi dyker ner, se till att du har:

- **.NET 6** (eller någon nyare .NET‑version) installerad.  
- NuGet‑paketet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`) – detta bibliotek tillhandahåller klasserna `Workbook`, `Worksheet` och `ListObject` som används nedan.  
- En utvecklingsmiljö du föredrar (Visual Studio, VS Code, Rider – välj det som passar dig).

Ingen ytterligare konfiguration behövs; koden körs direkt när paketet har refererats.

![Screenshot showing a newly created workbook in Excel – create new workbook](image.png)

*Bildtext: “skärmdump av skapa ny arbetsbok i Excel”*

## Steg 1: Skapa ny arbetsbok och hämta det första kalkylbladet

Det allra första du måste göra är att instansiera ett `Workbook`‑objekt. Tänk på det som att öppna en helt ny Excel‑fil som för närvarande innehåller ett enda standardsheet. Därefter hämtar du en referens till kalkylbladet så att du kan börja fylla i det.

```csharp
using Aspose.Cells;

public class WorkbookDemo
{
    public static void Main()
    {
        // Step 1: Create a new workbook (this is the "create new workbook" part)
        Workbook workbook = new Workbook();

        // Access the first worksheet – by default it is named "Sheet1"
        Worksheet worksheet = workbook.Worksheets[0];
```

**Varför detta är viktigt:** Att skapa arbetsboken ger dig en ren canvas; att hämta det första kalkylbladet säkerställer att du har ett mål för det kommande bordet. Hoppar du över detta får alla senare `ListObject`‑anrop ett null‑referensfel.

## Steg 2: Hur man lägger till ett bord i kalkylbladet

Nu när vi har ett kalkylblad, låt oss infoga ett bord som sträcker sig över cellerna **A1:C5**. I Aspose.Cells hanterar samlingen `ListObjects` bord (även kallade *list objects*). Att lägga till ett bord är en tvåstegs‑process: anropa `Add` för att skapa det, och kapsla sedan resultatet i en `ListObject`‑variabel för enkel manipulation.

```csharp
        // Step 2: Add a table named "MyTable" covering the range A1:C5
        int tableIndex = worksheet.ListObjects.Add("MyTable", "A1:C5", true);
        ListObject table = worksheet.ListObjects[tableIndex];
```

**Vad händer under huven?** Metoden `Add` registrerar bordet i Excels interna bordsmotor och tilldelar det ett unikt index. Genom att lagra det indexet i `tableIndex` kan vi hämta den faktiska `ListObject`‑instansen, vilket ger oss full kontroll över bordets egenskaper.

### Proffstips
Om du planerar att skapa flera bord, håll deras index i en lista – det gör senare uppdateringar enkla.

## Steg 3: Hur man aktiverar filter på bordet

Bord i Excel har en auto‑filter‑rad som standard, men beroende på hur du skapade bordet kan du behöva slå på den explicit. Egenskapen `ShowAutoFilter` styr om den raden visas eller inte.

```csharp
        // Step 3: Enable the auto‑filter for the table
        table.ShowAutoFilter = true;
```

När den är aktiverad kan användare klicka på rullgardinspilarna i rubrikraden för att filtrera rader baserat på värden. Detta är särskilt praktiskt för stora datamängder.

### Vad gör du om du inte vill ha ett filter?
Sätt bara `ShowAutoFilter` till `false` så försvinner pilarna. Följande rad demonstrerar den motsatta handlingen:

```csharp
        // Disable (remove) the auto‑filter
        table.ShowAutoFilter = false;
```

## Steg 4: Spara arbetsbok som XLSX

Allt tungt arbete är gjort; nu sparar vi arbetsboken till disk. Metoden `Save` tar emot en fullständig sökväg och bestämmer automatiskt filformatet utifrån filändelsen. Här sparar vi **explicit workbook as xlsx**.

```csharp
        // Step 4: Save the workbook to a file
        string outputPath = @"C:\Temp\NoFilter.xlsx"; // Change to your desired folder
        workbook.Save(outputPath);
    }
}
```

När du öppnar `NoFilter.xlsx` ser du ett enda blad med ett bord som heter **MyTable** och täcker A1:C5, och – eftersom vi satte `ShowAutoFilter` till `false` – visas inga filterpilar.

### Förväntat resultat
- En fil med namnet `NoFilter.xlsx` i den mapp du angav.  
- Sheet1 innehåller ett 5‑rader, 3‑kolumners bord med standarddata (tomma celler om du inte fyller i dem).  
- Ingen auto‑filter‑rad visas.

## Variationer och kantfall

### Behålla filtret aktiverat
Om ditt scenario kräver att filtret ska vara på, utelämna bara raden som sätter `ShowAutoFilter = false`. Bordet visas då med filterpilar redo för användarinteraktion.

### Lägga till flera bord
Du kan upprepa **Steg 2** med olika områden och namn:

```csharp
int secondTableIdx = worksheet.ListObjects.Add("SecondTable", "E1:G10", true);
ListObject secondTable = worksheet.ListObjects[secondTableIdx];
secondTable.ShowAutoFilter = true;
```

### Fyll i bordets data
Aspose.Cells låter dig skriva direkt till celler före eller efter att bordet skapats. Till exempel, för att fylla den första kolumnen med siffror:

```csharp
for (int i = 0; i < 5; i++)
{
    worksheet.Cells[i, 0].PutValue(i + 1); // A1‑A5 = 1‑5
}
```

### Kompatibilitetsnotering
Koden fungerar med **Aspose.Cells 23.9** och senare. Om du använder en äldre version kan signaturen för `Add` skilja sig något – kontrollera bibliotekets release‑noteringar.

## Vanliga fallgropar och hur du undviker dem

- **Glömt att referera Aspose.Cells** – kompilatorn klagar på okända typer. Säkerställ att NuGet‑paketet är installerat och att `using Aspose.Cells;` finns högst upp.  
- **Felaktig områdesträng** – Excel‑områden är skiftläges‑oberoende, men de måste vara giltiga (t.ex. `"A1:C5"` och inte `"A1:C"`). Ett stavfel kastar en `CellsException`.  
- **Behörighetsproblem för filsökväg** – att försöka spara till en skyddad mapp (som `C:\Program Files`) ger en `UnauthorizedAccessException`. Använd en skrivbar katalog som `%TEMP%` eller din användarprofil.

## Fullt fungerande exempel (Kopiera‑klistra‑klart)

```csharp
using Aspose.Cells;

public class WorkbookDemo
{
    public static void Main()
    {
        // 1️⃣ Create new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Add a table named "MyTable" covering A1:C5
        int tableIdx = worksheet.ListObjects.Add("MyTable", "A1:C5", true);
        ListObject table = worksheet.ListObjects[tableIdx];

        // 3️⃣ Enable auto‑filter (you can skip this if you don't need it)
        table.ShowAutoFilter = true;

        // OPTIONAL: Disable the filter if you don't want it visible
        // table.ShowAutoFilter = false;

        // 4️⃣ Save workbook as xlsx
        string outputPath = @"C:\Temp\NoFilter.xlsx";
        workbook.Save(outputPath);
    }
}
```

Kör programmet, öppna den genererade filen, och du ser exakt det resultat som beskrivits tidigare.

## Sammanfattning

Vi började med att **create new workbook**, sedan lärde vi oss **how to add table**, togglade **how to enable filter**‑funktionen, och slutligen **save workbook as xlsx**. Varje steg förklarades med *varför* det är viktigt, inte bara *vad* du ska skriva, så att du kan anpassa mönstret till mer komplexa scenarier.

## Vad blir nästa steg?

- **Styla bordet** – utforska `TableStyleType` för att ge dina data ett professionellt utseende.  
- **Infoga formler** – använd `Cells[i, j].Formula = "=SUM(A2:A5)"` för att lägga till beräkningar.  
- **Exportera till PDF** – Aspose.Cells kan också rendera arbetsboken som PDF med ett enda `Save`‑anrop.  
- **Läsa befintliga arbetsböcker** – ersätt `new Workbook()` med `new Workbook("ExistingFile.xlsx")` för att modifiera filer i farten.

Experimentera gärna med dessa idéer, och tveka inte att lämna en kommentar om något är oklart. Lycka till med kodandet, och njut av att automatisera Excel med C#!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}