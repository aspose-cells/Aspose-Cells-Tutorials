---
category: general
date: 2026-10-07
description: Lär dig hur du med Aspose.Cells tar bort rader i en Excel‑tabell, tar
  bort alla rader utom rubriken och hanterar radering av skyddade tabellrader med
  ren C#‑kod.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- aspose cells delete rows
- delete rows excel table
- excel table row deletion
- protect excel table rows
- remove rows except header
language: sv
lastmod: 2026-10-07
og_description: Aspose.Cells tar bort rader från en Excel‑tabell samtidigt som rubriken
  bevaras. Denna guide visar den kompletta C#‑lösningen, hanterar skyddade tabeller
  och vanliga kantfall.
og_image_alt: Aspose.Cells delete rows example showing code and Excel screenshot
og_title: Aspose.Cells ta bort rader – ta bort alla rader förutom rubriken i C#
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how Aspose.Cells delete rows from an Excel table, remove rows
    except header, and handle protected table row deletion with clean C# code.
  headline: How to use Aspose.Cells to delete rows in an Excel table while keeping
    the header
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hur du använder Aspose.Cells för att ta bort rader i en Excel‑tabell och behålla
  rubriken
url: /sv/net/row-and-column-management/how-to-use-aspose-cells-to-delete-rows-in-an-excel-table-whi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder Aspose.Cells för att ta bort rader i en Excel‑tabell samtidigt som rubriken behålls

Om du behöver **aspose cells delete rows** från en tabell men behålla rubrikraden, visar den här guiden en komplett, körbar lösning. Du kommer att se varför ett direkt anrop till `ListObject.DeleteRows` misslyckas när tabellen är skyddad, och hur du kan kringgå den begränsningen utan att äventyra dataintegriteten.

Handledningen täcker:

* Laddning av en arbetsbok som innehåller en skyddad tabell.  
* Upptäckt och tillfällig borttagning av tabellskydd.  
* Borttagning av alla datarader samtidigt som rubriken bevaras.  
* Återställning av det ursprungliga skyddstillståndet.  

När du har läst artikeln kan du på ett pålitligt sätt utföra **delete rows excel table**‑operationer i vilket Aspose.Cells‑projekt som helst.

## Förutsättningar

* .NET 6.0 eller senare (koden fungerar också med .NET Framework 4.7.2+).  
* Aspose.Cells för .NET 23.9 eller nyare.  
* Grundläggande kunskap om C# och Excel‑tabeller (även kallade ListObjects).  

Inga ytterligare NuGet‑paket krävs utöver Aspose.Cells.

## Steg 1: Skapa projektet och importera namnrymder

Skapa en ny konsolapplikation eller lägg till följande kod i ett befintligt projekt. Importera Aspose.Cells‑namnrymderna så att kompilatorn kan lösa `Workbook`, `Worksheet` och `ListObject`.

```csharp
using System;
using Aspose.Cells;

namespace AsposeCellsTableRowDeletion
{
    class Program
    {
        static void Main()
        {
            // The full solution starts in Step 2.
        }
    }
}
```

*Varför detta steg är viktigt* – Att importera rätt namnrymder förhindrar tvetydiga typfel och gör resten av koden tydligare.

## Steg 2: Ladda arbetsboken och lokalisera mål‑tabellen

Byt ut `"YOUR_DIRECTORY/TableProtection.xlsx"` mot sökvägen till din Excel‑fil. Exemplet förutsätter att tabellen du vill ändra heter **Orders**.

```csharp
// Load the workbook that contains the protected table
Workbook workbook = new Workbook("YOUR_DIRECTORY/TableProtection.xlsx");

// Get the first worksheet (index 0) and the ListObject named "Orders"
Worksheet worksheet = workbook.Worksheets[0];
ListObject ordersTable = worksheet.ListObjects["Orders"];
```

