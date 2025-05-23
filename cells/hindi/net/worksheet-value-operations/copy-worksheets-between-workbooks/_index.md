---
"description": "इस विस्तृत, चरण-दर-चरण ट्यूटोरियल में .NET के लिए Aspose.Cells का उपयोग करके Excel कार्यपुस्तिकाओं के बीच वर्कशीट कॉपी करना सीखें। Excel प्रक्रियाओं को स्वचालित करने के लिए बिल्कुल सही।"
"linktitle": "Aspose.Cells का उपयोग करके दो कार्यपुस्तिकाओं के बीच कार्यपत्रकों की प्रतिलिपि बनाएँ"
"second_title": "Aspose.Cells .NET एक्सेल प्रोसेसिंग API"
"title": "Aspose.Cells का उपयोग करके दो कार्यपुस्तिकाओं के बीच कार्यपत्रकों की प्रतिलिपि बनाएँ"
"url": "/hi/net/worksheet-value-operations/copy-worksheets-between-workbooks/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells का उपयोग करके दो कार्यपुस्तिकाओं के बीच कार्यपत्रकों की प्रतिलिपि बनाएँ

## परिचय
व्यावसायिक प्रक्रियाओं में डेटा हैंडलिंग को स्वचालित करने के लिए एक्सेल फ़ाइलों को प्रोग्रामेटिक रूप से प्रबंधित करना एक आवश्यकता बन गई है। चाहे आप एनालिटिक्स ऐप बनाने वाले डेवलपर हों या रिपोर्ट को स्वचालित करने की कोशिश करने वाले व्यवसाय विश्लेषक, .NET के लिए Aspose.Cells एक्सेल फ़ाइलों को आसानी से हेरफेर करने के लिए एक मजबूत टूलकिट प्रदान करता है। इस ट्यूटोरियल में, हम .NET के लिए Aspose.Cells का उपयोग करके दो वर्कबुक के बीच वर्कशीट कॉपी करने का तरीका बताएंगे। हम पूर्वापेक्षाएँ, आयात पैकेज और एक विस्तृत, चरण-दर-चरण मार्गदर्शिका को कवर करेंगे जिसका पालन करना आसान है।
## आवश्यक शर्तें
कोडिंग शुरू करने से पहले, आइए सुनिश्चित करें कि आपके पास कोडिंग के लिए आवश्यक सभी चीजें मौजूद हैं:
- Aspose.Cells for .NET: Aspose.Cells for .NET को डाउनलोड करें और इंस्टॉल करें [डाउनलोड पृष्ठ](https://releases.aspose.com/cells/net/).
- .NET फ्रेमवर्क: सुनिश्चित करें कि आपके विकास वातावरण पर .NET स्थापित है।
- IDE: आप किसी भी C# संगत IDE का उपयोग कर सकते हैं (विजुअल स्टूडियो अनुशंसित है)।
- लाइसेंस: आप Aspose.Cells को आज़मा सकते हैं [निःशुल्क अस्थायी लाइसेंस](https://purchase.aspose.com/temporary-license/) या विचार करें [पूर्ण लाइसेंस खरीदना](https://purchase.aspose.com/buy) पूर्ण कार्यक्षमता के लिए.
इसकी जाँच पड़ताल करो [.NET के लिए Aspose.Cells दस्तावेज़](https://reference.aspose.com/cells/net/) यदि आपको विशिष्ट सुविधाओं और क्षमताओं के बारे में अधिक जानकारी चाहिए।
## पैकेज आयात करें
आरंभ करने के लिए, आपको अपने कोड में आवश्यक नामस्थान आयात करने होंगे। आप इसे इस प्रकार कर सकते हैं:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
यह एकल पंक्ति आपको Aspose.Cells की सभी शक्तिशाली सुविधाओं तक पहुंच प्रदान करती है।
इस ट्यूटोरियल में, हम कार्य को प्रबंधनीय चरणों में विभाजित करेंगे। प्रत्येक चरण पिछले चरण पर आधारित होता है, इसलिए अंत तक आपके पास एक पूर्ण, कार्यशील कोड स्निपेट होगा।
## चरण 1: दस्तावेज़ निर्देशिका निर्धारित करें
सबसे पहले, आइए वह पथ निर्दिष्ट करें जहाँ हमारी कार्यपुस्तिका फ़ाइलें संग्रहीत हैं। यह पथ प्रोग्राम को बताएगा कि स्रोत कार्यपुस्तिका कहाँ ढूँढनी है और कॉपी की गई फ़ाइल को कहाँ सहेजना है।
```csharp
// दस्तावेज़ निर्देशिका का पथ.
string dataDir = "Your Document Directory";
```
यहाँ, प्रतिस्थापित करें `"Your Document Directory"` वास्तविक पथ के साथ जहां आपकी फ़ाइलें सहेजी गई हैं.
## चरण 2: इनपुट फ़ाइल पथ सेट करें
इस चरण में, हम उस मूल कार्यपुस्तिका का पथ परिभाषित करेंगे जिसमें वह कार्यपत्रक है जिसे हम कॉपी करना चाहते हैं। प्रदर्शन के लिए, मान लें कि फ़ाइल का नाम है `book1.xls`.
```csharp
string inputPath = dataDir + "book1.xls";
```
यह रेखा जोड़ती है `dataDir` फ़ाइल नाम के साथ, एक पूर्ण पथ बनाना `book1.xls`यह वह कार्यपुस्तिका है जिसमें वह शीट है जिसे हम कॉपी करेंगे।
## चरण 3: स्रोत कार्यपुस्तिका खोलें
अब, आइए स्रोत कार्यपुस्तिका खोलें (`book1.xls`) बनाकर `Workbook` वस्तु और में गुजर `inputPath` एक तर्क के रूप में.
```csharp
// एक कार्यपुस्तिका बनाएं.
// पहली पुस्तक में एक फ़ाइल खोलें.
Workbook sourceWorkbook = new Workbook(inputPath);
```
यहाँ, हम आरंभ करते हैं `sourceWorkbook` हमारी स्रोत कार्यपुस्तिका का प्रतिनिधित्व करने के लिए। यह ऑब्जेक्ट हमें फ़ाइल के भीतर सभी वर्कशीट तक पहुँच प्रदान करता है।
## चरण 4: गंतव्य कार्यपुस्तिका बनाएँ
इस चरण में, हम अपनी कॉपी की गई वर्कशीट के लिए गंतव्य के रूप में कार्य करने के लिए एक नई कार्यपुस्तिका बनाएंगे। यह एक खाली स्लेट के रूप में काम करेगा जहाँ हम कॉपी की गई शीट को चिपकाएँगे।
```csharp
// एक अन्य कार्यपुस्तिका बनाएं.
Workbook destinationWorkbook = new Workbook();
```
हमारा `destinationWorkbook` डिफ़ॉल्ट रूप से रिक्त होता है, तथा इसमें केवल एक ही कार्यपत्रक होता है।
## चरण 5: वर्कशीट को नई वर्कबुक में कॉपी करें
अब इस ट्यूटोरियल का मुख्य भाग आता है - वर्कशीट की प्रतिलिपि बनाना। हम स्रोत वर्कबुक से पहली वर्कशीट की प्रतिलिपि बनाकर उसे गंतव्य वर्कबुक के पहले वर्कशीट स्लॉट में पेस्ट करेंगे।
```csharp
// स्रोत कार्यपुस्तिका की पहली शीट को गंतव्य कार्यपुस्तिका में कॉपी करें।
destinationWorkbook.Worksheets[0].Copy(sourceWorkbook.Worksheets[0]);
```
इस कोड में:
- `sourceWorkbook.Worksheets[0]` हमारी स्रोत कार्यपुस्तिका में प्रथम कार्यपत्रक का प्रतिनिधित्व करता है।
- `destinationWorkbook.Worksheets[0]` गंतव्य कार्यपुस्तिका में प्रथम कार्यपत्रक को संदर्भित करता है।
- The `.Copy` यह विधि भारी काम करती है, तथा कार्यपत्रक को एक कार्यपुस्तिका से दूसरी कार्यपुस्तिका में निर्बाध रूप से स्थानांतरित करती है।
## चरण 6: गंतव्य कार्यपुस्तिका को सहेजें
अंत में, आइए अपनी गंतव्य कार्यपुस्तिका को सेव करें। यह कॉपी करने की प्रक्रिया को अंतिम रूप देगा और एक आउटपुट फ़ाइल बनाएगा जिसमें कॉपी की गई कार्यपत्रक शामिल होगी।
```csharp
// फ़ाइल सहेजें।
destinationWorkbook.Save(dataDir + "CopyWorksheetsBetweenWorkbooks_out.xls");
```
प्रतिस्थापित करें `"CopyWorksheetsBetweenWorkbooks_out.xls"` अपने पसंदीदा आउटपुट फ़ाइल नाम के साथ। अब, आपके पास कॉपी की गई वर्कशीट के साथ आपकी निर्दिष्ट निर्देशिका में एक नई फ़ाइल होगी।

## निष्कर्ष
बधाई हो! आपने .NET के लिए Aspose.Cells का उपयोग करके एक वर्कबुक से दूसरे में सफलतापूर्वक एक वर्कशीट कॉपी की है। कोड की कुछ ही पंक्तियों के साथ, आप कई वर्कबुक में वर्कशीट डुप्लिकेशन को स्वचालित कर सकते हैं, समय की बचत कर सकते हैं और त्रुटियों को कम कर सकते हैं। Aspose.Cells एक शक्तिशाली उपकरण है जो एक्सेल फ़ाइल हेरफेर को सुव्यवस्थित करता है, जो इसे सरल और जटिल दोनों डेटा स्वचालन कार्यों के लिए आदर्श बनाता है।
## अक्सर पूछे जाने वाले प्रश्न
### क्या मैं एक साथ कई वर्कशीट कॉपी कर सकता हूँ?  
हां, आप स्रोत कार्यपुस्तिका में कार्यपत्रकों के माध्यम से लूप कर सकते हैं और प्रत्येक को गंतव्य कार्यपुस्तिका में अलग-अलग कॉपी कर सकते हैं।
### क्या वर्कशीट की प्रतिलिपि बनाने से सभी स्वरूपण और डेटा स्थानांतरित हो जाते हैं?  
बिलकुल! `.Copy` Aspose.Cells में विधि डेटा, स्वरूपण और सूत्रों सहित सब कुछ स्थानांतरित करती है।
### क्या किसी वर्कशीट को किसी मौजूदा वर्कबुक में कॉपी करना संभव है?  
हां, आप गंतव्य कार्यपुस्तिका में कार्यपत्रक सूचकांक निर्दिष्ट करके किसी कार्यपत्रक को मौजूदा कार्यपुस्तिका में कॉपी कर सकते हैं।
### क्या मैं कॉपी की गई वर्कशीट का नाम बदल सकता हूँ?  
हाँ, कॉपी करने के बाद, इसका उपयोग करें `destinationWorkbook.Worksheets[0].Name = "NewSheetName";` कार्यपत्रक का नाम बदलने के लिए.
### क्या मुझे Aspose.Cells का उपयोग करने के लिए लाइसेंस की आवश्यकता है?  
आप Aspose.Cells को आज़मा सकते हैं [निःशुल्क अस्थायी लाइसेंस](https://purchase.aspose.com/temporary-license/) या अप्रतिबंधित पहुंच के लिए पूर्ण लाइसेंस खरीदें।

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}