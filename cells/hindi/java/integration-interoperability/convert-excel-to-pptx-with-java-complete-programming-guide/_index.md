---
category: general
date: 2026-06-18
description: Aspose.Cells का उपयोग करके जावा में Excel को PPTX में बदलें। जानें कि
  वर्कबुक को PowerPoint के रूप में कैसे सहेजें, Excel के टेक्स्ट बॉक्स और चार्ट शैलियों
  को प्रभावी ढंग से कैसे निर्यात करें।
draft: false
keywords:
- convert excel to pptx
- save workbook as powerpoint
- convert xlsx to pptx
- export excel text boxes
- export excel charts shapes
language: hi
og_description: जावा में एक्सेल को PPTX में बदलें। यह ट्यूटोरियल दिखाता है कि वर्कबुक
  को पॉवरपॉइंट के रूप में कैसे सहेजें और एक्सेल के टेक्स्ट बॉक्स और चार्ट शैप्स को
  निर्यात करें।
og_title: जावा के साथ एक्सेल को PPTX में बदलें – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Convert Excel to PPTX using Aspose.Cells in Java. Learn how to save
    workbook as PowerPoint, export Excel text boxes and chart shapes efficiently.
  headline: Convert Excel to PPTX with Java – Complete Programming Guide
  type: TechArticle
- description: Convert Excel to PPTX using Aspose.Cells in Java. Learn how to save
    workbook as PowerPoint, export Excel text boxes and chart shapes efficiently.
  name: Convert Excel to PPTX with Java – Complete Programming Guide
  steps:
  - name: Each worksheet turned into a separate slide (or a single slide if the workbook
      has one sheet).
    text: Each worksheet turned into a separate slide (or a single slide if the workbook
      has one sheet).
  - name: Text boxes that you can click and edit directly.
    text: Text boxes that you can click and edit directly.
  - name: Charts that you can re‑format, change data series, or move around.
    text: Charts that you can re‑format, change data series, or move around.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- PowerPoint
- File Conversion
title: जावा के साथ एक्सेल को PPTX में बदलें – पूर्ण प्रोग्रामिंग गाइड
url: /hi/java/integration-interoperability/convert-excel-to-pptx-with-java-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel को PPTX में Java के साथ बदलें – पूर्ण प्रोग्रामिंग गाइड

क्या आपको कभी **Excel को PPTX में बदलने** की ज़रूरत पड़ी, लेकिन यह नहीं पता था कि कौन‑सी लाइब्रेरी बिना कई वर्क‑अराउंड के यह काम कर सके? आप अकेले नहीं हैं। कई एंटरप्राइज़ प्रोजेक्ट्स में **वर्कबुक को PowerPoint के रूप में सहेजना** तब आवश्यक हो जाता है जब रिपोर्टिंग डैशबोर्ड को गैर‑Excel उपयोगकर्ताओं के साथ साझा करना पड़ता है।  

इस गाइड में हम Aspose.Cells for Java का उपयोग करके एक व्यावहारिक समाधान दिखाएंगे, जिससे आप **Excel को PPTX में केवल कुछ लाइनों के कोड** से बदल सकते हैं। अंत तक आप यह भी जान जाएंगे कि **Excel टेक्स्ट बॉक्स निर्यात** और **Excel चार्ट शैप्स निर्यात** कैसे करें ताकि आपकी स्लाइड्स मूल शीट जैसी दिखें।

## आप क्या सीखेंगे

- डिस्क से एक `.xlsx` वर्कबुक लोड करना।  
- संपादन योग्य टेक्स्ट बॉक्स और शैप्स को निर्यात करने को सक्षम करना ताकि वे PowerPoint में भी संपादन योग्य रहें।  
- **वर्कबुक को PowerPoint** (`.pptx`) के रूप में **सहेजना** एक ही मेथड कॉल से।  
- आउटपुट की जाँच करना और सामान्य समस्याओं का समाधान करना।  

कोई बाहरी स्क्रिप्ट नहीं, कोई मैन्युअल कॉपी‑पेस्ट नहीं—सिर्फ शुद्ध Java कोड जिसे आप किसी भी Maven या Gradle प्रोजेक्ट में डाल सकते हैं।

---

