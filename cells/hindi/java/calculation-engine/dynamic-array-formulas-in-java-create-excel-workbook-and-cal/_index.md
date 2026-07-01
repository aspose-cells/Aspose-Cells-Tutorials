---
category: general
date: 2026-06-30
description: जावा में डायनामिक एरे फ़ॉर्मूले आपको शक्तिशाली एक्सेल शीट्स बनाने में
  मदद करते हैं। जावा में एक्सेल वर्कबुक बनाना सीखें और सभी फ़ॉर्मूले जल्दी से गणना
  करें।
draft: false
keywords:
- dynamic array formulas
- calculate all formulas
- use lambda formula
- use expand function
- create excel workbook java
language: hi
og_description: जावा में डायनामिक एरे फ़ॉर्मूले एक्सेल ऑटोमेशन को सरल बनाते हैं। यह
  गाइड दिखाता है कि जावा में एक्सेल वर्कबुक कैसे बनाएं, एक्सपैंड फ़ंक्शन, लैम्ब्डा
  फ़ॉर्मूला का उपयोग करें, और सभी फ़ॉर्मूलों की गणना करें।
og_title: जावा में डायनामिक एरे फ़ॉर्मूले – वर्कबुक बनाएं और फ़ॉर्मूले गणना करें
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Dynamic array formulas in Java let you build powerful Excel sheets.
    Learn to create Excel workbook Java and calculate all formulas quickly.
  headline: 'Dynamic Array Formulas in Java: Create Excel Workbook and Calculate All
    Formulas'
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: 'जावा में डायनामिक एरे फ़ॉर्मूले: एक्सेल वर्कबुक बनाएं और सभी फ़ॉर्मूले गणना
  करें'
url: /hi/java/calculation-engine/dynamic-array-formulas-in-java-create-excel-workbook-and-cal/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में डायनेमिक एरे फ़ॉर्मूले: Excel वर्कबुक बनाएं और सभी फ़ॉर्मूले गणना करें

क्या आपने कभी सोचा है कि **डायनेमिक एरे फ़ॉर्मूले** जावा से Excel को ऑटोमेट करते समय कैसे काम करते हैं? आप अकेले नहीं हैं—कई डेवलपर्स को तब रुकावट आती है जब उन्हें `EXPAND` या `REDUCE` जैसे जटिल फ़ॉर्मूले वर्कबुक में डालने होते हैं बिना Excel को खोले।  

अच्छी खबर? कुछ ही लाइनों के जावा कोड से आप **create Excel workbook Java** शैली में वर्कबुक बना सकते हैं, उन आधुनिक एरे फ़ंक्शनों को डाल सकते हैं, और फिर **calculate all formulas** एक ही बार में कर सकते हैं। इस ट्यूटोरियल में हम हर कदम को विस्तार से देखेंगे, *क्यों* प्रत्येक भाग महत्वपूर्ण है समझाएंगे, और आपको एक पूर्ण, चलने योग्य उदाहरण देंगे जिसे आप सीधे अपने प्रोजेक्ट में कॉपी‑पेस्ट कर सकते हैं।

## आप क्या सीखेंगे

- जावा का उपयोग करके एक नई Excel वर्कबुक कैसे बनाते हैं (हां, कोई Excel UI नहीं चाहिए)।  
- `EXPAND` फ़ंक्शन के पीछे का मैकेनिज़्म और यह कैसे एक साधारण रेंज को डायनेमिक एरे में बदलता है।  
- कस्टम एग्रीगेशन के लिए `REDUCE` के साथ **lambda formula** सिंटैक्स का उपयोग कैसे करें।  
- त्रिकोणमितीय और हाइपरबोलिक फ़ंक्शन (`COT`, `COTH`) जोड़ना, जिन्हें कई लोग भूल जाते हैं कि Excel के फ़ॉर्मूला सेट में मौजूद हैं।  
- वह एक‑लाइनर जो **calculate all formulas** करने के लिए आवश्यक है ताकि वर्कबुक नवीनतम परिणाम दिखाए।  

> **Prerequisites:** Java 8+ (lambda समर्थन के लिए), Aspose.Cells for Java लाइब्रेरी, और Excel फ़ॉर्मूले की बुनियादी समझ। अन्य कोई निर्भरताएँ नहीं।

---

## डायनेमिक एरे फ़ॉर्मूले: वर्कबुक सेटअप करना

सबसे पहले—आइए एक वर्कबुक ऑब्जेक्ट को टेबल पर लाते हैं। Aspose.Cells की `Workbook` क्लास आपका एंट्री पॉइंट है; इसे एक खाली कैनवास समझें जहाँ हर डायनेमिक एरे फ़ॉर्मूला रहेगा।

```java
import com.aspose.cells.*;

public class DynamicArrayDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // default sheet is Sheet1
```

*Why this matters:* प्रोग्रामेटिक रूप से वर्कबुक को इंस्टैंशिएट करने से आपको फ़ाइल फ़ॉर्मेट, कल्चर सेटिंग्स, और—सबसे महत्वपूर्ण—डिस्क को कभी छुए बिना फ़ॉर्मूला इवैल्युएशन पर पूरी कंट्रोल मिलती है।

