---
"description": "इस चरण-दर-चरण मार्गदर्शिका के साथ .NET के लिए Aspose.Cells का उपयोग करके Excel में पाई चार्ट बनाना सीखें। अपने डेटा को आसानी से विज़ुअलाइज़ करें।"
"linktitle": "पाई चार्ट बनाएं"
"second_title": "Aspose.Cells .NET एक्सेल प्रोसेसिंग API"
"title": "पाई चार्ट बनाएं"
"url": "/hi/net/manipulating-chart-types/create-pie-chart/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# पाई चार्ट बनाएं

## परिचय

डेटा को विज़ुअली दिखाने के लिए चार्ट बनाना ज़रूरी है, और पाई चार्ट यह दिखाने के सबसे लोकप्रिय तरीकों में से एक है कि भाग कैसे एक पूरे को बनाते हैं। .NET के लिए Aspose.Cells के साथ, आप Excel फ़ाइलों में पाई चार्ट बनाने को आसानी से स्वचालित कर सकते हैं। इस ट्यूटोरियल में, हम .NET के लिए Aspose.Cells का उपयोग करके स्क्रैच से पाई चार्ट बनाने के तरीके के बारे में जानेंगे, जिसमें प्रक्रिया को आसान और सरल बनाने के लिए चरण-दर-चरण मार्गदर्शिका दी गई है। चाहे आप टूल के लिए नए हों या अपने एक्सेल ऑटोमेशन कौशल को बढ़ाना चाहते हों, यह मार्गदर्शिका आपके लिए है!

## आवश्यक शर्तें

कोड में आगे बढ़ने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित सेटअप है:

