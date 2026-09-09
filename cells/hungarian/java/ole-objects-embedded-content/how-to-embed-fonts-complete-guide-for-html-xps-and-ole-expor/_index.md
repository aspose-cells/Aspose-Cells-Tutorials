---
category: general
date: 2026-03-01
description: Tudja meg, hogyan lehet betűkészleteket beágyazni HTML-ben és más formátumokban.
  Lépésről lépésre útmutató, amely bemutatja a betűkészletek beágyazását HTML-be,
  az Excel HTML-be konvertálását, az OLE exportálásának módját, valamint az Excel
  XPS-be konvertálását.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- convert excel to html
- how to export ole
- convert excel to xps
language: hu
og_description: Hogyan ágyazzunk be betűtípusokat HTML, XPS és OLE exportokba. Ismerje
  meg a teljes munkafolyamatot, tekintse meg a futtatható Java kódot, és sajátítsa
  el a betűtípusok beágyazását HTML-ben az Excel konverziókhoz.
og_title: Betűtípusok beágyazása – Teljes Java útmutató
tags:
- Aspose.Cells
- Java
- Document Export
title: Betűtípusok beágyazása – Teljes útmutató HTML, XPS és OLE exporthoz
url: /hu/java/ole-objects-embedded-content/how-to-embed-fonts-complete-guide-for-html-xps-and-ole-expor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan kell betűtípusokat beágyazni – Teljes útmutató HTML, XPS és OLE exporthoz

Gondolkodtál már azon, **hogyan kell betűtípusokat beágyazni**, amikor egy Excel munkafüzetet weboldallá vagy nyomtatható dokumentummá alakítasz? Nem vagy egyedül. Sok fejlesztő szembesül azzal a problémával, hogy a kimenet a saját gépén rendben néz ki, de másik gépen hibás, mert a szükséges betűtípusok hiányoznak.  

Ebben az oktatóanyagban egy valós példán keresztül mutatjuk be az Aspose.Cells for Java használatát: betűtípusok beágyazása HTML-be, emoji variációs szelektorok megőrzése XPS-re konvertáláskor, valamint egy OLE objektum szerkeszthető állapotban tartása PPTX exportáláskor. A végére egy kész, másolás‑beillesztés megoldást kapsz, amely megválaszolja a „hogyan kell betűtípusokat beágyazni” kérdést, és érint olyan kulcsszavakat is, mint **embed fonts in html**, **convert excel to html**, **how to export ole**, és **convert excel to xps**.

## Előfeltételek

- Java 17 (vagy bármely friss JDK)  
- Aspose.Cells for Java 25.x vagy újabb  
- Fejlesztői IDE (IntelliJ IDEA, Eclipse vagy VS Code)  
- Alapvető ismeretek az Excel adatstruktúrákról  

Külső szolgáltatásokra nincs szükség – minden helyben fut.

## A megoldás áttekintése

1. **Munkafüzet létrehozása** és a `WRAPCOLS` függvény használata egy függőleges tartomány háromoszlopos elrendezéssé alakításához.  
2. **Munkafüzet mentése XPS‑ként** a betűtípus‑variációs szelektorok bekapcsolásával, hogy az emoji megmaradjon.  
3. **Exportálás HTML‑be** beágyazott betűtípusokkal, garantálva, hogy az oldal mindenhol ugyanúgy nézzen ki.  
4. **Munkafüzet exportálása OLE objektummal PPTX‑be**, a szerkeszthetőség megőrzésével.  
5. **Smart Marker sablon alkalmazása**, amely bemutatja a master‑detail adatkapcsolást.  

Minden lépés saját H2 szekcióban van, így az útmutató könnyen átfutható mind keresőmotorok, mind AI asszisztensek számára.

![Hogyan kell betűtípusokat beágyazni illusztráció](image.png "hogyan kell betűtípusokat beágyazni")

*Image alt text: hogyan kell betűtípusokat beágyazni diagram, amely az Excel → HTML, XPS és PPTX munkafolyamatot mutatja.*

---

## 1. lépés – Munkafüzet létrehozása és WRAPCOLS használata (Miért fontos ez a **embed fonts in html** szempontjából)

Mielőtt a betűtípusok beágyazásáról beszélnénk, szükségünk van egy olyan munkafüzetre, amely tényleges adatot tartalmaz. A `WRAPCOLS` függvény kényelmes módja egyetlen oszlop több oszlopra bontásának, ami gyakran olvashatóbbá teszi a végső HTML‑t.

