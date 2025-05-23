---
"description": "जानें कि .NET के लिए Aspose.Cells का उपयोग करके Excel में आकृतियों को आगे या पीछे कैसे भेजा जाए। यह गाइड टिप्स के साथ चरण-दर-चरण ट्यूटोरियल प्रदान करता है।"
"linktitle": "Excel में आकृति को आगे या पीछे भेजें"
"second_title": "Aspose.Cells .NET एक्सेल प्रोसेसिंग API"
"title": "Excel में आकृति को आगे या पीछे भेजें"
"url": "/hi/net/excel-shape-text-modifications/send-shape-front-back-excel/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel में आकृति को आगे या पीछे भेजें

## परिचय
एक्सेल फ़ाइलों के साथ काम करते समय, आपको अपनी स्प्रेडशीट में विज़ुअल तत्वों पर अधिक नियंत्रण की आवश्यकता हो सकती है। चित्र और ग्राफ़िक्स की तरह आकार आपके डेटा की प्रस्तुति को बेहतर बना सकते हैं। लेकिन क्या होता है जब ये आकार ओवरलैप होते हैं या उन्हें फिर से व्यवस्थित करने की आवश्यकता होती है? यहीं पर Aspose.Cells for .NET चमकता है। इस ट्यूटोरियल में, हम आपको एक्सेल वर्कशीट में आकृतियों में हेरफेर करने के चरणों के माध्यम से चलेंगे, विशेष रूप से आकृतियों को अन्य आकृतियों के सामने या पीछे भेजना। यदि आप अपने एक्सेल गेम को बढ़ाने के लिए तैयार हैं, तो चलिए शुरू करते हैं!
## आवश्यक शर्तें
आरंभ करने से पहले, आपको कुछ चीजें व्यवस्थित करनी होंगी:
1. Aspose.Cells लाइब्रेरी की स्थापना: सुनिश्चित करें कि आपके पास .NET के लिए Aspose.Cells लाइब्रेरी स्थापित है। आप इसे पा सकते हैं [यहाँ](https://releases.aspose.com/cells/net/).
2. विकास परिवेश: सुनिश्चित करें कि आपके पास .NET समर्थन वाला विकास परिवेश स्थापित है, जैसे कि Visual Studio.
3. C# का बुनियादी ज्ञान: C# प्रोग्रामिंग से परिचित होने से आपको कोड स्निपेट को बेहतर ढंग से समझने में मदद मिलेगी।
ठीक है, आपने पूर्वापेक्षा सूची के सभी बॉक्सों पर टिक लगा दिया है? बढ़िया! चलिए मज़ेदार भाग पर चलते हैं - कुछ कोड लिखना!
## पैकेज आयात करें
इससे पहले कि हम वास्तविक कोडिंग में उतरें, आइए आवश्यक पैकेज आयात करें। बस अपनी C# फ़ाइल के शीर्ष पर निम्न using निर्देश जोड़ें:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
ये नामस्थान महत्वपूर्ण हैं क्योंकि इनमें वे वर्ग और विधियां होती हैं जिनका उपयोग हम एक्सेल फाइलों और आकृतियों में परिवर्तन करने के लिए करेंगे।
## चरण 1: अपने फ़ाइल पथ निर्धारित करें
इस पहले चरण में, हमें स्रोत और आउटपुट निर्देशिकाएँ स्थापित करने की आवश्यकता है। यह वह जगह है जहाँ आपकी एक्सेल फ़ाइल स्थित है और जहाँ आप संशोधित फ़ाइल को सहेजना चाहते हैं।
```csharp
//स्रोत निर्देशिका
string sourceDir = "Your Document Directory";
//आउटपुट निर्देशिका
string outputDir = "Your Document Directory";
```
प्रतिस्थापित करें `"Your Document Directory"` वास्तविक पथ के साथ जहां आपकी एक्सेल फ़ाइलें संग्रहीत हैं।
## चरण 2: कार्यपुस्तिका लोड करें
अब जबकि हमने अपनी निर्देशिकाएं निर्धारित कर ली हैं, तो आइए कार्यपुस्तिका (एक्सेल फ़ाइल) को लोड करें जिसमें वे आकृतियां हैं जिनमें हम परिवर्तन करना चाहते हैं।
```csharp
//स्रोत एक्सेल फ़ाइल लोड करें
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
कोड की यह पंक्ति एक नया आरंभ करती है `Workbook` ऑब्जेक्ट, निर्दिष्ट एक्सेल फ़ाइल को मेमोरी में लोड करना ताकि हम इसके साथ काम कर सकें।
## चरण 3: वर्कशीट तक पहुंचें 
इसके बाद, हमें उस विशिष्ट वर्कशीट तक पहुँचने की आवश्यकता है जहाँ हमारी आकृतियाँ स्थित हैं। इस उदाहरण के लिए, हम पहली वर्कशीट का उपयोग करेंगे।
```csharp
//पहली वर्कशीट तक पहुंचें
Worksheet ws = wb.Worksheets[0];
```
संदर्भ देकर `Worksheets[0]`, हम अपनी कार्यपुस्तिका की पहली शीट को लक्षित कर रहे हैं। यदि आपकी आकृतियाँ किसी दूसरी शीट पर हैं, तो इंडेक्स को तदनुसार समायोजित करें।
## चरण 4: आकृतियों तक पहुँचें
वर्कशीट तक पहुँच तैयार होने के बाद, आइए उन आकृतियों को पकड़ें जिनमें हमारी रुचि है। इस उदाहरण के लिए, हम पहली और चौथी आकृति तक पहुँचेंगे।
```csharp
//पहले और चौथे आकार तक पहुँचें
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
ये रेखाएँ अपने सूचकांक के आधार पर वर्कशीट से विशिष्ट आकार प्राप्त करती हैं।
## चरण 5: आकृतियों की Z-ऑर्डर स्थिति प्रिंट करें
किसी भी आकृति को स्थानांतरित करने से पहले, आइए उनकी वर्तमान Z-ऑर्डर स्थिति को प्रिंट करें। इससे हमें बदलाव करने से पहले उनकी स्थिति को ट्रैक करने में मदद मिलती है।
```csharp
//आकृति की Z-ऑर्डर स्थिति प्रिंट करें
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
फोन करके `ZOrderPosition`, हम देख सकते हैं कि प्रत्येक आकृति ड्राइंग क्रम में कहाँ बैठती है।
## चरण 6: पहली आकृति को सामने भेजें
अब समय है कार्रवाई का! आइए पहले आकार को Z-ऑर्डर के सामने भेजें।
```csharp
//इस आकृति को आगे भेजें
sh1.ToFrontOrBack(2);
```
पास करके `2` को `ToFrontOrBack`, हम Aspose.Cells को इस आकृति को सामने लाने का निर्देश दे रहे हैं। 
## चरण 7: दूसरे आकार की Z-ऑर्डर स्थिति प्रिंट करें
इससे पहले कि हम दूसरी आकृति को पीछे भेजें, आइए देखें कि वह कहां स्थित है।
```csharp
//आकृति की Z-ऑर्डर स्थिति प्रिंट करें
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
इससे हमें कोई भी परिवर्तन करने से पहले चौथी आकृति की स्थिति के बारे में जानकारी मिल जाती है।
## चरण 8: चौथी आकृति को पीछे भेजें
अंत में, हम चौथी आकृति को Z-ऑर्डर स्टैक के पीछे भेजेंगे।
```csharp
//इस आकृति को वापस भेजें
sh4.ToFrontOrBack(-2);
```
का उपयोग करते हुए `-2` चूंकि पैरामीटर आकृति को स्टैक के पीछे की ओर भेजता है, जिससे यह सुनिश्चित होता है कि यह अन्य आकृतियों या पाठ को बाधित नहीं करेगा।
## चरण 9: कार्यपुस्तिका सहेजें 
अंतिम चरण है अपनी कार्यपुस्तिका को नई स्थित आकृतियों के साथ सहेजना।
```csharp
//आउटपुट एक्सेल फ़ाइल को सहेजें
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
यह आदेश संशोधित कार्यपुस्तिका को निर्दिष्ट आउटपुट निर्देशिका में सहेजता है।
## चरण 10: पुष्टिकरण संदेश
अंत में, आइए एक सरल पुष्टि प्रदान करें जिससे हमें पता चले कि हमारा कार्य सफलतापूर्वक पूरा हो गया है।
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
और इसी के साथ हमारा ट्यूटोरियल का कोड समाप्त हो गया!
## निष्कर्ष
.NET के लिए Aspose.Cells का उपयोग करके Excel में आकृतियों में हेरफेर करना न केवल सरल है, बल्कि शक्तिशाली भी है। इस गाइड का पालन करके, अब आप आसानी से आकृतियों को आगे या पीछे भेज पाएंगे, जिससे आपके Excel प्रेजेंटेशन पर बेहतर नियंत्रण हो सकेगा। इन उपकरणों के साथ, आप अपनी स्प्रेडशीट की दृश्य अपील को बढ़ाने के लिए तैयार हैं।
## अक्सर पूछे जाने वाले प्रश्न
### Aspose.Cells के लिए मुझे किस प्रोग्रामिंग भाषा की आवश्यकता है?  
Aspose.Cells के साथ काम करने के लिए आपको C# या किसी .NET समर्थित भाषा का उपयोग करना होगा।
### क्या मैं Aspose.Cells को निःशुल्क आज़मा सकता हूँ?  
हां, आप Aspose.Cells के निःशुल्क परीक्षण के साथ शुरुआत कर सकते हैं [यहाँ](https://releases.aspose.com/).
### एक्सेल में मैं किस प्रकार की आकृतियों में बदलाव कर सकता हूँ?  
आप विभिन्न आकृतियों जैसे आयत, वृत्त, रेखाएँ और छवियों में हेरफेर कर सकते हैं।
### मैं Aspose.Cells के लिए समर्थन कैसे प्राप्त कर सकता हूं?  
किसी भी सहायता या प्रश्न के लिए आप उनके सामुदायिक मंच पर जा सकते हैं [यहाँ](https://forum.aspose.com/c/cells/9).
### क्या Aspose.Cells के लिए कोई अस्थायी लाइसेंस उपलब्ध है?  
हां, आप अस्थायी लाइसेंस का अनुरोध कर सकते हैं [यहाँ](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}