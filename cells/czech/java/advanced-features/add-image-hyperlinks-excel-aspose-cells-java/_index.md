---
date: '2026-02-16'
description: Naučte se, jak vytvořit klikatelné obrázky v Excelu pomocí Aspose.Cells
  pro Javu, přidávat hypertextové odkazy k obrázkům pro interaktivní tabulky.
keywords:
- image hyperlinks in Excel
- Aspose.Cells for Java
- interactive Excel spreadsheets
title: Vytvořte klikací obrázek v Excelu pomocí Aspose.Cells pro Java
url: /cs/java/advanced-features/add-image-hyperlinks-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořte kliknutelný obrázek v Excelu pomocí Aspose.Cells pro Java

## Úvod

Pokud chcete **vytvořit kliknutelný obrázek v Excelu** sešity, které uživatelům umožní přejít na webové stránky, dokumenty nebo jiné zdroje jediným kliknutím, jste na správném místě. V tomto tutoriálu si ukážeme, jak Aspose.Cells pro Java umožňuje **přidávat hypertextové odkazy do obrázků v Excelu**, konfigurovat tipy obrazovky a udržet vaše tabulky jak krásné, tak funkční.

### Co se naučíte
- Inicializace sešitu Aspose.Cells v Javě.  
- Vložení obrázku a jeho převod na kliknutelný hypertextový odkaz.  
- Klíčové metody jako `addHyperlink`, `setPlacement` a `setScreenTip`.  
- Nejlepší postupy pro výkon a licencování.

## Rychlé odpovědi
- **Jaká knihovna je vyžadována?** Aspose.Cells pro Java.  
- **Mohu použít soubory .xlsx?** Ano – API funguje jak s .xls, tak s .xlsx.  
- **Potřebuji licenci?** Zkušební verze funguje pro hodnocení; pro produkci je vyžadována trvalá licence.  
- **Kolik řádků kódu?** Přibližně 20 řádků pro přidání klikatelného obrázku.  
- **Je to thread‑safe?** Objekt Workbook není thread‑safe; vytvořte samostatné instance pro každý vlákno.  
- **Mohu přidat tip obrazovky v Excelu?** Ano – použijte `Hyperlink.setScreenTip()` pro zobrazení užitečného textu při najetí.

## Jak vytvořit kliknutelný obrázek v Excelu pomocí Aspose.Cells pro Java

### Požadavky
Než začnete, ujistěte se, že máte:

- **Aspose.Cells pro Java** (v25.3 nebo novější).  
- **JDK 8+** nainstalovaný.  
- IDE (IntelliJ IDEA, Eclipse nebo NetBeans) a Maven nebo Gradle pro správu závislostí.  

### Požadované knihovny
Přidejte Aspose.Cells do svého projektu:

**Maven**
```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```

**Gradle**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Získání licence
Aspose.Cells je komerční, ale můžete začít s bezplatnou zkušební verzí nebo požádat o dočasnou licenci:

- Bezplatná zkušební verze: Stáhněte z [Aspose Downloads](https://releases.aspose.com/cells/java/).  
- Dočasná licence: Požádejte na [Temporary License page](https://purchase.aspose.com/temporary-license/).  
- Nákup: Pro dlouhodobé používání navštivte [Aspose Purchase](https://purchase.aspose.com/buy).

### Základní inicializace
Vytvořte sešit a získejte první list:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

// Initialize workbook
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Postupná implementace

### Krok 1: Připravte svůj sešit
Začínáme vytvořením nového sešitu a výběrem prvního listu.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Krok 2: Vložte popisek a upravte velikost buňky
Přidejte popisný popisek a dejte buňce dostatek místa pro obrázek.

```java
worksheet.getCells().get("C2").setValue("Image Hyperlink");
worksheet.getCells().setRowHeight(3, 100); // Set row height for C4
worksheet.getCells().setColumnWidth(2, 21); // Adjust column width for C column
```

### Krok 3: Přidejte obrázek
Načtěte soubor s obrázkem a umístěte jej na list.

```java
int index = worksheet.getPictures().add(3, 2, "path/to/aspose-logo.jpg");
```
*Tip*: Nahraďte `"path/to/aspose-logo.jpg"` skutečnou cestou k vašemu souboru s obrázkem.

### Krok 4: Nakonfigurujte umístění a přidejte hypertextový odkaz
Udělejte obrázek volně plovoucím a připojte k němu hypertextový odkaz.

```java
import com.aspose.cells.Picture;
import com.aspose.cells.PlacementType;

Picture pic = worksheet.getPictures().get(index);
pic.setPlacement(PlacementType.FREE_FLOATING);

// Add hyperlink to the picture
pic.addHyperlink("http://www.aspose.com/");
```

### Krok 5: Nastavte tip obrazovky a uložte sešit
Poskytněte užitečný tooltip a zapište sešit na disk.

```java
import com.aspose.cells.Hyperlink;

Hyperlink hlink = pic.getHyperlink();
hlink.setScreenTip("Click to go to Aspose site");

workbook.save("AIHyperlinks_out.xls");
```

## Proč přidávat hypertextový odkaz do obrázku v Excelu?
Vložení klikatelného obrázku vám umožní převést brandingové prvky, ikony nebo diagramy na přímé navigační body. To zlepšuje uživatelský zážitek v marketingových dashboardech, technických manuálech a vzdělávacích pracovních listech tím, že snižuje počet kliknutí potřebných k dosažení souvisejícího obsahu.

## Jak přidat tip obrazovky v Excelu
Metoda `setScreenTip` vám umožní definovat text, který se zobrazí při najetí kurzoru na obrázek. To je ideální pro poskytování kontextu, například „Zobrazit podrobnosti o produktu“ nebo „Otevřít výukové video“.

## Tipy pro řešení problémů
- **Chyby cesty k obrázku** – dvojitě zkontrolujte umístění souboru a ujistěte se, že aplikace má oprávnění ke čtení.  
- **Licence nebyla použita** – pokud zkušební verze vyprší, hypertextové odkazy mohou přestat fungovat; použijte platnou licenci pomocí `License.setLicense`.  
- **Hypertextový odkaz není klikací** – ověřte, že `PlacementType` obrázku je nastaven na `FREE_FLOATING`.

## Praktické aplikace
Vkládání klikatelých obrázků je užitečné v mnoha scénářích:

1. **Marketingové zprávy** – propojte loga značek s produktovými stránkami.  
2. **Technická dokumentace** – připojte diagramy, které otevřou podrobné schémata.  
3. **Vzdělávací pracovní listy** – proměňte ikony v zkratky pro doplňková videa.  
4. **Projektové dashboardy** – nechte ikony stavu otevírat související sledovače úkolů.

## Úvahy o výkonu
- Udržujte velikost souborů obrázků na rozumné úrovni; velké obrázky zvyšují paměťovou náročnost sešitu.  
- Uvolněte nepoužívané objekty (`workbook.dispose()`) při zpracování mnoha souborů ve smyčce.  
- Aktualizujte na nejnovější verzi Aspose.Cells pro zlepšení výkonu a opravy chyb.

## Závěr
Nyní víte, **jak přidat hypertextový odkaz** k obrázkům v Excelu pomocí Aspose.Cells pro Java, což vám umožní **vytvořit kliknutelný obrázek v Excelu** sešity, které jsou bohatší a interaktivnější. Experimentujte s různými URL, tipy obrazovky a umístěním obrázků, aby vyhovovaly vašim potřebám reportování. Dále můžete zkoumat přidávání hypertextových odkazů k tvarům nebo automatizaci hromadného vkládání obrázků napříč více listy.

## Často kladené otázky

**Q:** Jaká je maximální velikost obrázku podporovaná Aspose.Cells pro Java?  
**A:** Neexistuje přísný limit, ale velmi velké obrázky mohou ovlivnit výkon a zvýšit velikost souboru.

**Q:** Mohu tuto funkci použít s .xlsx soubory?  
**A:** Ano, API funguje jak s formáty `.xls`, tak `.xlsx`.

**Q:** Jak mám zacházet s výjimkami při přidávání hypertextových odkazů?  
**A:** Zabalte kód do bloku try‑catch a zaznamenejte podrobnosti `Exception` pro diagnostiku problémů s cestou nebo licencí.

**Q:** Je možné po přidání odstranit hypertextový odkaz z obrázku?  
**A:** Ano – načtěte objekt `Picture` a zavolejte `pic.getHyperlink().remove()` nebo obrázek odstraňte ze sbírky.

**Q:** Proč můj hypertextový odkaz nemusí fungovat podle očekávání?  
**A:** Časté příčiny zahrnují nesprávný řetězec URL, chybějící prefix `http://`/`https://` nebo nelicencovanou zkušební verzi, která některé funkce zakazuje.

## Další zdroje
- **Dokumentace:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Stáhnout:** [Aspose Cells Release](https://releases.aspose.com/cells/java/)  
- **Nákup a zkušební verze:** Navštivte [Aspose Purchase](https://purchase.aspose.com/buy) nebo [Temporary License Page](https://purchase.aspose.com/temporary-license/) pro možnosti licencování.  
- **Fórum podpory:** Pro pomoc se podívejte na [Aspose Support Forum](https://forum.aspose.com/c/cells/9).

---

**Poslední aktualizace:** 2026-02-16  
**Testováno s:** Aspose.Cells pro Java 25.3  
**Autor:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}