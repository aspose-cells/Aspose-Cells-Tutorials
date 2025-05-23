---
"description": "इस व्यापक, चरण-दर-चरण मार्गदर्शिका में .NET के लिए Aspose.Cells के साथ Excel में रनटाइम पर सशर्त स्वरूपण लागू करना सीखें।"
"linktitle": "एक्सेल में रनटाइम पर सशर्त स्वरूपण लागू करना"
"second_title": "Aspose.Cells .NET एक्सेल प्रोसेसिंग API"
"title": "एक्सेल में रनटाइम पर सशर्त स्वरूपण लागू करना"
"url": "/hi/net/excel-conditional-formatting/applying-conditional-formatting-at-runtime/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# एक्सेल में रनटाइम पर सशर्त स्वरूपण लागू करना

## परिचय

वे डेटा विश्लेषण और विज़ुअलाइज़ेशन के लिए शक्तिशाली उपकरण हैं। Excel की एक सबसे बढ़िया विशेषता सशर्त स्वरूपण है, जो उपयोगकर्ताओं को उनके मानों के आधार पर कोशिकाओं पर विशिष्ट स्वरूपण शैलियों को लागू करने की अनुमति देता है। इससे रुझानों की पहचान करना, महत्वपूर्ण डेटा बिंदुओं को हाइलाइट करना या डेटा को अधिक पठनीय बनाना आसान हो सकता है। यदि आप अपनी Excel फ़ाइलों में प्रोग्रामेटिक रूप से सशर्त स्वरूपण लागू करना चाहते हैं, तो आप सही जगह पर हैं! इस गाइड में, हम .NET के लिए Aspose.Cells का उपयोग करके रनटाइम पर सशर्त स्वरूपण लागू करने का तरीका बताएंगे।

## आवश्यक शर्तें
कोड में गोता लगाने से पहले, आइए सुनिश्चित करें कि आपके पास आरंभ करने के लिए आवश्यक सभी चीजें हैं:

