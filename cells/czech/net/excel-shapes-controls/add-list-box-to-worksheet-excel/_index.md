---
"description": "Naučte se, jak přidat seznam do listu aplikace Excel pomocí Aspose.Cells pro .NET. Postupujte podle našeho jednoduchého podrobného návodu a vytvořte interaktivní listy aplikace Excel."
"linktitle": "Přidat seznam do listu v Excelu"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Přidat seznam do listu v Excelu"
"url": "/cs/net/excel-shapes-controls/add-list-box-to-worksheet-excel/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidat seznam do listu v Excelu

## Zavedení
Přidání interaktivních prvků do excelových listů, jako je seznam, může výrazně zlepšit správu a prezentaci dat. Ať už vytváříte interaktivní formulář nebo vlastní nástroj pro zadávání dat, možnost ovládat vstup uživatele pomocí seznamu je neocenitelná. Aspose.Cells pro .NET poskytuje efektivní způsob, jak tyto ovládací prvky přidávat a spravovat v excelových souborech. V této příručce vás provedeme procesem přidání seznamu do listu pomocí Aspose.Cells pro .NET.
## Předpoklady
Než se pustíte do kódování, ujistěte se, že máte k dispozici následující nástroje a zdroje:
- Knihovna Aspose.Cells pro .NET: Můžete si ji stáhnout z [Stránka ke stažení Aspose.Cells pro .NET](https://releases.aspose.com/cells/net/).
- Vývojové prostředí: Jakékoli IDE, které podporuje vývoj v .NET, například Visual Studio.
- .NET Framework: Ujistěte se, že váš projekt cílí na podporovanou verzi rozhraní .NET Framework.
Zvažte také pořízení [dočasná licence](https://purchase.aspose.com/temporary-license/) pokud chcete prozkoumat všechny funkce bez omezení.
## Importovat balíčky
Než začnete, ujistěte se, že jste importovali potřebné jmenné prostory Aspose.Cells. Postupujte takto:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
V tomto tutoriálu si rozdělíme proces přidání seznamu do několika jednoduchých kroků. Pečlivě dodržujte každý krok, abyste se ujistili, že vše funguje podle očekávání.
## Krok 1: Nastavení adresáře dokumentů
Než vytvoříte jakýkoli soubor aplikace Excel, potřebujete umístění pro jeho uložení. Zde je návod, jak nastavit adresář:
```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě neexistuje.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
tomto kroku definujete, kam bude váš soubor uložen. Kód zkontroluje, zda adresář existuje, a pokud ne, vytvoří ho. Tím se zajistí, že se později nesetkáte s chybami „soubor nebyl nalezen“.
## Krok 2: Vytvořte nový sešit a získejte přístup k prvnímu listu
Dále vytvoříme nový sešit a otevřeme první list, kam přidáme náš seznam.
```csharp
// Vytvořte nový sešit.
Workbook workbook = new Workbook();
// Vezměte si první pracovní list.
Worksheet sheet = workbook.Worksheets[0];
```
Sešit je v podstatě váš soubor aplikace Excel. Zde vytváříme nový sešit a přistupujeme k prvnímu listu, kam umístíme náš seznam. Představte si to jako vytvoření prázdného plátna, na které budete malovat ovládací prvky.
## Krok 3: Zadání dat do seznamu
Než přidáme seznam, musíme vyplnit některá data, na která bude seznam odkazovat.
```csharp
// Získejte kolekci buněk pracovního listu.
Cells cells = sheet.Cells;
// Zadejte hodnotu pro popisek.
cells["B3"].PutValue("Choose Dept:");
// Nastavte popisek na tučné písmo.
cells["B3"].GetStyle().Font.IsBold = true;
// Zadejte hodnoty pro seznam.
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
Zde přidáváme do listu text. Popisek „Vybrat oddělení:“ je umístěn v buňce B3 a jeho písmo je nastaveno na tučné. Do sloupce A vkládáme hodnoty, které budou sloužit jako vstupní rozsah pro náš seznam a budou představovat různá oddělení. Tento vstupní rozsah je to, z čeho budou uživatelé vybírat při interakci se seznamem.
## Krok 4: Přidání seznamu do pracovního listu
Nyní, když jsme nastavili data, přidejme samotný ovládací prvek seznamu.
```csharp
// Přidat nový seznam.
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
Tento kód přidá seznam do listu. Parametry definují polohu a velikost seznamu. Seznam je umístěn na řádku 2, sloupci 0, má šířku 122 a výšku 100. Toto jsou souřadnice a velikost, které určují, kde se seznam v listu zobrazí.
## Krok 5: Nastavení vlastností seznamu
Dále nastavíme různé vlastnosti seznamu, aby byl plně funkční.
```csharp
// Nastavte typ umístění.
listBox.Placement = PlacementType.FreeFloating;
// Nastavte propojenou buňku.
listBox.LinkedCell = "A1";
// Nastavte vstupní rozsah.
listBox.InputRange = "A2:A7";
// Nastavte typ výběru.
listBox.SelectionType = SelectionType.Single;
// Nastavte seznam s 3D stínováním.
listBox.Shadow = true;
```
- PlacementType.FreeFloating: Tato vlastnost zajišťuje, že seznam zůstane na své pozici bez ohledu na to, jak je list upraven.
- Propojená buňka: Nastaví buňku (v tomto případě A1), kde se zobrazí vybraná hodnota ze seznamu.
- InputRange: Toto určuje seznamu, kde má hledat seznam možností (A2 až A7, které jsme nastavili dříve).
- SelectionType.Single: Toto omezuje uživatele na výběr pouze jedné položky ze seznamu.
- Stín: Efekt stínu dodává seznamu trojrozměrnější vzhled, díky čemuž je vizuálně atraktivnější.
## Krok 6: Uložte soubor Excel
Nakonec si uložme sešit se seznamem.
```csharp
// Uložte si sešit.
workbook.Save(dataDir + "book1.out.xls");
```
Tento řádek kódu uloží sešit do adresáře, který jsme dříve nastavili. Soubor se jmenuje „book1.out.xls“, ale můžete si zvolit libovolný název, který vyhovuje vašemu projektu.
## Závěr
tady to máte! Úspěšně jste přidali seznam do listu aplikace Excel pomocí knihovny Aspose.Cells pro .NET. S několika řádky kódu jsme vytvořili plně funkční seznam, díky čemuž je list interaktivnější a dynamičtější. Tento tutoriál by vám měl poskytnout solidní základ pro prozkoumání dalších ovládacích prvků a funkcí v knihovně Aspose.Cells pro .NET. Pokračujte v experimentování a brzy zvládnete rozsáhlé funkce knihovny!
## Často kladené otázky
### Mohu v seznamu povolit více výběrů?  
Ano, můžete změnit `SelectionType` na `SelectionType.Multi` aby bylo možné vybrat více možností.
### Mohu změnit vzhled seznamu?  
Rozhodně! Aspose.Cells umožňuje přizpůsobit vzhled seznamu, včetně jeho velikosti, písma a dokonce i barvy.
### Co když budu muset později seznam odstranit?  
Seznam můžete zobrazit a odebrat z `Shapes` sběr pomocí `sheet.Shapes.RemoveAt(index)`.
### Mohu propojit seznam s jinou buňkou?  
Ano, stačí změnit `LinkedCell` vlastnost do jakékoli jiné buňky, kde chcete zobrazit vybranou hodnotu.
### Jak přidám další položky do seznamu?  
Stačí aktualizovat vstupní rozsah vložením dalších hodnot do zadaných buněk a seznam se automaticky aktualizuje.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}