---
"date": "2025-04-09"
"description": "Aspose.Cells for Java का उपयोग करके A4, A3, A2, और Letter जैसे पेपर साइज़ सेट करना और प्राप्त करना सीखें। यह गाइड सेटअप से लेकर उन्नत कॉन्फ़िगरेशन तक सब कुछ कवर करती है।"
"title": "Aspose.Cells Java में मास्टर पेपर आकार सेटअप; हेडर और फूटर आसानी से कॉन्फ़िगर करें"
"url": "/hi/java/headers-footers/set-paper-size-aspose-cells-java-guide/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Aspose.Cells Java में मास्टर पेपर साइज़ सेटअप: हेडर और फ़ुटर आसानी से कॉन्फ़िगर करें

## Aspose.Cells Java का उपयोग करके पेपर का आकार कैसे सेट करें: एक डेवलपर गाइड

**परिचय**

क्या आप अपने Java एप्लीकेशन में स्प्रेडशीट के लिए अलग-अलग पेपर साइज़ सेट करने में परेशानी महसूस कर रहे हैं? Java के लिए Aspose.Cells के साथ, आप A2, A3, A4 और Letter जैसे विभिन्न पेपर आयामों को आसानी से प्रबंधित और कॉन्फ़िगर कर सकते हैं। यह गाइड आपको पेपर सेटिंग को कुशलतापूर्वक संभालने के लिए Aspose.Cells का उपयोग करने के बारे में बताता है।

**आप क्या सीखेंगे:**
- जावा अनुप्रयोग में Aspose.Cells का उपयोग करके विभिन्न पेपर आकार सेट करें।
- इन कागज़ आकारों की चौड़ाई और ऊंचाई इंच में प्राप्त करें।
- Aspose.Cells के लिए विशिष्ट प्रदर्शन युक्तियों के साथ अपने अनुप्रयोगों को अनुकूलित करें।

आइए जानें कि आप अपनी परियोजनाओं के लिए इस शक्तिशाली लाइब्रेरी का लाभ कैसे उठा सकते हैं!

**आवश्यक शर्तें**

शुरू करने से पहले, सुनिश्चित करें कि आपके पास:
- **जावा डेवलपमेंट किट (JDK):** आपकी मशीन पर संस्करण 8 या उससे ऊपर स्थापित है।
- **Aspose.Cells for Java लाइब्रेरी:** सुनिश्चित करें कि संस्करण 25.3 आपकी परियोजना निर्भरताओं में शामिल है।
- **आईडीई सेटअप:** जावा कोड लिखने और निष्पादित करने के लिए IntelliJ IDEA या Eclipse जैसे IDE का उपयोग करें।

सुनिश्चित करें कि आपको जावा प्रोग्रामिंग की बुनियादी समझ है, साथ ही यदि आप इन प्रणालियों के माध्यम से निर्भरताओं का प्रबंधन कर रहे हैं तो आपको मावेन या ग्रेडल बिल्ड टूल्स से भी परिचित होना चाहिए।

**Java के लिए Aspose.Cells सेट अप करना**

आरंभ करने के लिए, निर्भरता प्रबंधन उपकरणों का उपयोग करके अपने प्रोजेक्ट में Aspose.Cells लाइब्रेरी शामिल करें:

**मावेन**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**ग्रैडल**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