*Varför detta steg är viktigt* – Att komma åt `ListObject` ger dig en direkt referens till tabellen, vilket krävs för varje **excel table row deletion**‑operation.

## Steg 3: Kontrollera om tabellen är skyddad

Aspose.Cells blockerar partiell tabellborttagning när tabellen är skyddad. Ett anrop till `ordersTable.DeleteRows` i det tillståndet kastar ett undantag. Detektera skyddstillståndet först.

```csharp
bool wasProtected = ordersTable.IsProtected;
Console.WriteLine($"Table protection status: {(wasProtected ? "protected" : "unprotected")}");
```

*Varför detta steg är viktigt* – Att känna till skyddstillståndet låter dig avgöra om du temporärt ska ta bort skyddet, så att regeln **protect excel table rows** respekteras efter operationen.

## Steg 4: Tillfälligt ta bort skyddet på tabellen (om behövs)

Om tabellen är skyddad, använd `Unprotect` med lösenordet (om något). För tabeller utan lösenord, anropa helt enkelt `Unprotect()`.

```csharp
if (wasProtected)
{
    // Provide the password if the table was protected with one; otherwise, pass null.
    ordersTable.Unprotect(null);
    Console.WriteLine("Table temporarily unprotected.");
}
```

*Varför detta steg är viktigt* – Att ta bort skyddet på tabellen gör att Aspose.Cells kan utföra **aspose cells delete rows** utan att kasta ett undantag, samtidigt som du senare kan återställa skyddet.

## Steg 5: Ta bort alla rader utom rubriken

Rubriken upptar den första raden i tabellen (`RowCount` inkluderar rubriken). Att ta bort från index 1 tar bort varje datarad.

```csharp
int dataRows = ordersTable.RowCount - 1; // Exclude the header row
if (dataRows > 0)
{
    ordersTable.DeleteRows(1, dataRows);
    Console.WriteLine($"{dataRows} data rows removed, header preserved.");
}
else
{
    Console.WriteLine("Table contains only the header; nothing to delete.");
}
```

*Varför detta steg är viktigt* – Denna kod utför den centrala **remove rows except header**‑funktionen samtidigt som undantaget som uppstår vid partiella borttagningar i skyddade tabeller undviks.

## Steg 6: Återapplicera skyddet (om det var satt från början)

När raderna har tagits bort, återställ det ursprungliga skyddstillståndet så att arbetsboken beter sig exakt som tidigare.

```csharp
if (wasProtected)
{
    // Re‑apply protection with the same password (null if none was used)
    ordersTable.Protect(null);
    Console.WriteLine("Table protection restored.");
}
```

*Varför detta steg är viktigt* – Återställning av skyddet uppfyller kravet **protect excel table rows** och håller arbetsboken säker för efterföljande användare.

## Steg 7: Spara den modifierade arbetsboken

Välj ett nytt filnamn för att undvika att skriva över originalfilen, såvida du inte avsiktligt vill skriva över den.

```csharp
string outputPath = "YOUR_DIRECTORY/TableProtection_Modified.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Modified workbook saved to: {outputPath}");
```

*Varför detta steg är viktigt* – Att spara slutför **excel table row deletion**‑operationen och ger ett konkret resultat som du kan öppna i Excel för att verifiera.

## Fullt fungerande exempel

Att sätta ihop alla steg ger ett självständigt program som du kan kopiera, klistra in och köra.

