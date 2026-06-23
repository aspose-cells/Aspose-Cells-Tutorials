---
date: '2026-05-23'
description: Aspose.Cells का उपयोग करके Excel हाइपरलिंक्स को Java में संपादित करना,
  Excel वर्कबुक को Java में लोड करना, और टूटे हुए Excel लिंक को प्रभावी ढंग से हटाना
  सीखें।
keywords:
- edit excel hyperlinks java
- load excel workbook java
- remove broken excel links
- maven dependency aspose cells
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Learn how to edit Excel hyperlinks Java using Aspose.Cells, load Excel
    workbook Java, and remove broken Excel links efficiently.
  headline: Edit Excel Hyperlinks Java – Process Multiple Files
  type: TechArticle
- description: Learn how to edit Excel hyperlinks Java using Aspose.Cells, load Excel
    workbook Java, and remove broken Excel links efficiently.
  name: Edit Excel Hyperlinks Java – Process Multiple Files
  steps:
  - name: '**Updating Web Links:** Automatically refresh outdated URLs in quarterly
      financial reports.'
    text: '**Updating Web Links:** Automatically refresh outdated URLs in quarterly
      financial reports.'
  - name: '**Consistency Across Documents:** Enforce a corporate branding policy by
      standardizing hyperlink destinations across dozens of departmental spreadsheets.'
    text: '**Consistency Across Documents:** Enforce a corporate branding policy by
      standardizing hyperlink destinations across dozens of departmental spreadsheets.'
  - name: '**Data Integration:** Point hyperlinks to new API endpoints or internal
      data portals after a system migration.'
    text: '**Data Integration:** Point hyperlinks to new API endpoints or internal
      data portals after a system migration.'
  type: HowTo
