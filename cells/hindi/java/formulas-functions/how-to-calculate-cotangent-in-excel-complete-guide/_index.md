---
category: general
date: 2026-06-27
description: फ़ॉर्मूलों का उपयोग करके Excel में कोटैन्जेंट कैसे गणना करें। फ़ॉर्मूला
  सेट करना, EXPAND का उपयोग करना सीखें, और Excel के डायनेमिक एरे फ़ॉर्मूले में महारत
  हासिल करें।
draft: false
keywords:
- how to calculate cotangent
- how to set formula
- how to use expand
- excel dynamic array formula
- add expand function
language: hi
og_description: Excel में कोटैन्जेंट कैसे गणना करें, एक स्पष्ट उदाहरण के साथ। यह ट्यूटोरियल
  दिखाता है कि फ़ॉर्मूला कैसे सेट करें, EXPAND का उपयोग करें, और Excel के डायनेमिक
  एरे फ़ॉर्मूला के साथ कैसे काम करें।
og_title: Excel में कोटैन्जेंट कैसे गणना करें – चरण-दर-चरण मार्गदर्शिका
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to calculate cotangent in Excel using formulas. Learn how to set
    formula, how to use EXPAND, and master the excel dynamic array formula.
  headline: How to Calculate Cotangent in Excel – Complete Guide
  type: TechArticle
- description: How to calculate cotangent in Excel using formulas. Learn how to set
    formula, how to use EXPAND, and master the excel dynamic array formula.
  name: How to Calculate Cotangent in Excel – Complete Guide
  steps:
  - name: '**Workbook creation** – `new Workbook()` gives us a fresh Excel file in
      memory.'
    text: '**Workbook creation** – `new Workbook()` gives us a fresh Excel file in
      memory.'
  - name: '**Source data** – We fill `A2:A5` with numbers 1‑4; these values will be
      expanded later.'
    text: '**Source data** – We fill `A2:A5` with numbers 1‑4; these values will be
      expanded later.'
  - name: '**How to set formula** – `setFormula` attaches the `EXPAND` expression
      to `A1`. The function tells Excel to spill a 5‑row‑by‑2‑column block based on
      the source range.'
    text: '**How to set formula** – `setFormula` attaches the `EXPAND` expression
      to `A1`. The function tells Excel to spill a 5‑row‑by‑2‑column block based on
      the source range.'
  - name: '**How to calculate cotangent** – The `COT` call uses `PI()/4` (45°). This
      is the core answer to *how to calculate cotangent* in Excel.'
    text: '**How to calculate cotangent** – The `COT` call uses `PI()/4` (45°). This
      is the core answer to *how to calculate cotangent* in Excel.'
  - name: '**Recalculation** – `wb.calculateFormula()` forces Aspose.Cells to evaluate
      all formulas, just like pressing **F9** in the UI.'
    text: '**Recalculation** – `wb.calculateFormula()` forces Aspose.Cells to evaluate
      all formulas, just like pressing **F9** in the UI.'
  - name: '**Result output** – We loop through the spill range to prove that `EXPAND`
      actually created a dynamic array.'
    text: '**Result output** – We loop through the spill range to prove that `EXPAND`
      actually created a dynamic array.'
  - name: '**Saving** – The final workbook, `CotangentDemo.xlsx`, can be opened in
      Excel to see the formulas live.'
    text: '**Saving** – The final workbook, `CotangentDemo.xlsx`, can be opened in
      Excel to see the formulas live.'
  type: HowTo
tags:
- Excel
- Formulas
- Java
- Aspose.Cells
title: Excel में कोटैन्जेंट कैसे गणना करें – पूर्ण मार्गदर्शिका
url: /hi/java/formulas-functions/how-to-calculate-cotangent-in-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel में कोटैन्जेंट कैसे निकालें – पूर्ण गाइड

क्या आपने कभी **Excel में कोटैन्जेंट कैसे निकालें** के बारे में सोचा है बिना वैज्ञानिक कैलकुलेटर निकाले? आप अकेले नहीं हैं। चाहे आप वित्त मॉडल बना रहे हों, भौतिकी की वर्कशीट, या सिर्फ त्रिकोणमिति के साथ खेलना पसंद करते हों, Excel में कोटैन्जेंट फ़ंक्शन में महारत हासिल करने से आपका बहुत समय बच सकता है।

