---
date: 2026-01-29
description: Naučte se, jak převádět velikost písmen v Excelu a ovládnout další textové
  funkce s Aspose.Cells pro Javu. Tento tutoriál textových funkcí v Excelu ukazuje,
  jak spojovat buňky, počítat znaky a vyhledávat a nahrazovat text.
linktitle: convert text case excel using Aspose.Cells for Java
second_title: Aspose.Cells Java Excel Processing API
title: Převod velikosti písmen v Excelu pomocí Aspose.Cells pro Javu
url: /cs/java/basic-excel-functions/excel-text-functions-demystified/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Funkce textu v Excelu odhaleny

# Funkce textu v Excelu odhaleny pomocí Aspose.Cells pro Java

V tomto tutoriálu prozkoumáme, jak **convert text case excel** soubory a pracovat s kompletním souborem textových funkcí Excelu pomocí API Aspose.Cells pro Java. Ať už automatizujete reporty, čistíte data nebo vytváříte aplikaci řízenou tabulkami, zvládnutí těchto funkcí učiní váš kód výkonnějším a vaše listy čitelnějšími.

## Rychlé odpovědi
- **Jaká knihovna zpracovává textové funkce Excelu v Javě?** Aspose.Cells pro Java.  
- **Mohu převést velikost písmen v Excelu bez otevření uživatelského rozhraní Excel?** Ano – nastavením vzorců jako `=UPPER()` nebo `=LOWER()` programově.  
- **Jak spojit buňky v Excelu?** Použijte funkci `CONCATENATE` nebo operátor `&` ve vzorci.  
- **Jak spočítat znaky v Excelu?** Funkce `LEN` vrací délku řetězce.  
- **Je podporováno hledání a nahrazování textu v Excelu?** Ano – kombinujte vzorce `FIND` a `REPLACE` nebo použijte metody API pro nahrazení.

