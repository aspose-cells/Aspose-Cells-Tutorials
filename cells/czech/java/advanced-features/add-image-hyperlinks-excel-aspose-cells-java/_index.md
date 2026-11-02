---
date: '2026-09-02'
description: Zjistěte, jak vytvořit klikací obrázek v sešitech Excel pomocí Aspose.Cells
  for Java, přidáním hyperlinks do obrázků pro interaktivní tabulky.
keywords:
- create clickable image
- add image hyperlink
- add hyperlink to picture
- interactive excel spreadsheet
- how to add hyperlink
lastmod: '2026-09-02'
og_description: Zjistěte, jak vytvořit klikací obrázek v sešitech Excel pomocí Aspose.Cells
  for Java, přidáním hyperlinks, screen tips a optimizing performance během několika
  řádků kódu.
og_image_alt: 'Developer guide: create clickable image Excel using Aspose.Cells for
  Java'
og_title: Vytvořte klikací obrázek v Excelu pomocí Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  headline: Create clickable image Excel using Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  name: Create clickable image Excel using Aspose.Cells for Java
  steps:
  - name: prepare your workbook
    text: We start by creating a new workbook and selecting the first sheet.
  - name: insert a label and adjust cell size
    text: Add a descriptive label and give the cell enough space for the picture.
  - name: add the image
    text: '`Picture` represents an image object placed on a worksheet. *Tip*: Replace
      `"path/to/aspose-logo.jpg"` with the actual path to your image file.'
  - name: configure placement and add the hyperlink
    text: '`Hyperlink` defines a link associated with a cell, shape, or picture, enabling
      navigation when clicked.'
  - name: set a screen tip and save the workbook
    text: Provide a helpful tooltip and write the workbook to disk.
  type: HowTo
- questions:
  - answer: Aspose.Cells for Java.
    question: What library is required?
  - answer: Yes – the API works with both .xls and .xlsx.
    question: Can I use .xlsx files?
  - answer: A trial works for evaluation; a permanent license is required for production.
    question: Do I need a license?
  - answer: About 20 lines to add a clickable image.
    question: How many lines of code?
  - answer: Workbook objects are not thread‑safe; create separate instances per thread.
    question: Is it thread‑safe?
  type: FAQPage
tags:
- create clickable image
- Aspose.Cells
- Java Excel automation
title: Vytvořte klikací obrázek v Excelu pomocí Aspose.Cells for Java
url: /cs/java/advanced-features/add-image-hyperlinks-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření klikatelného obrázku v Excelu pomocí Aspose.Cells pro Java

## Úvod

Pokud chcete **vytvořit klikatelné obrázkové Excel** sešity, které uživatelům umožní jedním kliknutím přejít na webové stránky, dokumenty nebo jiné zdroje, jste na správném místě. V tomto tutoriálu si ukážeme, jak Aspose.Cells pro Java umožňuje **přidat hypertextový odkaz k obrázku v Excelu**, nastavit tipy obrazovky a udržet vaše tabulky jak krásné, tak funkční.

### Co se naučíte
- Inicializace sešitu Aspose.Cells v Javě.  
- Vložení obrázku a jeho převod na klikací hypertextový odkaz.  
- Klíčové metody jako `addHyperlink`, `setPlacement` a `setScreenTip`.  
- Nejlepší postupy pro výkon a licencování.

## Rychlé odpovědi
- **Jaká knihovna je vyžadována?** Aspose.Cells pro Java.  
- **Mohu používat soubory .xlsx?** Ano – API funguje jak s .xls, tak s .xlsx.  
- **Potřebuji licenci?** Zkušební verze funguje pro hodnocení; pro produkci je vyžadována trvalá licence.  
- **Kolik řádků kódu?** Přibližně 20 řádků pro přidání klikatelného obrázku.  
- **Je to thread‑safe?** Objekt Workbook není thread‑safe; vytvářejte samostatné instance pro každý vlákno.  
- **Mohu přidat tip obrazovky v Excelu?** Ano – použijte `Hyperlink.setScreenTip()` k zobrazení užitečného textu při najetí.

## Jak vytvořit klikatelný obrázek v Excelu pomocí Aspose.Cells pro Java

Klikatelný obrázkový Excel sešit vytvoříte načtením nebo vytvořením `Workbook`, vložením objektu `Picture`, připojením `Hyperlink` k tomuto obrázku, volitelným nastavením tipu obrazovky a nakonec uložením souboru. API zpracovává veškeré nízkoúrovňové Excel XML, takže napíšete jen několik jednoduchých řádků kódu v Javě.

### Požadavky
Před začátkem se ujistěte, že máte:

- **Aspose.Cells pro Java** (v25.3 nebo novější).  
- **JDK 8+** nainstalováno.  
- IDE (IntelliJ IDEA, Eclipse nebo NetBeans) a Maven nebo Gradle pro správu závislostí.  

