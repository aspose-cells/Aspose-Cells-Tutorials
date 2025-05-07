---
"date": "2025-04-08"
"description": "Naučte se, jak používat Aspose.Cells pro Javu k přidávání textových polí a nastavení řádkování v sešitech aplikace Excel. Vylepšete prezentace v sešitech stylizovanými textovými tvary."
"title": "Přidání textového pole a nastavení řádkování v Excelu pomocí Aspose.Cells pro Javu"
"url": "/cs/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Přidání textového pole a nastavení řádkování v Excelu pomocí Aspose.Cells pro Javu

## Zavedení

Vytváření dynamických sestav v Excelu často vyžaduje vlastní formátování textu, například přidání textových polí se specifickým řádkováním. S Aspose.Cells pro Javu je to jednoduché a efektivní. Tento tutoriál vás provede vylepšením prezentací vašich sešitů pomocí Aspose.Cells pro Javu a přidáním stylizovaných textových tvarů.

Na konci této příručky se naučíte, jak:
- Vytvoření nového sešitu aplikace Excel a přístup k jeho listům
- Přidání tvaru textového pole do listu
- Nastavení vlastního řádkování uvnitř textového tvaru
- Uložte formátovaný sešit ve formátu XLSX

Začněme nastavením vašeho prostředí.

### Předpoklady

Než začnete, ujistěte se, že máte následující:
- Na vašem počítači nainstalovaná sada pro vývojáře Java (JDK)
- IDE nebo editor pro psaní kódu v Javě
- Systém sestavení Maven nebo Gradle nakonfigurovaný pro správu závislostí

Základní znalost programování v Javě a znalost struktury souborů v Excelu bude výhodou.

## Nastavení Aspose.Cells pro Javu

Zahrňte Aspose.Cells do správy závislostí vašeho projektu pomocí Mavenu nebo Gradle:

**Znalec**

Přidejte následující blok závislostí do svého `pom.xml` soubor:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**

Zahrňte toto do svého `build.gradle` soubor:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

Dále si pořiďte licenci pro Aspose.Cells výběrem bezplatné zkušební verze, žádostí o dočasnou licenci nebo zakoupením plné licence.

### Inicializace Aspose.Cells

Jakmile je knihovna zahrnuta do vašeho projektu, inicializujte ji ve vaší Java aplikaci:

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // Inicializace instance sešitu (představuje soubor aplikace Excel)
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Průvodce implementací

### Vytvoření sešitu a pracovního listu v aplikaci Access

Začněte vytvořením nového sešitu aplikace Excel a přístupem k jeho prvnímu listu. Zde přidáte textové pole.

#### Přehled

Vytvoření nového sešitu poskytuje prázdný prostor pro přidání dat, tvarů a formátování podle potřeby.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // Vytvořit nový sešit (soubor aplikace Excel)
        Workbook workbook = new Workbook();
        
        // Přístup k prvnímu pracovnímu listu
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### Přidat textové pole do pracovního listu

Dále přidejte do vybraného listu tvar textového pole. Tento tvar může obsahovat libovolný textový obsah, který potřebujete.

#### Přehled

Textová pole jsou všestranné nástroje pro vkládání vlastních textů, jako jsou poznámky nebo pokyny, přímo do excelového listu.

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // Vytvořit nový sešit (soubor aplikace Excel)
        Workbook workbook = new Workbook();
        
        // Přístup k prvnímu pracovnímu listu
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Přidání tvaru textového pole do listu
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### Nastavit text do tvaru

Jakmile je textové pole připraveno, nastavte jeho obsah a naformátujte text uvnitř.

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // Vytvořit nový sešit (soubor aplikace Excel)
        Workbook workbook = new Workbook();
        
        // Přístup k prvnímu pracovnímu listu
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Přidání tvaru textového pole do listu
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Nastavení textového obsahu uvnitř tvaru
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### Přístup k odstavcům textu ve Shape

Pro použití specifického formátování můžete v textovém poli přistupovat k jednotlivým odstavcům.

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // Vytvořit nový sešit (soubor aplikace Excel)
        Workbook workbook = new Workbook();
        
        // Přístup k prvnímu pracovnímu listu
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Přidání tvaru textového pole do listu
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Nastavení textového obsahu uvnitř tvaru
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Přístup k druhému odstavci v obrazci
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### Nastavení řádkování odstavce

Úprava řádkování může zlepšit čitelnost. Zde je návod, jak ho nastavit:

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Vytvořit nový sešit (soubor aplikace Excel)
        Workbook workbook = new Workbook();
        
        // Přístup k prvnímu pracovnímu listu
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Přidání tvaru textového pole do listu
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Nastavení textového obsahu uvnitř tvaru
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Přístup k druhému odstavci v obrazci
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Nastavit řádkování na 20 bodů
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Nastavení mezer před a za odstavcem
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### Uložit sešit

Nakonec uložte sešit s nově přidaným a naformátovaným textovým polem.

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Vytvořit nový sešit (soubor aplikace Excel)
        Workbook workbook = new Workbook();
        
        // Přístup k prvnímu pracovnímu listu
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Přidání tvaru textového pole do listu
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Nastavení textového obsahu uvnitř tvaru
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Přístup k druhému odstavci v obrazci
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Nastavit řádkování na 20 bodů
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Nastavení mezer před a za odstavcem
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // Uložit sešit
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## Závěr

Úspěšně jste se naučili, jak přidat textové pole a nastavit řádkování v sešitu aplikace Excel pomocí Aspose.Cells pro Javu. To vám umožní vytvářet dynamické a vizuálně atraktivní sestavy.

## Doporučení klíčových slov
- „Aspose.Cells pro Javu“
- "Přidat textové pole v Excelu"
- "Nastavení řádkování v Excelu"
- "Sešit aplikace Excel se stylizovaným textem"
- „Java a Aspose.Cells“


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}