1. .NET लाइब्रेरी के लिए Aspose.Cells: सुनिश्चित करें कि आपके प्रोजेक्ट में Aspose.Cells इंस्टॉल है। अगर आपने इसे अभी तक इंस्टॉल नहीं किया है, तो आप इसे यहाँ से डाउनलोड कर सकते हैं [यहाँ](https://releases.aspose.com/cells/net/).
2. .NET विकास वातावरण: सुनिश्चित करें कि आपका प्रोजेक्ट .NET फ्रेमवर्क या .NET कोर का उपयोग करने के लिए सेट किया गया है।
3. C# का बुनियादी ज्ञान: आपको C# प्रोग्रामिंग, विशेष रूप से ऑब्जेक्ट-ओरिएंटेड प्रोग्रामिंग (OOP) में सहजता होनी चाहिए।

उन्नत उपयोगकर्ताओं के लिए, Aspose.Cells की सभी सुविधाओं को अनलॉक करने के लिए एक अस्थायी लाइसेंस लागू किया जा सकता है। आप यहाँ से अनुरोध कर सकते हैं [यहाँ](https://purchase.aspose.com/temporary-license/).

## पैकेज आयात करें

आरंभ करने के लिए, इस ट्यूटोरियल के लिए आवश्यक नेमस्पेस और पैकेज आयात करें। इनमें बुनियादी I/O ऑपरेशन और Aspose.Cells पैकेज शामिल हैं।

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## चरण 1: नई कार्यपुस्तिका बनाएँ

सबसे पहले, हमें इसका एक उदाहरण बनाना होगा `Workbook` क्लास, जो एक्सेल फ़ाइल का प्रतिनिधित्व करता है। एक कार्यपुस्तिका में कई शीट होती हैं, और हमारे उदाहरण के लिए, हम दो शीट के साथ काम करेंगे - एक डेटा के लिए और एक पाई चार्ट के लिए।

```csharp
Workbook workbook = new Workbook();
```

इससे एक नई एक्सेल वर्कबुक शुरू हो जाती है। लेकिन डेटा कहां जाता है? आइए अगले चरण में इसका ध्यान रखें।

## चरण 2: वर्कशीट में डेटा जोड़ें

वर्कबुक बन जाने के बाद, हमें पहली वर्कशीट तक पहुँचना होगा और उसे नाम देना होगा। यहीं पर हम पाई चार्ट के लिए ज़रूरी डेटा इनपुट करेंगे।

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

अब, हम विभिन्न क्षेत्रों का प्रतिनिधित्व करने वाले कुछ डमी बिक्री डेटा इनपुट कर सकते हैं:

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

यहाँ, हम दो कॉलम जोड़ रहे हैं: एक क्षेत्रों के लिए और दूसरा बिक्री के आंकड़ों के लिए। यह डेटा पाई चार्ट में दर्शाया जाएगा।

## चरण 3: चार्ट शीट जोड़ें

अब, आइए पाई चार्ट रखने के लिए एक अलग वर्कशीट जोड़ें।

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

यह नई शीट पाई चार्ट को होस्ट करेगी। इसे "चार्ट" जैसा नाम देने से यह सुनिश्चित होता है कि उपयोगकर्ता जानते हैं कि फ़ाइल खोलने पर उन्हें क्या उम्मीद करनी है।

## चरण 4: पाई चार्ट बनाएं

अब वास्तविक चार्ट बनाने का समय आ गया है। हम निर्दिष्ट करेंगे कि हमें पाई चार्ट चाहिए, और हम शीट पर इसकी स्थिति निर्धारित करेंगे।

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

विधि `Add()` चार्ट प्रकार के लिए पैरामीटर स्वीकार करता है (इस मामले में, `ChartType.Pie`), और वर्कशीट पर उसका स्थान। संख्याएँ पंक्ति और स्तंभ की स्थिति दर्शाती हैं।

## चरण 5: चार्ट का स्वरूप अनुकूलित करें

पाई चार्ट कुछ अनुकूलन के बिना पूरा नहीं होगा! आइए रंगों, लेबल और शीर्षक में बदलाव करके अपने चार्ट को देखने में आकर्षक बनाएं।

### चार्ट शीर्षक सेट करें
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### प्लॉट क्षेत्र को अनुकूलित करें
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

हम प्लॉट क्षेत्र के लिए ग्रेडिएंट भरण सेट करते हैं और साफ़ लुक के लिए बॉर्डर को छिपा देते हैं।

## चरण 6: चार्ट डेटा परिभाषित करें

अब समय आ गया है कि हम चार्ट को अपने डेटा से लिंक करें। `NSeries` चार्ट की यह संपत्ति बिक्री के आंकड़ों और क्षेत्रों को पाई चार्ट से बांधती है।

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

पहली पंक्ति यह निर्दिष्ट करती है कि हम सेल से बिक्री डेटा का उपयोग कर रहे हैं `B2:B8`. हम चार्ट को क्षेत्र के नामों का उपयोग करने के लिए भी कहते हैं `A2:A8` श्रेणी लेबल के रूप में.

## चरण 7: डेटा लेबल जोड़ें

चार्ट सेगमेंट में सीधे लेबल जोड़ने से इसे समझना आसान हो सकता है। आइए पाई चार्ट स्लाइस में क्षेत्र के नाम और बिक्री मूल्य शामिल करें।

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## चरण 8: चार्ट क्षेत्र और लेजेंड को अनुकूलित करें

अंत में, चार्ट क्षेत्र और लीजेंड को कुछ अंतिम रूप दें। इससे चार्ट की समग्र प्रस्तुति बेहतर हो जाती है।

### चार्ट क्षेत्र
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### दंतकथा
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## चरण 9: कार्यपुस्तिका सहेजें

अंत में, हम वर्कबुक को एक्सेल फ़ाइल में सेव करते हैं। आप आवश्यकतानुसार आउटपुट डायरेक्टरी और फ़ाइल नाम निर्दिष्ट कर सकते हैं।

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## निष्कर्ष

.NET के लिए Aspose.Cells के साथ पाई चार्ट बनाना एक सरल और अनुकूलन योग्य प्रक्रिया है। इस गाइड का पालन करके, आप एक पेशेवर दिखने वाला चार्ट बना सकते हैं जो कुछ ही चरणों में मूल्यवान जानकारी देता है। चाहे व्यावसायिक रिपोर्टिंग के लिए हो या शैक्षिक उद्देश्यों के लिए, चार्ट निर्माण में महारत हासिल करने से आपके एक्सेल ऑटोमेशन कौशल में वृद्धि होगी। याद रखें, Aspose.Cells आपको शानदार, डेटा-संचालित एक्सेल फ़ाइलें आसानी से बनाने के लिए आवश्यक लचीलापन प्रदान करता है।

## अक्सर पूछे जाने वाले प्रश्न

### क्या मैं .NET के लिए Aspose.Cells का उपयोग करके अन्य प्रकार के चार्ट बना सकता हूँ?
हाँ! Aspose.Cells विभिन्न चार्ट प्रकारों का समर्थन करता है, जिसमें बार चार्ट, लाइन चार्ट और स्कैटर प्लॉट शामिल हैं।

### क्या मुझे .NET के लिए Aspose.Cells का उपयोग करने के लिए सशुल्क लाइसेंस की आवश्यकता है?
आप कुछ सीमाओं के साथ मुफ़्त संस्करण का उपयोग कर सकते हैं। पूर्ण सुविधाओं के लिए, आपको लाइसेंस की आवश्यकता होगी, जिसे आप खरीद सकते हैं [यहाँ](https://purchase.aspose.com/buy).

### क्या मैं चार्ट को पीडीएफ या चित्र जैसे प्रारूपों में निर्यात कर सकता हूं?
बिल्कुल! Aspose.Cells आपको पीडीएफ और पीएनजी सहित विभिन्न प्रारूपों में चार्ट निर्यात करने की अनुमति देता है।

### क्या प्रत्येक पाई स्लाइस को अलग-अलग रंगों से सजाना संभव है?
हां, आप सेटिंग करके प्रत्येक स्लाइस पर अलग-अलग रंग लागू कर सकते हैं `IsColorVaried` संपत्ति को `true`जैसा कि ट्यूटोरियल में दिखाया गया है।

### क्या मैं एक ही कार्यपुस्तिका में एकाधिक चार्टों का निर्माण स्वचालित कर सकता हूँ?
हां, आप एक ही एक्सेल फ़ाइल में आवश्यकतानुसार कई चार्ट बना और अनुकूलित कर सकते हैं।

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}