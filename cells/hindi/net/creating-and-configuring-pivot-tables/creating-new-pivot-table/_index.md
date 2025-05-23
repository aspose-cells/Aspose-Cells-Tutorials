---
"description": "हमारे चरण-दर-चरण गाइड के साथ Aspose.Cells का उपयोग करके .NET में प्रोग्रामेटिक रूप से पिवट टेबल बनाना सीखें। अपने डेटा का कुशलतापूर्वक विश्लेषण करें।"
"linktitle": ".NET में प्रोग्रामेटिक रूप से एक नई पिवट तालिका बनाएँ"
"second_title": "Aspose.Cells .NET एक्सेल प्रोसेसिंग API"
"title": ".NET में प्रोग्रामेटिक रूप से एक नई पिवट तालिका बनाएँ"
"url": "/hi/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# .NET में प्रोग्रामेटिक रूप से एक नई पिवट तालिका बनाएँ

## परिचय
पिवट टेबल बनाना एक डरावना काम लग सकता है, खासकर जब आप इसे प्रोग्रामेटिक रूप से कर रहे हों। लेकिन डरें नहीं! .NET के लिए Aspose.Cells के साथ, पिवट टेबल बनाना न केवल सीधा है बल्कि डेटा विश्लेषण के लिए भी काफी शक्तिशाली है। इस ट्यूटोरियल में, हम आपको .NET एप्लिकेशन में एक नई पिवट टेबल बनाने के तरीके के बारे में चरण-दर-चरण मार्गदर्शन करेंगे। चाहे आप बिक्री, खेल या किसी अन्य व्यावसायिक मीट्रिक के लिए डेटा जोड़ रहे हों, यह गाइड आपको कुछ ही समय में अपनी पिवट टेबल को चालू करने में मदद करेगी।

## आवश्यक शर्तें
शुरू करने से पहले, आइए सुनिश्चित करें कि आपके पास जाने के लिए सब कुछ तैयार है। आपको ये करना होगा:

