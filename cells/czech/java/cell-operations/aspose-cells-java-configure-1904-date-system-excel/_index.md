---
date: '2026-02-22'
description: Naučte se, jak změnit datumový systém Excelu na 1904 pomocí Aspose.Cells
  pro Javu, nastavit formát data v Excelu a efektivně převést systém Excel 1904.
keywords:
- 1904 date system Excel
- Aspose.Cells Java configuration
- Excel workbook manipulation
title: Změna systému dat v Excelu na 1904 pomocí Aspose.Cells Java
url: /cs/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Změna systému dat v Excelu na 1904 pomocí Aspose.Cells Java

Správa historických dat v Excelu může být náročná, protože Excel podporuje dva různé systémy dat. **V tomto tutoriálu se naučíte, jak změnit systém dat v Excelu na formát 1904 pomocí Aspose.Cells pro Java**, což usnadňuje práci se starými daty. Provedeme vás inicializací sešitu, povolením systému dat 1904 a uložením změny.

## Rychlé odpovědi
- **Co dělá systém dat 1904?** Začíná počítat dny od 1. ledna 1904, posouvá všechny datumy o 1462 dní ve srovnání s výchozím systémem 1900.  
- **Proč použít Aspose.Cells ke změně systému dat?** Poskytuje jednoduché API, které funguje bez nainstalovaného Excelu a podporuje velké soubory.  
- **Které verze Javy jsou podporovány?** JDK 8 nebo novější.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro hodnocení; licence odstraňuje omezení používání.  
- **Mohu později převést zpět na systém 1900?** Ano, stačí nastavit `setDate1904(false)`.

## Co je v Excelu systém dat 1904?
Systém dat 1904 byl původně používán v raných verzích Excelu pro Macintosh. Počítá dny od 1. ledna 1904, což je užitečné pro kompatibilitu se staršími tabulkami a některými finančními modely.

## Proč změnit systém dat v Excelu pomocí Aspose.Cells?
- **Kompatibilita napříč platformami** – funguje na Windows, Linuxu i macOS.  
- **Není vyžadována instalace Excelu** – ideální pro zpracování na serveru.  
- **Vysoký výkon** – zpracovává velké sešity s minimální spotřebou paměti.  

## Předpoklady
- Java Development Kit (JDK) 8 nebo vyšší.  
- Maven nebo Gradle pro správu závislostí.  
- Základní znalost programování v Javě.  

## Nastavení Aspose.Cells pro Java

### Maven
Přidejte následující závislost do souboru `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Vložte tento řádek do souboru `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Získání licence
Aspose nabízí bezplatnou zkušební verzi, dočasnou licenci a plné komerční licence. Můžete začít s [bezplatnou zkušební verzí](https://releases.aspose.com/cells/java/) nebo získat dočasnou licenci na [stránce dočasné licence](https://purchase.aspose.com/temporary-license/).

## Změna systému dat v Excelu pomocí Aspose.Cells Java

Níže je podrobný návod, který skutečně **mění systém dat v Excelu**. Každý krok obsahuje krátké vysvětlení a následně přesný kód, který potřebujete.

### Krok 1: Inicializace a načtení sešitu
Nejprve vytvořte instanci `Workbook`, která odkazuje na váš existující soubor Excel.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Krok 2: Povolení systému dat 1904
Použijte nastavení sešitu k přepnutí systému dat.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Tip:** Můžete také později zavolat `setDate1904(false)`, pokud potřebujete vrátit změnu.

### Krok 3: Uložení upraveného sešitu
Nakonec zapište změny do nového souboru (nebo přepište originál).

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **Poznámka:** Výše uvedený kód používá název třídy `tWorkbook`, jak byl původně poskytnut. Ujistěte se, že tato překlep odpovídá konvencím pojmenování ve vašem projektu, nebo jej v případě potřeby opravte na `Workbook`.

## Nastavení data v Excelu programově (sekundární klíčové slovo)
Pokud potřebujete po změně systému upravit jednotlivé hodnoty buněk, můžete použít `Cells.get(i, j).putValue(Date)`, kde datum bude interpretováno podle aktivního systému dat.

## Převod systému Excel 1904 zpět na 1900 (sekundární klíčové slovo)
Pro návrat stačí zavolat:

```java
workbook.getSettings().setDate1904(false);
```

Poté znovu uložte sešit.

## Praktické aplikace
1. **Archivace dat** – Zachování starých časových razítek při migraci starých tabulek založených na Macu.  
2. **Cross‑platformové reportování** – Generování reportů, které lze otevřít jak na Windows, tak na macOS bez nesouladu dat.  
3. **Finanční modelování** – Zarovnání výpočtů dat s legacy finančními modely, které očekávají systém 1904.

## Úvahy o výkonu
- Omezte operace sešitu v jedné relaci, aby byla spotřeba paměti nízká.  
- Používejte ladění garbage‑collection v Javě pro velmi velké soubory.  

## Často kladené otázky

**Q: Jaký je rozdíl mezi systémy dat 1900 a 1904?**  
A: Systém 1900 začíná 1. ledna 1900, zatímco systém 1904 začíná 1. ledna 1904, což posouvá všechna data o 1462 dní.

**Q: Mohu změnit systém dat sešitu, který je aktuálně otevřený v Excelu?**  
A: Ano, ale nejprve musíte soubor v Excelu zavřít; jinak operace uložení selže.

**Q: Potřebuji licenci pro použití `setDate1904`?**  
A: Metoda funguje v bezplatné zkušební verzi, ale plná licence odstraňuje omezení hodnocení.

**Q: Je možné změnit systém dat pouze pro jeden list?**  
A: Ne, systém dat je nastavení na úrovni sešitu; platí pro všechny listy.

**Q: Jak mohu ověřit, že byl systém dat změněn?**  
A: Otevřete uložený soubor v Excelu, přejděte na **Soubor → Možnosti → Upřesnit** a zaškrtněte políčko **„Použít systém dat 1904“**.

## Závěr
Nyní víte, jak **změnit systém dat v Excelu** na 1904 pomocí Aspose.Cells pro Java, jak nastavit formáty dat v Excelu a jak se v případě potřeby vrátit zpět. Začleňte tyto úryvky do vašich datových zpracovatelských pipeline, abyste zajistili kompatibilitu dat napříč platformami.

---

**Poslední aktualizace:** 2026-02-22  
**Testováno s:** Aspose.Cells 25.3 pro Java  
**Autor:** Aspose  

**Zdroje**
- **Dokumentace:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Ke stažení:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Zakoupit licenci:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Bezplatná zkušební verze:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **Dočasná licence:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **Fórum podpory:** [Aspose Support](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}