इस ट्यूटोरियल में हम Java की Aspose.Cells लाइब्रेरी का उपयोग करके प्रोग्रामेटिक रूप से **फ़ॉर्मूला कैसे सेट करें** दिखाएंगे, **EXPAND का उपयोग कैसे करें** में गहराई से जाएंगे, और समझाएंगे कि **Excel डायनामिक एरे फ़ॉर्मूला** फीचर क्यों महत्वपूर्ण है। अंत तक आपके पास एक पूरी तरह चलने वाला उदाहरण होगा जो EXPAND फ़ंक्शन जोड़ता है, कोटैन्जेंट निकालता है, और परिणाम प्रिंट करता है—सभी दस लाइनों के कोड से कम में।

## आप क्या सीखेंगे

- Excel के `COT` फ़ंक्शन की सिंटैक्स और क्यों यह कोटैन्जेंट मान प्राप्त करने का सबसे तेज़ तरीका है।  
- Java कोड के माध्यम से वर्कशीट सेल पर **फ़ॉर्मूला कैसे सेट करें**।  
- डायनामिक एरे के लिए **EXPAND का उपयोग कैसे करें** के पीछे की यांत्रिकी।  
- कब और कैसे **EXPAND फ़ंक्शन जोड़ें** अपने वर्कबुक में spill‑range गणनाओं के लिए।  
- **Excel डायनामिक एरे फ़ॉर्मूला** व्यवहार में सामान्य समस्याओं को हल करने के लिए टिप्स।

> **पूर्वापेक्षाएँ:**  
> - Java 8+ स्थापित हो।  
> - Aspose.Cells for Java (फ्री ट्रायल या लाइसेंस्ड संस्करण)।  
> - Excel फ़ंक्शन्स की बुनियादी समझ।  

यदि आपके पास ये हैं, तो चलिए शुरू करते हैं.

---

## Excel में कोटैन्जेंट कैसे निकालें

`COT` फ़ंक्शन रैडियन में दिए गए कोण का कोटैन्जेंट लौटाता है। इसकी सिंटैक्स बस यह है:

```excel
=COT(number)
```

जहाँ *number* रैडियन में कोण है। क्लासिक 45° कोण (π/4 रैडियन) के लिए परिणाम `1` है क्योंकि `cot(π/4) = 1`।

### मैन्युअल गणना के बजाय `COT` क्यों उपयोग करें?

आप `=1/TAN(angle)` लिख सकते हैं लेकिन यह Excel को दो फ़ंक्शन मूल्यांकित करने के लिए मजबूर करता है और जब कोण π का गुणज हो तो संभावित शून्य से विभाजन त्रुटि उत्पन्न करता है। `COT` बिल्ट‑इन है, किनारे के मामलों को संभालता है, और पढ़ने में आसान है—विशेषकर जब आप शीट को टीम के साथ साझा कर रहे हों।

---

## चरण‑दर‑चरण: Java के साथ फ़ॉर्मूला सेट करें (फ़ॉर्मूला कैसे सेट करें)

नीचे एक **पूरा, चलने योग्य Java प्रोग्राम** दिया गया है जो एक वर्कबुक बनाता है, `COT` फ़ॉर्मूला को सेल `B1` में जोड़ता है, और उसे मूल्यांकित करता है। हम `EXPAND` फ़ंक्शन को भी जोड़ेंगे ताकि एक डायनामिक एरे दिखाया जा सके।

