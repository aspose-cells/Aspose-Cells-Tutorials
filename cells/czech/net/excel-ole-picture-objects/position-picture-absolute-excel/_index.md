---
"description": "Naučte se, jak absolutně umístit obrázky v Excelu pomocí Aspose.Cells pro .NET v tomto komplexním podrobném tutoriálu."
"linktitle": "Pozice obrázku (absolutní) v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Pozice obrázku (absolutní) v Excelu"
"url": "/cs/net/excel-ole-picture-objects/position-picture-absolute-excel/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Pozice obrázku (absolutní) v Excelu

## Zavedení
Už jste někdy měli problém se správným umístěním obrázků v excelové tabulce? Nejste sami! S tímto problémem se potýká mnoho uživatelů, zejména když jejich potřeby vizualizace dat vyžadují absolutní umístění pro lepší estetiku nebo přehlednost. Nehledejte dál; tato příručka vás provede jednoduchým procesem absolutního umístění obrázků v excelové tabulce pomocí Aspose.Cells pro .NET. Ať už jste vývojář pracující s Excelem, nebo datový analytik, který chce vylepšit své reporty, náš podrobný tutoriál je tu, aby vám zjednodušil práci s obrázky v Excelu!
## Předpoklady
Než se ponoříte do kódu a specifik, je třeba mít připraveno několik věcí:
1. Knihovna Aspose.Cells: Ujistěte se, že máte nejnovější verzi knihovny Aspose.Cells pro .NET. Můžete si ji stáhnout z [stránka s vydáními](https://releases.aspose.com/cells/net/).
2. Vývojové prostředí: Ujistěte se, že máte nastavené funkční vývojové prostředí .NET. Můžete použít Visual Studio nebo jakékoli jiné vývojové prostředí dle vlastního výběru.
3. Základní znalost C#: Znalost programovacího jazyka C# bude přínosem pro pochopení úryvků kódu.
4. Soubor s obrázkem: Mějte v určeném adresáři dokumentů uložený soubor s obrázkem (např. „logo.jpg“), který chcete vložit do listu aplikace Excel.

## Importovat balíčky
Pro začátek se ujistěme, že jsme importovali potřebné balíčky pro náš projekt. Soubor vašeho projektu by měl obsahovat následující jmenné prostory:
```csharp
using System.IO;
using Aspose.Cells;
```
Importem těchto jmenných prostorů zajistíme, aby náš program mohl využívat funkce poskytované Aspose.Cells.
Pro přehlednost si to rozdělme na zvládnutelné kroky.
## Krok 1: Nastavení adresáře dokumentů
tomto prvním kroku je třeba definovat adresář, kde se nacházejí vaše dokumenty. To je nezbytné pro to, aby program věděl, kam má soubory ukládat nebo načítat. Zde je návod, jak to nastavit:
```csharp
string dataDir = "Your Document Directory";
```
Jednoduše vyměňte `"Your Document Directory"` se skutečnou cestou, kde se nachází soubor s obrázkem. Může to být něco jako `"C:\\Users\\YourUsername\\Documents\\"`.
## Krok 2: Vytvoření instance objektu Workbook
Dále je třeba vytvořit novou instanci `Workbook` třída. Tento objekt představuje váš soubor aplikace Excel:
```csharp
Workbook workbook = new Workbook();
```
V tomto okamžiku máte sešit připravený k naplnění daty a obrázky.
## Krok 3: Přidání nového pracovního listu
Nyní, když máte sešit, musíte do něj přidat pracovní list. Zde se začne dít kouzlo přidávání a umisťování obrázků:
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
Tento řádek vytvoří nový list ve vašem sešitu a vrátí jeho index, který uložíme do proměnné `sheetIndex`.
## Krok 4: Získání nového pracovního listu
Odkazujme na nově vytvořený list. Pomocí indexu, který jsme právě získali, můžeme k listu přistupovat a manipulovat s ním:
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
Nyní můžete pracovat s `worksheet` objekt pro přidání obsahu, včetně obrázků.
## Krok 5: Přidání obrázku
A teď ta vzrušující část! Zde přidáme obrázek do našeho listu. Určíme indexy řádků a sloupců, kde chceme obrázek ukotvit (v tomto případě buňka „F6“, což je řádek 5 a sloupec 5):
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
Tato čára efektivně uzamkne obrázek na určeném místě vzhledem k celému listu. V tuto chvíli je však stále možné měnit jeho velikost spolu s buňkami.
## Krok 6: Přístup k nově přidanému obrázku
Pro další manipulaci s obrázkem je potřeba zobrazit jeho vlastnosti:
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
Tímto získáte přístup k vlastnostem obrázku, který jsme právě přidali!
## Krok 7: Nastavení absolutního umístění obrázku
Pro absolutní umístění obrázku (v pixelech) je nutné definovat jeho polohu pomocí `Left` a `Top` vlastnosti. Zde budete mít kontrolu nad tím, kde se obrázek zobrazí:
```csharp
picture.Left = 60;
picture.Top = 10;
```
Obě hodnoty můžete upravit podle potřeby; představují horizontální a vertikální umístění obrázku.
## Krok 8: Uložení souboru Excel
Nakonec, po provedení všech úprav, je čas sešit uložit:
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
Tím se vytvoří soubor aplikace Excel s názvem `book1.out.xls` ve vašem dříve definovaném adresáři dokumentů, který obsahuje váš pracovní list s absolutně umístěným obrázkem.

## Závěr
A je to! Úspěšně jste umístili obrázek v excelovém listu s absolutním umístěním pomocí Aspose.Cells pro .NET. Tento přímočarý proces nejen vylepšuje vizuální prezentaci vašich excelových dokumentů, ale také zajišťuje, že obrázky zůstanou přesně tam, kde je chcete mít – bez ohledu na jakékoli změny provedené ve velikostech buněk a výškách řádků. Nyní, ať už připravujete zprávu nebo vytváříte dashboard, můžete mít jistotu, že vaše obrázky budou pokaždé perfektně umístěny.
## Často kladené otázky
### Co je Aspose.Cells pro .NET?
Aspose.Cells pro .NET je knihovna pro .NET, která umožňuje vývojářům programově vytvářet, manipulovat a převádět tabulky aplikace Excel bez nutnosti používat Microsoft Excel.
### Mohu pomocí Aspose.Cells provádět i jiné manipulace s obrázky?
Ano, kromě umístění můžete také měnit velikost, otáčet a upravovat obrázky v tabulkách aplikace Excel pomocí knihovny Aspose.Cells.
### Je Aspose.Cells zdarma k použití?
Aspose.Cells je komerční produkt, ale můžete začít s bezplatnou zkušební verzí dostupnou na jejich [stránka s bezplatnou zkušební verzí](https://releases.aspose.com/).
### Jak získám dočasnou licenci pro Aspose.Cells?
O dočasnou licenci můžete požádat prostřednictvím [stránka s dočasnou licencí](https://purchase.aspose.com/temporary-license/) poskytuje Aspose.
### Kde najdu další příklady a dokumentaci?
Ten/Ta/To [Dokumentace k Aspose.Cells](https://reference.aspose.com/cells/net/) obsahuje rozsáhlé zdroje, včetně příkladů kódu a podrobnějších funkcí.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}