```java
import com.aspose.cells.*;

public class EmbedFontsDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Populate A2:A10 with sample data
        for (int i = 2; i <= 10; i++) {
            sheet.getCells().get("A" + i).putValue("Item " + (i - 1));
        }

        // Use WRAPCOLS to create a 3‑column block starting at A1
        Cell resultCell = sheet.getCells().get("A1");
        resultCell.setFormula("=WRAPCOLS(A2:A10,3)");
        workbook.calculateFormula();

        System.out.println("WRAPCOLS result: " + resultCell.getStringValue());
        // -----------------------------------------------------------------
        // The rest of the steps are demonstrated after this point.
        // -----------------------------------------------------------------
```

**Miért ez a lépés?**  
A `WRAPCOLS` hívás egy többoszlopos tartományt hoz létre, amely később HTML‑ben táblázatként jelenik meg. Amikor **betűtípusokat ágyazunk be HTML‑be**, a táblázat stílusa a beágyazott betűtípusokra támaszkodik, ezáltal biztosítva a konzisztens megjelenítést a böngészők között.

---

## 2. lépés – Munkafüzet mentése XPS‑ként az emoji megőrzésével (**convert excel to xps**)

Ha nyomtatásra kész formátumra van szükséged, az XPS egy stabil választás. A modern dokumentumok gyakran tartalmaznak emoji‑kat vagy szimbólumokat, amelyek variációs szelektorokat használnak. Az `EnableFontVariationSelectors` bekapcsolása biztosítja, hogy ezek a karakterek megmaradjanak a konvertálás során.

```java
        // --------------------------------------------------------------
        // Step 2: Save as XPS with font variation selectors enabled
        // --------------------------------------------------------------
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true); // crucial for emoji

        String xpsPath = "output/withVariations.xps";
        workbook.save(xpsPath, SaveFormat.XPS);
        System.out.println("Workbook saved as XPS at: " + xpsPath);
```

**Mit kapsz:**  
Egy XPS fájl, amely a beágyazott emoji‑kat pontosan úgy jeleníti meg, mint a forrás munkafüzetben. Ez teljesíti a **convert excel to xps** követelményt, és azt is bizonyítja, hogy a betűtípus‑kezelés nem korlátozódik csak HTML‑re.

---

## 3. lépés – Exportálás HTML‑be beágyazott betűtípusokkal (**how to embed fonts** & **embed fonts in html**)

Most jön a tutorial központi része: **hogyan kell betűtípusokat beágyazni** Excel → HTML konvertáláskor. Az Aspose.Cells lehetővé teszi, hogy a betűtípusokat közvetlenül a generált HTML‑fájlba ágyazzuk, ezzel kiküszöbölve a külső betűtípus‑fájlok szükségességét.

```java
        // --------------------------------------------------------------
        // Step 3: Export to HTML with embedded fonts
        // --------------------------------------------------------------
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setEmbedFonts(true); // this is the key line for embed fonts in html
        htmlOptions.setExportImagesAsBase64(true); // optional, keeps all assets in one file

        String htmlPath = "output/embeddedFonts.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML with embedded fonts saved at: " + htmlPath);
```

**Működési elv:**  
A `setEmbedFonts(true)` utasítás azt mondja a renderelőnek, hogy olvassa be a munkafüzetben használt betűtípus‑fájlokat, és Base64‑kódolt `@font-face` szabályokként ágyazza be a `<style>` címkébe. Az eredmény egy önálló HTML, amelyet bármely szerveren elhelyezve a betűtípusok helyesen jelennek meg – pontosan ez, amit a fejlesztők keresnek a **how to embed fonts** kifejezésre.

**Várható kimeneti részlet (`embeddedFonts.html`):**

```html
<style>
@font-face{font-family:"Arial";src:url(data:font/ttf;base64,AAEAAA... ) format('truetype');}
</style>
<table>
  <tr><td>Item 1</td><td>Item 4</td><td>Item 7</td></tr>
  <tr><td>Item 2</td><td>Item 5</td><td>Item 8</td></tr>
  <tr><td>Item 3</td><td>Item 6</td><td>Item 9</td></tr>
</table>
```

Vedd észre az `@font-face` szabályt – ez a konkrét válasz a **embed fonts in html** kérdésre.

---

## 4. lépés – Munkafüzet exportálása OLE objektummal PPTX‑be (**how to export ole**)

Sok üzleti jelentés Word dokumentumokat, PDF‑eket vagy más Excel‑lapokat ágyaz be OLE objektumként. Amikor ilyen munkafüzetet exportálsz PowerPointba, gyakran elveszik a szerkeszthetőség. Az Aspose.Cells alapból megőrzi ezt a funkciót.