1. .NET फ्रेमवर्क स्थापित करें: सुनिश्चित करें कि आपके मशीन पर .NET फ्रेमवर्क स्थापित है। Aspose.Cells विभिन्न संस्करणों का समर्थन करता है, लेकिन नवीनतम संस्करण का उपयोग करना सबसे अच्छा है।
2. Aspose.Cells लाइब्रेरी: आपके पास Aspose.Cells लाइब्रेरी होनी चाहिए। आप ऐसा कर सकते हैं [यहाँ पर डाउनलोड करो](https://releases.aspose.com/cells/net/) या प्राप्त करें [अस्थायी लाइसेंस](https://purchase.aspose.com/temporary-license/) मूल्यांकन हेतु.
3. IDE सेटअप: एक C# संगत IDE तैयार रखें, जैसे Visual Studio, जहां आप एक नया प्रोजेक्ट शुरू कर सकें।
4. C# का बुनियादी ज्ञान: C# प्रोग्रामिंग से परिचित होने से आपको बिना ज्यादा परेशान हुए इसे समझने में मदद मिलेगी।

क्या आप पूरी तरह तैयार हैं? बढ़िया! चलिए आवश्यक पैकेज आयात करना शुरू करते हैं।

## पैकेज आयात करें
सबसे पहले, आपको अपने C# प्रोजेक्ट में आवश्यक नेमस्पेस को आयात करना होगा। अपनी C# फ़ाइल खोलें और निम्नलिखित using निर्देश जोड़ें:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

ये नामस्थान आपको कार्यपुस्तिका, कार्यपत्रक और पिवट तालिका कार्यात्मकताओं तक पहुंच प्रदान करते हैं जिनका उपयोग हम इस ट्यूटोरियल में करेंगे।

## चरण 1: वर्कबुक ऑब्जेक्ट बनाएँ
वर्कबुक बनाना आपकी यात्रा की शुरुआत है। आइए एक नई वर्कबुक को इंस्टेंटिएट करके और पहली वर्कशीट तक पहुँचकर शुरुआत करें।

```csharp
// दस्तावेज़ निर्देशिका का पथ.
string dataDir = "Your Document Directory";
// वर्कबुक ऑब्जेक्ट को इंस्टैंशिएट करना
Workbook workbook = new Workbook();

// नये जोड़े गए वर्कशीट का संदर्भ प्राप्त करना
Worksheet sheet = workbook.Worksheets[0];
```

इस चरण में, हम एक बनाते हैं `Workbook` उदाहरण जो हमारी एक्सेल फ़ाइल का प्रतिनिधित्व करता है और सबसे पहले वर्कशीट को पकड़ता है, जो पिवट टेबल के लिए हमारा खेल का मैदान होगा।

## चरण 2: कक्षों में डेटा डालें
इसके बाद, आइए अपनी वर्कशीट में कुछ सैंपल डेटा भरें। हम अपनी पिवट टेबल को सारांशित करने के लिए कुछ देने के लिए अलग-अलग खेल, क्वार्टर और बिक्री के आंकड़ों के लिए पंक्तियाँ इनपुट करने जा रहे हैं।

```csharp
Cells cells = sheet.Cells;

// कक्षों में मान सेट करना
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

// डेटा भरनाcell = cells["A2"];
cell.PutValue("Golf");
// ... अधिक डेटा प्रविष्टियाँ
```

यहाँ, हम अपने कॉलम हेडर को परिभाषित कर रहे हैं और प्रत्येक हेडर के नीचे मान डाल रहे हैं। यह डेटा हमारी पिवट टेबल के स्रोत के रूप में कार्य करेगा, इसलिए सुनिश्चित करें कि यह व्यवस्थित है! इस ब्लॉक का पालन करें, और आप एक व्यापक डेटासेट बना लेंगे।

## चरण 3: पिवट तालिका जोड़ना
हमारा डेटा तैयार होने के बाद, पिवट टेबल बनाने का समय आ गया है। हम अपनी नई पिवट टेबल जोड़ने के लिए वर्कशीट से पिवट टेबल संग्रह का उपयोग करेंगे।

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// वर्कशीट में PivotTable जोड़ना
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

इस स्निपेट में, हम वर्कशीट में एक पिवट टेबल जोड़ते हैं जो हमारी डेटा रेंज (इस मामले में, सेल A1 से C8) को संदर्भित करता है। हम पिवट टेबल को सेल E3 से शुरू करते हैं, और इसे "PivotTable2" नाम देते हैं। बहुत आसान है, है न?

## चरण 4: पिवट तालिका को अनुकूलित करें
अब जब हमारे पास पिवट टेबल है, तो आइए इसे सार्थक सारांश दिखाने के लिए कस्टमाइज़ करें। हम नियंत्रित कर सकते हैं कि पिवट टेबल की पंक्तियों, स्तंभों और डेटा क्षेत्रों में क्या दिखाई देता है।

```csharp
// नए जोड़े गए PivotTable के उदाहरण तक पहुँचना
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

// पंक्तियों के लिए कुल योग प्रदर्शित नहीं किया जा रहा है।
pivotTable.RowGrand = false;

// प्रथम फ़ील्ड को पंक्ति क्षेत्र में खींचना.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

// दूसरे फ़ील्ड को स्तंभ क्षेत्र में खींचना.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

// तीसरे फ़ील्ड को डेटा क्षेत्र में खींचना.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

इस चरण में, हम पिवट टेबल को पंक्तियों के लिए कुल योग छिपाने के लिए कहते हैं और फिर निर्दिष्ट करते हैं कि कौन से फ़ील्ड पंक्ति, कॉलम और डेटा क्षेत्रों में जाते हैं। खेल के नाम पंक्तियों को भरेंगे, तिमाहियों को कॉलम भरेंगे, और बिक्री के आंकड़े सारांश प्रदान करेंगे।

## चरण 5: कार्यपुस्तिका सहेजें
अंत में, हम अपने श्रम का फल देखने के लिए अपनी नव निर्मित कार्यपुस्तिका को सहेजना चाहते हैं।

```csharp
// एक्सेल फ़ाइल को सहेजना
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

बस एक उचित पथ प्रदान करें, और आपकी पिवट तालिका आउटपुट एक एक्सेल फ़ाइल में सहेजी जाएगी जिसे आप खोलकर समीक्षा कर सकते हैं।

## निष्कर्ष
.NET के लिए Aspose.Cells का उपयोग करके प्रोग्रामेटिक रूप से पिवट टेबल बनाना आपका समय बचा सकता है, खासकर जब बड़े डेटासेट से निपटना हो। आपने सीखा है कि कैसे अपना प्रोजेक्ट सेट अप करें, आवश्यक पैकेज आयात करें, डेटा पॉप्युलेट करें और स्क्रैच से एक कस्टमाइज़ करने योग्य पिवट टेबल बनाएँ। तो, अगली बार जब आप संख्याओं में डूब रहे हों, तो इस ट्यूटोरियल को याद रखें और Aspose.Cells को आपके लिए भारी काम करने दें।

## अक्सर पूछे जाने वाले प्रश्न
### Aspose.Cells क्या है?
Aspose.Cells एक्सेल स्प्रेडशीट को प्रोग्रामेटिक रूप से बनाने और प्रबंधित करने के लिए एक शक्तिशाली .NET लाइब्रेरी है।

### क्या Aspose.Cells के लिए कोई निःशुल्क परीक्षण उपलब्ध है?
हां, आप निःशुल्क परीक्षण प्राप्त कर सकते हैं [यहाँ](https://releases.aspose.com/).

### क्या मैं पिवट तालिका के स्वरूप को अनुकूलित कर सकता हूँ?
बिल्कुल! आप अपनी आवश्यकताओं के अनुसार पिवट टेबल के स्वरूपण, लेआउट और यहां तक कि शैलियों को भी अनुकूलित कर सकते हैं।

### मैं Aspose.Cells पर अधिक उदाहरण और दस्तावेज़ कहां पा सकता हूं?
आप जाँच कर सकते हैं [प्रलेखन](https://reference.aspose.com/cells/net/) विस्तृत मार्गदर्शिका और उदाहरण के लिए.

### मैं Aspose.Cells के लिए समर्थन कैसे प्राप्त करूं?
आप इसके माध्यम से सहायता प्राप्त कर सकते हैं [एस्पोज फोरम](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}