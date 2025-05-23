---
"description": "जानें कि .NET के लिए Aspose.Cells का उपयोग करके Excel में शानदार 3D चार्ट कैसे बनाएं। हमारे सरल चरण-दर-चरण गाइड का पालन करें।"
"linktitle": "चार्ट पर 3D प्रारूप लागू करें"
"second_title": "Aspose.Cells .NET एक्सेल प्रोसेसिंग API"
"title": "चार्ट पर 3D प्रारूप लागू करें"
"url": "/hi/net/advanced-chart-operations/apply-3d-format-to-chart/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# चार्ट पर 3D प्रारूप लागू करें

## परिचय

ऐसे युग में जहाँ डेटा विज़ुअलाइज़ेशन सर्वोपरि है, जिस तरह से हम अपना डेटा प्रस्तुत करते हैं वह बुनियादी ग्राफ़ और चार्ट से परे है। .NET के लिए Aspose.Cells जैसे टूल के साथ, आप अपने डेटा प्रेजेंटेशन को शानदार 3D चार्ट के साथ बढ़ा सकते हैं जो न केवल ध्यान आकर्षित करते हैं बल्कि जानकारी को प्रभावी ढंग से संप्रेषित भी करते हैं। यह गाइड आपको Aspose.Cells का उपयोग करके चार्ट पर 3D फ़ॉर्मेट लागू करने के चरणों के माध्यम से मार्गदर्शन करेगा, जिससे आपका कच्चा डेटा एक आकर्षक डिस्प्ले में बदल जाएगा।

## आवश्यक शर्तें

इससे पहले कि हम चार्ट पर 3D प्रारूप लागू करने की बारीकियों में उतरें, आइए सुनिश्चित करें कि आपके पास वह सब कुछ है जो आपको चाहिए।

### सॉफ़्टवेयर आवश्यकताएं