```java
        // --------------------------------------------------------------
        // Step 4: Export a workbook with an OLE object to PPTX
        // --------------------------------------------------------------
        // Load a workbook that already contains an OLE object.
        Workbook oleWorkbook = new Workbook("input/oleObject.xlsx");

        String pptxPath = "output/oleEditable.pptx";
        oleWorkbook.save(pptxPath, SaveFormat.PPTX);
        System.out.println("PPTX with editable OLE object saved at: " + pptxPath);
```

**Miért fontos:**  
Ha a **how to export ole** keresést végzed, ez a kódrészlet pontosan megmutatja a szükséges API‑hívást. A kapott PowerPoint‑dia egy élő, dupla‑kattintás‑szerkeszthető OLE objektumot tartalmaz – további utófeldolgozás nélkül.

---

## 5. lépés – Smart Marker sablon alkalmazása (master‑detail) és a demo befejezése

A Smart Markerek lehetővé teszik, hogy egy adatforrást (Map, JSON, DataTable) közvetlenül egy Excel sablonhoz kössünk. Íme egy minimális példa, amely master‑detail sorokat nyomtat.

```java
        // --------------------------------------------------------------
        // Step 5: Apply Smart Marker template (master‑detail)
        // --------------------------------------------------------------
        String smartMarkerTemplate = "${Orders.Master:OrderID,Customer}\n${Orders.Detail:Product,Qty,Price}";
        // Simulated data source
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();
        java.util.List<java.util.Map<String, Object>> master = new java.util.ArrayList<>();
        java.util.Map<String, Object> masterRow = new java.util.HashMap<>();
        masterRow.put("OrderID", 1001);
        masterRow.put("Customer", "Acme Corp");
        master.add(masterRow);
        dataSource.put("Orders.Master", master);

        java.util.List<java.util.Map<String, Object>> detail = new java.util.ArrayList<>();
        java.util.Map<String, Object> detailRow = new java.util.HashMap<>();
        detailRow.put("Product", "Widget");
        detailRow.put("Qty", 5);
        detailRow.put("Price", 9.99);
        detail.add(detailRow);
        dataSource.put("Orders.Detail", detail);

        SmartMarkerProcessor processor = new SmartMarkerProcessor(new Workbook());
        processor.apply(smartMarkerTemplate, dataSource);
        processor.getWorkbook().save("output/smartMarkerResult.xlsx");
        System.out.println("Smart Marker workbook saved.");
    }
}
```

**Mit látsz:**  
Egy új munkafüzet (`smartMarkerResult.xlsx`), ahol a sablonhelyettesítők a valós adatokkal lettek helyettesítve. Ez a lépés nem közvetlenül a betűtípusokról szól, de kerekíti az útmutatót egy tipikus jelentéskészítési folyamat bemutatásával, amely gyakran megelőzi a **embed fonts in html** exportot.

---

## Gyakori hibák és tippek (A sikeres betűtípus‑beágyazás biztosítása)

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| A betűtípusok hiányoznak a HTML‑fájlban | A munkafüzet olyan rendszer‑betűtípust használ, amely nincs telepítve a szerveren. | Használd a `Workbook.getSettings().setDefaultFont("Arial")` hívást az adatok betöltése előtt, vagy ágyazd be manuálisan a szükséges betűtípus‑fájlokat. |
| A kimeneti HTML túl nagy | Sok nagy betűtípus beágyazása megnöveli a fájlméretet. | Korlátozd a beágyazást csak a ténylegesen használt betűtípusokra: `htmlOptions.setFontEmbeddingMode(HtmlFontEmbeddingMode.EmbedSubset)`. |
| Emoji eltűnik XPS konvertálás után | A variációs szelektorok alapértelmezés szerint le vannak vágva. | Engedélyezd a `settings.setEnableFontVariationSelectors(true)` beállítást, ahogy a 2. lépésben látható. |
| OLE objektum statikus képpé válik PPTX‑ben | A forrás munkafüzetet a `setSuppressOLEObjects(true)` opcióval mentették. | Győződj meg róla, hogy **nem** tiltod le az OLE objektumokat PPTX mentésekor. |

---

## Az eredmények ellenőrzése

1. Nyisd meg az `embeddedFonts.html` fájlt Chrome‑ban vagy Firefox‑ban. A táblázatnak a beágyazott betűtípussal (pl. Arial) kell megjelenni, még akkor is, ha az a gépen nincs telepítve.  
2. Nyisd meg a `withVariations.xps` fájlt a Windows XPS Viewer‑ben. Az emoji‑k, például 👍, helyesen kell, hogy megjelenjenek.  
3. Nyisd meg az `oleEditable.pptx` fájlt PowerPoint‑ban. Dupla‑kattints az OLE alakzatra;

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}