- questions:
  - answer: Yes, iterate through `workbook.getWorksheets()` and apply hyperlink changes
      to each worksheet.
    question: Can I edit multiple worksheets at once?
  - answer: Use error‑handling techniques such as try‑catch blocks and the removal
      logic shown in the editing example.
    question: How do I handle broken links with Aspose.Cells Java?
  - answer: Absolutely. Use `worksheet.getHyperlinks().add()` to insert new links
      into your worksheet.
    question: Is it possible to add new hyperlinks using Aspose.Cells Java?
  - answer: Yes, Aspose.Cells is available for .NET, C++, and more. Check out the
      [official website](https://www.aspose.com/) for language‑specific guides.
    question: Can I use Aspose.Cells with other programming languages besides Java?
  - answer: Regularly check your subscription status on the Aspose dashboard and renew
      or update your license as needed.
    question: How can I ensure my license remains active when using Aspose.Cells?
  type: FAQPage
title: Excel हाइपरलिंक्स को Java में संपादित करें – कई फ़ाइलों को प्रोसेस करें
url: /hi/java/advanced-features/edit-excel-hyperlinks-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel Hyperlinks Java को संपादित करें – कई फ़ाइलों को प्रोसेस करें

जब आपको बैच में कई वर्कबुक्स में **edit Excel hyperlinks Java** को संपादित करने की आवश्यकता होती है, तो इसे हाथ से करना त्रुटिप्रवण और समय‑साध्य होता है। चाहे आप एक कॉर्पोरेट वेबसाइट को माइग्रेट कर रहे हों, पुरानी URLs को ठीक कर रहे हों, या डेटा माइग्रेशन के बाद टूटे हुए लिंक को साफ़ कर रहे हों, Aspose.Cells for Java आपको प्रोग्रामेटिकली Excel वर्कबुक Java ऑब्जेक्ट्स को लोड करने, hyperlink URLs को संशोधित करने, और सुरक्षित रूप से टूटे हुए Excel लिंक को हटाने की सुविधा देता है—सभी एक ही स्वचालित रन में। यह गाइड आपको पूरे वर्कफ़्लो के माध्यम से ले जाता है, प्रोजेक्ट सेटअप से लेकर अपडेटेड फ़ाइलों को सहेजने तक।

## त्वरित उत्तर
- **यह ट्यूटोरियल क्या कवर करता है?** Aspose.Cells for Java का उपयोग करके एक या कई Excel फ़ाइलों में hyperlinks को संपादित और अपडेट करना।  
- **क्या मुझे लाइसेंस की आवश्यकता है?** एक मुफ्त ट्रायल परीक्षण के लिए काम करता है; उत्पादन के लिए एक व्यावसायिक लाइसेंस आवश्यक है।  
- **क्या मैं एक साथ कई फ़ाइलों को प्रोसेस कर सकता हूँ?** हाँ – बस एक डायरेक्टरी में फ़ाइलों पर लूप करें।  
- **टूटे हुए लिंक कैसे हटाएँ?** लूप में अमान्य URLs का पता लगाएँ और उन्हें `worksheet.getHyperlinks().remove(i)` से हटाएँ।  
- **कौन सा Java संस्करण आवश्यक है?** Java 8 या उससे ऊपर।

## edit excel hyperlinks java क्या है?
Edit Excel hyperlinks Java वह प्रक्रिया है जिसमें Aspose.Cells लाइब्रेरी का उपयोग करके Excel वर्कबुक के भीतर Hyperlink ऑब्जेक्ट्स की `address` प्रॉपर्टी को प्रोग्रामेटिकली बदलते हैं। यह तरीका मैन्युअल संपादन को समाप्त करता है, स्थिरता की गारंटी देता है, और सेकंडों में हजारों फ़ाइलों पर लागू किया जा सकता है।

## hyperlink संपादन के लिए Aspose.Cells क्यों उपयोग करें?
Aspose.Cells **50+ इनपुट और आउटपुट फ़ॉर्मेट**—जैसे XLSX, XLS, CSV, और ODS—को समर्थन देता है और **1 million rows** तक के वर्कबुक को पूरी फ़ाइल को मेमोरी में लोड किए बिना प्रोसेस कर सकता है, इसके स्ट्रीमिंग API के कारण। यह लाइब्रेरी सेल फ़ॉर्मेटिंग, फ़ॉर्मूले, और चार्ट डेटा को भी संरक्षित रखती है, यह सुनिश्चित करते हुए कि केवल hyperlink लक्ष्य बदलता है जबकि वर्कशीट का बाकी हिस्सा अपरिवर्तित रहता है।

## आवश्यकताएँ
- **Aspose.Cells for Java** संस्करण 25.3 या बाद का (नीचे Maven/Gradle स्निपेट देखें)।  
- आपके विकास मशीन पर JDK 8 या नया स्थापित होना चाहिए।  
- IntelliJ IDEA या Eclipse जैसे IDE।  
- बुनियादी Java ज्ञान और Excel अवधारणाओं की परिचितता।

## Excel workbook Java को कैसे लोड करें?
`Workbook` Aspose.Cells क्लास है जो पूरी Excel फ़ाइल का प्रतिनिधित्व करता है, वर्कशीट्स, सेल्स, और दस्तावेज‑स्तर की प्रॉपर्टीज़ तक पहुँच प्रदान करता है।  
अपने वर्कबुक को लोड करने के लिए एक `Workbook` इंस्टेंस बनाएँ जो डिस्क पर स्थित Excel फ़ाइल की ओर इशारा करता हो। यह एकल पंक्ति फ़ाइल को मेमोरी में पढ़ती है, hyperlink हेरफेर के लिए तैयार। एक बार इंस्टैंशिएट होने के बाद, आप उसकी वर्कशीट्स के माध्यम से नेविगेट कर सकते हैं, सेल मान पढ़ सकते हैं, और आवश्यकतानुसार hyperlinks, चार्ट्स, या फ़ॉर्मूले जैसे ऑब्जेक्ट्स को संशोधित कर सकते हैं।

```text
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```
```

### परिभाषा एंकर
`Workbook` क्लास Aspose.Cells का कोर ऑब्जेक्ट है जो पूरी Excel फ़ाइल का प्रतिनिधित्व करता है, वर्कशीट्स, सेल्स, और दस्तावेज‑स्तर की प्रॉपर्टीज़ को प्रोग्रामेटिक एक्सेस के लिए उजागर करता है।

## Aspose.Cells for Java सेट अप करना
समर्थित बिल्ड टूल्स में से एक का उपयोग करके लाइब्रेरी को अपने प्रोजेक्ट में जोड़ें।

**Maven:**
```text
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```
```

**Gradle:**
```text
```java
import com.aspose.cells.Workbook;

public class InitializeAsposeCells {
    public static void main(String[] args) throws Exception {
        // Set the license (optional if you have a valid temporary or purchased license)
        // License license = new License();
        // license.setLicense("path_to_your_license_file");

        // Create a Workbook object to work with an Excel file
        Workbook workbook = new Workbook();
    }
}
```
```

### लाइसेंस प्राप्त करने के चरण
To use Aspose.Cells, you can start with a free trial or request a temporary license for evaluation purposes:
- **Free Trial:** [Aspose रिलीज़र्स](https://releases.aspose.com/cells/java/) से डाउनलोड करें।  
- **Temporary License:** सीमाओं के बिना सभी फीचर अनलॉक करने के लिए [यहाँ](https://purchase.aspose.com/temporary-license/) अनुरोध करें।  
- **Purchase:** व्यावसायिक उपयोग के लिए, [Aspose खरीदारी](https://purchase.aspose.com/buy) पर लाइसेंस खरीदें।

#### बुनियादी इनिशियलाइज़ेशन और सेटअप
```text
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class LoadWorkbook {
    public static void main(String[] args) throws Exception {
        // Specify the directory path for your data files
        String dataDir = "path_to_your_data_directory/";

        // Open an existing workbook from the specified file path
        Workbook workbook = new Workbook(dataDir + "source.xlsx");

        // Access the first worksheet in the workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);
    }
}
```
```

## Excel worksheets में hyperlinks को कैसे संपादित करें?
`Hyperlink` Aspose.Cells ऑब्जेक्ट है जो सेल में क्लिक करने योग्य लिंक का प्रतिनिधित्व करता है, और इसके address को प्राप्त और सेट करने के मेथड्स प्रदान करता है।  
प्रत्येक वर्कशीट की hyperlink कलेक्शन पर इटररेट करें, `address` प्रॉपर्टी को अपडेट करें, और वैकल्पिक रूप से उन एंट्रीज़ को हटाएँ जो अमान्य URLs की ओर इशारा करती हैं। निम्न पैटर्न एक संक्षिप्त लूप में दोनों कार्यों को संभालता है, यह सुनिश्चित करते हुए कि सभी लिंक लगातार अपडेट हों जबकि अन्य सेल डेटा सुरक्षित रहे।

```text
```java
import com.aspose.cells.Hyperlink;

public class EditHyperlinks {
    public static void main(String[] args) throws Exception {
        String dataDir = "path_to_your_data_directory/";
        
        // Load the workbook and get the first worksheet
        Workbook workbook = new Workbook(dataDir + "source.xlsx");
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Iterate through each hyperlink in the worksheet
        for (int i = 0; i < worksheet.getHyperlinks().getCount(); i++) {
            Hyperlink hl = worksheet.getHyperlinks().get(i);
            
            // Example: change hyperlink URL Excel to a new address
            hl.setAddress("http://www.aspose.com");
            
            // Optional: remove if the URL is empty or malformed
            if (hl.getAddress() == null || hl.getAddress().trim().isEmpty()) {
                worksheet.getHyperlinks().remove(i);
                i--; // adjust index after removal
            }
        }

        // Save the changes to a new file
        workbook.save(dataDir + "EHOfWorksheet_out.xlsx");
    }
}
```
```

### परिभाषा एंकर
`Hyperlink` क्लास सेल में क्लिक करने योग्य लिंक का प्रतिनिधित्व करता है; इसका `setAddress(String)` मेथड URL को अपडेट करता है, जबकि `getAddress()` वर्तमान लक्ष्य को प्राप्त करता है।

#### कोड स्निपेट्स की व्याख्या
- **Hyperlink Access:** `worksheet.getHyperlinks().get(i)` प्रत्येक hyperlink ऑब्जेक्ट को प्राप्त करता है।  
- **Updating Hyperlinks:** `hl.setAddress("http://www.aspose.com")` लिंक को नए पते में बदलता है, जिससे **change hyperlink url excel** आवश्यकता पूरी होती है।  
- **Removing Broken Links:** यह कंडीशनल ब्लॉक दिखाता है कि **remove broken excel links** को सुरक्षित रूप से कैसे हटाएँ।

## टूटे हुए Excel लिंक को कैसे हटाएँ?
एक टूटे हुए लिंक का पता लगाने के लिए जांचें कि URL `http://` या `https://` से शुरू होता है और एक सरल regex पैटर्न को पूरा करता है। यदि यह वैधता में विफल रहता है, तो वर्कबुक को साफ़ रखने के लिए इसे कलेक्शन से हटा दें। यह तरीका उपयोगकर्ताओं को डेड लिंक से बचाता है और दस्तावेज़ की पेशेवर उपस्थिति बनाए रखता है।

```text
```java
// Save the updated workbook
dataDir + "EHOfWorksheet_out.xlsx";
```
```

## अपडेटेड वर्कबुक को सहेजना
सभी संशोधनों के बाद, वर्कबुक को डिस्क पर वापस सहेजें। Aspose.Cells फ़ाइल को उसी फ़ॉर्मेट में लिखता है जिसमें यह लोड किया गया था, सभी non‑hyperlink डेटा को संरक्षित रखता है।

```text
```java
// Save the updated workbook
dataDir + "EHOfWorksheet_out.xlsx";
```
```

## व्यावहारिक अनुप्रयोग
Here are some real‑world scenarios where you might apply hyperlink editing with Aspose.Cells Java:
1. **Updating Web Links:** त्रैमासिक वित्तीय रिपोर्टों में पुरानी URLs को स्वचालित रूप से रिफ्रेश करें।  
2. **Consistency Across Documents:** कई विभागीय स्प्रेडशीट्स में hyperlink गंतव्यों को मानकीकृत करके कॉर्पोरेट ब्रांडिंग नीति लागू करें।  
3. **Data Integration:** सिस्टम माइग्रेशन के बाद hyperlinks को नए API एंडपॉइंट्स या आंतरिक डेटा पोर्टल्स की ओर निर्देशित करें।

## प्रदर्शन विचार
When you **process multiple Excel files**, keep these optimization tips in mind:
- **Efficient Memory Management:** Java के try‑with‑resources का उपयोग करें ताकि वर्कबुक्स तुरंत बंद हो जाएँ।  
- **Batch Processing:** अलग-अलग प्रोसेस लॉन्च करने के बजाय एक ही JVM रन में फ़ाइलों की डायरेक्टरी पर इटररेट करें।  
- **Minimize Loop Work:** CPU ओवरहेड कम करने के लिए URL वैधता को आंतरिक hyperlink लूप के बाहर करें।

## निष्कर्ष
Aspose.Cells Java के साथ Excel में hyperlinks को संपादित करना दस्तावेज़ लिंक प्रबंधन को कुशल बनाता है। इस गाइड का पालन करके, आपने सीखा कि कैसे **process multiple Excel files**, hyperlink URLs को संशोधित करें, और टूटे हुए लिंक को हटाएँ—सभी आपके Java एप्लिकेशन में सहजता से एकीकृत।

इन कौशलों को अभ्यास में लाने के लिए तैयार हैं? अधिक उन्नत फीचर्स का पता लगाने के लिए [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/) में गहराई से देखें।

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या मैं एक साथ कई वर्कशीट्स को संपादित कर सकता हूँ?**  
A: हाँ, `workbook.getWorksheets()` पर इटररेट करें और प्रत्येक वर्कशीट में hyperlink परिवर्तन लागू करें।

**Q: Aspose.Cells Java के साथ टूटे हुए लिंक को कैसे संभालें?**  
A: try‑catch ब्लॉक्स जैसी एरर‑हैंडलिंग तकनीकों और संपादन उदाहरण में दिखाए गए हटाने लॉजिक का उपयोग करें।

**Q: क्या Aspose.Cells Java का उपयोग करके नए hyperlinks जोड़ना संभव है?**  
A: बिल्कुल। `worksheet.getHyperlinks().add()` का उपयोग करके अपनी वर्कशीट में नए लिंक डालें।

**Q: क्या मैं Java के अलावा अन्य प्रोग्रामिंग भाषाओं के साथ Aspose.Cells का उपयोग कर सकता हूँ?**  
A: हाँ, Aspose.Cells .NET, C++, आदि के लिए उपलब्ध है। भाषा‑विशिष्ट गाइड्स के लिए [official website](https://www.aspose.com/) देखें।

**Q: Aspose.Cells का उपयोग करते समय मैं कैसे सुनिश्चित करूँ कि मेरा लाइसेंस सक्रिय रहे?**  
A: Aspose डैशबोर्ड पर नियमित रूप से अपनी सब्सक्रिप्शन स्थिति जांचें और आवश्यकतानुसार लाइसेंस को नवीनीकृत या अपडेट करें।

## अतिरिक्त संसाधन
- [Aspose रिलीज़र्स](https://releases.aspose.com/cells/java/)
- [Aspose डाउनलोड्स](https://releases.aspose.com/cells/java/)
- [रिलीज़ पेज](https://releases.aspose.com/cells/java/)
- [Aspose.Cells Java रेफ़रेंस](https://reference.aspose.com/cells/java/)
- [Aspose.Cells डॉक्यूमेंटेशन](https://reference.aspose.com/cells/java/)
- [Aspose खरीदारी](https://purchase.aspose.com/buy)
- [यहाँ](https://purchase.aspose.com/buy)
- [Aspose टेम्पररी लाइसेंस](https://purchase.aspose.com/temporary-license/)
- [यहाँ](https://purchase.aspose.com/temporary-license/)
- [आधिकारिक वेबसाइट](https://www.aspose.com/)
- [Aspose सपोर्ट फ़ोरम](https://forum.aspose.com/c/cells/9)

---

**अंतिम अपडेट:** 2026-05-23  
**परीक्षण किया गया:** Aspose.Cells 25.3 for Java  
**लेखक:** Aspose  

{{< blocks/products/products-backtop-button >}}

## संबंधित ट्यूटोरियल्स

- [Aspose.Cells for Java में महारत: Excel वर्कबुक्स को कुशलतापूर्वक लोड और संशोधित करें](/cells/java/workbook-operations/aspose-cells-java-load-modify-excel/)
- [Aspose.Cells for Java में महारत: Excel फ़ाइलों को कुशलतापूर्वक लोड और सहेजें](/cells/java/workbook-operations/aspose-cells-java-load-save-excel-files/)
- [Aspose.Cells for Java के साथ Excel से URL निकालें – डेटा कनेक्शन लोड करें](/cells/java/advanced-features/aspose-cells-java-excel-data-connections/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}