### Požadované knihovny
Add Aspose.Cells to your project:

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
- Dočasná licence: Požádejte přes [Temporary License page](https://purchase.aspose.com/temporary-license/).  
- Koupě: Pro dlouhodobé používání navštivte [Aspose Purchase](https://purchase.aspose.com/buy).

### Základní inicializace
Třída `Workbook` představuje celý Excel soubor v paměti. Vytvoříte její instanci a poté získáte odkaz na první list. `Worksheet` představuje jednotlivý list v sešitu.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

// Initialize workbook
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

## Postupná implementace

### Krok 1: připravte sešit
Začneme vytvořením nového sešitu a výběrem prvního listu.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

### Krok 2: vložte popisek a upravte velikost buňky
Přidejte popisný popisek a dejte buňce dostatek místa pro obrázek.

```java
worksheet.getCells().get("C2").setValue("Image Hyperlink");
worksheet.getCells().setRowHeight(3, 100); // Set row height for C4
worksheet.getCells().setColumnWidth(2, 21); // Adjust column width for C column
```  

### Krok 3: přidejte obrázek
`Picture` představuje objekt obrázku umístěný na listu.

```java
int index = worksheet.getPictures().add(3, 2, "path/to/aspose-logo.jpg");
```  
*Tip*: Nahraďte `"path/to/aspose-logo.jpg"` skutečnou cestou k vašemu souboru obrázku.

### Krok 4: nakonfigurujte umístění a přidejte hypertextový odkaz
`Hyperlink` definuje odkaz spojený s buňkou, tvarem nebo obrázkem, který umožňuje navigaci po kliknutí.

```java
import com.aspose.cells.Picture;
import com.aspose.cells.PlacementType;

Picture pic = worksheet.getPictures().get(index);
pic.setPlacement(PlacementType.FREE_FLOATING);

// Add hyperlink to the picture
pic.addHyperlink("http://www.aspose.com/");
```  

### Krok 5: nastavte tip obrazovky a uložte sešit
Poskytněte užitečný tip a zapište sešit na disk.

```java
import com.aspose.cells.Hyperlink;

Hyperlink hlink = pic.getHyperlink();
hlink.setScreenTip("Click to go to Aspose site");

workbook.save("AIHyperlinks_out.xls");
```  

## Proč přidat hypertextový odkaz k obrázku v Excelu?

Vložení klikatelného obrázku vám umožní proměnit brandingové prvky, ikony nebo diagramy na přímé navigační body, čímž snížíte počet kliknutí potřebných k dosažení souvisejícího obsahu. Tento přístup zvyšuje efektivitu uživatelů v marketingových přehledech, technických manuálech a výukových pracovních listech.

## Jak přidat tip obrazovky v Excelu

Tip obrazovky přidáte voláním `hyperlink.setScreenTip("Your tip here")` na objektu `Hyperlink` připojeném k obrázku. Tip se zobrazí, když kurzor přejede nad obrázkem, a poskytne uživatelům kontextové vedení bez zaplnění listu.

## Tipy pro řešení problémů
- **Chyby cesty k obrázku** – zkontrolujte umístění souboru a ujistěte se, že aplikace má oprávnění ke čtení.  
- **Licence není použita** – pokud zkušební verze vyprší, hypertextové odkazy mohou přestat fungovat; použijte platnou licenci pomocí `License.setLicense`.  
- **Hypertextový odkaz není klikací** – ověřte, že `PlacementType` obrázku je nastaven na `FREE_FLOATING`.

## Praktické aplikace
Vkládání klikatelných obrázků je užitečné v mnoha scénářích:

1. **Marketingové zprávy** – propojte loga značek na stránky produktů.  
2. **Technická dokumentace** – připojte diagramy, které otevřou podrobné schémata.  
3. **Výukové pracovní listy** – proměňte ikony na zkratky pro doplňková videa.  
4. **Projektové přehledy** – nechte ikony stavu otevírat související sledovače úkolů.

## Úvahy o výkonu
- Udržujte velikost souboru obrázku rozumnou; velké obrázky zvyšují paměťovou náročnost sešitu.  
- Uvolněte nepoužívané objekty (`workbook.dispose()`) při zpracování mnoha souborů ve smyčce.  
- Aktualizujte na nejnovější verzi Aspose.Cells pro zlepšení výkonu a opravy chyb.

## Závěr
Nyní víte, jak přidat hypertextový odkaz k obrázkům v Excelu pomocí Aspose.Cells pro Java, což vám umožní **vytvořit klikatelné obrázkové Excel** sešity, které jsou bohatší a interaktivnější. Experimentujte s různými URL, tipy obrazovky a umístěním obrázků, aby vyhovovaly vašim potřebám reportování. Dále můžete zkoumat přidávání hypertextových odkazů k tvarům nebo automatizaci hromadného vkládání obrázků do více listů.

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
**A:** Časté příčiny zahrnují nesprávný řetězec URL, chybějící prefix `http://`/`https://` nebo nelicencovanou zkušební verzi, která zakazuje některé funkce.

## Další zdroje
- **Dokumentace:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Stáhnout:** [Aspose Cells Release](https://releases.aspose.com/cells/java/)  
- **Koupě a zkušební verze:** Navštivte [Aspose Purchase](https://purchase.aspose.com/buy) nebo [Temporary License Page](https://purchase.aspose.com/temporary-license/) pro možnosti licencování.  
- **Fórum podpory:** Pro pomoc navštivte [Aspose Support Forum](https://forum.aspose.com/c/cells/9).

---

**Poslední aktualizace:** 2026-09-02  
**Testováno s:** Aspose.Cells pro Java 25.3  
**Autor:** Aspose

## Související tutoriály

- [Jak vytvořit hypertextové odkazy v Excelu pomocí Aspose.Cells pro Java – průvodce krok za krokem](/cells/java/advanced-features/create-hyperlinks-excel-aspose-cells-java/)
- [Jak stylovat buňky v Excelu a přidávat hypertextové odkazy pomocí Aspose.Cells pro Java](/cells/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Přidání obrázku do komentáře v Excelu pomocí Aspose.Cells pro Java: kompletní průvodce](/cells/java/comments-annotations/add-image-excel-comment-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}