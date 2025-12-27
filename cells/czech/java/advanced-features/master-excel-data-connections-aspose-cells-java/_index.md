---
date: '2025-12-27'
description: Naučte se, jak programově změnit zdroj dat v Excelu pomocí Aspose.Cells
  pro Javu, upravit datová připojení v Excelu a automatizovat svůj pracovní postup.
keywords:
- Excel data connections
- Aspose.Cells Java
- modify Excel data connections programmatically
title: Jak změnit zdroj dat v Excelu pomocí Aspose.Cells pro Javu
url: /cs/java/advanced-features/master-excel-data-connections-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Změna zdroje dat Excel pomocí Aspose.Cells pro Java

## Úvod
Máte potíže **change Excel data source** a upravit datové připojení v souborech Excel programově? Tento komplexní průvodce je určen vývojářům, kteří chtějí automatizovat své reportingové pipeline pomocí výkonné knihovny **Aspose.Cells for Java**. Provedeme vás načtením sešitu Excel, aktualizací jeho externího připojení a uložením změn – vše pomocí kódu v jazyce Java.

### Co se naučíte
- Jak nastavit Aspose.Cells pro Java v Maven nebo Gradle.  
- **Load Excel workbook Java** – načíst existující soubor do paměti.  
- **Modify Excel data connections** – aktualizovat název připojení, cestu ODC a SQL příkaz.  
- **Save Excel workbook Java** – zapsat aktualizovaný sešit zpět na disk.  

Ujistěte se, že máte vše potřebné, než se ponoříme dál.

## Rychlé odpovědi
- **Jaká je hlavní knihovna?** Aspose.Cells for Java.  
- **Která metoda načítá sešit?** `new Workbook(filePath)`.  
- **Jak aktualizuji řetězec připojení?** Použijte `DBConnection.setConnectionInfo(...)`.  
- **Mohu změnit cestu k souboru ODC?** Ano, pomocí `ExternalConnection.setOdcFile(...)`.  
- **Potřebuji licenci pro produkci?** Komerční licence odstraňuje omezení hodnocení.

## Předpoklady
Než začneme, ověřte, že máte následující:

### Požadované knihovny
Aspose.Cells for Java verze 25.3 nebo novější poskytuje API použité v tomto tutoriálu.

### Nastavení prostředí
- Nainstalovaný Java Development Kit (JDK).  
- IDE, jako je IntelliJ IDEA, Eclipse nebo NetBeans.

### Požadované znalosti
Znalost Javy, Maven nebo Gradle a základních konceptů SQL vám pomůže plynule sledovat tutoriál.

## Nastavení Aspose.Cells pro Java
Pro zahájení používání Aspose.Cells přidejte knihovnu do svého projektu:

**Nastavení Maven**  
Add the dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Nastavení Gradle**  
Insert the following line into `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Kroky získání licence
Aspose.Cells nabízí bezplatnou zkušební verzi, abyste si mohli knihovnu vyzkoušet před zakoupením:

- Navštivte [free trial page](https://releases.aspose.com/cells/java/) a stáhněte evaluační balíček.  
- Pro plnohodnotné použití zakupte licenci na [purchase portal](https://purchase.aspose.com/buy).  
- Potřebujete dočasný přístup? Požádejte o [temporary license](https://purchase.aspose.com/temporary-license/).

Jakmile je knihovna odkazována a licencována, jste připraveni kódovat.

## Průvodce implementací

### Funkce 1: Načtení sešitu ze souboru
**Co tento krok dělá?** Ukazuje, jak **load Excel workbook Java**, abyste mohli pracovat s jeho datovými připojeními.

#### Krok‑za‑krokem instrukce
**Definujte svůj datový adresář** – sdělte programu, kde se nachází zdrojový soubor:

```java
String dataDir = "YOUR_DATA_DIRECTORY";
```
Ujistěte se, že `DataConnection.xlsx` existuje v tomto adresáři.

**Načtěte sešit** – vytvořte instanci objektu `Workbook`:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook(dataDir + "DataConnection.xlsx");
```
Instance `Workbook` nyní představuje váš Excel soubor v paměti.

### Funkce 2: Úprava datového připojení v sešitu
**Proč upravovat?** Aktualizace externího připojení vám umožní **change Excel data source** bez ručního otevření souboru.

#### Krok‑za‑krokem instrukce
**Přístup k datovému připojení** – získejte první připojení (pro více můžete použít smyčku):