![Excel को PPTX में बदलने के लिए Java कोड स्निपेट](https://example.com/images/convert-excel-to-pptx-java.png "Excel को PPTX में बदलने के लिए Java कोड")

## चरण 1: अपने प्रोजेक्ट में Aspose.Cells सेट अप करें

सबसे पहले, आपको Aspose.Cells for Java लाइब्रेरी चाहिए। यदि आप Maven उपयोग कर रहे हैं, तो अपने `pom.xml` में डिपेंडेंसी जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

Gradle के लिए भी यही प्रक्रिया है:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **प्रो टिप:** Aspose मूल्यांकन के लिए एक मुफ्त अस्थायी लाइसेंस प्रदान करता है। उनकी साइट पर रजिस्टर करें, `Aspose.Cells.lic` फ़ाइल डाउनलोड करें, और इसे अपने क्लासपाथ में रखें ताकि मूल्यांकन वॉटरमार्क न दिखे।

## चरण 2: Excel वर्कबुक लोड करें

अब लाइब्रेरी तैयार है, आप **Excel वर्कबुक** लोड कर सकते हैं जिसे आप बदलना चाहते हैं। `Workbook` क्लास पूरी फ़ाइल को एब्स्ट्रैक्ट करता है, जिससे आप निर्यात से पहले सेटिंग्स को बदल सकते हैं।

```java
import com.aspose.cells.*;

public class ExportEditableShapesDemo {
    public static void main(String[] args) throws Exception {
        // Load the source .xlsx file
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        // ... further steps follow
    }
}
```

> **यह क्यों महत्वपूर्ण है:** वर्कबुक को पहले लोड करने से आपको `Settings` ऑब्जेक्ट तक पहुँच मिलती है, जहाँ आप **Excel टेक्स्ट बॉक्स निर्यात** और **Excel चार्ट शैप्स निर्यात** विकल्पों को सक्षम करेंगे।

## चरण 3: संपादन योग्य टेक्स्ट बॉक्स निर्यात को सक्षम करें

यदि आपके स्प्रेडशीट में टिप्पणी‑समान टेक्स्ट बॉक्स हैं जिन्हें आप बाद में PowerPoint में संपादित करना चाहते हैं, तो संबंधित फ़्लैग को ऑन करना आवश्यक है। यह चरण एक सच्चे **convert excel to pptx** अनुभव के लिए आवश्यक है जहाँ शैप्स इंटरैक्टिव रहते हैं।

```java
// Enable exporting of editable text boxes
workbook.getSettings().setExportEditableTextBoxes(true);
```

> **सामान्य प्रश्न:** *अगर मैं इसे छोड़ दूँ तो क्या होगा?* टेक्स्ट बॉक्स स्लाइड में स्थिर इमेज बन जाएंगे और संपादन योग्य नहीं रहेंगे। फ़्लैग को ऑन करने से उनका मूल व्यवहार बना रहता है।

## चरण 4: संपादन योग्य शैप्स (चार्ट, SmartArt, आदि) निर्यात को सक्षम करें

चार्ट, SmartArt और अन्य ड्रॉइंग ऑब्जेक्ट्स को भी शैप माना जाता है। परिवर्तन के बाद उन्हें संपादन योग्य रखने के लिए अगला फ़्लैग सेट करें:

```java
// Enable exporting of editable shapes (charts, SmartArt, etc.)
workbook.getSettings().setExportEditableShapes(true);
```

> **एज केस:** कुछ जटिल चार्ट प्रकार (जैसे 3‑D सरफ़ेस चार्ट) PowerPoint की सीमाओं के कारण पूरी तरह संपादन योग्य नहीं रह सकते। ऐसे मामलों में लाइब्रेरी रास्टर इमेज पर फ़ॉल्बैक करती है, लेकिन स्लाइड का बाकी हिस्सा संपादन योग्य रहता है।

## चरण 5: वर्कबुक को PowerPoint के रूप में सहेजें (XLSX को PPTX में बदलें)

अब असली काम—**convert xlsx to pptx** एक ही लाइन में। `save` मेथड गंतव्य पाथ और `SaveFormat.PPTX` एनेम लेता है।

```java
// Save the workbook as a PowerPoint presentation
workbook.save("YOUR_DIRECTORY/presentation.pptx", SaveFormat.PPTX);
```

बस इतना ही। इस कॉल के समाप्त होने के बाद आपके पास एक पूर्ण `.pptx` फ़ाइल होगी जो मूल Excel शीट की लेआउट को प्रतिबिंबित करती है, साथ ही संपादन योग्य टेक्स्ट बॉक्स और चार्ट शैप्स भी शामिल हैं।

## चरण 6: आउटपुट की जाँच करें

`presentation.pptx` को Microsoft PowerPoint या LibreOffice Impress में खोलें। आपको दिखना चाहिए:

1. प्रत्येक वर्कशीट एक अलग स्लाइड में बदल गई है (या यदि वर्कबुक में केवल एक शीट है तो एक ही स्लाइड)।  
2. टेक्स्ट बॉक्स जिन्हें आप क्लिक करके सीधे संपादित कर सकते हैं।  
3. चार्ट जिन्हें आप पुनः‑फ़ॉर्मेट, डेटा सीरीज़ बदल या स्थानांतरित कर सकते हैं।

यदि कुछ गड़बड़ दिखे, तो चरण 3 और 4 में हमने जो दो सेटिंग्स सक्षम की थीं, उन्हें दोबारा जांचें। ये ही एकमात्र स्विच हैं जो संपादन योग्यता को प्रभावित करते हैं।

---

## पूर्ण कार्यशील उदाहरण

नीचे वह पूरा, तैयार‑चलाने योग्य Java क्लास है जिसमें ऊपर बताए गए सभी चरण शामिल हैं। इसे अपने IDE में कॉपी‑पेस्ट करके उपयोग करें।

```java
import com.aspose.cells.*;

public class ExportEditableShapesDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the Excel workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2️⃣ Enable exporting of editable text boxes
        workbook.getSettings().setExportEditableTextBoxes(true);

        // 3️⃣ Enable exporting of editable shapes (charts, SmartArt, etc.)
        workbook.getSettings().setExportEditableShapes(true);

        // 4️⃣ Save the workbook as a PowerPoint presentation (convert xlsx to pptx)
        workbook.save("YOUR_DIRECTORY/presentation.pptx", SaveFormat.PPTX);

        System.out.println("Conversion complete! Check YOUR_DIRECTORY/presentation.pptx");
    }
}
```

**अपेक्षित कंसोल आउटपुट**

```
Conversion complete! Check YOUR_DIRECTORY/presentation.pptx
```

और `presentation.pptx` फ़ाइल टार्गेट फ़ोल्डर में बन जाएगी, साझा करने के लिए तैयार।

## सामान्य समस्याएँ एवं समाधान

| लक्षण | संभावित कारण | समाधान |
|---------|--------------|-----|
| टेक्स्ट बॉक्स इमेज के रूप में दिख रहे हैं | `setExportEditableTextBoxes(false)` या फ़्लैग न सेट किया गया | सुनिश्चित करें कि आप `setExportEditableTextBoxes(true)` कॉल कर रहे हैं। |
| चार्ट रास्टराइज़्ड हैं | `setExportEditableShapes(false)` या असमर्थित चार्ट प्रकार | `setExportEditableShapes(true)` ऑन करें; असमर्थित चार्ट के लिए पहले Excel में चार्ट को सरल बनाएं। |
| फ़ाइल नहीं मिली त्रुटि | `new Workbook(...)` में गलत पाथ | पूर्ण पाथ उपयोग करें या फ़ाइल को प्रोजेक्ट रूट के सापेक्ष रखें। |
| लाइसेंस अपवाद | वैध Aspose.Cells लाइसेंस नहीं | एप्लिकेशन स्टार्ट पर `Aspose.Cells.lic` लोड करें: `License lic = new License(); lic.setLicense("Aspose.Cells.lic");` |

## प्रदर्शन टिप्स

- **बैच रूपांतरण:** यदि आपको दर्जनों वर्कबुक बदलनी हों, तो प्रत्येक फ़ाइल को क्रमिक रूप से लोड करके एक ही `Workbook` इंस्टेंस को पुन: उपयोग करें—इससे JVM ओवरहेड कम होता है।  
- **मेमोरी प्रबंधन:** बहुत बड़े Excel फ़ाइलों के लिए `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` को सक्षम करें ताकि मेमोरी उपयोग नियंत्रित रहे।  
- **पैरेलल प्रोसेसिंग:** Java का `ForkJoinPool` कई रूपांतरणों को समानांतर में संभाल सकता है, लेकिन लाइसेंस मॉडल का ध्यान रखें—प्रत्येक थ्रेड अभी भी एक लाइसेंस सीट का उपभोग करता है।

## आगे क्या?

अब जब आप **convert excel to pptx** वर्कफ़्लो में निपुण हो गए हैं, तो इन आगे के प्रयोगों पर विचार करें:

- **Export Excel charts shapes** को कस्टम स्टाइलिंग के साथ PowerPoint में निर्यात करना (जैसे, रूपांतरण के बाद थीम रंग बदलना)।  
- **फ़ोल्डर में मौजूद कई `.xlsx` फ़ाइलों को एक ही PowerPoint डेक में बैच रूपांतरण** करना, इसके लिए `Presentation` API का उपयोग करके स्लाइड मर्ज करना।  
- प्रत्येक स्लाइड के लिए प्रोग्रामेटिक रूप से `NotesSlide` जोड़कर **स्पीकर नोट्स** जोड़ना—स्वचालित रिपोर्टिंग पाइपलाइन के लिए उत्तम।  

इनमें से प्रत्येक विषय उसी बुनियाद पर आधारित है जिसे हमने कवर किया है, इसलिए आप समाधान को आगे बढ़ाने के लिए पूरी तरह तैयार हैं।

---

### सारांश

हमने Aspose.Cells for Java का उपयोग करके **Excel को PPTX में बदलने** की एक सीधी विधि देखी, जिसमें **वर्कबुक को PowerPoint के रूप में सहेजना**, **Excel टेक्स्ट बॉक्स निर्यात** और **Excel चार्ट शैप्स निर्यात** को सक्षम करना शामिल था। पूरा कोड उदाहरण बॉक्स से बाहर चलाने योग्य है, और ऊपर दी गई टिप्स आपको सबसे आम अड़चनों से बचाएंगी।

क्या आपके पास कोई नया तरीका है जिसे आप साझा करना चाहते हैं? टिप्पणी छोड़ें, या कोड के साथ प्रयोग करें और हमें बताएं कि कैसे रहा। हैप्पी कन्वर्ज़न!

## अगला क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर कर सकें।

- [How to Convert Excel Charts to SVG Using Aspose.Cells in Java](/cells/english/java/charts-graphs/convert-excel-charts-svg-aspose-cells-java/)
- [How to Create and Configure Text Boxes in Excel Using Aspose.Cells Java for Enhanced Data Presentation](/cells/english/java/images-shapes/create-text-boxes-excel-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}