```java
import com.aspose.cells.*;

public class CotangentDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.getWorksheets().get(0);
        Cells cells = ws.getCells();

        // 2️⃣ Populate source data for EXPAND (A2:A5)
        for (int i = 0; i < 4; i++) {
            cells.get(i + 1, 0).putValue(i + 1); // A2=1, A3=2, A4=3, A5=4
        }

        // 3️⃣ **How to set formula** – Apply EXPAND to cell A1
        //    EXPAND(source, rows, columns) creates a spill range.
        cells.get("A1").setFormula("=EXPAND(A2:A5,5,2)");

        // 4️⃣ **How to calculate cotangent** – Apply COT to cell B1
        //    COT(PI()/4) = 1 because cot(45°) = 1
        cells.get("B1").setFormula("=COT(PI()/4)");

        // 5️⃣ Recalculate the workbook so formulas resolve
        wb.calculateFormula();

        // 6️⃣ Retrieve and print results
        System.out.println("EXPAND result (A1 spill range):");
        for (int r = 0; r < 5; r++) {
            for (int c = 0; c < 2; c++) {
                System.out.print(cells.get(r, c).getStringValue() + "\t");
            }
            System.out.println();
        }

        System.out.println("\nCotangent of π/4 (B1): " + cells.get("B1").getStringValue());

        // 7️⃣ Save the workbook (optional)
        wb.save("CotangentDemo.xlsx");
    }
}
```

#### कोड की व्याख्या

1. **वर्कबुक निर्माण** – `new Workbook()` मेमोरी में एक नई Excel फ़ाइल देता है।  
2. **स्रोत डेटा** – हम `A2:A5` को संख्याएँ 1‑4 से भरते हैं; ये मान बाद में विस्तारित किए जाएंगे।  
3. **फ़ॉर्मूला कैसे सेट करें** – `setFormula` `EXPAND` अभिव्यक्ति को `A1` से जोड़ता है। यह फ़ंक्शन Excel को स्रोत रेंज के आधार पर 5‑पंक्तियों‑और‑2‑स्तंभों का ब्लॉक फैलाने को कहता है।  
4. **कोटैन्जेंट कैसे निकालें** – `COT` कॉल `PI()/4` (45°) का उपयोग करता है। यह Excel में *कोटैन्जेंट कैसे निकालें* का मुख्य उत्तर है।  
5. **पुनः गणना** – `wb.calculateFormula()` Aspose.Cells को सभी फ़ॉर्मूले मूल्यांकित करने के लिए मजबूर करता है, ठीक उसी तरह जैसे UI में **F9** दबाना।  
6. **परिणाम आउटपुट** – हम स्पिल रेंज के माध्यम से लूप करते हैं यह साबित करने के लिए कि `EXPAND` वास्तव में एक डायनामिक एरे बना चुका है।  
7. **सेविंग** – अंतिम वर्कबुक, `CotangentDemo.xlsx`, को Excel में खोलकर फ़ॉर्मूले लाइव देखे जा सकते हैं।

> **प्रो टिप:** यदि आप Excel का वह संस्करण उपयोग कर रहे हैं जो डायनामिक एरे का समर्थन करता है (Office 365 या Excel 2021+), तो `EXPAND` फ़ंक्शन स्वचालित रूप से निकटवर्ती सेल्स में “स्पिल” करेगा। पुराने संस्करण `#NAME?` त्रुटि लौटाएंगे—इसलिए जब आप **EXPAND फ़ंक्शन जोड़ें** तो हमेशा अपने Excel संस्करण की जाँच करें।

---

## EXPAND का उपयोग कैसे करें – Excel डायनामिक एरे फ़ॉर्मूला को समझना

`EXPAND` Excel के **डायनामिक एरे** परिवार का हिस्सा है, जिसे जटिल मैन्युअल रेंज परिभाषाओं को बदलने के लिए पेश किया गया था। इसका सिग्नेचर:

```excel
=EXPAND(array, rows, columns, [pad_with])
```

- **array** – वह स्रोत रेंज जिसे आप विस्तारित करना चाहते हैं।  
- **rows** – स्पिल रेंज के लिए पंक्तियों की संख्या (मूल ऊँचाई रखने के लिए `0` उपयोग करें)।  
- **columns** – स्पिल रेंज के लिए स्तंभों की संख्या (मूल चौड़ाई रखने के लिए `0` उपयोग करें)।  
- **pad_with** – खाली सेल्स को भरने के लिए वैकल्पिक मान।

