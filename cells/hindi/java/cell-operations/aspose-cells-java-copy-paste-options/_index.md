---
date: '2026-02-22'
description: Aspose.Cells in Java का उपयोग करके CopyOptions और PasteOptions के साथ
  Excel रिपोर्टिंग को स्वचालित करना सीखें, जिससे सूत्र सटीक रहें और केवल दृश्यमान
  मान पेस्ट हों।
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
title: एक्सेल रिपोर्टिंग को स्वचालित करें – जावा में Aspose.Cells के साथ CopyOptions
  और PasteOptions में निपुणता
url: /hi/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells के साथ Excel रिपोर्टिंग को स्वचालित करें: Java में CopyOptions और PasteOptions

क्या आप Java का उपयोग करके **Excel रिपोर्टिंग को स्वचालित** करना चाहते हैं? Aspose.Cells के साथ आप प्रोग्रामेटिकली कॉपी, पेस्ट और फ़ॉर्मूले समायोजित कर सकते हैं ताकि आपकी रिपोर्टें सटीक रहें और केवल आवश्यक डेटा ही ट्रांसफ़र हो। इस ट्यूटोरियल में हम दो आवश्यक फीचर्स—**CopyOptions.ReferToDestinationSheet** और **PasteOptions**—के माध्यम से चलेंगे, जो आपको फ़ॉर्मूला रेफ़रेंसेज़ को संरक्षित रखने और केवल दृश्यमान कोशिकाओं से मान पेस्ट करने की अनुमति देते हैं।

## त्वरित उत्तर
- **`CopyOptions.ReferToDestinationSheet` क्या करता है?** डेटा कॉपी करते समय फ़ॉर्मूले को गंतव्य शीट की ओर इंगित करने के लिए समायोजित करता है।  
- **मैं केवल दृश्यमान कोशिकाओं को कैसे पेस्ट कर सकता हूँ?** `PasteOptions.setOnlyVisibleCells(true)` को `PasteType.VALUES` के साथ सेट करें।  
- **कौन सा लाइब्रेरी संस्करण आवश्यक है?** Aspose.Cells 25.3 या बाद का।  
- **उत्पादन के लिए लाइसेंस चाहिए?** हाँ, एक स्थायी या अस्थायी लाइसेंस मूल्यांकन सीमाओं को हटा देता है।  
- **क्या मैं Maven या Gradle का उपयोग कर सकता हूँ?** दोनों समर्थित हैं; नीचे निर्भरता स्निपेट देखें।

## “Excel रिपोर्टिंग को स्वचालित” क्या है?
Excel रिपोर्टिंग को स्वचालित करने का मतलब है प्रोग्रामेटिकली Excel वर्कबुक्स को जनरेट, कंसॉलिडेट और फ़ॉर्मेट करना, जिससे मैन्युअल कॉपी‑पेस्ट चरण समाप्त होते हैं और त्रुटियों में कमी आती है। Aspose.Cells एक समृद्ध API प्रदान करता है जो Java डेवलपर्स को बड़े पैमाने पर स्प्रेडशीट्स को नियंत्रित करने देता है।

## रिपोर्टिंग के लिए CopyOptions और PasteOptions का उपयोग क्यों करें?
- **फ़ॉर्मूला की अखंडता बनाए रखें** जब शीट्स के बीच डेटा स्थानांतरित किया जाता है।  
- **छिपी हुई पंक्तियों/कॉलमों को बाहर रखें** ताकि रिपोर्ट साफ़ और केंद्रित रहे।  
- **प्रदर्शन बढ़ाएँ** केवल आवश्यक डेटा को कॉपी करके, पूरी रेंज की बजाय।

## पूर्वापेक्षाएँ
- Java 8 या उससे ऊपर।  
- निर्भरता प्रबंधन के लिए Maven या Gradle।  
- Aspose.Cells 25.3+ (ट्रायल, अस्थायी, या स्थायी लाइसेंस)।

## Java के लिए Aspose.Cells सेटअप करना

