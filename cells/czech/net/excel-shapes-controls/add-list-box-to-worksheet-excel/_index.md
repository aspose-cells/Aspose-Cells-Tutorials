---
title: Přidat pole seznamu do listu v aplikaci Excel
linktitle: Přidat pole seznamu do listu v aplikaci Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se, jak přidat seznam do listu aplikace Excel pomocí Aspose.Cells for .NET. Postupujte podle našeho jednoduchého průvodce krok za krokem a udělejte ze svých tabulek Excel interaktivní.
weight: 20
url: /cs/net/excel-shapes-controls/add-list-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidat pole seznamu do listu v aplikaci Excel

## Zavedení
Přidání interaktivních prvků do listů aplikace Excel, jako je seznam, může výrazně zlepšit správu a prezentaci dat. Ať už vytváříte interaktivní formulář nebo vlastní nástroj pro zadávání dat, schopnost ovládat vstup uživatele pomocí seznamu je neocenitelná. Aspose.Cells for .NET poskytuje efektivní způsob, jak přidat a spravovat tyto ovládací prvky v souborech aplikace Excel. V této příručce vás provedeme procesem přidání seznamu do listu pomocí Aspose.Cells for .NET.
## Předpoklady
Než se ponoříte do kódování, ujistěte se, že máte připraveny následující nástroje a zdroje:
-  Aspose.Cells for .NET Library: Můžete si ji stáhnout z[Stránka ke stažení Aspose.Cells for .NET](https://releases.aspose.com/cells/net/).
- Vývojové prostředí: Jakékoli IDE, které podporuje vývoj .NET, jako je Visual Studio.
- .NET Framework: Ujistěte se, že váš projekt cílí na podporovanou verzi rozhraní .NET Framework.
 Zvažte také získání a[dočasná licence](https://purchase.aspose.com/temporary-license/) pokud chcete prozkoumat všechny funkce bez omezení.
## Importujte balíčky
Než začnete, ujistěte se, že jste importovali potřebné jmenné prostory Aspose.Cells. Postup:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
V tomto tutoriálu rozdělíme proces přidávání seznamu do několika jednoduchých kroků. Dodržujte pečlivě každý krok, abyste zajistili, že vše funguje podle očekávání.
## Krok 1: Nastavení adresáře dokumentů
Než vytvoříte jakýkoli soubor aplikace Excel, potřebujete umístění pro jeho uložení. Zde je návod, jak nastavit adresář:
```csharp
// Cesta k adresáři dokumentů.
string dataDir = "Your Document Directory";
// Vytvořte adresář, pokud ještě neexistuje.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
V tomto kroku definujete, kde bude váš soubor uložen. Kód zkontroluje, zda adresář existuje, a pokud ne, vytvoří ho za vás. To zajistí, že později nenarazíte na žádné chyby „soubor nenalezen“.
## Krok 2: Vytvořte nový sešit a otevřete první sešit
Dále vytvoříme nový sešit a přistoupíme k prvnímu listu, kam přidáme pole se seznamem.
```csharp
// Vytvořte nový sešit.
Workbook workbook = new Workbook();
// Získejte první pracovní list.
Worksheet sheet = workbook.Worksheets[0];
```
Sešit je v podstatě váš soubor Excel. Zde vytváříme nový sešit a přistupujeme k prvnímu listu, kam umístíme pole se seznamem. Berte to jako vytvoření prázdného plátna, kde budete malovat ovládací prvky.
## Krok 3: Zadejte data pro pole seznamu
Než přidáme pole se seznamem, musíme vyplnit některá data, na která bude pole se seznamem odkazovat.
```csharp
// Získejte kolekci buněk listu.
Cells cells = sheet.Cells;
// Zadejte hodnotu štítku.
cells["B3"].PutValue("Choose Dept:");
// Nastavte štítek na tučné.
cells["B3"].GetStyle().Font.IsBold = true;
// Zadejte hodnoty pro pole se seznamem.
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
Zde přidáváme nějaký text do listu. Do buňky B3 je umístěn štítek "Vybrat oddělení:" a jeho písmo je nastaveno na tučné. Do sloupce A vkládáme hodnoty, které budou sloužit jako vstupní rozsah pro pole se seznamem představující různá oddělení. Tento vstupní rozsah je to, z čeho budou uživatelé vybírat při interakci se seznamem.
## Krok 4: Přidejte pole seznamu do listu
Nyní, když jsme nastavili data, přidejte samotný ovládací prvek seznamu.
```csharp
// Přidat nový seznam.
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
Tento kód přidá seznam do listu. Parametry definují pozici a velikost seznamu. Pole se seznamem je umístěno na řádku 2, sloupci 0 s šířkou 122 a výškou 100. Toto jsou souřadnice a velikost, které určují, kde se bude seznam v listu zobrazovat.
## Krok 5: Nastavte vlastnosti seznamu
Dále nastavíme různé vlastnosti pro seznam, aby byl plně funkční.
```csharp
// Nastavte typ umístění.
listBox.Placement = PlacementType.FreeFloating;
// Nastavte propojenou buňku.
listBox.LinkedCell = "A1";
// Nastavte vstupní rozsah.
listBox.InputRange = "A2:A7";
// Nastavte typ výběru.
listBox.SelectionType = SelectionType.Single;
// Nastavte pole seznamu s 3D stínováním.
listBox.Shadow = true;
```
- PlacementType.FreeFloating: Tato vlastnost zajišťuje, že seznam zůstane na své pozici bez ohledu na to, jak je list upraven.
- LinkedCell: Nastaví buňku (v tomto případě A1), kde se zobrazí vybraná hodnota ze seznamu.
- InputRange: Toto říká seznamu, kde má hledat svůj seznam možností (A2 až A7, které jsme nastavili dříve).
- SelectionType.Single: Toto omezuje uživatele na výběr pouze jedné položky ze seznamu.
- Stín: Efekt stínu dává seznamu více trojrozměrný vzhled, takže je vizuálně přitažlivý.
## Krok 6: Uložte soubor Excel
Nakonec uložme náš sešit se začleněným seznamem.
```csharp
// Uložte sešit.
workbook.Save(dataDir + "book1.out.xls");
```
Tento řádek kódu uloží sešit do adresáře, který jsme nastavili dříve. Soubor se jmenuje „book1.out.xls“, ale můžete si vybrat jakýkoli název, který vyhovuje vašemu projektu.
## Závěr
A tady to máte! Úspěšně jste přidali seznam do listu aplikace Excel pomocí Aspose.Cells for .NET. Pomocí několika řádků kódu jsme vytvořili plně funkční seznam, díky kterému je list interaktivnější a dynamičtější. Tento tutoriál by vám měl poskytnout pevný základ pro prozkoumání dalších ovládacích prvků a funkcí v Aspose.Cells pro .NET. Pokračujte v experimentování a brzy si osvojíte rozsáhlé funkce knihovny!
## FAQ
### Mohu povolit více výběrů v seznamu?  
 Ano, můžete změnit`SelectionType` na`SelectionType.Multi` umožňující vícenásobný výběr.
### Mohu změnit vzhled pole se seznamem?  
Absolutně! Aspose.Cells umožňuje přizpůsobit vzhled seznamu, včetně jeho velikosti, písma a dokonce i barvy.
### Co když budu později potřebovat odstranit pole se seznamem?  
 Můžete přistupovat k seznamu a odstranit jej z`Shapes` sběr pomocí`sheet.Shapes.RemoveAt(index)`.
### Mohu propojit seznam s jinou buňkou?  
 Ano, stačí změnit`LinkedCell` vlastnost do jakékoli jiné buňky, kde chcete zobrazit vybranou hodnotu.
### Jak přidám další položky do seznamu?  
Stačí aktualizovat vstupní rozsah vložením více hodnot do určených buněk a seznam se automaticky aktualizuje.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
