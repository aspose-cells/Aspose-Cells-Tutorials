---
"description": ".NET के लिए Aspose.Cells का उपयोग करके XLS और XLSX फ़ॉर्मेट द्वारा समर्थित अधिकतम पंक्तियों और स्तंभों की खोज करें। इस व्यापक ट्यूटोरियल के साथ अपने Excel डेटा प्रबंधन को अधिकतम करें।"
"linktitle": "XLS और XLSX प्रारूपों द्वारा समर्थित अधिकतम पंक्तियाँ और कॉलम खोजें"
"second_title": "Aspose.Cells .NET एक्सेल प्रोसेसिंग API"
"title": "XLS और XLSX प्रारूपों द्वारा समर्थित अधिकतम पंक्तियाँ और कॉलम खोजें"
"url": "/hi/net/workbook-settings/find-maximum-supported-rows-columns/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# XLS और XLSX प्रारूपों द्वारा समर्थित अधिकतम पंक्तियाँ और कॉलम खोजें

## परिचय
एक्सेल की दुनिया में, बड़े डेटासेट को मैनेज करना एक कठिन काम हो सकता है, खासकर जब अलग-अलग फ़ाइल फ़ॉर्मेट द्वारा समर्थित अधिकतम पंक्तियों और स्तंभों को संभालने की बात आती है। यह ट्यूटोरियल आपको .NET लाइब्रेरी के लिए Aspose.Cells का उपयोग करके XLS और XLSX फ़ॉर्मेट द्वारा समर्थित अधिकतम पंक्तियों और स्तंभों को खोजने की प्रक्रिया के माध्यम से मार्गदर्शन करेगा। इस लेख के अंत तक, आपको इस शक्तिशाली टूल का उपयोग करके अपने एक्सेल-संबंधित कार्यों को कुशलतापूर्वक संभालने के तरीके के बारे में व्यापक समझ होगी।
## आवश्यक शर्तें
इससे पहले कि हम ट्यूटोरियल में आगे बढ़ें, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:
1. [.NET फ्रेमवर्क](https://dotnet.microsoft.com/en-us/download) या [.NET कोर](https://dotnet.microsoft.com/en-us/download) आपके सिस्टम पर स्थापित है.
2. [.NET के लिए Aspose.Cells](https://releases.aspose.com/cells/net/) लाइब्रेरी को डाउनलोड करें और अपने प्रोजेक्ट में संदर्भित करें।
यदि आपने पहले से ऐसा नहीं किया है, तो आप .NET लाइब्रेरी के लिए Aspose.Cells डाउनलोड कर सकते हैं [वेबसाइट](https://releases.aspose.com/cells/net/) या इसे स्थापित करें [नुगेट](https://www.nuget.org/packages/Aspose.Cells/).
## पैकेज आयात करें
आरंभ करने के लिए, आपको Aspose.Cells for .NET लाइब्रेरी से आवश्यक पैकेज आयात करने होंगे। अपनी C# फ़ाइल के शीर्ष पर निम्नलिखित using कथन जोड़ें:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## चरण 1: XLS प्रारूप द्वारा समर्थित अधिकतम पंक्तियाँ और कॉलम ज्ञात करें
आइए XLS (एक्सेल 97-2003) प्रारूप द्वारा समर्थित अधिकतम पंक्तियों और स्तंभों की खोज से शुरुआत करें।
```csharp
// XLS प्रारूप के बारे में संदेश मुद्रित करें.
Console.WriteLine("Maximum Rows and Columns supported by XLS format.");
// XLS प्रारूप में कार्यपुस्तिका बनाएँ.
Workbook wb = new Workbook(FileFormatType.Excel97To2003);
// XLS प्रारूप द्वारा समर्थित अधिकतम पंक्तियों और स्तंभों को प्रिंट करें।
int maxRows = wb.Settings.MaxRow + 1;
int maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
Console.WriteLine();
```
इस चरण में, हम:
1. यह बताने के लिए एक संदेश प्रिंट करें कि हम XLS प्रारूप के साथ काम कर रहे हैं।
2. एक नया बनाएँ `Workbook` उदाहरण का उपयोग कर `FileFormatType.Excel97To2003` enum, जो XLS प्रारूप का प्रतिनिधित्व करता है.
3. XLS प्रारूप द्वारा समर्थित अधिकतम पंक्तियों और स्तंभों को पुनर्प्राप्त करें `Workbook.Settings.MaxRow` और `Workbook.Settings.MaxColumn` गुण, क्रमशः। हम वास्तविक अधिकतम पंक्ति और स्तंभ संख्या प्राप्त करने के लिए इन मानों में 1 जोड़ते हैं (क्योंकि वे शून्य-आधारित हैं)।
4. कंसोल पर अधिकतम पंक्तियाँ और कॉलम प्रिंट करें.
## चरण 2: XLSX प्रारूप द्वारा समर्थित अधिकतम पंक्तियाँ और कॉलम ज्ञात करें
आगे, आइए XLSX (एक्सेल 2007 और बाद के संस्करण) प्रारूप द्वारा समर्थित अधिकतम पंक्तियों और स्तंभों का पता लगाएं।
```csharp
// XLSX प्रारूप के बारे में संदेश मुद्रित करें।
Console.WriteLine("Maximum Rows and Columns supported by XLSX format.");
// XLSX प्रारूप में कार्यपुस्तिका बनाएँ.
wb = new Workbook(FileFormatType.Xlsx);
// XLSX प्रारूप द्वारा समर्थित अधिकतम पंक्तियों और स्तंभों को प्रिंट करें।
maxRows = wb.Settings.MaxRow + 1;
maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
```
इस चरण में, हम:
1. यह बताने के लिए एक संदेश प्रिंट करें कि हम XLSX प्रारूप के साथ काम कर रहे हैं।
2. एक नया बनाएँ `Workbook` उदाहरण का उपयोग कर `FileFormatType.Xlsx` enum, जो XLSX प्रारूप का प्रतिनिधित्व करता है।
3. XLSX प्रारूप द्वारा समर्थित अधिकतम पंक्तियों और स्तंभों को पुनर्प्राप्त करें `Workbook.Settings.MaxRow` और `Workbook.Settings.MaxColumn` गुण, क्रमशः। हम वास्तविक अधिकतम पंक्ति और स्तंभ संख्या प्राप्त करने के लिए इन मानों में 1 जोड़ते हैं (क्योंकि वे शून्य-आधारित हैं)।
4. कंसोल पर अधिकतम पंक्तियाँ और कॉलम प्रिंट करें.
## चरण 3: सफलता संदेश प्रदर्शित करें
अंत में, आइए एक सफलता संदेश प्रदर्शित करें जो यह इंगित करे कि "FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats" उदाहरण सफलतापूर्वक निष्पादित हो गया है।
```csharp
Console.WriteLine("FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats executed successfully.");
```
यह चरण केवल कंसोल पर एक सफलता संदेश प्रिंट करता है।
## निष्कर्ष
इस ट्यूटोरियल में, आपने सीखा है कि XLS और XLSX फ़ाइल फ़ॉर्मेट द्वारा समर्थित अधिकतम पंक्तियों और स्तंभों को खोजने के लिए Aspose.Cells for .NET लाइब्रेरी का उपयोग कैसे करें। इन फ़ॉर्मेट की सीमाओं को समझकर, आप अपने Excel-आधारित प्रोजेक्ट की बेहतर योजना बना सकते हैं और उन्हें प्रबंधित कर सकते हैं, यह सुनिश्चित करते हुए कि आपका डेटा समर्थित श्रेणियों के भीतर फिट बैठता है।
## अक्सर पूछे जाने वाले प्रश्न
### XLS प्रारूप द्वारा समर्थित पंक्तियों की अधिकतम संख्या कितनी है?
XLS (एक्सेल 97-2003) प्रारूप द्वारा समर्थित पंक्तियों की अधिकतम संख्या 65,536 है।
### XLS प्रारूप द्वारा समर्थित स्तंभों की अधिकतम संख्या कितनी है?
XLS (एक्सेल 97-2003) प्रारूप द्वारा समर्थित स्तंभों की अधिकतम संख्या 256 है।
### XLSX प्रारूप द्वारा समर्थित पंक्तियों की अधिकतम संख्या कितनी है?
XLSX (Excel 2007 और बाद के संस्करण) प्रारूप द्वारा समर्थित पंक्तियों की अधिकतम संख्या 1,048,576 है।
### XLSX प्रारूप द्वारा समर्थित स्तंभों की अधिकतम संख्या क्या है?
XLSX (एक्सेल 2007 और बाद के संस्करण) प्रारूप द्वारा समर्थित स्तंभों की अधिकतम संख्या 16,384 है।
### क्या मैं अन्य Excel फ़ाइल स्वरूपों के साथ काम करने के लिए Aspose.Cells for .NET लाइब्रेरी का उपयोग कर सकता हूँ?
हां, Aspose.Cells for .NET लाइब्रेरी एक्सेल फ़ाइल स्वरूपों की एक विस्तृत श्रृंखला का समर्थन करती है, जिसमें XLS, XLSX, ODS और बहुत कुछ शामिल है। आप एक्सप्लोर कर सकते हैं [प्रलेखन](https://reference.aspose.com/cells/net/) उपलब्ध सुविधाओं और कार्यात्मकताओं के बारे में जानने के लिए।


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}