---

## EXPAND फ़ंक्शन का उपयोग करके रेंज को बढ़ाना

`EXPAND` फ़ंक्शन Excel का वह उत्तर है जो एक रेंज को आपके द्वारा निर्दिष्ट आकार के आधार पर बड़े क्षेत्र में “स्पिल” करता है। यह तब परफेक्ट है जब स्रोत डेटा रनटाइम पर लंबाई बदल सकता है।

```java
        // Step 2: Add a formula that expands B1:B3 into a 5‑row, 1‑column array
        worksheet.getCells().get("A1").setFormula("=EXPAND(B1:B3,5,1)");
```

*Explanation:*  
- `B1:B3` स्रोत रेंज है।  
- `5` Excel को पाँच पंक्तियाँ उत्पन्न करने को कहता है, भले ही स्रोत छोटा हो।  
- `1` एकल कॉलम को मजबूर करता है।  

जब आप बाद में **calculate all formulas** करेंगे, तो `A1` में परिणाम पाँच मानों की वर्टिकल स्पिल होगी, आवश्यक होने पर खाली सेल्स से पैड होगी।

---

## REDUCE के साथ LAMBDA फ़ॉर्मूला लागू करना

यदि आप कभी किसी कॉलम का योग करना चाहते थे लेकिन साथ ही एक कस्टम एग्रीगेटर चाहिए था, तो `REDUCE` को **lambda formula** के साथ उपयोग करना सही तरीका है। सिंटैक्स शुरू में थोड़ा अजीब लग सकता है, लेकिन यह सिर्फ Excel फ़ॉर्मूला के अंदर एक छोटा अनाम फ़ंक्शन एम्बेड करने का जावा तरीका है।

```java
        // Step 3: Add a REDUCE formula that sums the values in B1:B5
        worksheet.getCells().get("A2").setFormula(
            "=REDUCE(0,B1:B5,LAMBDA(a,b,a+b))"
        );
```

*Why use it?*  
- `0` प्रारंभिक सीड (शुरुआती कुल) है।  
- `B1:B5` वह एरे है जिस पर हम फोल्ड कर रहे हैं।  
- `LAMBDA(a,b,a+b)` कहता है “एक्यूम्यूलेटर `a` और अगला एलिमेंट `b` ले, उनका योग लौटाओ।”  

आप `a+b` को किसी भी कस्टम लॉजिक से बदल सकते हैं—औसत, अधिकतम, या यहाँ तक कि स्ट्रिंग कंकैटनेशन—जिससे `REDUCE` एक बहुमुखी बिल्डिंग ब्लॉक बन जाता है।

---

## त्रिकोणमितीय फ़ंक्शन (COT, COTH) जोड़ना

Excel में कुछ त्रिकोणमितीय हेल्पर फ़ंक्शन होते हैं जो अक्सर अनदेखे रह जाते हैं। यहाँ दिखाया गया है कि कैसे एक साधारण कोटैन्जेंट और उसका हाइपरबोलिक कज़िन शीट में डालें।

```java
        // Step 4: COT of π/4 (equals 1)
        worksheet.getCells().get("A3").setFormula("=COT(PI()/4)");

        // Step 5: COTH of 2 (hyperbolic cotangent)
        worksheet.getCells().get("A4").setFormula("=COTH(2)");
```

*Tip:* ये फ़ंक्शन स्वचालित रूप से वर्कबुक के कैलकुलेशन मोड का सम्मान करते हैं, इसलिए आपको डिग्री को रेडियन में बदलने के लिए अतिरिक्त कोड की जरूरत नहीं है—`PI()` ही भारी काम कर देता है।

---

## वर्कबुक में सभी फ़ॉर्मूले गणना करना

अब फ़ॉर्मूले जगह पर हैं, हमें **calculate all formulas** करना होगा ताकि सेल्स में केवल फ़ॉर्मूला टेक्स्ट नहीं बल्कि वास्तविक मान हों। Aspose.Cells इसे एक ही मेथड कॉल में कर देता है।

```java
        // Step 6: Force evaluation of every formula in the workbook
        workbook.calculateFormula();

        // Optional: Save to disk to see the result
        workbook.save("DynamicArrayDemo.xlsx");
    }
}
```

*What happens under the hood?* लाइब्रेरी हर सेल को ट्रैवर्स करती है, डिपेंडेंसीज़ को रिजॉल्व करती है, और जहाँ ज़रूरत हो एरे परिणामों को स्पिल करती है। यदि आप बड़े शीट्स के साथ काम कर रहे हैं, तो प्रदर्शन के लिए कैलकुलेशन ऑप्शन्स को ट्यून कर सकते हैं, लेकिन डिफ़ॉल्ट अधिकांश परिदृश्यों में शानदार काम करता है।

