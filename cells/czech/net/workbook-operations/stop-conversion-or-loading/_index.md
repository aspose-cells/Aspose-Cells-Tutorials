---
"description": "Naučte se zastavit konverzi sešitu v Aspose.Cells pro .NET pomocí Monitoru přerušení s podrobným návodem krok za krokem."
"linktitle": "Zastavení převodu nebo načítání pomocí monitoru přerušení"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Zastavení převodu nebo načítání pomocí monitoru přerušení"
"url": "/cs/net/workbook-operations/stop-conversion-or-loading/"
"weight": 26
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Zastavení převodu nebo načítání pomocí monitoru přerušení

## Zavedení
Práce s velkými soubory aplikace Excel často zahrnuje zdlouhavé procesy, které mohou zabírat čas a zdroje. Co kdybyste ale mohli proces převodu zastavit uprostřed, když si uvědomíte, že je třeba něco změnit? Aspose.Cells pro .NET má funkci s názvem Monitor přerušení, která umožňuje přerušit převod sešitu do jiného formátu, jako je PDF. To může být záchrana, zejména při práci s rozsáhlými datovými soubory. V této příručce si ukážeme, jak přerušit proces převodu pomocí Monitoru přerušení v Aspose.Cells pro .NET.
## Předpoklady
Než se ponoříte, ujistěte se, že máte připraveno následující:
1. Aspose.Cells pro .NET - Stáhněte si jej [zde](https://releases.aspose.com/cells/net/).
2. Vývojové prostředí .NET – například Visual Studio.
3. Základní znalost programování v C# – Znalost syntaxe C# vám pomůže s nácvikem.
## Importovat balíčky
Pro začátek importujme potřebné balíčky. Mezi tyto importy patří:
- Aspose.Cells: Hlavní knihovna pro manipulaci s Excelovými soubory.
- System.Threading: Pro správu vláken, protože v tomto příkladu budou spuštěny dva paralelní procesy.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.IO;
```
Rozeberme si proces do podrobných kroků. Každý krok vám pomůže pochopit důležitost nastavení a používání monitoru přerušení pro správu převodu sešitů aplikace Excel.
## Krok 1: Vytvořte třídu a nastavte výstupní adresář
Nejprve potřebujeme třídu pro zapouzdření našich funkcí a také adresář, kam bude uložen výstupní soubor.
```csharp
class StopConversionOrLoadingUsingInterruptMonitor
{
    static string outputDir = "Your Document Directory";
}
```
Nahradit `"Your Document Directory"` se skutečnou cestou, kam chcete soubor PDF uložit.
## Krok 2: Vytvoření instance monitoru přerušení
Dále vytvořte objekt InterruptMonitor. Tento monitor pomůže řídit proces nastavením možnosti jeho přerušení v libovolném daném bodě.
```csharp
InterruptMonitor im = new InterruptMonitor();
```
Tento monitor přerušení bude připojen k našemu sešitu, což nám umožní spravovat proces převodu.
## Krok 3: Nastavení sešitu pro převod
Nyní si vytvořme objekt sešitu, přiřadíme mu InterruptMonitor a poté otevřeme první list pro vložení ukázkového textu.
```csharp
void CreateWorkbookAndConvertItToPdfFormat()
{
    Workbook wb = new Workbook();
    wb.InterruptMonitor = im;
    Worksheet ws = wb.Worksheets[0];
    Cell cell = ws.Cells["J1000000"];
    cell.PutValue("This is text.");
}
```
Výše uvedený kód vytvoří sešit, nastaví pro něj InterruptMonitor a umístí text do vzdálené buňky (`J1000000`). Umístění textu na tuto pozici buňky zajistí, že zpracování sešitu bude časově náročnější, což poskytne InterruptMonitoru dostatek času na zásah.
## Krok 4: Uložení sešitu jako PDF a zpracování přerušení
Nyní se pokusme uložit sešit jako PDF. Použijeme `try-catch` blok pro zpracování jakéhokoli přerušení, ke kterému by mohlo dojít.
```csharp
try
{
    wb.Save(outputDir + "output_InterruptMonitor.pdf");
}
catch (Aspose.Cells.CellsException ex)
{
    Console.WriteLine("Process Interrupted - Message: " + ex.Message);
}
```
Pokud je proces přerušen, výjimka jej zachytí a zobrazí příslušnou zprávu. V opačném případě se sešit uloží jako PDF.
## Krok 5: Přerušení procesu převodu
Hlavní funkcí je možnost přerušení procesu. Zpoždění přidáme pomocí `Thread.Sleep` a pak zavolejte `Interrupt()` metoda pro zastavení konverze po 10 sekundách.
```csharp
void WaitForWhileAndThenInterrupt()
{
    Thread.Sleep(1000 * 10);
    im.Interrupt();
}
```
Toto zpoždění dává sešitu čas na zahájení převodu do PDF před odesláním signálu přerušení.
## Krok 6: Současné spuštění vláken
Abychom vše spojili, musíme obě funkce spustit v oddělených vláknech. Tímto způsobem může konverze sešitu a čekání na přerušení probíhat současně.
```csharp
public void TestRun()
{
    ThreadStart ts1 = new ThreadStart(this.CreateWorkbookAndConvertItToPdfFormat);
    Thread t1 = new Thread(ts1);
    t1.Start();
    ThreadStart ts2 = new ThreadStart(this.WaitForWhileAndThenInterrupt);
    Thread t2 = new Thread(ts2);
    t2.Start();
    t1.Join();
    t2.Join();
}
```
Výše uvedený kód běží `CreateWorkbookAndConvertItToPdfFormat` a `WaitForWhileAndThenInterrupt` v paralelních vláknech a jejich spojení po dokončení obou procesů.
## Krok 7: Konečné provedení
Nakonec přidáme `Run()` metoda pro spuštění kódu.
```csharp
public static void Run()
{
    new StopConversionOrLoadingUsingInterruptMonitor().TestRun();
    Console.WriteLine("StopConversionOrLoadingUsingInterruptMonitor executed successfully.");
}
```
Tento `Run` Metoda je vstupním bodem pro spuštění a pozorování přerušení v akci.
## Závěr
tomto tutoriálu jsme se podívali na to, jak přerušit proces převodu v Aspose.Cells pro .NET. Monitor přerušení je užitečný nástroj při práci s velkými soubory aplikace Excel, který umožňuje zastavit procesy bez čekání na jejich dokončení. To je obzvláště užitečné v situacích, kdy je čas a zdroje vzácné a je potřeba rychlá zpětná vazba.
## Často kladené otázky
### Co je monitor přerušení v Aspose.Cells pro .NET?  
Monitor přerušení umožňuje zastavit převod sešitu nebo proces načítání v jeho průběhu.
### Mohu použít Monitor přerušení pro jiné formáty než PDF?  
Ano, můžete přerušit i převody do jiných podporovaných formátů.
### Jak Thread.Sleep() ovlivňuje načasování přerušení?  
Thread.Sleep() vytvoří zpoždění před spuštěním přerušení, což dává čas na zahájení konverze.
### Mohu proces přerušit před uplynutím 10 sekund?  
Ano, upravit zpoždění v `WaitForWhileAndThenInterrupt()` na kratší dobu.
### Ovlivní proces přerušení výkon?  
Dopad je minimální a je to velmi prospěšné pro správu dlouhodobých procesů.
Více informací naleznete v [Dokumentace k Aspose.Cells pro .NET](https://reference.aspose.com/cells/net/)Pokud potřebujete pomoc, podívejte se na [Fórum podpory](https://forum.aspose.com/c/cells/9) nebo si pořiďte [Bezplatná zkušební verze](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}