- विज़ुअल स्टूडियो: सुनिश्चित करें कि आपके पास .NET अनुप्रयोगों के साथ काम करने के लिए विज़ुअल स्टूडियो स्थापित है।
- .NET के लिए Aspose.Cells: यदि आपने अभी तक ऐसा नहीं किया है, तो यहां से Aspose.Cells डाउनलोड और इंस्टॉल करें [यहाँ](https://releases.aspose.com/cells/net/).

### कोडिंग वातावरण सेटअप

1. नया .NET प्रोजेक्ट बनाएँ: Visual Studio खोलें, “नया प्रोजेक्ट बनाएँ” चुनें, और कंसोल एप्लिकेशन चुनें।
2. Aspose.Cells संदर्भ जोड़ें: NuGet पैकेज मैनेजर के माध्यम से, Aspose.Cells को खोजकर या पैकेज मैनेजर कंसोल के माध्यम से जोड़ें:

```bash
Install-Package Aspose.Cells
```

3. आउटपुट निर्देशिका सेटअप करें: एक आउटपुट निर्देशिका निर्दिष्ट करें जहां आपकी जेनरेट की गई फ़ाइलें सहेजी जाएंगी - यह आपके डेस्कटॉप पर एक फ़ोल्डर बनाने जितना सरल हो सकता है।

अब जब आप पूरी तरह से तैयार हो गए हैं, तो कोड में कूदने और कुछ चमकदार 3D चार्ट बनाने का समय आ गया है!

## पैकेज आयात करें

शुरू करने के लिए, आपको आवश्यक नामस्थानों को आयात करना होगा। इससे आपको Aspose.Cells द्वारा प्रदान की गई कक्षाओं और विधियों तक पहुँचने में मदद मिलेगी। यहाँ बताया गया है कि आप ऐसा कैसे करते हैं:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

यह अनुभाग प्रक्रिया को प्रबंधनीय चरणों में विभाजित करेगा, जिससे आपको प्रत्येक चरण की स्पष्ट समझ प्राप्त होगी।

## चरण 1: अपनी कार्यपुस्तिका आरंभ करें

सबसे पहले, आपको इसका एक उदाहरण बनाना होगा `Workbook` क्लास। यह ऑब्जेक्ट आपके एक्सेल दस्तावेज़ के लिए आधार के रूप में काम करेगा।

```csharp
//आउटपुट निर्देशिका
string outputDir = "Your Document Directory";
Workbook book = new Workbook();
```
इस पर विचार करें `Workbook` एक खाली कैनवास के रूप में - जिसे आप रंगीन डेटा और प्रभावशाली विज़ुअलाइज़ेशन से भर सकते हैं।

## चरण 2: पहली वर्कशीट का नाम बदलें

अब, आइए पहले वर्कशीट का नाम बदलें। इससे यह स्पष्ट हो जाएगा कि हम किस डेटा के साथ काम कर रहे हैं।

```csharp
book.Worksheets[0].Name = "DataSheet";
```

नाम सहज होने चाहिए। इस मामले में, हम इसे "डेटाशीट" नाम दे रहे हैं ताकि हमें पता चले कि हमारा डेटा कहाँ रहता है।

## चरण 3: चार्ट के लिए डेटा बनाएँ

अब, हम अपनी "डेटाशीट" में कुछ डेटा जोड़ेंगे। आइए इसे उन मानों से भरें जिनका उपयोग हमारा चार्ट करेगा।

```csharp
Worksheet dataSheet = book.Worksheets["DataSheet"];
dataSheet.Cells["B1"].PutValue(1);
dataSheet.Cells["B2"].PutValue(2);
dataSheet.Cells["B3"].PutValue(3);
dataSheet.Cells["A1"].PutValue("A");
dataSheet.Cells["A2"].PutValue("B");
dataSheet.Cells["A3"].PutValue("C");
```

जिस प्रकार एक नुस्खा सामग्री पर निर्भर करता है, उसी प्रकार आपके चार्ट की प्रभावशीलता आपके इनपुट डेटा की गुणवत्ता और संगठन पर निर्भर करती है।

## चरण 4: एक नया चार्ट वर्कशीट सेटअप करें

चार्ट के लिए एक नई वर्कशीट बनाने का समय आ गया है। इससे आपके डेटा विज़ुअलाइज़ेशन को व्यवस्थित रखने में मदद मिलती है।

```csharp
Worksheet sheet = book.Worksheets.Add("MyChart");
```

इस वर्कशीट को अपना मंच मानें - जहां आपके डेटा का प्रदर्शन सामने आता है।

## चरण 5: चार्ट जोड़ें

यहां, हम नई बनाई गई वर्कशीट में एक कॉलम चार्ट जोड़ेंगे।  

```csharp
ChartCollection charts = sheet.Charts;
int chartSheetIdx = charts.Add(ChartType.Column, 5, 0, 25, 15);
```

हम अपने चार्ट के लिए एक स्थान निर्धारित कर रहे हैं और यह निर्दिष्ट कर रहे हैं कि यह किस प्रकार का है। बस इसे अपने आर्टवर्क के लिए फ़्रेम के प्रकार का चयन करने के रूप में सोचें।

## चरण 6: चार्ट का स्वरूप अनुकूलित करें

अब, पृष्ठभूमि रंग निर्धारित करके अपने चार्ट के स्वरूप को अनुकूलित करें। 

```csharp
Aspose.Cells.Charts.Chart chart = book.Worksheets["MyChart"].Charts[0];
chart.PlotArea.Area.BackgroundColor = Color.White;
chart.ChartArea.Area.BackgroundColor = Color.White;
chart.PlotArea.Area.ForegroundColor = Color.White;
chart.ChartArea.Area.ForegroundColor = Color.White;
chart.ShowLegend = false;
```

एक साफ सफेद पृष्ठभूमि अक्सर आपके डेटा के रंगों को उजागर करती है, जिससे दृश्यता बढ़ जाती है।

## चरण 7: चार्ट में डेटा श्रृंखला जोड़ें

अब समय आ गया है कि हम अपने चार्ट में डेटा डालें। हम अपने "डेटाशीट" से डेटा सीरीज जोड़ेंगे ताकि यह सुनिश्चित हो सके कि हमारा चार्ट हमारे लिए आवश्यक डेटा को दर्शाता है।

```csharp
chart.NSeries.Add("DataSheet!B1:B3", true);
chart.NSeries.CategoryData = "DataSheet!A1:A3";
```

यह एक शेफ द्वारा विशिष्ट सामग्रियों से व्यंजन तैयार करने के समान है। प्रत्येक डेटा बिंदु मायने रखता है!

## चरण 8: डेटा श्रृंखला तक पहुंचें और उसे प्रारूपित करें

अब जबकि हमारा डेटा लिंक हो गया है, तो चलिए डेटा श्रृंखला लेते हैं और कुछ 3D प्रभाव लागू करना शुरू करते हैं।

```csharp
Aspose.Cells.Charts.Series ser = chart.NSeries[0];
ShapePropertyCollection spPr = ser.ShapeProperties;
Format3D fmt3d = spPr.Format3D;
```

हम अपने पकवान में कुछ नयापन जोड़ने की तैयारी कर रहे हैं - इसे ऐसे मसाले के रूप में सोचें जो समग्र स्वाद को बढ़ा देता है।

## चरण 9: 3D बेवल प्रभाव लागू करें

इसके बाद, हम अपने चार्ट को कुछ आयाम देने के लिए बेवल प्रभाव जोड़ेंगे।

```csharp
Bevel bevel = fmt3d.TopBevel;
bevel.Type = BevelPresetType.Circle;
bevel.Height = 2;
bevel.Width = 5;
```

जैसे एक मूर्तिकार पत्थर को आकार देता है, वैसे ही हम गहराई पैदा कर रहे हैं जो हमारे चार्ट को जीवंत बनाती है!

## चरण 10: सतह सामग्री और प्रकाश व्यवस्था को अनुकूलित करें

आइए अपने चार्ट को चमकदार बनाएं! हम सतह की सामग्री और प्रकाश व्यवस्था की सेटिंग को समायोजित करेंगे।

```csharp
fmt3d.SurfaceMaterialType = PresetMaterialType.WarmMatte;
fmt3d.SurfaceLightingType = LightRigType.ThreePoint;
fmt3d.LightingAngle = 20;
```

उचित प्रकाश व्यवस्था और सामग्री एक सपाट वस्तु को एक आकर्षक दृश्य में बदल सकती है। एक फिल्म सेट के बारे में सोचें जिसमें हर दृश्य को बेहतर बनाने के लिए विशेष रूप से रोशनी की गई हो।

## चरण 11: श्रृंखला की उपस्थिति पर अंतिम रूप

अब हम अपने डेटा श्रृंखला के रंग को समायोजित करके उसके स्वरूप को अंतिम रूप देंगे।

```csharp
ser.Area.BackgroundColor = Color.Maroon;
ser.Area.ForegroundColor = Color.Maroon;
ser.Border.Color = Color.Maroon;
```

सही रंग कुछ विशेष भावनाएं और प्रतिक्रियाएं उत्पन्न कर सकता है - मैरून रंग सुंदरता और परिष्कार का स्पर्श जोड़ता है।

## चरण 12: अपनी कार्यपुस्तिका सहेजें

अंत में, अपनी उत्कृष्ट कृति को सहेजने का समय आ गया है! उस स्थान को निर्दिष्ट करना न भूलें जहाँ आप इसे संग्रहीत करना चाहते हैं।

```csharp
book.Save(outputDir + "outputApplying3DFormat.xlsx");
Console.WriteLine("Applying3DFormat executed successfully.");
```

अपने काम को सहेजना अपनी कला को गैलरी में रखने जैसा है; यह संजोने और साझा करने का क्षण है।

## निष्कर्ष

बधाई हो! आपने .NET के लिए Aspose.Cells का उपयोग करके सफलतापूर्वक एक आकर्षक 3D चार्ट बनाया है। इन चरणों का पालन करके, अब आपके पास अपने डेटा प्रस्तुतियों को बढ़ाने के लिए एक शक्तिशाली उपकरण है, जो उन्हें न केवल जानकारीपूर्ण बनाता है बल्कि नेत्रहीन रूप से आकर्षक भी बनाता है। जैसे ही आप अपने चार्ट को परिष्कृत करते हैं, याद रखें कि प्रत्येक विज़ुअलाइज़ेशन एक कहानी है - इसे आकर्षक, स्पष्ट और प्रभावशाली बनाएं!

## अक्सर पूछे जाने वाले प्रश्न

### .NET के लिए Aspose.Cells क्या है?
.NET के लिए Aspose.Cells एक शक्तिशाली लाइब्रेरी है जो डेवलपर्स को चार्ट और आरेख बनाने सहित एक्सेल दस्तावेजों को प्रोग्रामेटिक रूप से हेरफेर करने की अनुमति देती है।

### क्या मैं Aspose.Cells में चार्ट प्रकार को अनुकूलित कर सकता हूँ?
हाँ! Aspose.Cells विभिन्न चार्ट प्रकारों जैसे कॉलम, लाइन, पाई और कई अन्य का समर्थन करता है, जिन्हें आसानी से अनुकूलित किया जा सकता है।

### क्या Aspose.Cells के लिए कोई निःशुल्क परीक्षण उपलब्ध है?
बिलकुल! आप यहाँ से निःशुल्क परीक्षण डाउनलोड कर सकते हैं [यहाँ](https://releases.aspose.com/).

### क्या मैं 3D प्रारूप के अलावा चार्ट पर अन्य प्रभाव भी लागू कर सकता हूँ?
हां, आप अपने चार्ट को 3D से परे बढ़ाने के लिए छाया, ग्रेडिएंट और विभिन्न शैलियों जैसे विभिन्न प्रभाव लागू कर सकते हैं।

### मैं Aspose.Cells के लिए समर्थन कहां पा सकता हूं?
सहायता के लिए आप यहां जा सकते हैं [एस्पोज फोरम](https://forum.aspose.com/c/cells/9) सामुदायिक सहायता और मदद के लिए.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}