---
"date": "2025-04-05"
"description": "Naučte se automatizovat extrakci a ukládání objektů OLE ze souborů aplikace Excel pomocí Aspose.Cells pro .NET a vylepšit tak svůj pracovní postup zpracování dat."
"title": "Automatizace extrakce a ukládání objektů OLE v Excelu pomocí Aspose.Cells pro .NET"
"url": "/cs/net/ole-objects-embedded-content/excel-automation-extract-save-ole-aspose-cells-dotnet/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Automatizujte extrakci a ukládání objektů OLE v Excelu pomocí Aspose.Cells pro .NET

## Zavedení

Chcete zefektivnit svůj pracovní postup automatizací extrakce vložených objektů v souborech Excelu? Ať už jste vývojář nebo datový analytik, využití... **Aspose.Cells pro .NET** může výrazně snížit manuální úsilí a chyby. Tento tutoriál vás provede extrakcí a uložením objektů OLE (Object Linking and Embedding) ze sešitů aplikace Excel na základě jejich formátů souborů.

### Co se naučíte:
- Otevření a načtení sešitu aplikace Excel pomocí Aspose.Cells.
- Přístup ke kolekci objektů OLE v listu.
- Extrakce a ukládání objektů OLE podle jejich specifických formátů.

Pojďme si nastavit prostředí a implementovat tuto efektivní funkci!

## Předpoklady

Než začneme, ujistěte se, že máte splněny následující předpoklady:

### Požadované knihovny:
- **Aspose.Cells pro .NET** - Nezbytné pro práci s excelovými soubory v prostředí .NET.

### Nastavení prostředí:
- Vývojové prostředí jako Visual Studio nebo jakékoli kompatibilní IDE s podporou C# a .NET.

### Předpoklady znalostí:
- Základní znalost programování v C#.
- Znalost frameworku .NET, zejména operací se soubory.

## Nastavení Aspose.Cells pro .NET

Chcete-li používat Aspose.Cells pro .NET, musíte si ho nainstalovat do svého projektu. Postupujte takto:

### Pokyny k instalaci:

**Použití .NET CLI:**
```bash
dotnet add package Aspose.Cells
```

**Používání Správce balíčků:**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

### Získání licence:
- **Bezplatná zkušební verze:** Začněte s 30denní bezplatnou zkušební verzí a prozkoumejte všechny funkce.
- **Dočasná licence:** Požádejte o dočasnou licenci pro prodloužený přístup.
- **Nákup:** Pokud tento nástroj splňuje vaše potřeby, kupte si plnou licenci.

Po instalaci inicializujte Aspose.Cells ve vašem projektu takto:

```csharp
using Aspose.Cells;

// Inicializace knihovny
Aspose.Cells.License license = new Aspose.Cells.License();
license.SetLicense("Path to License File");
```

## Průvodce implementací

### Funkce 1: Otevřít a načíst sešit

Načtěme si sešit aplikace Excel ze zadaného adresáře.

#### Postupná implementace:

**Definovat zdrojový adresář:**
```csharp
string sourceDir = "YOUR_SOURCE_DIRECTORY";
```

**Vytvořit instanci sešitu:**
```csharp
Workbook workbook = new Workbook(sourceDir + "sampleExtractOLEObjects.xlsx");
```
Tento krok načte váš soubor Excel do `Workbook` objekt, což vám umožňuje programově manipulovat s jeho obsahem.

### Funkce 2: Přístup ke kolekci OleObject v pracovním listu

Nyní zpřístupněte objekty OLE vložené do prvního listu sešitu.

#### Postupná implementace:

**Přístup k prvnímu pracovnímu listu:**
```csharp
OleObjectCollection oles = workbook.Worksheets[0].OleObjects;
```
Tento úryvek kódu načte všechny objekty OLE ze zadaného listu pro další zpracování.

### Funkce 3: Extrakce a uložení objektů OLE na základě formátu

Dále iterujte každým objektem OLE, abyste extrahovali jeho data a uložili je podle jeho formátu.

#### Postupná implementace:

**Iterovat přes objekty OLE:**
```csharp
using System.IO;

for (int i = 0; i < oles.Count; i++)
{
    OleObject ole = oles[i];
    byte[] oleData = ole.ObjectData;
    string fileName = outputDir + "outputExtractOLEObjects" + (i+1) + ".";

    switch (ole.FileFormatType)
    {
        case FileFormatType.Doc:
            fileName += "doc";
            break;
        case FileFormatType.Docx:
            fileName += "docx";
            break;
        case FileFormatType.Excel97To2003:
            fileName += "xls";
            break;
        case FileFormatType.Xlsx:
            // Speciální manipulace s formáty XLSX
            using (MemoryStream ms = new MemoryStream())
            {
                ms.Write(ole.ObjectData, 0, ole.ObjectData.Length);
                Workbook oleBook = new Workbook(ms);
                oleBook.Settings.IsHidden = false;

                ms.SetLength(0); // Vyčistit stream
                oleBook.Save(ms, SaveFormat.Xlsx);

                ms.Position = 0;
                byte[] bts = new byte[ms.Length];
                ms.Read(bts, 0, (int)ms.Length);
                oleData = bts;
            }
            fileName += "xlsx";
            break;
        case FileFormatType.Ppt:
            fileName += "ppt";
            break;
        case FileFormatType.Pdf:
            fileName += "pdf";
            break;
        case FileFormatType.Unknown:
            Guid g = new Guid(ole.ClassIdentifier);
            if (g.ToString() == "b801ca65-a1fc-11d0-85ad-444553540000")
            {
                fileName += "pdf";
            }
            else
            {
                fileName += "jpg";
            }                      
            break;
        default:
            // Zpracování jiných formátů nebo vyvolání výjimky
            break;
    }

    File.WriteAllBytes(fileName, oleData);
}
```
Tato část ukazuje, jak dynamicky zpracovávat různé formáty souborů a jak je správně ukládat.

## Praktické aplikace

Zde je několik reálných případů použití pro extrakci objektů OLE ze souborů aplikace Excel:
1. **Automatizované reportování dat:** Automaticky extrahovat vložené dokumenty nebo obrázky jako součást procesu vytváření datových sestav.
2. **Systémy pro archivaci dat:** Archivujte vložený obsah v tabulkách pro účely dodržování předpisů.
3. **Integrace se systémy pro správu dokumentů:** Bezproblémově integrujte extrahované objekty OLE do jiných platforem pro správu dokumentů.

## Úvahy o výkonu

Pro zajištění optimálního výkonu při práci s Aspose.Cells:
- **Optimalizace využití paměti:** Použití `MemoryStream` moudře efektivně spravovat paměť během operací se soubory.
- **Dávkové zpracování:** Pokud pracujete s velkými datovými sadami, zpracovávejte soubory dávkově, abyste zabránili nadměrnému využití zdrojů.
- **Nejlepší postupy:** Pravidelně aktualizujte své knihovny .NET a využívejte nejnovější funkce Aspose.Cells pro lepší výkon.

## Závěr

Dodržováním tohoto návodu jste se naučili, jak automatizovat extrakci objektů OLE ze sešitů aplikace Excel pomocí Aspose.Cells pro .NET. Tato dovednost zvyšuje efektivitu zpracování dat a snižuje počet chyb při ručním zpracování ve vašich pracovních postupech.

### Další kroky:
- Experimentujte s různými formáty souborů.
- Prozkoumejte další funkce, které Aspose.Cells nabízí, a zefektivníte tak své úkoly.

Jste připraveni to vyzkoušet? Začněte tyto techniky implementovat do svých projektů ještě dnes!

## Sekce Často kladených otázek

1. **Jak mám zpracovat nepodporované formáty objektů OLE?**
   - Pro neznámé nebo nepodporované formáty použijte `FileFormatType.Unknown` případ a implementovat vlastní logiku dle potřeby.

2. **Dokáže Aspose.Cells efektivně zpracovávat velké soubory aplikace Excel?**
   - Ano, je optimalizováno pro výkon. Pro zachování efektivity zvažte dávkové zpracování velmi velkých datových sad.

3. **Co když je formát extrahovaného souboru nesprávný?**
   - Zkontrolujte znovu `FileFormatType` ve vašem příkazu switch a zajistěte správné mapování formátů.

4. **Je Aspose.Cells .NET zdarma k použití?**
   - Můžete začít s 30denní bezplatnou zkušební verzí a zakoupit si licence pro delší používání.

5. **Jak integruji extrahované objekty OLE do jiných systémů?**
   - Pro přesun souborů do požadovaného systému použijte standardní operace se soubory I/O nebo integrační nástroje.

## Zdroje
- **Dokumentace:** [Dokumentace k Aspose.Cells .NET](https://reference.aspose.com/cells/net/)
- **Stáhnout:** [Nejnovější vydání](https://releases.aspose.com/cells/net/)
- **Licence k zakoupení:** [Koupit nyní](https://purchase.aspose.com/buy)
- **Bezplatná zkušební verze:** [Začít](https://releases.aspose.com/cells/net/)
- **Dočasná licence:** [Žádost zde](https://purchase.aspose.com/temporary-license/)
- **Fórum podpory:** [Podpora Aspose](https://forum.aspose.com/c/cells/9)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}