## Co je “convert text case excel”?
Převod velikosti písmen v Excelisu písmen v obsahu buněk – buď na velká, malá nebo na správný zápis – pomocí funkcí jako `UPPER`, `LOWER` nebo `PROPER`. S Aspose.Cells můžete tyto funkce aplikovat přímo ve vašem sešitu bez spose.Cells s textem?
- **Bez nutnosti instalace Excelu** – funguje na jakémkoli serveru nebo v cloudovém prostředí.  
- **Plná podpora vzorců** – všechny nativní textové funkce Excelu se chovají přesně jako v desktopové aplikaci.  
- **Vysoký výkon** – zpracujte tisíce řádků během několika sekund.  
- **Cross‑platformky
- Java Development Kit (JDK 8 nebo novější).  
- Knihovna Aspose.Cells pro Java (stáhněte **[here](https://releases.aspose.com/cells/java/)**).  
- Základní znalost Javy a Excelových vzorců.

## Jak spojit buňky v Excelu? (how to concatenate excel cells)

Funkce `CONCATENATE` spojuje text z více buněk. Níže je přesný kód, který potřebujete; všimněte si, že zachováváme původní blok beze změny.

```java
// Java code to concatenate text using Aspose.Cells
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
Cell cell = worksheet.getCells().get("A1");

cell.putValue("Hello, ");
cell = worksheet.getCells().get("B1");
cell.putValue("World!");

// Concatenate A1 and B1 into C1
cell = worksheet.getCells().get("C1");
cell.setFormula("=CONCATENATE(A1,B1)");

workbook.calculateFormula();
```

Po provedení bude buňka **C1** obsahovat **“Hello, World!”**.

## LEFT a RIGHT – extrahování znaků (extract text)

`LEFT` a `RIGHT` vám umožní získat konkrétní počet znaků ze začátku nebo konce řetězce.

```java
// Java code to extract text using Aspose.Cells
Cell cell = worksheet.getCells().get("A2");
cell.putValue("Excel Rocks!");

// Extract the first 5 characters
cell = worksheet.getCells().get("B2");
cell.setFormula("=LEFT(A2, 5)");

// Extract the last 5 characters
cell = worksheet.getCells().get("C2");
cell.setFormula("=RIGHT(A2, 5)");

workbook.calculateFormula();
```

**B2** → “Excel” **C2** → “Rocks!”.

## LEN – počítání znaků (count characters excel len)

Funkce `LEN` vrací délku řetězce. Toto je jádro úkolu **count characters excel len**.

```java
// Java code to count characters using Aspose.Cells
Cell cell = worksheet.getCells().get("A3");
cell.putValue("Excel");

// Count the characters
cell = worksheet.getCells().get("B3");
cell.setFormula("=LEN(A3)");

workbook.calculateFormula();
```

****, protože “Excel” má pět znaků.

## UPPER a LOWER – převod velikosti písmen (convert text case excel)

Změna velikosti písmen je přesně to, co hlavní klíčové slovo požaduje. Použijte `UPPER` pro velká písmena a `LOWER` pro malá.

```java
// Java code to change case using Aspose.Cells
Cell cell = worksheet.getCells().get("A4");
cell.putValue("java programming");

// Convert to uppercase
cell = worksheet.getCells().get("B4");
cell.setFormula("=UPPER(A4)");

// Convert to lowercase
cell = worksheet.getCells().get("C4");
cell.setFormula("=LOWER(A4)");

workbook.calculateFormula();
```

**B4** → “JAVA PROGRAMMING” **C4** → “java programming”.

## FIND a REPLACE – vyhledání a výměna textu (find and replace text excel)

Kombinujte `FIND` pro nalezení podřetězce a `REPLACE` pro jeho nahrazení.

```java
// Java code to find and replace using Aspose.Cells
Cell cell = worksheet.getCells().get("A5");
cell.putValue("Search for me");

// Find the position of "for"
cell = worksheet.getCells().get("B5");
cell.setFormula("=FIND(\"for\", A5)");

// Replace "for" with "with"
cell = worksheet.getCells().get("C5");
cell.setFormula("=REPLACE(A5, B5, 3, \"with\")");

workbook.calculateFormula();
```

**B5** → 9 (pozice “for”) **C5** → “Search with me”.

## Časté problémy a řešení
- **Vzorec se nepočítá** – Ujistěte se, že po nastavení vzorců je zavolána metoda `workbook.calculateFormula()`.  
- **Locale‑specifické desetinné oddělovače** – Použijte `WorkbookSettings.setCultureInfo()`, pokud narazíte na problémy s čárkami vs. tečkami.  
- **Velké listy** – Zavolejte `worksheet.calculateFormula()` na úrovni jednotlivení paměťové náročnosti.

## FAQ

### Jak spojím text z více buněk?

Pro spojení textu z více buněk použijte funkci `CONCATENATE`. Například:
```java
Cell cell = worksheet.getCells().get("A1");
cell.setFormula("=CONCATENATE(A1, B1)");
```

### Mohu extrahovat první a poslední znaky z textového řetězce?

Ano, můžete použít funkce `LEFT` a `RIGHT` pro extrahování znaků ze začátku nebo konce řetězce. Například:
```java
Cell cell = worksheet.getCells().get("A2");
cell.setFormula("=LEFT(A2, 5)");
```

### Jak mohu spočítat znaky v textovém řetězci?

Použijte funkci `LEN` pro spočítání znaků v textovém řetězci. Například:
```java
Cell cell = worksheet.getCells().get("A3");
cell.setFormula("=LEN(A3)");
```

### Je možné změnit velikost písmen textu?

Ano, můžete převést text na velká nebo malá písmena pomocí funkcí `UPPER` a `LOWER`. Například:
```java
Cell cell = worksheet.getCells().get("A4");
cell.setFormula("=UPPER(A4)");
```

### Jak najdu a nahradím text v řetězci?

Pro vyhledání a nahrazení textu v řetězci použijte funkce `FIND` a `REPLACE`. Například:
```java
Cell cell = worksheet.getCells().get("A5");
cell.setFormula("=FIND(\"for\", A5)");
```

## Často kladené otázky

**Q: Podporuje Aspose.Cells i další funkce pro převod velikosti písmen, jako `PROPER`?**  
A: Ano, můžete použít `PROPER` stejným způsobem a `LOWER` pro kapitalizaci prvního písmena každého slova.

**Q: Mohu aplikovat tyto vzorce na celý sloupec bez smyčky v Javě?**  
A: Rozhodně. Nastavte vzorec jednou (např. `=UPPER(A1)`) a poté použijte `worksheet.getCells().copyRows()` nebo vyplňte dolů metodou `AutoFill`.

**Q: Existuje způsob, jak nahradit text bez použití vzorců?**  
A: API poskytuje `Worksheet.replace()`, který provádí operaci najít‑a‑nahradit přímo na hodnotách buněk.

**Q: Jaká verze Aspose.Cells je pro tyto funkce vyžadována?**  
A: Všechny uvedené funkce jsou podporovány v Aspose.Cells pro Java 20.10 a novějších.

**Q: Jak uložit sešit po provedení změn?**  
A: Zavolejte `workbook.save("output.xlsx");` a specifikujte požadovaný formát (XLSX, XLS, CSV, atd.).

## Závěr

Ovládnutím těchto textových funkcí v Excelu – zejména **convert text case excel** – můžete automatizovat čištění dat, generovat dynamické reporty a vytvářet chytřejší Java aplikace. API Aspose.Cells pro Java vám dává plnou kontrolu nad vzorci jako `CONCATENATE`, `LEFT`, `RIGHT`, `LEN`, `UPPER`, `LOWER`, `FIND` a `REPLACE`, čímž promění běžné tabulky v výkonné datové motory. Prozkoumejte zbytek knihovny a odemkněte další možnosti, jako je podmíněné formátů a konverze do PDF.

---

**Poslední aktualizace:** 2026-01-29  
**Testováno s:** Aspose.Cells pro Java 24.12  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}