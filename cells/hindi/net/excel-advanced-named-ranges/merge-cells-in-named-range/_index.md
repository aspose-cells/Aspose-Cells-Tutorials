---
"description": "इस चरण-दर-चरण ट्यूटोरियल में Aspose.Cells for .NET का उपयोग करके नामित श्रेणी में सेल मर्ज करना सीखें। Excel रिपोर्ट को फ़ॉर्मेट, स्टाइल और स्वचालित करने का तरीका जानें।"
"linktitle": "एक्सेल में नामित श्रेणी में कक्षों को मर्ज करें"
"second_title": "Aspose.Cells .NET एक्सेल प्रोसेसिंग API"
"title": "एक्सेल में नामित श्रेणी में कक्षों को मर्ज करें"
"url": "/hi/net/excel-advanced-named-ranges/merge-cells-in-named-range/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# एक्सेल में नामित श्रेणी में कक्षों को मर्ज करें

## परिचय

एक्सेल फ़ाइलों के साथ प्रोग्रामेटिक रूप से काम करते समय, आपके सामने आने वाले सामान्य कार्यों में से एक नामित श्रेणी के भीतर कोशिकाओं को मर्ज करना है। चाहे आप रिपोर्ट जनरेशन को स्वचालित कर रहे हों, डैशबोर्ड बना रहे हों, या बस बड़े डेटासेट का प्रबंधन कर रहे हों, कोशिकाओं को मर्ज करना एक आवश्यक तकनीक है। इस ट्यूटोरियल में, हम .NET के लिए Aspose.Cells का उपयोग करके नामित श्रेणी में कोशिकाओं को मर्ज करने का तरीका जानेंगे - एक शक्तिशाली लाइब्रेरी जो डेवलपर्स को Microsoft Excel इंस्टॉल किए बिना Excel फ़ाइलों में हेरफेर करने की अनुमति देती है।

## आवश्यक शर्तें

शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित चीज़ें तैयार हैं:

- .NET के लिए Aspose.Cells: आप इसे यहाँ से डाउनलोड कर सकते हैं [Aspose.Cells रिलीज़ पेज](https://releases.aspose.com/cells/net/).
- आपके मशीन पर .NET फ्रेमवर्क स्थापित है।
- C# की बुनियादी समझ: क्लासेस, मेथड्स और ऑब्जेक्ट्स जैसी अवधारणाओं से परिचित होना सहायक होगा।

## पैकेज आयात करें

कोडिंग में कूदने से पहले, आपको आवश्यक नेमस्पेस आयात करने की आवश्यकता है। ये नेमस्पेस आपको Aspose.Cells लाइब्रेरी की कार्यक्षमता तक पहुँच प्रदान करेंगे।

```csharp
using System;
using System.IO;
using Aspose.Cells;
```

पूर्वापेक्षाओं और पैकेजों को निपटाने के बाद, आइए मज़ेदार भाग की ओर बढ़ें: कोडिंग!

यहां बताया गया है कि आप .NET के लिए Aspose.Cells का उपयोग करके Excel शीट में नामित श्रेणी में कक्षों को कैसे मर्ज कर सकते हैं।

## चरण 1: नई कार्यपुस्तिका बनाएँ

सबसे पहले हमें एक वर्कबुक की जरूरत है। एक्सेल की भाषा में वर्कबुक एक्सेल फाइल के बराबर होती है। चलिए एक वर्कबुक बनाते हैं।

```csharp
// एक नई कार्यपुस्तिका का इन्स्टेन्सिएट करें.
Workbook wb1 = new Workbook();
```

एक नई कार्यपुस्तिका आरंभ करने से, अब हमारे पास हेरफेर करने के लिए एक खाली एक्सेल फ़ाइल तैयार है। यह एक खाली कैनवास के साथ शुरू करने जैसा है!

## चरण 2: पहली वर्कशीट तक पहुँचें

हर वर्कबुक में वर्कशीट होती है, और इस मामले में, हम पहली वाली के साथ काम करना चाहते हैं। चलो इसे पकड़ो!

```csharp
// कार्यपुस्तिका में प्रथम कार्यपत्रक प्राप्त करें।
Worksheet worksheet1 = wb1.Worksheets[0];
```

वर्कशीट को एक्सेल फ़ाइल में अलग-अलग टैब के रूप में सोचें जहाँ वास्तविक डेटा रहता है। डिफ़ॉल्ट रूप से, हम सबसे पहले टैब तक पहुँच रहे हैं।

## चरण 3: कोशिकाओं की एक श्रेणी बनाएँ

अब जब हमारे पास वर्कशीट है, तो रेंज बनाने का समय आ गया है। रेंज से तात्पर्य कोशिकाओं के एक ब्लॉक से है, जो कई पंक्तियों और स्तंभों में फैल सकता है।

```csharp
// एक रेंज बनाएं.
Range mrange = worksheet1.Cells.CreateRange("D6", "I12");
```

यहाँ, हम D6 से I12 तक की कोशिकाओं का चयन कर रहे हैं - एक ब्लॉक जो कई पंक्तियों और स्तंभों को कवर करता है। हम जल्द ही इस श्रेणी को मर्ज कर देंगे!

## चरण 4: रेंज का नाम दें

किसी श्रेणी को नाम देने से बाद में उसका संदर्भ लेना आसान हो जाता है, विशेष रूप से बड़े डेटासेट के साथ काम करते समय।

```csharp
// रेंज का नाम बताइए.
mrange.Name = "TestRange";
```

इस श्रेणी को "TestRange" नाम देकर, हम इसे बाद में कोड में शीघ्रता से प्राप्त कर सकते हैं, बिना पुनः सेल निर्देशांक निर्दिष्ट करने की आवश्यकता के।

## चरण 5: कोशिकाओं की श्रेणी को मर्ज करें

अब जादू की बारी है - हमारे द्वारा अभी-अभी बनाई गई श्रेणी के भीतर कोशिकाओं को विलय करना!

```csharp
// श्रेणी की कोशिकाओं को मर्ज करें.
mrange.Merge();
```

यह चरण D6 से I12 तक सभी सेल को एक एकल सेल में मर्ज कर देता है। शीर्षक या सारांश जैसी चीज़ों के लिए बिल्कुल सही!

## चरण 6: नामित श्रेणी पुनः प्राप्त करें

एक बार जब सेल मर्ज हो जाते हैं, तो हम कुछ फ़ॉर्मेटिंग लागू करना चाह सकते हैं। आइए सबसे पहले अपनी नामित श्रेणी प्राप्त करें।

```csharp
// सीमा प्राप्त करें.
Range range1 = wb1.Worksheets.GetRangeByName("TestRange");
```

नाम से श्रेणी प्राप्त करने से हमें आगे के कार्य करने की अनुमति मिलती है, जैसे शैलियाँ जोड़ना या डेटा इनपुट करना।

## चरण 7: मर्ज किए गए कक्षों के लिए शैली निर्धारित करें

अगर मर्ज किया गया सेल पॉलिश नहीं दिखता तो उसका क्या फायदा? चलिए टेक्स्ट को संरेखित करने और बैकग्राउंड कलर लगाने के लिए स्टाइल ऑब्जेक्ट बनाते हैं।

```csharp
// एक शैली ऑब्जेक्ट परिभाषित करें.
Style style = wb1.CreateStyle();

// संरेखण सेट करें.
style.HorizontalAlignment = TextAlignmentType.Center;
style.VerticalAlignment = TextAlignmentType.Center;
style.Pattern = BackgroundType.Solid;
style.ForegroundColor = System.Drawing.Color.Aqua;
```

यहाँ, हम टेक्स्ट को क्षैतिज और लंबवत दोनों तरह से बीच में संरेखित कर रहे हैं, और एक हल्का नीला (एक्वा) बैकग्राउंड रंग सेट कर रहे हैं। स्टाइलिश है, है न?

## चरण 8: रेंज पर स्टाइल लागू करें

शैली को परिभाषित करने के बाद, इसे मर्ज की गई श्रेणी पर लागू करने का समय आ गया है।

```csharp
// एक स्टाइलफ्लैग ऑब्जेक्ट बनाएं.
StyleFlag flag = new StyleFlag();

// सापेक्ष शैली विशेषता को चालू करें.
flag.HorizontalAlignment = true;
flag.VerticalAlignment = true;
flag.CellShading = true;

// शैली को श्रेणी पर लागू करें.
range1.ApplyStyle(style, flag);
```

The `StyleFlag` Aspose.Cells को बताता है कि कौन से स्टाइल गुण लागू करने हैं - संरेखण, छायांकन, आदि। यह आपको इस बात पर बारीक नियंत्रण देता है कि स्टाइल कैसे लागू किया जाता है।

## चरण 9: मर्ज की गई रेंज में डेटा इनपुट करें

बिना विषय-वस्तु के स्वरूपित श्रेणी क्या है? चलिए कुछ पाठ जोड़ते हैं।

```csharp
// रेंज में डेटा इनपुट करें.
range1[0, 0].PutValue("Welcome to Aspose APIs.");
```

यह हमारे मर्ज किए गए रेंज के पहले सेल में "वेलकम टू एस्पोज एपीआई" टेक्स्ट को रखता है। सेल के मर्ज होने के साथ, यह टेक्स्ट D6 से I12 तक सभी सेल में फैल जाएगा।

## चरण 10: एक्सेल फ़ाइल को सेव करें

अंत में, आइए कार्यपुस्तिका को एक्सेल फ़ाइल के रूप में सेव करें।

```csharp
// एक्सेल फ़ाइल को सहेजें.
wb1.Save(dataDir + "outputMergeCellsInNamedRange.xlsx");
```

यहां, कार्यपुस्तिका आपके निर्दिष्ट निर्देशिका में "outputMergeCellsInNamedRange.xlsx" नाम से सहेजी गई है।

## निष्कर्ष

और अब यह हो गया! आपने नामित श्रेणी में सफलतापूर्वक सेल मर्ज कर लिए हैं, कुछ सुंदर फ़ॉर्मेटिंग लागू कर दी है, और कुछ डेटा भी इनपुट कर दिया है—ये सब Aspose.Cells for .NET के साथ। चाहे आप रिपोर्ट को स्वचालित करने, एक्सेल फ़ाइलों में हेरफेर करने या सिर्फ़ नई तकनीक सीखने पर काम कर रहे हों, यह चरण-दर-चरण मार्गदर्शिका आपको वह आधार प्रदान करेगी जिसकी आपको आवश्यकता है।

## अक्सर पूछे जाने वाले प्रश्न

### क्या मैं Aspose.Cells में एकाधिक गैर-सन्निहित श्रेणियों को मर्ज कर सकता हूँ?  
नहीं, आप केवल Aspose.Cells में सन्निहित कोशिकाओं को ही मर्ज कर सकते हैं।

### क्या मैं प्रोग्रामेटिक रूप से मर्ज ऑपरेशन को पूर्ववत कर सकता हूँ?  
एक बार जब कोशिकाएं मर्ज हो जाती हैं, तो आप उनका उपयोग करके उन्हें अलग कर सकते हैं `UnMerge()` Aspose.Cells में विधि.

### क्या कोशिकाओं को मर्ज करने से उनमें मौजूद डेटा हट जाता है?  
यदि विलय से पहले कक्षों में कोई डेटा है, तो यह श्रेणी के पहले कक्ष के डेटा को बनाए रखेगा।

### क्या मैं मर्ज की गई श्रेणी के भीतर अलग-अलग कक्षों पर अलग-अलग शैलियाँ लागू कर सकता हूँ?  
नहीं, मर्ज की गई श्रेणी एकल कक्ष के रूप में कार्य करती है, इसलिए आप इसके अंदर अलग-अलग कक्षों पर अलग-अलग शैलियाँ लागू नहीं कर सकते।

### विलय के बाद मैं विलयित सेल तक कैसे पहुंच सकता हूं?  
विलय के बाद भी आप विलय किए गए सेल तक उसके ऊपरी-बाएं कोने के निर्देशांकों का उपयोग करके पहुंच सकते हैं।

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}