---
title: Egyéni adatérvényesítés létrehozása
linktitle: Egyéni adatérvényesítés létrehozása
second_title: Aspose.Cells Java Excel Processing API
description: Ismerje meg, hogyan hozhat létre egyéni adatellenőrzést az Aspose.Cells for Java használatával. Lépésről lépésre útmutató forráskóddal.
weight: 10
url: /hu/java/data-validation-rules/creating-custom-data-validation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Egyéni adatérvényesítés létrehozása


## Bevezetés

Az adatellenőrzés segít megőrizni az adatok integritását azáltal, hogy megakadályozza, hogy a felhasználók hibás vagy érvénytelen adatokat vigyenek be az Excel-táblázatokba. Míg az Excel beépített adatellenőrzési lehetőségeket kínál, vannak olyan esetek, amikor egyéni érvényesítési szabályokat kell meghatározni. Az Aspose.Cells for Java feljogosítja Önt ennek hatékony elérésére.

## Előfeltételek

Mielőtt belemerülne a kódba, győződjön meg arról, hogy rendelkezik a következő előfeltételekkel:

-  Aspose.Cells for Java: Töltse le és telepítse a könyvtárat innen[itt](https://releases.aspose.com/cells/java/).

## 1. lépés: A Java projekt beállítása

A kezdéshez hozzon létre egy új Java-projektet a kívánt integrált fejlesztési környezetben (IDE). Adja hozzá az Aspose.Cells for Java könyvtárat a projekt osztályútvonalához.

## 2. lépés: Excel-munkafüzet létrehozása

Kezdjük egy új Excel-munkafüzet létrehozásával az Aspose.Cells for Java segítségével.

```java
// Java-kód új Excel-munkafüzet létrehozásához
Workbook workbook = new Workbook();
```

## 3. lépés: Munkalap hozzáadása

Most adjunk hozzá egy munkalapot a munkafüzethez, ahol alkalmazni fogjuk az egyéni adatellenőrzést.

```java
// Java kód munkalap hozzáadásához
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## 4. lépés: Egyéni érvényesítési kritériumok meghatározása

Ebben a lépésben meghatározzuk azokat az egyéni érvényesítési feltételeket, amelyeknek az adatainknak meg kell felelniük. Tegyük fel, hogy a cellába beírt életkort 18 és 60 év közöttire szeretnénk korlátozni.

```java
// Java kód az egyéni érvényesítési feltételek meghatározásához
Validation validation = worksheet.getValidations().add();
validation.setType(ValidationType.WHOLE);
validation.setOperator(OperatorType.BETWEEN);
validation.setFormula1("18");
validation.setFormula2("60");
validation.setShowError(true);
validation.setAlertStyle(ValidationAlertType.STOP);
validation.setErrorTitle("Invalid Age");
validation.setErrorMessage("Age must be between 18 and 60.");
```

## 5. lépés: Adatérvényesítés alkalmazása egy tartományra

Most, hogy meghatároztuk egyéni érvényesítési feltételeinket, alkalmazzuk azokat egy adott cellatartományra.

```java
// Java kód az adatellenőrzés alkalmazásához egy tartományra
CellArea area = new CellArea();
area.startRow = 0;
area.startColumn = 0;
area.endRow = 9; // Alkalmazza az érvényesítést az első tíz sorra
area.endColumn = 0;

validation.addArea(area);
```

## 6. lépés: Az Excel fájl mentése

Végül mentse az Excel-fájlt az alkalmazott egyéni adatérvényesítési szabályokkal.

```java
// Java kód az Excel fájl mentéséhez
workbook.save("CustomDataValidation.xlsx");
```

## Következtetés

Ebben az oktatóanyagban megvizsgáltuk, hogyan hozhat létre egyéni adatérvényesítési szabályokat az Aspose.Cells for Java használatával. Ha követi ezeket a lépéseket, biztosíthatja, hogy Excel-adatai megfeleljenek bizonyos feltételeknek, javítva az adatok integritását és pontosságát.

## GYIK

### Hogyan tölthetem le az Aspose.Cells for Java fájlt?

 Az Aspose.Cells for Java letölthető a következő webhelyről:[itt](https://releases.aspose.com/cells/java/).

### Alkalmazhatok egyéni adatellenőrzést több tartományra ugyanazon a munkalapon?

Igen, ugyanazon a munkalapon belül több tartományra is alkalmazhat egyéni adatellenőrzést az 5. lépés megismétlésével minden kívánt tartományra.

### Támogatja az Aspose.Cells for Java más típusú adatellenőrzést?

Igen, az Aspose.Cells for Java különféle típusú adatellenőrzést támogat, beleértve az egész számot, a tizedesjegyet, a dátumot, az időt, a szöveg hosszát stb.

### Hogyan szabhatom testre az adatellenőrzés sikertelensége esetén megjelenő hibaüzenetet?

 A hibaüzenetet személyre szabhatja a`setErrorMessage` módszert a 4. lépésben, ahol meghatározza az érvényesítési feltételeket.

### Működik az Aspose.Cells for Java különböző formátumú Excel-fájlokkal?

Igen, az Aspose.Cells for Java az Excel fájlformátumok széles skáláját támogatja, beleértve az XLS-t, XLSX-et, XLSM-et stb.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