1. विज़ुअल स्टूडियो: सुनिश्चित करें कि आपके मशीन पर विज़ुअल स्टूडियो स्थापित है। आप .NET डेवलपमेंट का समर्थन करने वाले किसी भी संस्करण का उपयोग कर सकते हैं।
2. Aspose.Cells for .NET: आपको Aspose.Cells for .NET इंस्टॉल करना होगा। आप इसे यहाँ से डाउनलोड कर सकते हैं [Aspose वेबसाइट](https://releases.aspose.com/cells/net/).
3. C# का बुनियादी ज्ञान: C# प्रोग्रामिंग से परिचित होने से आपको कोड स्निपेट को बेहतर ढंग से समझने में मदद मिलेगी।
4. .NET फ्रेमवर्क: सुनिश्चित करें कि आपका प्रोजेक्ट .NET फ्रेमवर्क के संगत संस्करण को लक्षित कर रहा है।

अब जब हमने सभी पूर्वापेक्षाएं पूरी कर ली हैं, तो चलिए मज़ेदार भाग में प्रवेश करें!

## पैकेज आयात करें
Aspose.Cells के साथ आरंभ करने के लिए, आपको अपने C# प्रोजेक्ट में आवश्यक नामस्थान आयात करने होंगे। यहाँ बताया गया है कि आप ऐसा कैसे कर सकते हैं:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

ये नामस्थान आपको एक्सेल फाइलों में हेरफेर करने और सशर्त स्वरूपण लागू करने के लिए आवश्यक कक्षाओं और विधियों तक पहुंच प्रदान करेंगे।

अब, आइए सशर्त स्वरूपण लागू करने की प्रक्रिया को प्रबंधनीय चरणों में विभाजित करें।

## चरण 1: अपना प्रोजेक्ट सेट करें
सबसे पहले, आपको Visual Studio में एक नया C# प्रोजेक्ट बनाना होगा। यहाँ बताया गया है कि कैसे:

1. विज़ुअल स्टूडियो खोलें और फ़ाइल > नया > प्रोजेक्ट चुनें।
2. कंसोल ऐप (.NET फ्रेमवर्क) चुनें और अपने प्रोजेक्ट को एक नाम दें।
3. बनाएँ पर क्लिक करें.

## चरण 2 : Aspose.Cells संदर्भ जोड़ें
एक बार आपका प्रोजेक्ट सेट हो जाने के बाद, आपको Aspose.Cells लाइब्रेरी में एक संदर्भ जोड़ना होगा:

1. समाधान एक्सप्लोरर में अपने प्रोजेक्ट पर राइट-क्लिक करें।
2. NuGet पैकेज प्रबंधित करें चुनें.
3. Aspose.Cells खोजें और इसे स्थापित करें।

यह आपको Aspose.Cells लाइब्रेरी द्वारा प्रदान की गई सभी कार्यक्षमता का उपयोग करने की अनुमति देगा।

## चरण 3: वर्कबुक ऑब्जेक्ट बनाएँ
इसके बाद, आइए एक नई वर्कबुक और वर्कशीट बनाएं। यहीं पर सारा जादू होता है:

```csharp
// दस्तावेज़ निर्देशिका का पथ.
string dataDir = "Your Document Directory";
string filePath = dataDir + "Book1.xlsx";

// वर्कबुक ऑब्जेक्ट को इंस्टैंशिएट करना
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

इस चरण में, हम उस डायरेक्टरी को परिभाषित कर रहे हैं जहां हमारी एक्सेल फ़ाइल सहेजी जाएगी, एक नई कार्यपुस्तिका बनाएंगे, और पहली कार्यपत्रक तक पहुंचेंगे।

## चरण 4: सशर्त स्वरूपण जोड़ें
अब, आइए कुछ सशर्त स्वरूपण जोड़ें। हम एक खाली सशर्त स्वरूपण ऑब्जेक्ट बनाकर शुरू करेंगे:

```csharp
// एक रिक्त सशर्त स्वरूपण जोड़ता है
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```

यहां, हम अपनी वर्कशीट में एक नया सशर्त स्वरूपण संग्रह जोड़ रहे हैं, जिसमें हमारे स्वरूपण नियम होंगे।

## चरण 5: प्रारूप सीमा निर्धारित करें
इसके बाद, हमें उन कक्षों की श्रेणी निर्दिष्ट करनी होगी जिन पर सशर्त स्वरूपण लागू होगा। मान लें कि हम पहली पंक्ति और दूसरे कॉलम को स्वरूपित करना चाहते हैं:

```csharp
// सशर्त प्रारूप सीमा निर्धारित करता है.
CellArea ca = new CellArea();
ca.StartRow =0;
ca.EndRow =0;
ca.StartColumn =0;
ca.EndColumn =0;
fcs.AddArea(ca);

ca = new CellArea();
ca.StartRow =1;
ca.EndRow =1;
ca.StartColumn =1;
ca.EndColumn =1;
fcs.AddArea(ca);
```

इस कोड में, हम सशर्त स्वरूपण के लिए दो क्षेत्र परिभाषित करते हैं। पहला क्षेत्र (0,0) पर सेल के लिए है और दूसरा (1,1) के लिए है। अपनी विशिष्ट आवश्यकताओं के आधार पर इन श्रेणियों को समायोजित करने के लिए स्वतंत्र महसूस करें!

## चरण 6: सशर्त स्वरूपण शर्तें जोड़ें
अब समय आ गया है कि हम अपने फ़ॉर्मेटिंग के लिए शर्तें तय करें। मान लीजिए कि हम सेल को उनके मानों के आधार पर हाइलाइट करना चाहते हैं:

```csharp
// शर्त जोड़ता है.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "=A2", "100");

// शर्त जोड़ता है.
int conditionIndex2 = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```

इस चरण में, हम दो शर्तें जोड़ रहे हैं: एक के बीच के मानों के लिए `A2` और `100`, और दूसरा के बीच के मानों के लिए `50` और `100`यह आपको कोशिकाओं को उनके मानों के आधार पर गतिशील रूप से हाइलाइट करने की अनुमति देता है।

## चरण 7: फ़ॉर्मेटिंग शैलियाँ सेट करें
हमारी शर्तें पूरी होने के बाद, अब हम फ़ॉर्मेटिंग स्टाइल सेट कर सकते हैं। आइए अपनी शर्तों के लिए पृष्ठभूमि का रंग बदलें:

```csharp
// पृष्ठभूमि का रंग सेट करता है.
FormatCondition fc = fcs[conditionIndex];
fc.Style.BackgroundColor = Color.Red;
```

यहाँ, हम पहली शर्त का बैकग्राउंड रंग लाल सेट कर रहे हैं। आप आवश्यकतानुसार फ़ॉन्ट रंग, बॉर्डर और अन्य शैलियों को बदलकर इसे और भी कस्टमाइज़ कर सकते हैं!

## चरण 8: एक्सेल फ़ाइल को सेव करें
अंत में, अब हमारे काम को सहेजने का समय आ गया है! हम कार्यपुस्तिका को निर्दिष्ट निर्देशिका में सहेजेंगे:

```csharp
// एक्सेल फ़ाइल को सहेजना
workbook.Save(dataDir + "output.xls");
```

कोड की यह पंक्ति एक्सेल फ़ाइल को सशर्त स्वरूपण के साथ सहेजती है। अपनी आउटपुट फ़ाइल के लिए निर्दिष्ट निर्देशिका की जाँच करना सुनिश्चित करें!

## निष्कर्ष
और अब आप इसे प्राप्त कर चुके हैं! आपने .NET के लिए Aspose.Cells का उपयोग करके Excel में रनटाइम पर सफलतापूर्वक सशर्त स्वरूपण लागू किया है। यह शक्तिशाली लाइब्रेरी प्रोग्रामेटिक रूप से Excel फ़ाइलों में हेरफेर करना आसान बनाती है, जिससे आप थकाऊ कार्यों को स्वचालित कर सकते हैं और अपने डेटा प्रस्तुतियों को बेहतर बना सकते हैं। चाहे आप किसी छोटे प्रोजेक्ट पर काम कर रहे हों या किसी बड़े पैमाने के एप्लिकेशन पर, Aspose.Cells आपके वर्कफ़्लो को सुव्यवस्थित करने और आपकी उत्पादकता में सुधार करने में आपकी मदद कर सकता है।

## अक्सर पूछे जाने वाले प्रश्न

### Aspose.Cells क्या है?
Aspose.Cells एक .NET लाइब्रेरी है जो डेवलपर्स को प्रोग्रामेटिक रूप से Excel फ़ाइलों को बनाने, उनमें हेरफेर करने और उन्हें परिवर्तित करने की अनुमति देती है।

### क्या मैं अन्य प्रोग्रामिंग भाषाओं के साथ Aspose.Cells का उपयोग कर सकता हूँ?
हां, Aspose.Cells कई प्रोग्रामिंग भाषाओं के लिए उपलब्ध है, जिनमें Java, Python और अन्य शामिल हैं।

### क्या Aspose.Cells के लिए कोई निःशुल्क परीक्षण उपलब्ध है?
हां, आप यहां से निःशुल्क परीक्षण संस्करण डाउनलोड कर सकते हैं [Aspose वेबसाइट](https://releases.aspose.com/).

### मैं Aspose.Cells के लिए समर्थन कैसे प्राप्त कर सकता हूं?
आप यहां जाकर सहायता प्राप्त कर सकते हैं [Aspose समर्थन मंच](https://forum.aspose.com/c/cells/9).

### क्या मुझे Aspose.Cells का उपयोग करने के लिए लाइसेंस की आवश्यकता है?
हां, व्यावसायिक उपयोग के लिए लाइसेंस की आवश्यकता होती है, लेकिन आप अस्थायी लाइसेंस का अनुरोध कर सकते हैं [यहाँ](https://purchase.aspose.com/temporary-license/).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}