यहाँ से निःशुल्क परीक्षण डाउनलोड करें [Aspose वेबसाइट](https://releases.aspose.com/cells/java/) या पूर्ण सुविधा तक पहुंच के लिए अस्थायी लाइसेंस प्राप्त करें।

### सुविधा कार्यान्वयन मार्गदर्शिका

#### पेपर का आकार A2 पर सेट करें

**अवलोकन**
यह सुविधा आपके वर्कशीट के पेपर साइज़ को A2 पर सेट करने और इसके आयामों को इंच में प्राप्त करने का प्रदर्शन करती है। विशिष्ट आयामों की आवश्यकता वाली रिपोर्ट बनाने के लिए उपयोगी है।

**चरण-दर-चरण मार्गदर्शिका:**
1. **कार्यपुस्तिका और कार्यपत्रक आरंभ करें**
   ```java
   import com.aspose.cells.*;

   public class PaperSizeA2 {
       public static void main(String[] args) throws Exception {
           // एक नई कार्यपुस्तिका इंस्टेंस बनाएँ
           Workbook wb = new Workbook();

           // कार्यपुस्तिका में पहली कार्यपत्रिका तक पहुँचें
           Worksheet ws = wb.getWorksheets().get(0);
   ```
2. **कागज़ का आकार निर्धारित करें**
   ```java
           // कागज़ का आकार A2 पर सेट करें
           ws.getPageSetup().setPaperSize(PaperSizeType.PAPER_A_2);
   ```
3. **आयाम प्राप्त करें और प्रिंट करें**
   ```java
           // कागज़ की चौड़ाई और ऊंचाई इंच में प्राप्त करें और प्रिंट करें
           double paperWidth = ws.getPageSetup().getPaperWidth() / 72; // पॉइंट को इंच में बदलें
           double paperHeight = ws.getPageSetup().getPaperHeight() / 72;

           System.out.println("A2 Paper Width: " + paperWidth + " inches");
           System.out.println("A2 Paper Height: " + paperHeight + " inches");
       }
   }
   ```
**पैरामीटर और विधि उद्देश्य**
- `setPaperSize(PaperSizeType.PAPER_A_2)`: कागज़ का आकार A2 पर सेट करता है.
- `getPaperWidth()` और `getPaperHeight()`: आयामों को पॉइंट में प्राप्त करें, प्रदर्शन के लिए इंच में परिवर्तित करें।

#### कागज़ का आकार A3 पर सेट करें

**अवलोकन**
A2 को सेट करने के समान, यह सुविधा आपके वर्कशीट की पेपर सेटिंग को A3 में समायोजित करती है।

**चरण-दर-चरण मार्गदर्शिका:**
1. **कार्यपुस्तिका और कार्यपत्रक आरंभ करें**
   ```java
   import com.aspose.cells.*;

   public class PaperSizeA3 {
       public static void main(String[] args) throws Exception {
           // एक नई कार्यपुस्तिका इंस्टेंस बनाएँ
           Workbook wb = new Workbook();

           // कार्यपुस्तिका में पहली कार्यपत्रिका तक पहुँचें
           Worksheet ws = wb.getWorksheets().get(0);
   ```
2. **कागज़ का आकार निर्धारित करें**
   ```java
           // कागज़ का आकार A3 पर सेट करें
           ws.getPageSetup().setPaperSize(PaperSizeType.PAPER_A_3);
   ```
3. **आयाम प्राप्त करें और प्रिंट करें**
   ```java
           // कागज़ की चौड़ाई और ऊंचाई इंच में प्राप्त करें और प्रिंट करें
           double paperWidth = ws.getPageSetup().getPaperWidth() / 72; // पॉइंट को इंच में बदलें
           double paperHeight = ws.getPageSetup().getPaperHeight() / 72;

           System.out.println("A3 Paper Width: " + paperWidth + " inches");
           System.out.println("A3 Paper Height: " + paperHeight + " inches");
       }
   }
   ```
#### कागज़ का आकार A4 पर सेट करें

**अवलोकन**
यह अनुभाग कार्यपत्रक के आयाम को A4 पर सेट करने के बारे में बताता है, जो दस्तावेज़ निर्माण के लिए एक सामान्य आवश्यकता है।

**चरण-दर-चरण मार्गदर्शिका:**
1. **कार्यपुस्तिका और कार्यपत्रक आरंभ करें**
   ```java
   import com.aspose.cells.*;

   public class PaperSizeA4 {
       public static void main(String[] args) throws Exception {
           // एक नई कार्यपुस्तिका इंस्टेंस बनाएँ
           Workbook wb = new Workbook();

           // कार्यपुस्तिका में पहली कार्यपत्रिका तक पहुँचें
           Worksheet ws = wb.getWorksheets().get(0);
   ```
2. **कागज़ का आकार निर्धारित करें**
   ```java
           // कागज़ का आकार A4 पर सेट करें
           ws.getPageSetup().setPaperSize(PaperSizeType.PAPER_A_4);
   ```
3. **आयाम प्राप्त करें और प्रिंट करें**
   ```java
           // कागज़ की चौड़ाई और ऊंचाई इंच में प्राप्त करें और प्रिंट करें
           double paperWidth = ws.getPageSetup().getPaperWidth() / 72; // पॉइंट को इंच में बदलें
           double paperHeight = ws.getPageSetup().getPaperHeight() / 72;

           System.out.println("A4 Paper Width: " + paperWidth + " inches");
           System.out.println("A4 Paper Height: " + paperHeight + " inches");
       }
   }
   ```
#### पेपर आकार को लेटर पर सेट करें

**अवलोकन**
यह सुविधा आपके वर्कशीट के आकार को मानक लेटर प्रारूप में कॉन्फ़िगर करने में सक्षम बनाती है, जिसका व्यापक रूप से उत्तरी अमेरिका में उपयोग किया जाता है।

**चरण-दर-चरण मार्गदर्शिका:**
1. **कार्यपुस्तिका और कार्यपत्रक आरंभ करें**
   ```java
   import com.aspose.cells.*;

   public class PaperSizeLetter {
       public static void main(String[] args) throws Exception {
           // एक नई कार्यपुस्तिका इंस्टेंस बनाएँ
           Workbook wb = new Workbook();

           // कार्यपुस्तिका में पहली कार्यपत्रिका तक पहुँचें
           Worksheet ws = wb.getWorksheets().get(0);
   ```
2. **कागज़ का आकार निर्धारित करें**
   ```java
           // कागज़ का आकार लेटर पर सेट करें
           ws.getPageSetup().setPaperSize(PaperSizeType.PAPER_LETTER);
   ```
3. **आयाम प्राप्त करें और प्रिंट करें**
   ```java
           // कागज़ की चौड़ाई और ऊंचाई इंच में प्राप्त करें और प्रिंट करें
           double paperWidth = ws.getPageSetup().getPaperWidth() / 72; // पॉइंट को इंच में बदलें
           double paperHeight = ws.getPageSetup().getPaperHeight() / 72;

           System.out.println("Letter Paper Width: " + paperWidth + " inches");
           System.out.println("Letter Paper Height: " + paperHeight + " inches");
       }
   }
   ```
**व्यावहारिक अनुप्रयोगों**
- **रिपोर्ट मुद्रण:** रिपोर्ट को विभिन्न मानक आकारों जैसे A2, A3, A4, या लेटर पर प्रिंट करने के लिए स्वचालित रूप से कॉन्फ़िगर करें।
- **दस्तावेज़ प्रबंधन प्रणालियाँ:** एकीकृत सॉफ्टवेयर समाधानों में दस्तावेज़ प्रारूपों को समायोजित और प्रबंधित करें।
- **अनुकूलित टेम्पलेट्स:** ऐसे टेम्पलेट बनाएं जो विशिष्ट कागज़ आकार आवश्यकताओं के अनुकूल हों।

**प्रदर्शन संबंधी विचार**
- **स्मृति प्रबंधन:** हमेशा बंद `Workbook` संसाधनों को मुक्त करने के लिए उपयोग के बाद उदाहरण।
- **प्रचय संसाधन:** बैच प्रोसेसिंग लॉजिक सेट अप करके एकाधिक दस्तावेज़ों को कुशलतापूर्वक संभालें।

**निष्कर्ष**
जावा में Aspose.Cells का उपयोग करके वर्कशीट पेपर के आकार को सेट करने और प्राप्त करने की क्षमता में महारत हासिल करना दस्तावेज़ निर्माण के साथ काम करने वाले डेवलपर्स के लिए एक मूल्यवान कौशल है। यह मार्गदर्शिका सुनिश्चित करती है कि आपके अनुप्रयोग विशिष्ट आवश्यकताओं को सहजता से पूरा करते हैं।

इसके बाद, Aspose.Cells की अधिक सुविधाओं का पता लगाएं या उन्नत कॉन्फ़िगरेशन में गोता लगाएँ।

**अक्सर पूछे जाने वाले प्रश्न:**
- **मैं आयामों को पॉइंट से इंच में कैसे परिवर्तित करूं?**
  अंकों की संख्या को 72 से विभाजित करें।
- **क्या मैं इस गाइड का उपयोग व्यावसायिक अनुप्रयोगों के लिए कर सकता हूँ?**
  हां, जब तक आप Aspose.Cells लाइसेंसिंग शर्तों का पालन करते हैं।

**अग्रिम पठन:**
- [Aspose.Cells दस्तावेज़ीकरण](https://docs.aspose.com/cells/java/)
- [जावा प्रोग्रामिंग मूल बातें](https://docs.oracle.com/javase/tutorial/index.html)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}