```csharp
using System;
using Aspose.Cells;

namespace AsposeCellsTableRowDeletion
{
    class Program
    {
        static void Main()
        {
            // 1. Load workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/TableProtection.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];
            ListObject ordersTable = worksheet.ListObjects["Orders"];

            // 2. Remember protection state
            bool wasProtected = ordersTable.IsProtected;
            Console.WriteLine($"Table protection status: {(wasProtected ? "protected" : "unprotected")}");

            // 3. Unprotect if needed
            if (wasProtected)
            {
                ordersTable.Unprotect(null); // use password if applicable
                Console.WriteLine("Table temporarily unprotected.");
            }

            // 4. Delete all rows except header
            int dataRows = ordersTable.RowCount - 1;
            if (dataRows > 0)
            {
                ordersTable.DeleteRows(1, dataRows);
                Console.WriteLine($"{dataRows} data rows removed, header preserved.");
            }
            else
            {
                Console.WriteLine("Table contains only the header; nothing to delete.");
            }

            // 5. Restore protection
            if (wasProtected)
            {
                ordersTable.Protect(null); // re‑apply with original password if any
                Console.WriteLine("Table protection restored.");
            }

            // 6. Save the workbook
            string outputPath = "YOUR_DIRECTORY/TableProtection_Modified.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"Modified workbook saved to: {outputPath}");
        }
    }
}
```

### Förväntad output

```
Table protection status: protected
Table temporarily unprotected.
5 data rows removed, header preserved.
Table protection restored.
Modified workbook saved to: YOUR_DIRECTORY/TableProtection_Modified.xlsx
```

Öppna `TableProtection_Modified.xlsx` i Excel. Du kommer att se **Orders**‑tabellen med endast rubrikraden kvar; alla datarader har tagits bort.

## Hantering av vanliga variationer och kantfall

| Situation | Rekommenderad justering | Orsak |
|-----------|------------------------|-------|
| Tabell använder ett lösenord | Skicka lösenordet till `Unprotect` och `Protect` | Säkerställer samma säkerhetsnivå efter operationen |
| Tabell har inga datarader | Hoppa över anropet till `DeleteRows` | Förhindrar ett `ArgumentOutOfRangeException` |
| Flera tabeller behöver rensas | Loopa igenom `worksheet.ListObjects` och tillämpa samma logik | Skalar **delete rows excel table**‑mönstret till hela bladet |
| Du vill behålla rubriken och den första dataraden | Ändra till `DeleteRows(2, dataRows‑1)` | Påbörjar borttagning efter den andra raden, vilket bevarar den första dataraden |

Dessa variationer visar robust **excel table row deletion**‑hantering och understryker varför den presenterade metoden är den rekommenderade.

## Pro‑tips

* **Batch‑behandling** – Om du behöver ta bort rader från många arbetsböcker, kapsla in logiken i en återanvändbar metod som accepterar `Workbook` och `tableName`‑parametrar.  
* **Prestanda** – Att ta bort rader i ett enda anrop (`DeleteRows`) är snabbare än att ta bort rader en åt gången eftersom Aspose.Cells uppdaterar de interna datastrukturerna bara en gång.  
* **Säkerhet** – Arbeta alltid på en kopia av originalfilen eller behåll en backup innan du utför borttagningar, särskilt när **protect excel table rows** är inblandat.

## Slutsats

Du har nu en komplett, produktionsklar lösning för **aspose cells delete rows** samtidigt som rubriken i en Excel‑tabell bevaras. Guiden gick igenom hur du laddar arbetsboken, hanterar skyddade tabeller, utför **remove rows except header**‑operationen och återställer skyddet. Använd samma mönster för alla **excel table row deletion**‑scenarier, och anpassa koden för ytterligare krav såsom lösenordsskyddade tabeller eller batch‑behandling.

---

*Nästa steg* – Utforska relaterade ämnen som **delete rows excel table** med filter, sammanslagning av celler efter radborttagning, eller att använda Aspose.Cells för att kopiera tabeller mellan arbetsböcker. Alla dessa bygger på de grundläggande koncept som demonstrerats här och fördjupar din behärskning av Excel‑automation med Aspose.Cells.

## Vad bör du lära dig härnäst?

De följande handledningarna täcker nära besläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Aspose Cells Delete Rows – Protect Header Row in Excel](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [How to Insert and Delete Rows in Excel with Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [How to Delete Blank Rows in Excel Using Aspose.Cells .NET for Data Cleanup](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}