```java
import com.aspose.cells.DBConnection;
import com.aspose.cells.ExternalConnection;
import com.aspose.cells.OLEDBCommandType;

ExternalConnection conn = workbook.getDataConnections().get(0);
```
`getDataConnections()` vrací kolekci všech připojení, což vám umožní **modify excel data connections** jednotlivě.

**Upravte vlastnosti připojení** – změňte název, soubor ODC, typ příkazu a SQL dotaz:

```java
conn.setName("MyConnectionName");
conn.setOdcFile(dataDir + "MyDefaulConnection.odc");
```

"Přetypujte na `DBConnection` pro nastavení specifická pro databázi:

```java
DBConnection dbConn = (DBConnection) conn;
dbConn.setCommandType(OLEDBCommandType.SQL_STATEMENT);
dbConn.setCommand("SELECT * FROM AdminTable");

String connectionString = "Server=myServerAddress;Database=myDataBase;User ID=myUsername;Password=myPassword;Trusted_Connection=False";
dbConn.setConnectionInfo(connectionString);
```
Zde **update excel external connection** detaily, jako je SQL dotaz a řetězec připojení.

### Funkce 3: Uložení sešitu do souboru
**Co se děje dál?** Po aktualizaci připojení musíte **save Excel workbook Java**, aby změny zůstaly.

#### Krok‑za‑krokem instrukce
**Definujte výstupní adresář** – kam bude upravený soubor zapsán:

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
```

**Uložte sešit** – zapište sešit zpět na disk:

```java
workbook.save(outDir + "MESQLDataConnection_out.xlsx");
```
Metoda `save()` dokončuje operaci **change excel data source**.

## Praktické aplikace
Programová úprava datových připojení v Excelu otevírá mnoho možností:

1. **Automatizované reportování** – generujte zprávy, které vždy načtou nejnovější data z databáze.  
2. **Synchronizace dat** – udržujte sešity synchronizované s živými systémy bez ručního obnovení.  
3. **Dynamické dashboardy** – vytvořte dashboardy, které odrážejí metriky v reálném čase.  

Integrace Aspose.Cells s platformami CRM, ERP nebo BI může výrazně snížit ruční úsilí.

## Úvahy o výkonu
Při práci s velkými sešity nebo obrovskými výsledkovými sadami:

- Zpracovávejte data po dávkách, aby nedocházelo k výkyvům paměti.  
- Optimalizujte své SQL dotazy pro rychlost.  
- Uvolněte prostředky okamžitě; zavolejte `workbook.dispose()`, pokud objekt již nepotřebujete.  

Tyto postupy zajišťují, že vaše aplikace zůstane responzivní při **changing Excel data source**.

## Závěr
Nyní jste se naučili, jak **change Excel data source** načtením sešitu, **modify excel data connections** a uložením aktualizovaného souboru pomocí **Aspose.Cells for Java**. Tato schopnost vám umožní automatizovat workflow založené na datech a udržovat soubory Excel synchronizované s externími systémy.

### Další kroky
- Experimentujte s více připojeními pomocí smyčky přes `workbook.getDataConnections()`.  
- Prozkoumejte další funkce Aspose.Cells, jako je generování grafů, stylování buněk a manipulace s kontingenčními tabulkami.  

Jste připraveni posílit svou automatizaci? Implementujte dnes tyto úryvky kódu a sledujte, jak vaše produktivita stoupá!

## Často kladené otázky

**Q1: Jak zvládnu více datových připojení v sešitu?**  
A1: Použijte `workbook.getDataConnections().get(index)` ve smyčce pro přístup k jednotlivým připojením.

**Q2: Mohu pomocí Aspose.Cells Java upravit i jiné vlastnosti souboru Excel?**  
A2: Rozhodně! Aspose.Cells podporuje formátování buněk, správu listů, tvorbu grafů a mnoho dalšího.

**Q3: Co když můj SQL příkaz selže při provádění?**  
A3: Ověřte řetězec připojení, zkontrolujte oprávnění databáze a prohlédněte si podrobnosti výjimky pro vodítka.

**Q4: Kde mohu získat podporu pro problémy s Aspose.Cells?**  
A4: Navštivte [Aspose forum](https://forum.aspose.com/c/cells/9), kde můžete klást otázky nebo procházet existující řešení.

**Q5: Existují omezení ve verzi zdarma?**  
A5: Evaluační verze přidává vodoznaky a může omezovat kapacitu zpracování. Zakupte licenci pro neomezené používání.

## Zdroje
- **Dokumentace:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Stáhnout:** [Aspose.Cells for Java Releases](https://releases.aspose.com/cells/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Poslední aktualizace:** 2025-12-27  
**Testováno s:** Aspose.Cells Java 25.3  
**Autor:** Aspose