---
"description": ".NET के लिए Aspose.Cells का उपयोग करके Excel वर्कशीट में पेज ऑर्डर सेट करना सीखें, एक सरल, चरण-दर-चरण गाइड में। शुरुआती और विशेषज्ञों के लिए बिल्कुल सही।"
"linktitle": "वर्कशीट में पेज ऑर्डर लागू करें"
"second_title": "Aspose.Cells .NET एक्सेल प्रोसेसिंग API"
"title": "वर्कशीट में पेज ऑर्डर लागू करें"
"url": "/hi/net/worksheet-page-setup-features/implement-page-order/"
"weight": 24
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# वर्कशीट में पेज ऑर्डर लागू करें

## परिचय
एक्सेल वर्कशीट में पेज ऑर्डर को एडजस्ट करना चाहते हैं? कभी-कभी, डेटा प्रिंट करने के तरीके को नियंत्रित करना आवश्यक होता है, खासकर बड़ी स्प्रेडशीट के साथ जो एक पेज पर अच्छी तरह से फिट नहीं होती हैं। यहाँ Aspose.Cells for .NET काम आता है, जो आपको अपने प्रिंट किए गए पेजों को अपनी पसंद के अनुसार संरचित करने के लिए शक्तिशाली उपकरण प्रदान करता है। इस गाइड में, हम आपको वर्कशीट में पेज ऑर्डर सेट करने के बारे में बताएंगे, विशेष रूप से पहले पंक्तियों में और फिर कॉलम में प्रिंट करने के लिए। तकनीकी लगता है? चिंता न करें—मैं इसे सरल रखूँगा, हर चीज़ को चरण-दर-चरण तोड़कर।
## आवश्यक शर्तें
शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित सेटअप है:
1. .NET के लिए Aspose.Cells: यदि आपने पहले से नहीं किया है, तो डाउनलोड करें [.NET के लिए Aspose.Cells यहाँ](https://releases.aspose.com/cells/net/). हमारे द्वारा उपयोग की जाने वाली सुविधाओं तक पहुंचने के लिए इसे अपने प्रोजेक्ट में इंस्टॉल करें।
2. विकास वातावरण: विजुअल स्टूडियो जैसा कोई भी .NET-संगत IDE काम करेगा।
3. बुनियादी C# ज्ञान: हम कुछ C# कोड के साथ काम करेंगे, इसलिए बुनियादी प्रोग्रामिंग अवधारणाओं से परिचित होना उपयोगी होगा।
कोशिश करें [.NET के लिए Aspose.Cells निःशुल्क परीक्षण के साथ](https://releases.aspose.com/) या प्राप्त करें [अस्थायी लाइसेंस](https://purchase.aspose.com/temporary-license/) सभी सुविधाओं तक पहुँचने के लिए!
## पैकेज आयात करें
शुरू करने के लिए, हमें आवश्यक Aspose.Cells नामस्थानों को आयात करने की आवश्यकता है। इससे हमें हमारे संचालन के लिए आवश्यक सभी चीज़ों तक पहुँच मिलेगी।
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
आइए इस ट्यूटोरियल को कुछ सरल चरणों में विभाजित करें। हम एक नई कार्यपुस्तिका बनाकर शुरू करेंगे, वर्कशीट के पेज सेटअप तक पहुंचेंगे, पेज ऑर्डर सेट करेंगे और फिर उसे सेव करेंगे। 
## चरण 1: कार्यपुस्तिका बनाएँ
सबसे पहले हमें एक वर्कबुक ऑब्जेक्ट बनाना होगा। यह Aspose.Cells में हमारी एक्सेल फ़ाइल को दर्शाता है।
```csharp
// वर्कबुक ऑब्जेक्ट को इंस्टैंशिएट करना
Workbook workbook = new Workbook();
```
यहाँ, हम इसका एक उदाहरण बना रहे हैं `Workbook` इसे अपने प्रोग्राम में एक नई, खाली एक्सेल वर्कबुक खोलने के रूप में सोचें।
## चरण 2: वर्कशीट का एक्सेस पेज सेटअप
प्रिंट सेटिंग्स को नियंत्रित करने के लिए, हमें एक्सेस करने की आवश्यकता है `PageSetup` वर्कशीट का ऑब्जेक्ट। यह हमें यह समायोजित करने की अनुमति देगा कि वर्कशीट कैसे मुद्रित या निर्यात की जाती है।
```csharp
// कार्यपत्रक के पेजसेटअप का संदर्भ प्राप्त करना
PageSetup pageSetup = workbook.Worksheets[0].PageSetup;
```
इस पंक्ति में, हम पकड़ रहे हैं `PageSetup` प्रथम कार्यपत्रक का (`Worksheets[0]`) यह वह जगह है जहां हम अपनी प्रिंट सेटिंग्स कॉन्फ़िगर करेंगे, जिसमें पृष्ठों को प्रिंट करने का क्रम भी शामिल होगा।
## चरण 3: पृष्ठ क्रम को OverThenDown पर सेट करें
अब मुख्य चरण के लिए: पृष्ठ क्रम सेट करना। डिफ़ॉल्ट रूप से, Excel अगली पंक्ति पर जाने से पहले प्रत्येक कॉलम को प्रिंट कर सकता है, लेकिन यहाँ हम इसे "ओवरथेनडाउन" जाने के लिए निर्दिष्ट कर रहे हैं - पहले क्षैतिज रूप से, फिर लंबवत रूप से।
```csharp
// पृष्ठों के मुद्रण क्रम को पहले ऊपर फिर नीचे सेट करना
pageSetup.Order = PrintOrderType.OverThenDown;
```
हमने निर्धारित किया है `Order` की संपत्ति `PageSetup` को `PrintOrderType.OverThenDown`यह एक्सेल को पृष्ठों की अगली पंक्ति पर जाने से पहले पंक्तियों में प्रिंट करने के लिए कहता है। यदि आप एक विस्तृत स्प्रेडशीट प्रिंट कर रहे हैं, तो यह सेटिंग सुनिश्चित करती है कि प्रिंटआउट पर सब कुछ तार्किक रूप से प्रवाहित हो।
## चरण 4: कार्यपुस्तिका सहेजें
अंत में, परिणाम देखने के लिए अपनी कार्यपुस्तिका को सेव करें। हम फ़ाइल पथ और नाम निर्दिष्ट करेंगे जहाँ इसे सेव किया जाना चाहिए।
```csharp
// दस्तावेज़ निर्देशिका का पथ
string dataDir = "Your Document Directory";
// कार्यपुस्तिका सहेजें
workbook.Save(dataDir + "SetPageOrder_out.xls");
```
उपरोक्त कोड में, हम कार्यपुस्तिका को निर्दिष्ट निर्देशिका में नाम के साथ सहेज रहे हैं `SetPageOrder_out.xls`। प्रतिस्थापित करें `"Your Document Directory"` उस पथ के साथ जहाँ आप अपनी फ़ाइल सहेजना चाहते हैं.
आउटपुट फॉर्मेट के साथ मदद चाहिए? Aspose.Cells कई फॉर्मेट का समर्थन करता है, इसलिए जैसे फॉर्मेट के साथ प्रयोग करें `.xlsx` यदि आपको नवीनतम एक्सेल प्रारूप की आवश्यकता है।
## निष्कर्ष
और अब यह हो गया! आपने .NET के लिए Aspose.Cells का उपयोग करके Excel वर्कशीट में पेज ऑर्डर सेट कर दिया है। कोड की कुछ ही पंक्तियों के साथ, हमने नियंत्रित किया कि डेटा कैसे प्रिंट होता है, जो कागज़ पर बड़े डेटासेट को स्पष्ट रूप से प्रस्तुत करने के लिए एक गेम-चेंजर हो सकता है। यह उन कई प्रिंट सेटिंग्स में से एक है जिन्हें आप Aspose.Cells के साथ कस्टमाइज़ कर सकते हैं। इसलिए, चाहे आप रिपोर्ट तैयार कर रहे हों, प्रिंट-रेडी स्प्रेडशीट या संगठित दस्तावेज़, Aspose.Cells आपके लिए है।
## अक्सर पूछे जाने वाले प्रश्न
### क्या मैं एक साथ कई कार्यपत्रकों के पृष्ठ क्रम को बदल सकता हूँ?
हां, बस कार्यपुस्तिका में प्रत्येक वर्कशीट के माध्यम से लूप करें और समान लागू करें `PageSetup.Order` सेटिंग।
### ओवरदैनडाउन के अलावा प्रिंट ऑर्डर के लिए अन्य विकल्प क्या हैं?
वैकल्पिक विकल्प है `DownThenOver`, जो पहले कॉलम के नीचे प्रिंट करेगा, फिर पंक्तियों के पार।
### क्या इस कोड के लिए लाइसेंस की आवश्यकता है?
बिना लाइसेंस के कुछ सुविधाएँ सीमित हो सकती हैं। आप कोशिश कर सकते हैं [.NET के लिए Aspose.Cells निःशुल्क परीक्षण के साथ](https://releases.aspose.com/).
### क्या मैं मुद्रण से पहले पृष्ठ क्रम का पूर्वावलोकन कर सकता हूँ?
यद्यपि Aspose.Cells प्रिंट सेटअप की अनुमति देता है, लेकिन आपको पूर्वावलोकन करने के लिए Excel में सहेजी गई फ़ाइल को खोलना होगा, क्योंकि Aspose में कोई प्रत्यक्ष पूर्वावलोकन नहीं है।
### क्या यह पृष्ठ क्रम सेटिंग PDF जैसे अन्य प्रारूपों के साथ संगत है?
हां, एक बार सेट हो जाने पर, पृष्ठ क्रम पीडीएफ निर्यात या अन्य समर्थित प्रारूपों पर लागू होगा, जिससे पृष्ठ प्रवाह सुसंगत रहेगा।


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}