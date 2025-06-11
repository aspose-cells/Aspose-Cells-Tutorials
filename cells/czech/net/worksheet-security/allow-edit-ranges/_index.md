---
"description": "Naučte se vytvářet upravitelné oblasti v listech aplikace Excel pomocí Aspose.Cells pro .NET, což umožňuje upravovat určité buňky a zároveň zabezpečuje zbytek pomocí ochrany listu."
"linktitle": "Povolit uživatelům upravovat rozsahy v pracovním listu pomocí Aspose.Cells"
"second_title": "Rozhraní API pro zpracování dat v Excelu Aspose.Cells v .NET"
"title": "Povolit uživatelům upravovat rozsahy v pracovním listu pomocí Aspose.Cells"
"url": "/cs/net/worksheet-security/allow-edit-ranges/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Povolit uživatelům upravovat rozsahy v pracovním listu pomocí Aspose.Cells

## Zavedení
Dokumenty aplikace Excel často obsahují citlivá data nebo strukturovaný obsah, který chcete chránit před nežádoucí úpravou. Mohou však existovat určité buňky nebo oblasti, které chcete pro určité uživatele nastavit jako upravitelné. A právě zde přichází na řadu Aspose.Cells pro .NET jako výkonný nástroj, který vám umožní chránit celý list a zároveň udělit oprávnění k úpravám určeným oblastem. Představte si sdílení tabulky rozpočtu, kde lze upravovat pouze určité buňky a ostatní zůstávají zabezpečené – Aspose.Cells to usnadňuje a zefektivňuje.
## Předpoklady
Než se pustíme do kódování, ujistěte se, že máte vše, co potřebujete:
- Aspose.Cells pro .NET: Ujistěte se, že máte nainstalovanou knihovnu Aspose.Cells pro .NET. Můžete si ji stáhnout [zde](https://releases.aspose.com/cells/net/).
- Vývojové prostředí: Visual Studio nebo jakékoli IDE kompatibilní s C#.
- .NET Framework: Verze 4.0 nebo novější.
- Licence: Zvažte pořízení licence, abyste se vyhnuli omezením zkušební doby. Můžete získat [dočasná licence zde](https://purchase.aspose.com/temporary-license/).
## Importovat balíčky
Nezapomeňte na začátek kódu zahrnout potřebný jmenný prostor Aspose.Cells:
```csharp
using System.IO;
using Aspose.Cells;
```
Tím zajistíte, že budete mít přístup ke všem třídám a metodám potřebným k nastavení chráněných rozsahů v souborech aplikace Excel.
Nyní, když máme základy připravené, pojďme si kód projít podrobně, krok za krokem.
## Krok 1: Nastavení adresáře
Než začnete pracovat se soubory, je třeba nastavit adresář, kam uložíte soubor Excel. Tím zajistíte, že vaše soubory budou dobře uspořádané a bezpečně uloženy.
```csharp
// Definujte cestu k adresáři s dokumenty
string dataDir = "Your Document Directory";
// Zkontrolujte, zda adresář existuje, pokud ne, vytvořte jej
bool isExists = Directory.Exists(dataDir);
if (!isExists)
{
    Directory.CreateDirectory(dataDir);
}
```
Tato část kódu zajišťuje, že váš adresář je připraven pro operace se soubory. Představte si to jako položení základů pro vše, co následuje.
## Krok 2: Inicializace sešitu a listu
Nyní se přesuňme k vytvoření nového sešitu a přístupu k jeho výchozímu listu.
```csharp
// Inicializace nového sešitu
Workbook book = new Workbook();
// Přístup k prvnímu listu v sešitu
Worksheet sheet = book.Worksheets[0];
```
Zde inicializujeme sešit aplikace Excel a vybíráme v něm první list. Tento list bude plátnem, na kterém použijeme nastavení ochrany a definujeme upravitelné rozsahy.
## Krok 3: Přístup ke kolekci Povolit rozsahy úprav
Aspose.Cells má funkci s názvem `AllowEditRanges`, což je kolekce rozsahů, které lze upravovat, a to i v případě, že je list chráněn.
```csharp
// Přístup ke kolekci Povolit rozsahy úprav
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```
Tento řádek nastavuje přístup ke speciální kolekci rozsahů, které bude možné upravovat. Představte si ji jako „VIP“ oblast ve vašem listu, kde je povoleno obejít ochranu pouze pro určité rozsahy.
## Krok 4: Definování a vytvoření chráněného rozsahu
Nyní si v našem listu definujme a vytvořme chráněný rozsah. Určíme počáteční a koncové buňky pro tento rozsah.
```csharp
// Definování proměnné ProtectedRange
ProtectedRange protectedRange;
// Přidat do kolekce nový rozsah s konkrétním názvem a pozicemi buněk
int idx = allowRanges.Add("EditableRange", 1, 1, 3, 3);
protectedRange = allowRanges[idx];
```
V tomto bloku kódu:
- `EditableRange` je název přiřazený rozsahu.
- Čísla (1, 1, 3, 3) definují souřadnice rozsahu, což znamená, že začíná od buňky B2 (řádek 1, sloupec 1) do buňky D4 (řádek 3, sloupec 3).
## Krok 5: Nastavení hesla pro chráněný rozsah
Pro zvýšení zabezpečení můžete pro chráněný rozsah nastavit heslo. Tento krok přidává další vrstvu ochrany, která zajišťuje, že rozsah mohou upravovat pouze oprávnění uživatelé.
```csharp
// Nastavte heslo pro upravitelný rozsah
protectedRange.Password = "123";
```
Zde jsme přidali heslo (`"123"`) do chráněného rozsahu. Tento požadavek na heslo poskytuje další úroveň kontroly nad tím, kdo může provádět změny.
## Krok 6: Ochrana pracovního listu
Po nastavení upravitelného rozsahu je dalším krokem ochrana celého listu. Toto nastavení ochrany zajistí, že všechny buňky mimo definovaný rozsah budou uzamčeny a nebude možné je upravovat.
```csharp
// Aplikovat ochranu listu tak, aby všechny ostatní buňky nebyly upravitelné
sheet.Protect(ProtectionType.All);
```
Ten/Ta/To `Protect` Metoda uzamkne celý list, s výjimkou oblastí, které jsme definovali jako upravitelné. Tento krok v podstatě vytváří bezpečné prostředí „pouze pro čtení“ s přístupem ke konkrétním buňkám dle potřeby.
## Krok 7: Uložení sešitu
Posledním krokem je uložení sešitu, aby se vaše nastavení použila a uložila.
```csharp
// Uložte soubor Excel do zadaného adresáře
book.Save(dataDir + "protectedrange.out.xls");
```
V tomto kroku ukládáme náš sešit jako „protectedrange.out.xls“ do adresáře, který jsme nastavili v kroku 1. Nyní máte plně funkční a zabezpečený soubor aplikace Excel, kde lze upravovat pouze určité rozsahy!
## Závěr
Aspose.Cells pro .NET nabízí vynikající způsob správy ochrany a oprávnění v rámci vašich souborů aplikace Excel. Vytvořením upravitelných rozsahů můžete zabezpečit své pracovní listy a zároveň ponechat přístup k určitým oblastem. Tato funkce je obzvláště užitečná pro dokumenty pro spolupráci, kde by pro úpravy mělo být otevřeno pouze několik buněk, zatímco ostatní by měly zůstat uzamčené.
## Často kladené otázky
### Mohu do listu přidat více upravitelných oblastí?
Ano, můžete přidat více rozsahů pouhým opakováním `allowRanges.Add()` metodu pro každý nový rozsah.
### Co když chci později odebrat chráněný rozsah?
Použijte `allowRanges.RemoveAt()` s indexem rozsahu, který chcete odstranit.
### Mohu pro každý rozsah nastavit různá hesla?
Rozhodně. Každý `ProtectedRange` může mít své vlastní jedinečné heslo, což vám poskytuje podrobnou kontrolu.
### Co se stane, když zamknu list bez upravitelných rozsahů?
Pokud nedefinujete upravitelné rozsahy, celý list po nastavení ochrany nebude upravitelný.
### Je chráněný rozsah viditelný pro ostatní uživatele?
Ne, ochrana je interní. Uživatelé budou vyzváni k zadání hesla pouze v případě, že se pokusí upravit chráněnou oblast.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}