जब आप `=EXPAND(A2:A5,5,2)` लिखते हैं, तो Excel चार‑पंक्तियों वाले कॉलम को पढ़ता है और उसे 5‑बाय‑2 मैट्रिक्स में विस्तारित करता है, अतिरिक्त सेल्स को डिफ़ॉल्ट रूप से `0` से भरता है। परिणाम पड़ोसी सेल्स में “स्पिल” होता है, जो **Excel डायनामिक एरे फ़ॉर्मूला** जैसा व्यवहार करता है।

### कब EXPAND फ़ंक्शन जोड़ें

- **डेटा सामान्यीकरण** – आपके पास एकल कॉलम है लेकिन चार्ट के लिए मैट्रिक्स चाहिए।  
- **अन्य एरे फ़ंक्शनों के लिए पूर्व‑प्रसंस्करण** – `FILTER` या `SORT` जैसे फ़ंक्शन सीधे स्पिल रेंज को स्वीकार करते हैं।  
- **मैन्युअल कॉपी‑डाउन से बचना** – डायनामिक एरे स्रोत डेटा बदलने पर स्वचालित रूप से समायोजित होते हैं।

---

## सामान्य समस्याएँ और उन्हें कैसे ठीक करें

| समस्या | कारण | समाधान |
|-------|----------------|-----|
| `#SPILL!` error | लक्षित सेल्स में पहले से डेटा मौजूद है | क्षेत्र को साफ़ करें या फ़ॉर्मूला को खाली सेल में ले जाएँ। |
| `#NAME?` on `EXPAND` | Excel संस्करण डायनामिक एरे का समर्थन नहीं करता | Office 365/Excel 2021 में अपग्रेड करें या `INDEX` जैसे वैकल्पिक का उपयोग करें। |
| `#DIV/0!` from `COT` | कोण `0` या `π` के बराबर है (कोटैन्जेंट अपरिभाषित) | फ़ॉर्मूला को इस प्रकार रैप करें: `=IF(MOD(angle,PI())=0,NA(),COT(angle))`। |
| Formula not updating in Java | `Workbook.calculateFormula()` नहीं बुलाया गया | सभी फ़ॉर्मूले सेट करने के बाद `calculateFormula()` को कॉल करना सुनिश्चित करें। |

---

## उदाहरण का विस्तार – कोटैन्जेंट निकालने के और तरीके

यदि आपको किसी *डिग्री* मान का कोटैन्जेंट चाहिए, तो पहले उसे परिवर्तित करें:

```java
cells.get("C1").setFormula("=COT(RADIANS(30))"); // cot(30°) ≈ 1.732
```

या, `COT` को अन्य एरे फ़ंक्शनों के साथ मिलाएँ:

```excel
=MAP(A2:A5, LAMBDA(x, COT(RADIANS(x))))
```

`MAP` फ़ंक्शन (नए Excel संस्करणों में उपलब्ध) `COT` को रेंज के प्रत्येक तत्व पर लागू करता है, जिससे कोटैन्जेंट मानों का एक डायनामिक एरे प्राप्त होता है—बड़ी मात्रा में गणनाओं के लिए उपयुक्त।

---

## पूर्ण कार्यशील उदाहरण का सारांश

नीचे **पूरा स्रोत फ़ाइल** है जिसे आप अपने IDE में कॉपी‑पेस्ट कर सकते हैं। कोई छिपी हुई निर्भरताएँ नहीं, आपको जो चाहिए वह सब यहाँ है।



## आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API सुविधाओं में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन तरीकों का पता लगाने में मदद करेंगे।

- [Excel IF फ़ंक्शन का उपयोग कैसे करें](/cells/english/java/basic-excel-functions/how-to-use-excel-if-function/)
- [Aspose.Cells for Java का उपयोग करके Excel दस्तावेज़ संस्करण कैसे सेट करें](/cells/english/java/workbook-operations/set-excel-version-aspose-cells-java/)
- [बहुभाषी समर्थन के लिए Aspose.Cells .NET का उपयोग करके Excel फ़ाइलों में भाषा कैसे सेट करें](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}