अपने प्रोजेक्ट में लाइब्रेरी जोड़ने के लिए नीचे में से एक का उपयोग करें:

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
implementation 'com.aspose:aspose-cells:25.3'
```

### लाइसेंस प्राप्ति
- **Free Trial** – मूल्यांकन के लिए पूर्ण फीचर सेट।  
- **Temporary License** – परीक्षण के दौरान ट्रायल सीमाओं को हटाता है।  
- **Permanent License** – उत्पादन कार्यभार के लिए अनुशंसित।

अपने Java कोड में Aspose.Cells को इनिशियलाइज़ करें:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## चरण‑दर‑चरण गाइड

### 1. ReferToDestinationSheet के साथ CopyOptions

#### अवलोकन
`CopyOptions.ReferToDestinationSheet` को `true` सेट करने से फ़ॉर्मूला रेफ़रेंसेज़ को पुनर्लेखित किया जाता है ताकि कॉपी ऑपरेशन के बाद वे नई शीट की ओर संकेत करें।

#### चरण 1: Workbook और Worksheets को इनिशियलाइज़ करें
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### चरण 2: CopyOptions को कॉन्फ़िगर करें
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### चरण 3: कॉपी ऑपरेशन निष्पादित करें
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*क्यों यह महत्वपूर्ण है*: जो फ़ॉर्मूले मूल रूप से `Sheet1` को संदर्भित करते थे, अब सही ढंग से `DestSheet` को संदर्भित करेंगे, जिससे आपकी स्वचालित रिपोर्टें विश्वसनीय बनी रहेंगी।

**समस्या निवारण टिप**: यदि फ़ॉर्मूले अभी भी पुरानी शीट को संदर्भित कर रहे हैं, तो सुनिश्चित करें कि `setReferToDestinationSheet(true)` को कॉपी से **पहले** कॉल किया गया है।

### 2. दृश्यमान कोशिकाओं से केवल मानों के लिए PasteOptions

#### अवलोकन
`PasteOptions` आपको यह निर्धारित करने देता है कि क्या पेस्ट किया जाए। `PasteType.VALUES` को `onlyVisibleCells=true` के साथ उपयोग करने से केवल प्रदर्शित मान कॉपी होते हैं, छिपी हुई पंक्तियों/कॉलमों और फ़ॉर्मेटिंग को अनदेखा किया जाता है।

#### चरण 1: Workbook और Worksheets को इनिशियलाइज़ करें
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### चरण 2: PasteOptions को कॉन्फ़िगर करें
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### चरण 3: पेस्ट ऑपरेशन निष्पादित करें
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*क्यों यह महत्वपूर्ण है*: फ़िल्टर किए गए डेटा को निकालने या बिना छिपी पंक्तियों या फ़ॉर्मेटिंग शोर के साफ़ रिपोर्ट बनाने के लिए आदर्श।

**समस्या निवारण टिप**: कॉपी करने से पहले सुनिश्चित करें कि पंक्तियाँ/कॉलम Excel में वास्तव में छिपी हुई हैं; अन्यथा, वे शामिल हो जाएँगी।

## व्यावहारिक अनुप्रयोग
1. **Financial Consolidation** – सभी फ़ॉर्मूले सटीक रखते हुए मासिक शीट्स को एक मास्टर वर्कबुक में मिलाएँ।  
2. **Filtered Data Export** – फ़िल्टर की गई तालिका से केवल दृश्यमान पंक्तियों को सारांश शीट में खींचें।  
3. **Scheduled Report Generation** – सटीक सेल मान और सही रेफ़रेंसेज़ के साथ रात्रीकालीन Excel रिपोर्ट निर्माण को स्वचालित करें।

## प्रदर्शन संबंधी विचार
- **वर्कबुक्स को डिस्पोज़ करें** जब काम समाप्त हो (`wb.dispose();`) ताकि नेटिव संसाधन मुक्त हों।  
- **बैच ऑपरेशन्स** – ओवरहेड कम करने के लिए कई कॉपी/पेस्ट कॉल्स को समूहित करें।  
- **मेमोरी मॉनिटर करें** – बड़े वर्कबुक्स को बढ़े हुए हीप (`-Xmx2g`) की आवश्यकता हो सकती है।

## अक्सर पूछे जाने वाले प्रश्न

**Q1: `CopyOptions.ReferToDestinationSheet` का उपयोग किस लिए किया जाता है?**  
A: यह फ़ॉर्मूला रेफ़रेंसेज़ को पुनर्लेखित करता है ताकि कॉपी के बाद वे गंतव्य शीट की ओर संकेत करें, जिससे रिपोर्टिंग फ़ॉर्मूले सही बने रहें।

**Q2: मैं केवल दृश्यमान कोशिकाओं को कैसे पेस्ट करूँ?**  
A: `PasteOptions.setOnlyVisibleCells(true)` सेट करें और `PasteType.VALUES` चुनें।

**Q3: क्या मैं बिना लाइसेंस खरीदे Aspose.Cells का उपयोग कर सकता हूँ?**  
A: हाँ, मूल्यांकन के लिए एक फ्री ट्रायल या अस्थायी लाइसेंस उपलब्ध है, लेकिन उत्पादन के लिए स्थायी लाइसेंस आवश्यक है।

**Q4: कॉपी करने के बाद कुछ रेफ़रेंसेज़ अभी भी गलत क्यों हैं?**  
A: यह सुनिश्चित करें कि `ReferToDestinationSheet` कॉपी ऑपरेशन से **पहले** सक्षम हो और स्रोत फ़ॉर्मूले में बाहरी वर्कबुक लिंक न हों।

**Q5: मुझे कौन सी मेमोरी‑मैनेजमेंट सर्वोत्तम प्रथाएँ अपनानी चाहिए?**  
A: समाप्त होने पर `Workbook` ऑब्जेक्ट्स को डिस्पोज़ करें, बड़े फ़ाइलों को भागों में प्रोसेस करें, और JVM हीप उपयोग की निगरानी रखें।

**Q6: क्या एक ही ऑपरेशन में CopyOptions और PasteOptions को मिलाया जा सकता है?**  
A: हाँ, आप पहले `CopyOptions` से कॉपी करके और फिर लक्ष्य रेंज पर `PasteOptions` लागू करके उन्हें चेन कर सकते हैं।

## संसाधन
- **दस्तावेज़ीकरण**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **डाउनलोड**: [Aspose.Cells Releases for Java](https://releases.aspose.com/cells/java/)  
- **खरीदें**: [Aspose.Cells खरीदें](https://purchase.aspose.com/buy)  
- **फ्री ट्रायल**: [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **अस्थायी लाइसेंस**: [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **सपोर्ट फ़ोरम**: [Aspose Support](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**अंतिम अपडेट:** 2026-02-22  
**परीक्षित संस्करण:** Aspose.Cells 25.3 for Java  
**लेखक:** Aspose