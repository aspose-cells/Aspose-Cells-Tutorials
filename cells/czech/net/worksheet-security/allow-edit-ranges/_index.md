---
title: Povolit uživatelům upravovat rozsahy v listu pomocí Aspose.Cells
linktitle: Povolit uživatelům upravovat rozsahy v listu pomocí Aspose.Cells
second_title: Aspose.Cells .NET Excel Processing API
description: Naučte se vytvářet upravitelné rozsahy v listech aplikace Excel pomocí Aspose.Cells pro .NET, což umožňuje upravovat konkrétní buňky a zbytek je možné zabezpečit ochranou listu.
weight: 10
url: /cs/net/worksheet-security/allow-edit-ranges/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Povolit uživatelům upravovat rozsahy v listu pomocí Aspose.Cells

## Zavedení
Excelové dokumenty často obsahují citlivá data nebo strukturovaný obsah, který chcete chránit před nechtěnými úpravami. Mohou však existovat určité buňky nebo rozsahy, které chcete upravit pro určité uživatele. To je místo, kde Aspose.Cells for .NET vstupuje do hry jako výkonný nástroj, který vám umožňuje chránit celý list a přitom stále udělovat oprávnění k úpravám určeným rozsahům. Představte si sdílení rozpočtové tabulky, kde lze upravovat pouze určité buňky a ostatní zůstávají v bezpečí – Aspose.Cells to usnadňuje a zefektivňuje.
## Předpoklady
Než se ponoříte do kódovací části, ujistěte se, že máte vše, co potřebujete:
-  Aspose.Cells for .NET: Ujistěte se, že jste nainstalovali knihovnu Aspose.Cells for .NET. Můžete si jej stáhnout[zde](https://releases.aspose.com/cells/net/).
- Vývojové prostředí: Visual Studio nebo jakékoli IDE kompatibilní s C#.
- .NET Framework: Verze 4.0 nebo novější.
- Licence: Zvažte získání licence, abyste se vyhnuli omezením zkušební verze. Můžete získat a[dočasná licence zde](https://purchase.aspose.com/temporary-license/).
## Importujte balíčky
Nezapomeňte na začátek kódu zahrnout potřebný jmenný prostor Aspose.Cells:
```csharp
using System.IO;
using Aspose.Cells;
```
Tím zajistíte, že budete mít přístup ke všem třídám a metodám potřebným k nastavení chráněných rozsahů v souborech aplikace Excel.
Nyní, když jsou připraveny základy, pojďme si projít kód podrobně, krok za krokem.
## Krok 1: Nastavte adresář
Než začnete pracovat se soubory, musíte nastavit adresář, kam budete soubor Excelu ukládat. Díky tomu budou vaše soubory dobře uspořádány a bezpečně uloženy.
```csharp
// Definujte cestu k adresáři dokumentů
string dataDir = "Your Document Directory";
// Zkontrolujte, zda adresář existuje, pokud ne, vytvořte jej
bool isExists = Directory.Exists(dataDir);
if (!isExists)
{
    Directory.CreateDirectory(dataDir);
}
```
Tato část kódu zajišťuje, že váš adresář je připraven pro operace se soubory. Berte to jako položení základů pro vše, co následuje.
## Krok 2: Inicializujte sešit a pracovní list
Nyní pojďme kupředu vytvořením nového sešitu a přístupem k jeho výchozímu listu.
```csharp
// Inicializujte nový sešit
Workbook book = new Workbook();
// Otevřete první list v sešitu
Worksheet sheet = book.Worksheets[0];
```
Zde inicializujeme sešit aplikace Excel a vybíráme první list v něm. Tento pracovní list bude plátnem, kde použijeme naše nastavení ochrany a definujeme upravitelné rozsahy.
## Krok 3: Otevřete kolekci Povolit úpravy rozsahů
 Aspose.Cells má funkci nazvanou`AllowEditRanges`, což je kolekce rozsahů, které lze upravovat, i když je list chráněný.
```csharp
// Otevřete kolekci Povolit úpravy rozsahů
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```
Tento řádek nastavuje přístup ke speciální kolekci rozsahů, které bude možné upravovat. Představte si to jako „VIP“ oblast ve vašem pracovním listu, kde je povoleno obejít ochranu pouze u konkrétních rozsahů.
## Krok 4: Definujte a vytvořte chráněný rozsah
Nyní definujme a vytvořte chráněný rozsah v našem listu. Určíme počáteční a koncovou buňku pro tento rozsah.
```csharp
// Definujte proměnnou ProtectedRange
ProtectedRange protectedRange;
// Přidejte do kolekce nový rozsah s konkrétním názvem a pozicemi buněk
int idx = allowRanges.Add("EditableRange", 1, 1, 3, 3);
protectedRange = allowRanges[idx];
```
V tomto bloku kódu:
- `EditableRange` je název přiřazený rozsahu.
- Čísla (1, 1, 3, 3) definují souřadnice rozsahu, což znamená, že začíná od buňky B2 (řádek 1, sloupec 1) do buňky D4 (řádek 3, sloupec 3).
## Krok 5: Nastavte heslo pro chráněný rozsah
Pro zvýšení bezpečnosti můžete nastavit heslo pro chráněný rozsah. Tento krok přidává další vrstvu ochrany, aby bylo zajištěno, že rozsah mohou upravovat pouze oprávnění uživatelé.
```csharp
// Nastavte heslo pro upravitelný rozsah
protectedRange.Password = "123";
```
Zde jsme přidali heslo (`"123"`) do chráněného rozsahu. Tento požadavek na heslo poskytuje další úroveň kontroly nad tím, kdo může provádět změny.
## Krok 6: Chraňte pracovní list
Po zavedení našeho upravitelného rozsahu je dalším krokem ochrana celého listu. Toto nastavení ochrany zajistí, že všechny buňky mimo definovaný rozsah budou uzamčeny a nebude možné je upravovat.
```csharp
// Použít ochranu listu, aby všechny ostatní buňky neupravitelné
sheet.Protect(ProtectionType.All);
```
 The`Protect`metoda uzamkne celý list, kromě rozsahů, které jsme definovali jako upravitelné. Tento krok v podstatě vytváří bezpečné prostředí „pouze pro čtení“ s přístupem ke konkrétním buňkám podle potřeby.
## Krok 7: Uložte sešit
Posledním krokem je uložení sešitu, aby byla vaše nastavení použita a uložena.
```csharp
// Uložte soubor Excel do zadaného adresáře
book.Save(dataDir + "protectedrange.out.xls");
```
V tomto kroku ukládáme náš sešit jako „protectedrange.out.xls“ do adresáře, který jsme nastavili v kroku 1. Nyní máte plně funkční, zabezpečený soubor Excel, kde lze upravovat pouze určité rozsahy!
## Závěr
Aspose.Cells for .NET poskytuje vynikající způsob, jak spravovat ochranu a oprávnění v rámci souborů aplikace Excel. Vytvořením upravitelných rozsahů můžete zabezpečit své listy a zároveň umožnit, aby určité oblasti zůstaly přístupné. Tato funkce je užitečná zejména pro dokumenty pro spolupráci, kde by mělo být otevřeno pro úpravy pouze několik buněk, zatímco ostatní zůstanou zamčené.
## FAQ
### Mohu do listu přidat více upravitelných rozsahů?
Ano, můžete přidat více rozsahů pouhým opakováním`allowRanges.Add()` metoda pro každý nový rozsah.
### Co když chci později odstranit chráněný rozsah?
 Použijte`allowRanges.RemoveAt()` metoda s indexem rozsahu, který chcete odstranit.
### Mohu nastavit různá hesla pro každý rozsah?
 Absolutně. Každý`ProtectedRange` může mít své vlastní jedinečné heslo, které vám poskytne podrobnou kontrolu.
### Co se stane, když ochráním list bez jakýchkoli upravitelných rozsahů?
Pokud nedefinujete upravitelné rozsahy, bude celý list po ochraně neupravitelný.
### Je chráněný rozsah viditelný pro ostatní uživatele?
Ne, ochrana je vnitřní. Uživatelé budou vyzváni k zadání hesla pouze v případě, že se pokusí upravit chráněnou oblast.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