---

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा प्रोग्राम है, जिसे आप सीधे IDE में डाल सकते हैं। इसमें इम्पोर्ट्स, एक `main` मेथड, और एक अंतिम `save` कॉल शामिल है ताकि आप परिणामी फ़ाइल को Excel में खोलकर स्पिल्स देख सकें।

```java
import com.aspose.cells.*;

public class DynamicArrayDemo {
    public static void main(String[] args) throws Exception {
        // Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Populate source data for demonstration
        worksheet.getCells().get("B1").putValue(10);
        worksheet.getCells().get("B2").putValue(20);
        worksheet.getCells().get("B3").putValue(30);
        worksheet.getCells().get("B4").putValue(40);
        worksheet.getCells().get("B5").putValue(50);

        // EXPAND: spill B1:B3 into a 5‑row array
        worksheet.getCells().get("A1").setFormula("=EXPAND(B1:B3,5,1)");

        // REDUCE with LAMBDA: sum B1:B5
        worksheet.getCells().get("A2").setFormula("=REDUCE(0,B1:B5,LAMBDA(a,b,a+b))");

        // Trig functions
        worksheet.getCells().get("A3").setFormula("=COT(PI()/4)");
        worksheet.getCells().get("A4").setFormula("=COTH(2)");

        // Evaluate everything
        workbook.calculateFormula();

        // Save the file for inspection
        workbook.save("DynamicArrayDemo.xlsx");
    }
}
```

**जब आप `DynamicArrayDemo.xlsx` खोलते हैं तो अपेक्षित आउटपुट:**  

| A (परिणाम) | B (स्रोत) |
|------------|-----------|
| 10         | 10 |
| 20         | 20 |
| 30         | 30 |
| (खाली)    | 40 |
| (खाली)    | 50 |
| 150 (योग)  |   |
| 1 (cot)    |   |
| 1.0373… (coth) | |

*ध्यान दें कि `A1` पाँच पंक्तियों में स्पिल करता है, जबकि स्रोत में केवल तीन मान थे। यही है **डायनेमिक एरे फ़ॉर्मूले** की शक्ति।*

---

## सामान्य गलतियाँ और प्रो टिप्स

- **कैल्कुलेशन मोड सेट करना न भूलें** यदि आपने कहीं ऑटोमैटिक कैलकुलेशन बंद कर दिया है; नहीं तो `calculateFormula()` कुछ नहीं करेगा।  
- **एरे स्पिल टकराव:** यदि कोई अन्य सेल पहले से ही स्पिल रेंज को घेर रहा है, तो Excel `#SPILL!` त्रुटि देगा। कोड में आप लक्ष्य क्षेत्र को `worksheet.getCells().clear(0, 0, maxRow, maxColumn)` से पहले साफ़ कर सकते हैं।  
- **Lambda सिंटैक्स की बारीकियाँ:** `LAMBDA` फ़ंक्शन पैरामीटर को कॉमा से अलग करता है, सेमीकोलन नहीं। कॉमा भूल जाने पर पूरी फ़ॉर्मूला पार्स नहीं होगी।  
- **प्रदर्शन टिप:** हजारों पंक्तियों के साथ काम करते समय, डेटा को बल्क‑इन्सर्ट करने से पहले `workbook.getSettings().setCalculateFormulaOnOpen(false)` कॉल करें, फिर अंतिम `calculateFormula()` से पहले इसे फिर से एनेबल करें।

---

## अगले कदम

अब जब आप **डायनेमिक एरे फ़ॉर्मूले** में महारत हासिल कर चुके हैं, तो आप नीचे दिए गए विषयों को एक्सप्लोर कर सकते हैं:

- **`FILTER`** और **`SORT`** फ़ंक्शन ऑन‑द‑फ़्लाई डेटा शेपिंग के लिए।  
- **`SEQUENCE`** का उपयोग करके बिना किसी स्रोत रेंज के न्यूमेरिक एरे जेनरेट करना।  
- **नामित रेंज** को `EXPAND` के साथ मिलाकर साफ़, पुन: उपयोग योग्य फ़ॉर्मूले बनाना।  

इन सभी का आधार वही अवधारणाएँ हैं जो हमने कवर की हैं—सिर्फ फ़ॉर्मूला स्ट्रिंग बदलें और Aspose.Cells को भारी काम करने दें।

---

## निष्कर्ष

इस गाइड में हमने ठीक‑ठीक दिखाया कि **create Excel workbook Java** कैसे किया जाता है,

## आपको आगे क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स निकटतम संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण, चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [जावा में Aspose.Cells का उपयोग करके Excel वर्कबुक बनाएं: चरण-दर-चरण गाइड](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [जावा में Excel फ़ॉर्मूले गणना करें: Aspose.Cells के साथ अनुकूलित करें](/cells/english/java/calculation-engine/optimize-excel-aspose-cells-java-calculation-chains/)
- [Aspose.Cells जावा के साथ Excel एरे फ़ॉर्मूले में महारत: गणनाओं और फ़ॉर्मेटिंग को सरल बनाएं](/cells/english/java/formulas-functions/aspose-cells-java-array-formulas-custom-calculations/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}