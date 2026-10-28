---
category: general
date: 2026-06-18
description: जावा में WRAPCOLS का उपयोग करके सूची को कॉलम में रैप करना, एक्सेल शैली
  में एरे फ़ॉर्मूला लागू करना, और जल्दी से जावा में एक्सेल वर्कबुक बनाना सीखें।
draft: false
keywords:
- how to use wrapcols
- apply array formula excel
- list to matrix excel
- wrap list into columns
- create excel workbook java
language: hi
og_description: जानेँ कैसे Java में WRAPCOLS का उपयोग करें, सूची को कॉलम में रैप करें,
  Excel में एरे फ़ॉर्मूला लागू करें, और एक पूर्ण, चलाने योग्य उदाहरण के साथ Java में
  Excel वर्कबुक बनाएं।
og_title: जावा में WRAPCOLS का उपयोग कैसे करें – पूर्ण एक्सेल एरे फ़ॉर्मूला गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Learn how to use WRAPCOLS in Java to wrap a list into columns, apply
    array formula Excel style, and create Excel workbook Java quickly.
  headline: How to Use WRAPCOLS in Java – Complete Guide to Excel Array Formulas
  type: TechArticle
- questions:
  - answer: The library works in trial mode, which adds a watermark. For production
      you’ll need a commercial license, but the API usage stays the same.
    question: Do I need a license for Aspose.Cells?
  - answer: Absolutely. Replace `{1,2,3}` with a named range like `MyNumbers`. The
      formula becomes `=WRAPCOLS(MyNumbers,3)`.
    question: Can I use WRAPCOLS with named ranges instead of literal arrays?
  - answer: 'POI currently doesn’t evaluate array formulas out of the box, so you’d
      need a custom evaluator or switch to Aspose for full support. --- ## Conclusion
      We’ve covered **how to use WRAPCOLS** in Java, shown you how to **apply array
      formula Excel** techniques, and demonstrated a practical **list to matr'
    question: What if I’m using Apache POI instead of Aspose?
  type: FAQPage
tags:
- Excel
- Java
- Aspose.Cells
- Array Formula
title: जावा में WRAPCOLS का उपयोग कैसे करें – एक्सेल एरे फ़ॉर्मूले की पूरी गाइड
url: /hi/java/integration-interoperability/how-to-use-wrapcols-in-java-complete-guide-to-excel-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java में WRAPCOLS का उपयोग कैसे करें – Excel Array Formulas के लिए पूर्ण गाइड

क्या आप कभी सोचते थे **how to use WRAPCOLS** जब आप Java से स्प्रेडशीट्स को ऑटोमेट कर रहे हों? आप अकेले नहीं हैं। चाहे आप मानों की एक सपाट सूची को एक व्यवस्थित 3‑कॉलम तालिका में बदल रहे हों या डेटा को पुनः आकार देने का तेज़ तरीका चाहिए, WRAPCOLS फ़ंक्शन एक जीवनरक्षक है।  

इस ट्यूटोरियल में हम एक वास्तविक उदाहरण के माध्यम से चलेंगे जो दिखाता है **how to use WRAPCOLS**, कैसे **apply array formula Excel** शैली को लागू करें, और यहां तक कि कैसे **create Excel workbook Java** को शुरू से बनाएं। अंत तक आपके पास एक पूर्ण कार्यशील `.xlsx` फ़ाइल होगी जो **list to matrix Excel** परिवर्तन को दर्शाती है—सभी स्पष्ट व्याख्याओं और तैयार‑चलाने योग्य कोड के साथ।

## आप क्या सीखेंगे

* `WRAPCOLS` एरे फ़ंक्शन की सटीक सिंटैक्स और जब यह उपयोगी होता है।  
* Aspose.Cells for Java का उपयोग करके **apply array formula Excel** अवधारणाओं को कैसे लागू करें।  
* **list to matrix Excel** के तरीके – कॉलम‑वाइज और रो‑वाइज दोनों।  
* **wrap list into columns** को कुशलतापूर्वक करने के टिप्स, और एक पूर्ण **create Excel workbook Java** उदाहरण।  

Aspose.Cells का कोई पूर्व अनुभव नहीं है? कोई समस्या नहीं। आपको केवल एक Java विकास पर्यावरण और Aspose.Cells for Java लाइब्रेरी की एक प्रति चाहिए (नि:शुल्क ट्रायल ठीक काम करता है)।

---

## WRAPCOLS का उपयोग कैसे करें – चरण‑दर‑चरण कार्यान्वयन

> **Pro tip:** WRAPCOLS एक *array* फ़ंक्शन है, जिसका मतलब है कि आपको इसे एक फ़ॉर्मूला के रूप में दर्ज करना होगा जो एक साथ कई कोशिकाएँ लौटाता है। Java में, Aspose.Cells आपके लिए एरे मूल्यांकन को संभालता है जब आप पुनः गणना ट्रिगर करते हैं।

