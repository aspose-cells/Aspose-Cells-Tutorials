---
title: .NET में आउटपुट HTML में HTML क्रॉसटाइप को प्रोग्रामेटिक रूप से निर्दिष्ट करना
linktitle: .NET में आउटपुट HTML में HTML क्रॉसटाइप को प्रोग्रामेटिक रूप से निर्दिष्ट करना
second_title: Aspose.Cells .NET एक्सेल प्रोसेसिंग API
description: .NET के लिए Aspose.Cells में HTML CrossType निर्दिष्ट करना सीखें। Excel फ़ाइलों को सटीकता के साथ HTML में बदलने के लिए हमारे चरण-दर-चरण ट्यूटोरियल का पालन करें।
weight: 17
url: /hi/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET में आउटपुट HTML में HTML क्रॉसटाइप को प्रोग्रामेटिक रूप से निर्दिष्ट करना

## परिचय
जब .NET अनुप्रयोगों में Excel फ़ाइलों को HTML में बदलने की बात आती है, तो आपको यह निर्दिष्ट करने की आवश्यकता हो सकती है कि आउटपुट में क्रॉस-रेफरेंस को कैसे संभाला जाए। .NET के लिए Aspose.Cells में HtmlSaveOptions वर्ग रूपांतरण प्रक्रिया को नियंत्रित करने के लिए विभिन्न सेटिंग्स प्रदान करता है, और उन विकल्पों में से एक HtmlCrossType है। इस ट्यूटोरियल में, हम Excel फ़ाइलों को HTML प्रारूप में निर्यात करते समय HTML क्रॉस-टाइप को प्रोग्रामेटिक रूप से निर्दिष्ट करने का तरीका बताएंगे। 
## आवश्यक शर्तें
कोड में आगे बढ़ने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:
-  .NET के लिए Aspose.Cells: सुनिश्चित करें कि आपके प्रोजेक्ट में Aspose.Cells लाइब्रेरी स्थापित है। आप इसे यहाँ से डाउनलोड कर सकते हैं[Aspose वेबसाइट](https://releases.aspose.com/cells/net/).
- विजुअल स्टूडियो: विजुअल स्टूडियो या किसी अन्य .NET विकास वातावरण की कार्यशील स्थापना।
- C# का बुनियादी ज्ञान: C# प्रोग्रामिंग से परिचित होने से आपको उदाहरणों को बेहतर ढंग से समझने में मदद मिलेगी।
-  नमूना एक्सेल फ़ाइल: काम करने के लिए एक नमूना एक्सेल फ़ाइल तैयार रखें। इस उदाहरण के लिए, हम उपयोग करेंगे`sampleHtmlCrossStringType.xlsx`.
## पैकेज आयात करें
आरंभ करने के लिए, आपको आवश्यक Aspose.Cells नामस्थानों को आयात करना होगा। आप इसे इस प्रकार कर सकते हैं:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
आइये इसे चरण-दर-चरण समझें, जिससे आपके लिए इसका अनुसरण करना और अपनी परियोजनाओं में इस कार्यक्षमता को क्रियान्वित करना आसान हो जाएगा।
## चरण 1: अपने स्रोत और आउटपुट निर्देशिकाएँ परिभाषित करें
सबसे पहले, आपको अपनी स्रोत एक्सेल फ़ाइल के लिए निर्देशिकाएँ सेट करनी होंगी और यह भी कि आप आउटपुट HTML फ़ाइल को कहाँ सहेजना चाहते हैं।
```csharp
// स्रोत निर्देशिका
string sourceDir = "Your Document Directory";
// आउटपुट निर्देशिका
string outputDir = "Your Document Directory";
```
## चरण 2: नमूना एक्सेल फ़ाइल लोड करें
 इसके बाद, अपनी नमूना एक्सेल फ़ाइल को एक में लोड करें`Workbook` वस्तु। यहीं से सारा जादू शुरू होता है।
```csharp
// नमूना एक्सेल फ़ाइल लोड करें
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
 यहाँ, प्रतिस्थापित करें`"Your Document Directory"` वास्तविक पथ के साथ जहाँ आपकी एक्सेल फ़ाइल स्थित है। यह लाइन एक्सेल फ़ाइल को मेमोरी में पढ़ती है ताकि आप उसमें बदलाव कर सकें।
## चरण 3: HTML सहेजें विकल्प निर्दिष्ट करें
 अब, हम इसका एक उदाहरण बनाएंगे`HtmlSaveOptions`, जो आपको यह कॉन्फ़िगर करने की अनुमति देता है कि एक्सेल फ़ाइल को HTML में कैसे परिवर्तित किया जाएगा।
```csharp
// HTML क्रॉस प्रकार निर्दिष्ट करें
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
 इस चरण में, हमने सेट किया है`HtmlCrossStringType` को`HtmlCrossType.Default`, जो आउटपुट HTML में क्रॉस-रेफरेंस को संभालने के लिए उपलब्ध विकल्पों में से एक है।
## चरण 4: आवश्यकतानुसार क्रॉस प्रकार बदलें
 आप इसके लिए अलग-अलग प्रकार निर्दिष्ट कर सकते हैं`HtmlCrossStringType` आपकी आवश्यकताओं के आधार पर। यहाँ विभिन्न विकल्प दिए गए हैं जिनका आप उपयोग कर सकते हैं:
- `HtmlCrossType.Default`: डिफ़ॉल्ट क्रॉस प्रकार.
- `HtmlCrossType.MSExport`: HTML को MS Excel जैसे व्यवहार के साथ निर्यात करता है।
- `HtmlCrossType.Cross`: क्रॉस संदर्भ बनाता है.
- `HtmlCrossType.FitToCell`: सेल आयामों के लिए क्रॉस संदर्भों को फिट करता है।
 आप संशोधित कर सकते हैं`HtmlCrossStringType` इस कदर:
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExport;
// या
opts.HtmlCrossStringType = HtmlCrossType.Cross;
// या
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## चरण 5: आउटपुट HTML फ़ाइल को सेव करें
 एक बार जब आप अपने विकल्पों को कॉन्फ़िगर कर लेते हैं, तो परिवर्तित HTML फ़ाइल को सहेजने का समय आ जाता है।`Save` विधि आपके`Workbook` वस्तु:
```csharp
// आउटपुट HTML
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
 यहाँ, हम आउटपुट फ़ाइल का नामकरण उसके नाम के आधार पर कर रहे हैं।`HtmlCrossStringType` हमने सेट किया है। इस तरह, आप आसानी से पहचान सकते हैं कि रूपांतरण में किस क्रॉस प्रकार का उपयोग किया गया था।
## चरण 6: सफल निष्पादन की पुष्टि करें
अंत में, यह पुष्टि करना हमेशा एक अच्छा अभ्यास है कि आपका ऑपरेशन सफल रहा। आप कंसोल पर एक संदेश प्रिंट कर सकते हैं:
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
इससे आपको पता चल जाएगा कि प्रक्रिया बिना किसी त्रुटि के पूरी हो गई है।
## निष्कर्ष
और अब यह हो गया! आपने Aspose.Cells का उपयोग करके .NET में अपने Excel निर्यात के लिए HTML क्रॉस-टाइप को सफलतापूर्वक निर्दिष्ट कर लिया है। यह कार्यक्षमता विशेष रूप से तब उपयोगी होती है जब आपको अपने HTML आउटपुट में विशिष्ट स्वरूपण या संदर्भ बनाए रखने की आवश्यकता होती है, यह सुनिश्चित करते हुए कि आपके परिवर्तित दस्तावेज़ आपकी आवश्यकताओं को पूरा करते हैं।
## अक्सर पूछे जाने वाले प्रश्न
### Aspose.Cells में HtmlCrossType क्या है?  
HtmlCrossType यह परिभाषित करता है कि HTML रूपांतरण के दौरान Excel फ़ाइल में क्रॉस-रेफ़रेंस को कैसे हैंडल किया जाता है। आप डिफ़ॉल्ट, MSExport, Cross, और FitToCell जैसे विकल्प चुन सकते हैं।
### क्या मैं Aspose.Cells का निःशुल्क उपयोग कर सकता हूँ?  
 Aspose.Cells एक निःशुल्क परीक्षण संस्करण प्रदान करता है। आप इसे उनके यहां से डाउनलोड कर सकते हैं[वेबसाइट](https://releases.aspose.com/).
### मैं अपने .NET प्रोजेक्ट में Aspose.Cells कैसे स्थापित करूं?  
 आप निम्न आदेश चलाकर Visual Studio में NuGet पैकेज मैनेजर के माध्यम से Aspose.Cells स्थापित कर सकते हैं:`Install-Package Aspose.Cells`.
### मैं Aspose.Cells के लिए दस्तावेज़ कहां पा सकता हूं?  
 आप Aspose.Cells पर व्यापक दस्तावेज़ पा सकते हैं[यहाँ](https://reference.aspose.com/cells/net/).
### यदि HTML फ़ाइल को सहेजते समय मुझे कोई त्रुटि आती है तो मुझे क्या करना चाहिए?  
सुनिश्चित करें कि निर्देशिका पथ सही हैं और आपके पास आउटपुट निर्देशिका के लिए लिखने की अनुमति है। यदि समस्या बनी रहती है, तो सहायता के लिए Aspose समर्थन फ़ोरम देखें।
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
