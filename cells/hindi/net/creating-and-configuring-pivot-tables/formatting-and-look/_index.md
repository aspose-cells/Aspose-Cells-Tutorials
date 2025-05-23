---
"description": ".NET के लिए Aspose.Cells के साथ अपने Excel पिवट टेबल को बेहतर बनाएँ। अपने डेटा प्रेजेंटेशन को आसानी से फ़ॉर्मेट, कस्टमाइज़ और ऑटोमेट करना सीखें।"
"linktitle": ".NET में प्रोग्रामेटिक रूप से पिवट टेबल का स्वरूपण और स्वरूप"
"second_title": "Aspose.Cells .NET एक्सेल प्रोसेसिंग API"
"title": ".NET में प्रोग्रामेटिक रूप से पिवट टेबल का स्वरूपण और स्वरूप"
"url": "/hi/net/creating-and-configuring-pivot-tables/formatting-and-look/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# .NET में प्रोग्रामेटिक रूप से पिवट टेबल का स्वरूपण और स्वरूप

## परिचय
एक्सेल में पिवट टेबल शानदार उपकरण हैं जो उपयोगकर्ताओं को जटिल डेटासेट को सारांशित करने और उनका विश्लेषण करने की अनुमति देते हैं। वे सामान्य डेटा को आकर्षक और जानकारीपूर्ण रिपोर्ट में बदल सकते हैं, जिससे उपयोगकर्ता जल्दी से जानकारी प्राप्त कर सकते हैं। इस ट्यूटोरियल में, हम .NET के लिए Aspose.Cells का उपयोग करके पिवट टेबल शैलियों में हेरफेर करने का तरीका जानेंगे, जिससे आप अपनी एक्सेल रिपोर्ट को आसानी से स्वचालित और अनुकूलित कर सकेंगे। क्या आप अपने डेटा प्रस्तुति कौशल को बढ़ाने के लिए तैयार हैं? आइए शुरू करते हैं!
## आवश्यक शर्तें
इससे पहले कि हम इस यात्रा पर निकलें, कुछ आवश्यक चीजें आपके पास होनी चाहिए:
1. विजुअल स्टूडियो: यह कोडिंग और परीक्षण के लिए हमारा मुख्य वातावरण होगा।
2. Aspose.Cells for .NET: सुनिश्चित करें कि आपके पास यह लाइब्रेरी स्थापित है। आप ऐसा कर सकते हैं [यहाँ पर डाउनलोड करो](https://releases.aspose.com/cells/net/).
3. C# की बुनियादी समझ: C# प्रोग्रामिंग से परिचित होने से आपको आसानी से अनुसरण करने में मदद मिलेगी।
4. एक्सेल फ़ाइल: आपको एक मौजूदा एक्सेल फ़ाइल की आवश्यकता होगी जिसमें पिवट टेबल हो। यदि आपके पास पिवट टेबल नहीं है, तो आप Microsoft Excel का उपयोग करके एक सरल पिवट टेबल बना सकते हैं।
एक बार जब आपने सब कुछ सेट कर लिया, तो चलिए आवश्यक पैकेजों को आयात करने के लिए आगे बढ़ते हैं!
## पैकेज आयात करें
आरंभ करने के लिए, हमें अपने C# प्रोजेक्ट में आवश्यक लाइब्रेरीज़ को आयात करना होगा। यहाँ बताया गया है कि आप ऐसा कैसे कर सकते हैं:
### एक नया C# प्रोजेक्ट बनाएं
सबसे पहले, Visual Studio खोलें और एक नया कंसोल एप्लीकेशन प्रोजेक्ट बनाएँ। इससे हम अपना कोड आसानी से चला पाएँगे।
### संदर्भ जोड़ें
एक बार आपका प्रोजेक्ट सेट हो जाने के बाद, आपको Aspose.Cells लाइब्रेरी में एक संदर्भ जोड़ना होगा:
- समाधान एक्सप्लोरर में अपने प्रोजेक्ट पर राइट-क्लिक करें।
- "NuGet पैकेज प्रबंधित करें" चुनें.
- "Aspose.Cells" खोजें और पैकेज स्थापित करें।
ऐसा करने के बाद, आप Aspose.Cells नामस्थान को आयात करने के लिए तैयार हैं। नीचे आवश्यक पैकेज आयात करने के लिए कोड दिया गया है:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
अब जबकि हमने अपने पैकेज आयात कर लिए हैं, आइए एक्सेल में पिवट टेबल के स्वरूपण में बदलाव करने के तरीके पर करीब से नज़र डालें।
## चरण 1: अपनी दस्तावेज़ निर्देशिका सेट करें
सबसे पहले, हम अपनी एक्सेल फ़ाइल का पथ निर्धारित करेंगे। इसे इस प्रकार करें:
```csharp
// दस्तावेज़ निर्देशिका का पथ.
string dataDir = "Your Document Directory";
```
प्रतिस्थापित करना सुनिश्चित करें `"Your Document Directory"` वास्तविक पथ के साथ जहां आपकी एक्सेल फ़ाइल संग्रहीत है।
## चरण 2: कार्यपुस्तिका लोड करें
इसके बाद, हमें आपकी मौजूदा एक्सेल फ़ाइल को लोड करना होगा। इस चरण में, हम इसका उपयोग करेंगे `Workbook` Aspose.Cells द्वारा प्रदान किया गया वर्ग.
```csharp
// टेम्पलेट फ़ाइल लोड करें
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
जब आप प्रतिस्थापित करते हैं `"Book1.xls"` आपके वास्तविक फ़ाइल नाम के साथ, `workbook` ऑब्जेक्ट में अब एक्सेल डेटा शामिल होगा.
## चरण 3: वर्कशीट और पिवट टेबल तक पहुंचें
अब, हम उस शीट और पिवट टेबल को लेना चाहते हैं जिसके साथ हम काम करेंगे:
```csharp
// पहली वर्कशीट प्राप्त करें
Worksheet worksheet = workbook.Worksheets[0];
var pivot = workbook.Worksheets[0].PivotTables[0];
```
इस मामले में, हम पहली वर्कशीट और पहली पिवट टेबल का उपयोग कर रहे हैं। यदि आपकी एक्सेल फ़ाइल में कई शीट या पिवट टेबल हैं, तो इंडेक्स मानों को तदनुसार समायोजित करना सुनिश्चित करें।

अब जब हमारे पास पिवट टेबल तक पहुँच है, तो इसे देखने में आकर्षक बनाने का समय आ गया है! हम एक स्टाइल सेट कर सकते हैं और पूरी पिवट टेबल को फ़ॉर्मेट कर सकते हैं। यहाँ बताया गया है कि कैसे:
## चरण 4: पिवट तालिका शैली सेट करना
आइए अपनी पिवट तालिका पर एक पूर्व-निर्धारित शैली लागू करें:
```csharp
pivot.PivotTableStyleType = PivotTableStyleType.PivotTableStyleDark1;
```
कोड की यह पंक्ति पिवट टेबल की शैली को डार्क थीम में बदल देती है। आप अपनी ज़रूरतों के हिसाब से कोई एक स्टाइल ढूँढने के लिए Aspose.Cells लाइब्रेरी में उपलब्ध विभिन्न स्टाइल को एक्सप्लोर कर सकते हैं।
## चरण 5: पिवट तालिका शैली को अनुकूलित करें
आगे के अनुकूलन के लिए, हम अपनी शैली बना सकते हैं। यह कितना बढ़िया है? यहाँ बताया गया है कि आप इसे कैसे कर सकते हैं:
```csharp
Style style = workbook.CreateStyle();
style.Font.Name = "Arial Black";
style.ForegroundColor = Color.Yellow;
style.Pattern = BackgroundType.Solid;
```
इस स्निपेट में:
- हमने फ़ॉन्ट को "एरियल ब्लैक" के रूप में निर्दिष्ट किया है।
- अग्रभूमि का रंग पीला सेट किया गया है।
- हमने पैटर्न को ठोस पर सेट किया।
## चरण 6: पिवट तालिका पर कस्टम शैली लागू करें
अंत में, आइए इस नव निर्मित शैली को संपूर्ण पिवट तालिका को प्रारूपित करने के लिए लागू करें:
```csharp
pivot.FormatAll(style);
```
यह लाइन पिवट टेबल के सभी डेटा पर आपकी कस्टम शैली लागू करती है। अब आपकी टेबल शानदार दिखनी चाहिए!
## चरण 7: अपने परिवर्तन सहेजें
एक बार जब आप अपनी पिवट टेबल को फ़ॉर्मेट करना समाप्त कर लें, तो परिवर्तनों को सहेजना न भूलें। दस्तावेज़ को सहेजने का तरीका इस प्रकार है:
```csharp
// एक्सेल फ़ाइल को सहेजना
workbook.Save(dataDir + "output.xls");
```
प्रतिस्थापित करें `"output.xls"` नए स्वरूपित एक्सेल फ़ाइल के लिए आप जो भी नाम चाहते हैं, उसे चुनें। और देखिए! आपने .NET के लिए Aspose.Cells का उपयोग करके पिवट टेबल को सफलतापूर्वक स्वरूपित कर लिया है।
## निष्कर्ष
संक्षेप में, हमने .NET के लिए Aspose.Cells का उपयोग करके Excel में पिवट टेबल को प्रोग्रामेटिक रूप से फ़ॉर्मेट करने की यात्रा शुरू की है। हमने आवश्यक पैकेज आयात करके शुरुआत की, एक मौजूदा Excel कार्यपुस्तिका लोड की, पिवट टेबल शैलियों को अनुकूलित किया, और अंत में हमारे फ़ॉर्मेट किए गए आउटपुट को सहेजा। अपने वर्कफ़्लो में ऐसे कौशल को एकीकृत करके, आप थकाऊ फ़ॉर्मेटिंग कार्यों को स्वचालित कर सकते हैं जो आपका बहुमूल्य समय खर्च कर सकते हैं। तो, क्यों न इसे आज़माया जाए? इसे स्वयं आज़माएँ और अपने Excel गेम को आगे बढ़ाएँ!
## अक्सर पूछे जाने वाले प्रश्न
### Aspose.Cells क्या है?
Aspose.Cells .NET अनुप्रयोगों में Excel फ़ाइलों में हेरफेर करने के लिए एक शक्तिशाली लाइब्रेरी है, जो स्वचालित और प्रोग्रामेटिक कार्यों को आसानी से पूरा करने की अनुमति देता है।
### क्या मैं Aspose.Cells को निःशुल्क आज़मा सकता हूँ?
हाँ! आप क्लिक करके निःशुल्क परीक्षण शुरू कर सकते हैं [यहाँ](https://releases.aspose.com).
### किस प्रकार की पिवट टेबल शैलियाँ उपलब्ध हैं?
Aspose.Cells विभिन्न पूर्वनिर्धारित शैलियाँ प्रदान करता है, जिन्हें इसके माध्यम से एक्सेस किया जा सकता है `PivotTableStyleType`.
### मैं एक्सेल में पिवट टेबल कैसे बना सकता हूँ?
आप टूलबार में "इन्सर्ट" टैब का उपयोग करके और विकल्पों में से "पिवटटेबल" का चयन करके एक्सेल में पिवट टेबल बना सकते हैं।
### मैं Aspose.Cells के लिए समर्थन कहां से प्राप्त कर सकता हूं?
आप Aspose फ़ोरम पर सहायता पा सकते हैं [यहाँ](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}