```java
// ---------------------------------------------------------------------
// 1️⃣  Import the Aspose.Cells library
// ---------------------------------------------------------------------
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {

        // -----------------------------------------------------------------
        // 2️⃣  Create a new workbook – this is the foundation of any Java‑Excel task
        // -----------------------------------------------------------------
        Workbook workbook = new Workbook();               // create excel workbook java

        // -----------------------------------------------------------------
        // 3️⃣  Grab the first worksheet (index 0) – the default sheet is ready
        // -----------------------------------------------------------------
        Worksheet sheet = workbook.getWorksheets().get(0);

        // -----------------------------------------------------------------
        // 4️⃣  Set a WRAPCOLS formula that turns a simple list into a 3‑column matrix
        // -----------------------------------------------------------------
        // The array {1,2,3,4,5,6} will be laid out column‑wise, three columns wide.
        sheet.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3,4,5,6},3)"); // how to use wrapcols

        // -----------------------------------------------------------------
        // 5️⃣  Set a WRAPROWS formula – just for comparison, creates a 2‑row matrix
        // -----------------------------------------------------------------
        sheet.getCells().get("B1").setFormula("=WRAPROWS({1,2,3,4,5,6},2)"); // apply array formula excel

        // -----------------------------------------------------------------
        // 6️⃣  Recalculate all formulas so the array results become actual cell values
        // -----------------------------------------------------------------
        workbook.calculateFormula();                     // forces evaluation of array formulas

        // -----------------------------------------------------------------
        // 7️⃣  Save the workbook to disk – you now have a real Excel file
        // -----------------------------------------------------------------
        workbook.save("wrap_demo.xlsx");                 // create excel workbook java
        System.out.println("Workbook saved successfully!");
    }
}
```

**Why this works:**  
* `Workbook` Java में किसी भी Excel हेरफेर का प्रवेश बिंदु है।  
* `WRAPCOLS` दो तर्क लेता है – स्रोत एरे और इच्छित कॉलम संख्या।  
* `calculateFormula()` को कॉल करके, Aspose.Cells एरे फ़ॉर्मूला का मूल्यांकन करता है और परिणामी मैट्रिक्स को शीट में लिखता है, प्रभावी रूप से **wrapping a list into columns**।  

> **What if you need a dynamic column count?** बस हार्ड‑कोडेड `3` को एक सेल रेफ़रेंस या एक वेरिएबल से बदलें जिसे आप रन‑टाइम पर गणना करते हैं।

## Java के साथ Excel में एरे फ़ॉर्मूले लागू करना

यदि आपने प्रोग्रामेटिक रूप से एरे फ़ॉर्मूले कभी नहीं संभाले हैं, तो यह अवधारणा थोड़ी रहस्यमयी लग सकती है। Excel UI में आप फ़ॉर्मूला को लॉक करने के लिए `Ctrl+Shift+Enter` दबाते हैं; Java में लाइब्रेरी आपके लिए यह भारी काम करती है।  

* **Set the formula** – जैसा ऊपर दिखाया गया है, आप एक सेल पर `setFormula()` का उपयोग करते हैं।  
* **Trigger recalculation** – `workbook.calculateFormula()` इंजन को हर फ़ॉर्मूला, एरे सहित, का मूल्यांकन करने के लिए मजबूर करता है।  

यह तरीका सर्वर साइड पर वर्कबुक बनाते समय **apply array formula Excel** शैली को लागू करने की अनुशंसित विधि है। यह सुनिश्चित करता है कि परिणामी कोशिकाएँ गणना किए गए मान रखती हैं, न कि केवल फ़ॉर्मूला स्ट्रिंग।

## Excel में सूची को मैट्रिक्स में बदलना

`WRAPCOLS` और `WRAPROWS` फ़ंक्शन एक-आयामी सूची को दो-आयामी लेआउट में बदलने के लिए उत्तम हैं। यहाँ एक त्वरित तुलना है:

| फ़ंक्शन   | इच्छित आकार | उदाहरण कॉल                               | परिणाम (पहले कुछ कोशिकाएँ) |
|------------|---------------|--------------------------------------------|--------------------------|
| `WRAPCOLS` | 3 कॉलम     | `=WRAPCOLS({1,2,3,4,5,6},3)`               | A1=1, A2=2, A3=3, B1=4… |
| `WRAPROWS` | 2 पंक्तियाँ        | `=WRAPROWS({1,2,3,4,5,6},2)`               | A1=1, B1=2, C1=3, A2=4… |

ध्यान दें कि समान सपाट सूची को दो पूरी तरह अलग तरीकों से दर्शाया जा सकता है। जब आपको **list to matrix Excel** परिवर्तन चाहिए, तो बस वह फ़ंक्शन चुनें जो आपकी इच्छित अभिविन्यास से मेल खाता हो।

### ध्यान रखने योग्य किनारे के मामले

