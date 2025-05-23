---
"description": "इस व्यापक चरण-दर-चरण मार्गदर्शिका के साथ .NET के लिए Aspose.Cells में चार्ट शीट के लिए पीडीएफ बुकमार्क बनाने का तरीका जानें।"
"linktitle": "Aspose.Cells में चार्ट शीट के लिए पीडीएफ बुकमार्क बनाएं"
"second_title": "Aspose.Cells .NET एक्सेल प्रोसेसिंग API"
"title": "Aspose.Cells में चार्ट शीट के लिए पीडीएफ बुकमार्क बनाएं"
"url": "/hi/net/rendering-and-export/create-pdf-bookmark-entry-for-chart-sheet/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells में चार्ट शीट के लिए पीडीएफ बुकमार्क बनाएं

## परिचय
Aspose.Cells for .NET डेवलपर्स को एक्सेल फाइलों को प्रोग्रामेटिक रूप से मैनिपुलेट करने की अनुमति देता है। इसकी एक उपयोगी विशेषता व्यक्तिगत चार्ट शीट के लिए पीडीएफ बुकमार्क बनाने की क्षमता है। यह ट्यूटोरियल आपको चरण दर चरण प्रक्रिया के माध्यम से ले जाएगा, जिससे आपके प्रोग्रामिंग अनुभव की परवाह किए बिना इसे अनुसरण करना आपके लिए आसान हो जाएगा। अपना कोड एडिटर लें, और चलिए शुरू करते हैं!
## आवश्यक शर्तें
आरंभ करने से पहले, आइए सुनिश्चित करें कि आपके पास अनुसरण करने के लिए आवश्यक सभी चीजें मौजूद हैं:
1. .NET के लिए Aspose.Cells: आपको Aspose.Cells लाइब्रेरी की आवश्यकता होगी। यदि आपके पास अभी तक यह नहीं है, तो आप इसे यहाँ से डाउनलोड कर सकते हैं [यहाँ](https://releases.aspose.com/cells/net/).
2. विजुअल स्टूडियो या कोई भी .NET IDE: आपको एक विकास वातावरण की आवश्यकता होगी जहां आप अपना C# कोड लिख और निष्पादित कर सकें।
3. C# की बुनियादी समझ: यद्यपि हम आपको प्रत्येक चरण में मार्गदर्शन करेंगे, लेकिन C# कोडिंग का बुनियादी ज्ञान आपके लिए उपयोगी होगा।
4. नमूना एक्सेल फ़ाइल: एक नमूना एक्सेल फ़ाइल प्राप्त करें जिसमें चार्ट शामिल हों। आप इसे स्वयं बना सकते हैं या इस अभ्यास के लिए नमूना फ़ाइल का उपयोग कर सकते हैं।
इन पूर्वावश्यकताओं को पूरा करने के बाद, आप आसानी से चार्ट शीट के लिए पीडीएफ बुकमार्क बनाने के लिए तैयार हैं!
## पैकेज आयात करें
अब जब हम सभी आवश्यक शर्तों के साथ तैयार हैं, तो चलिए कोड में कूदते हैं। एक्सेल फ़ाइलों में हेरफेर शुरू करने से पहले, आपको आवश्यक पैकेज आयात करने की आवश्यकता है। यहाँ बताया गया है कि आप इसे कैसे करते हैं:
### अपना विकास वातावरण सेटअप करें
1. नया प्रोजेक्ट बनाएँ: Visual Studio खोलें और एक नया C# कंसोल एप्लिकेशन बनाएँ। आइए इसे “AsposePDFBookmarkExample” कहते हैं।
2. Aspose.Cells संदर्भ जोड़ें: समाधान एक्सप्लोरर में अपने प्रोजेक्ट पर राइट-क्लिक करें, "Manage NuGet Packages" चुनें, और "Aspose.Cells" खोजें। नवीनतम संस्करण स्थापित करें।
3. उपयोग निर्देश जोड़ें:
आपके `Program.cs` फ़ाइल में, शीर्ष पर निम्नलिखित पंक्तियाँ जोड़ें:
```csharp
using System;
using System.Collections;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```
ये पैकेज आपको एक्सेल फाइलों के साथ काम करने और उन्हें बुकमार्क के साथ पीडीएफ में प्रस्तुत करने की अनुमति देते हैं।
आइए PDF बुकमार्क बनाने के लिए कोड को समझें। हम प्रत्येक भाग को चरण दर चरण समझेंगे।
## चरण 1: अपनी निर्देशिका पथ निर्धारित करें
अपने कोड को व्यवस्थित करने के लिए, आइए परिभाषित करें कि हमारी फ़ाइलें कहाँ स्थित हैं।
```csharp
string sourceDir = "Your Document Directory"; // उदाहरणार्थ, @"C:\Documents\"
string outputDir = "Your Document Directory"; // उदाहरणार्थ, @"C:\Documents\Output\"
```
प्रतिस्थापित करें `Your Document Directory` वास्तविक पथों के साथ जहां आपकी नमूना एक्सेल फ़ाइल संग्रहीत है और जहां आप आउटपुट पीडीएफ को सहेजना चाहते हैं।
## चरण 2: एक्सेल वर्कबुक लोड करें
इसके बाद, हमें उस एक्सेल वर्कबुक को लोड करना होगा जिसे आप संशोधित करना चाहते हैं।
```csharp
Workbook wb = new Workbook(sourceDir + "sampleCreatePdfBookmarkEntryForChartSheet.xlsx");
```
यहाँ हम इसका एक उदाहरण बनाते हैं `Workbook` क्लास में, हमारी नमूना एक्सेल फ़ाइल लोड हो रही है। सुनिश्चित करें कि फ़ाइल नाम आपकी वास्तविक फ़ाइल से मेल खाता है।
## चरण 3: वर्कशीट तक पहुंचें
एक बार कार्यपुस्तिका लोड हो जाने पर, आप इसके कार्यपत्रकों तक पहुँच सकते हैं। 
```csharp
Worksheet sheet1 = wb.Worksheets[0];
Worksheet sheet2 = wb.Worksheets[1];
Worksheet sheet3 = wb.Worksheets[2];
Worksheet sheet4 = wb.Worksheets[3];
```
कोड कार्यपुस्तिका में चार कार्यपत्रकों का संदर्भ देता है। सुनिश्चित करें कि आपकी एक्सेल फ़ाइल में कम से कम चार शीट हों।
## चरण 4: पीडीएफ बुकमार्क प्रविष्टियाँ बनाएँ
यहाँ जादू होता है! हम प्रत्येक शीट के लिए बुकमार्क प्रविष्टियाँ बनाएंगे।
```csharp
PdfBookmarkEntry ent1 = new PdfBookmarkEntry {
    Destination = sheet1.Cells["A1"],
    Text = "Bookmark-I"
};
PdfBookmarkEntry ent2 = new PdfBookmarkEntry {
    Destination = sheet2.Cells["A1"],
    Text = "Bookmark-II-Chart1"
};
PdfBookmarkEntry ent3 = new PdfBookmarkEntry {
    Destination = sheet3.Cells["A1"],
    Text = "Bookmark-III"
};
PdfBookmarkEntry ent4 = new PdfBookmarkEntry {
    Destination = sheet4.Cells["A1"],
    Text = "Bookmark-IV-Chart2"
};
```
प्रत्येक `PdfBookmarkEntry` ऑब्जेक्ट में एक गंतव्य सेल और एक टेक्स्ट लेबल है। यह सेटअप पीडीएफ में बुकमार्क बनाएगा जो एक्सेल शीट में क्षेत्रों के अनुरूप होगा।
## चरण 5: बुकमार्क प्रविष्टियों को व्यवस्थित करें
बुकमार्क्स की पदानुक्रमित संरचना बनाने के लिए, हमें उन्हें व्यवस्थित करने की आवश्यकता है।
```csharp
ArrayList lst = new ArrayList();
ent1.SubEntry = lst;
lst.Add(ent2);
lst.Add(ent3);
lst.Add(ent4);
```
यह कोड दूसरे, तीसरे और चौथे बुकमार्क को पहले बुकमार्क के अंतर्गत उप-प्रविष्टियों के रूप में जोड़ता है। अब, जब आप पीडीएफ में "बुकमार्क-I" पर क्लिक करेंगे, तो यह आपको अन्य बुकमार्क तक ले जाएगा।
## चरण 6: बुकमार्क प्रविष्टियों के साथ पीडीएफ सेव विकल्प बनाएं
अब, आइए अपने बुकमार्क के साथ पीडीएफ सेविंग विकल्प तैयार करें।
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
opts.Bookmark = ent1;
```
The `PdfSaveOptions` कॉन्फ़िगरेशन हमें पीडीएफ को सहेजते समय बुकमार्क शामिल करने की अनुमति देता है।
## चरण 7: आउटपुट पीडीएफ को सेव करें
अंततः, अब आपके कार्य को सहेजने का समय आ गया है!
```csharp
wb.Save(outputDir + "outputCreatePdfBookmarkEntryForChartSheet.pdf", opts);
```
यह कमांड कार्यपुस्तिका को निर्दिष्ट आउटपुट पथ पर एक पीडीएफ फाइल में आपके उपयोगी बुकमार्क्स के साथ सहेज देता है।
## चरण 8: निष्पादन की पुष्टि
अंत में, सब कुछ सुचारू रूप से हो गया, इसकी पुष्टि करने के लिए एक सफलता संदेश प्रिंट करें।
```csharp
Console.WriteLine("CreatePdfBookmarkEntryForChartSheet executed successfully.");
```
## निष्कर्ष 
.NET के लिए Aspose.Cells का उपयोग करके चार्ट शीट के लिए PDF बुकमार्क बनाना एक सरल प्रक्रिया है जो आपके Excel दस्तावेज़ों की उपयोगिता को बढ़ा सकती है। कोड की कुछ ही पंक्तियों के साथ, आप अपने PDF के माध्यम से आसानी से नेविगेट कर सकते हैं, मूल्यवान समय बचा सकते हैं और अपने वर्कफ़्लो में सुधार कर सकते हैं।
चाहे आप रिपोर्ट बना रहे हों या जटिल डेटासेट बनाए रख रहे हों, ये बुकमार्क जानकारी तक पहुँच को बहुत आसान बनाते हैं। तो आगे बढ़िए, अपने दस्तावेज़ों पर नियंत्रण रखें और उन्हें इस शानदार सुविधा से समृद्ध करें!
## अक्सर पूछे जाने वाले प्रश्न
### Aspose.Cells क्या है?
Aspose.Cells एक शक्तिशाली .NET लाइब्रेरी है जिसे एक्सेल फ़ाइल हेरफेर को संभालने के लिए डिज़ाइन किया गया है, जिसमें स्प्रेडशीट पढ़ना, लिखना और परिवर्तित करना शामिल है।
### क्या मैं केवल विशिष्ट कक्षों के लिए ही बुकमार्क बना सकता हूँ?
हां, आप बुकमार्क के लिए गंतव्य को अपनी वर्कशीट में किसी भी सेल के रूप में सेट कर सकते हैं।
### क्या मुझे Aspose.Cells का उपयोग करने के लिए लाइसेंस की आवश्यकता है?
जबकि Aspose.Cells निःशुल्क परीक्षण प्रदान करता है, उत्पादन उपयोग हेतु पूर्ण कार्यक्षमता के लिए सशुल्क लाइसेंस की आवश्यकता होती है।
### क्या मैं चार से अधिक शीटों के लिए बुकमार्क बना सकता हूँ?
बिल्कुल! आप कोड में समान संरचना का पालन करके जितनी चाहें उतनी शीट के लिए बुकमार्क बना सकते हैं।
### मुझे और अधिक सहायता कहां मिल सकती है?
आप इसकी जांच कर सकते हैं [Aspose समुदाय समर्थन मंच](https://forum.aspose.com/c/cells/9) किसी भी समस्या या प्रश्न के लिए.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}