* **Uneven division** – यदि सूची की लंबाई कॉलम/पंक्ति संख्या का पूर्ण गुणज नहीं है, तो अंतिम कॉलम/पंक्ति में शेष आइटम रहेंगे। कोई त्रुटि नहीं फेंकी जाएगी।  
* **Empty source array** – `{}` का उपयोग करने से #VALUE! त्रुटि उत्पन्न होगी; फ़ॉर्मूला सेट करने से पहले सूची आकार की जाँच करके इसे रोकें।  
* **Large data sets** – हजारों आइटमों के लिए, `calculateFormula()` के दौरान मेमोरी स्पाइक से बचने के लिए ऑपरेशन को भागों में विभाजित करने पर विचार करें।

## सूची को कॉलम में लपेटना बनाम पंक्तियों में – कब कौन सा चुनें?

* **Wrap into columns (`WRAPCOLS`)** जब आप एक निश्चित संख्या के कॉलम में लंबवत विस्तार चाहते हैं – उन रिपोर्टों के लिए शानदार है जो प्रत्येक कॉलम में आइटम सूचीबद्ध करती हैं।  
* **Wrap into rows (`WRAPROWS`)** जब आप क्षैतिज फैलाव पसंद करते हैं – डैशबोर्ड के लिए उपयोगी जहाँ प्रत्येक पंक्ति एक श्रेणी का प्रतिनिधित्व करती है।  

दोनों फ़ंक्शन Excel के **array formula** परिवार का हिस्सा हैं, जिसका अर्थ है कि वे मानों का एरे लौटाते हैं। चयन आपके स्टेकहोल्डर्स की अपेक्षित दृश्य लेआउट पर निर्भर करता है।

## Java में Excel वर्कबुक बनाना – पूर्ण उदाहरण

नीचे एक स्व-समाहित प्रोग्राम है जो हमने चर्चा की सभी चीज़ों को दर्शाता है। कॉपी, पेस्ट और चलाएँ; आपको अपने प्रोजेक्ट फ़ोल्डर में `wrap_demo.xlsx` मिलेगा।

```java
import com.aspose.cells.*;

public class FullWrapExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣  Instantiate a new workbook – the starting point for create excel workbook java
        Workbook wb = new Workbook();

        // 2️⃣  Access the default worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // 3️⃣  Demonstrate WRAPCOLS – turning a simple list into a 3‑column matrix
        ws.getCells().get("A1").setFormula("=WRAPCOLS({10,20,30,40,50,60,70,80,90},3)"); // how to use wrapcols

        // 4️⃣  Demonstrate WRAPROWS – turning the same list into a 2‑row matrix
        ws.getCells().get("E1").setFormula("=WRAPROWS({10,20,30,40,50,60,70,80,90},2)"); // apply array formula excel

        // 5️⃣  Force calculation so the array results are materialized
        wb.calculateFormula();

        // 6️⃣  Save the file – you’ve now created an Excel workbook Java can open
        wb.save("full_wrap_demo.xlsx"); // create excel workbook java

        System.out.println("Excel file generated: full_wrap_demo.xlsx");
    }
}
```

**Expected output:**  

* Cells `A1:C3` में संख्याएँ 10‑90 कॉलम‑वाइज (3 कॉलम) व्यवस्थित होंगी।  
* Cells `E1:M2` में वही संख्याएँ रो‑वाइज (2 पंक्तियाँ) व्यवस्थित होंगी।  

Excel में फ़ाइल खोलें, और आप एक साफ़ मैट्रिक्स देखेंगे बिना किसी मैन्युअल कॉपी के—बस Java द्वारा संचालित **wrap list into columns** (और rows) की शक्ति।

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या मुझे Aspose.Cells के लिए लाइसेंस चाहिए?**  
A: लाइब्रेरी ट्रायल मोड में काम करती है, जो एक वॉटरमार्क जोड़ती है। प्रोडक्शन के लिए आपको एक व्यावसायिक लाइसेंस चाहिए, लेकिन API उपयोग वही रहता है।

**Q: क्या मैं WRAPCOLS को लिटरल एरे के बजाय नेम्ड रेंज के साथ उपयोग कर सकता हूँ?**  
A: बिल्कुल। `{1,2,3}` को `MyNumbers` जैसे नेम्ड रेंज से बदलें। फ़ॉर्मूला बन जाता है `=WRAPCOLS(MyNumbers,3)`।

**Q: यदि मैं Aspose के बजाय Apache POI का उपयोग कर रहा हूँ तो?**  
A: वर्तमान में POI एरे फ़ॉर्मूले का मूल्यांकन बॉक्स से बाहर नहीं करता, इसलिए आपको एक कस्टम इवैल्युएटर चाहिए या पूर्ण समर्थन के लिए Aspose पर स्विच करना पड़ेगा।

## निष्कर्ष

हमने Java में **how to use WRAPCOLS** को कवर किया, आपको **apply array formula Excel** तकनीकों को दिखाया, और एक व्यावहारिक **list to matrix Excel** रूपांतरण प्रदर्शित किया। पूर्ण चलाने योग्य स्निपेट भी **

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API सुविधाओं में निपुण बनने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [Aspose.Cells for Java&#58; How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [How to Create an Excel Data Validation List with Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [How to Apply Styles to Excel Cells Using Aspose.Cells for Java - Complete Guide](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}