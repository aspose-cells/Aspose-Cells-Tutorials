---
title: Excel में डेटाटेबल पंक्तियाँ सम्मिलित करते समय पहली पंक्ति को नीचे खिसकाएँ
linktitle: Excel में डेटाटेबल पंक्तियाँ सम्मिलित करते समय पहली पंक्ति को नीचे खिसकाएँ
second_title: Aspose.Cells .NET एक्सेल प्रोसेसिंग API
description: .NET के लिए Aspose.Cells का उपयोग करके Excel में DataTable पंक्तियाँ सम्मिलित करना सीखें, बिना पहली पंक्ति को नीचे खिसकाए। सरल स्वचालन के लिए चरण-दर-चरण मार्गदर्शिका।
weight: 11
url: /hi/net/excel-data-import-export/shift-first-row-down-when-inserting-cells-datatable-rows-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel में डेटाटेबल पंक्तियाँ सम्मिलित करते समय पहली पंक्ति को नीचे खिसकाएँ

## परिचय

क्या आप अपने एक्सेल स्प्रेडशीट में नया डेटा डालते समय मैन्युअल रूप से पंक्तियों को शिफ्ट करने से थक गए हैं? खैर, आप भाग्यशाली हैं! इस लेख में, हम .NET के लिए Aspose.Cells का उपयोग करके इस प्रक्रिया को स्वचालित करने के तरीके के बारे में जानेंगे। इस ट्यूटोरियल के अंत तक, आप न केवल एक्सेल में डेटा टेबल के साथ काम करना सीखेंगे, बल्कि अपनी ज़रूरतों के हिसाब से आयात विकल्पों को कस्टमाइज़ करना भी सीखेंगे। मेरा विश्वास करें; इससे आपका बहुत समय और परेशानी बच सकती है! तो, एक कप कॉफ़ी लें और चलिए शुरू करते हैं!

## आवश्यक शर्तें

इससे पहले कि हम कोडिंग शुरू करें, आइए सुनिश्चित करें कि आपने सब कुछ सेट कर लिया है:

1. विज़ुअल स्टूडियो: सुनिश्चित करें कि आपके पास विज़ुअल स्टूडियो स्थापित है (2017 या बाद का संस्करण ठीक काम करेगा)।
2.  .NET के लिए Aspose.Cells: आपके पास Aspose.Cells लाइब्रेरी होनी चाहिए। अगर आपने अभी तक ऐसा नहीं किया है, तो आप इसे डाउनलोड कर सकते हैं[यहाँ](https://releases.aspose.com/cells/net/).
3. C# और Excel की बुनियादी समझ: C# प्रोग्रामिंग और Excel कैसे काम करता है, इसकी बुनियादी समझ निश्चित रूप से आपको अधिक प्रभावी ढंग से अनुसरण करने में मदद करेगी।

 आप एक नमूना एक्सेल फ़ाइल भी अपने पास रखना चाहेंगे। इस गाइड में, हम एक नमूना का उपयोग करेंगे जिसे कहा जाता है`sampleImportTableOptionsShiftFirstRowDown.xlsx`आप यह फ़ाइल बना सकते हैं या अपनी आवश्यकताओं के अनुरूप एक टेम्पलेट पा सकते हैं।

## पैकेज आयात करें

कोडिंग में उतरने से पहले, हमें यह सुनिश्चित करना होगा कि हम आवश्यक पैकेज आयात कर लें। अपने C# प्रोजेक्ट में, निम्नलिखित नेमस्पेस शामिल करें:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

ये पैकेज कार्यपुस्तिका, कार्यपत्रक और तालिकाओं के साथ काम करने के लिए आवश्यक हैं।

## चरण 1: अपना प्रोजेक्ट सेट करें

### एक नया C# प्रोजेक्ट बनाएं

Visual Studio में एक नया C# कंसोल एप्लिकेशन बनाकर शुरुआत करें। अपने प्रोजेक्ट को एक उपयुक्त नाम दें, जैसे “ExcelDataImport”.

### Aspose.Cells NuGet पैकेज जोड़ें

Aspose.Cells पैकेज जोड़ने के लिए, सॉल्यूशन एक्सप्लोरर में अपने प्रोजेक्ट पर राइट-क्लिक करें, मैनेज नुगेट पैकेज चुनें, और “Aspose.Cells” खोजें। यह सुनिश्चित करने के लिए पैकेज इंस्टॉल करें कि आप हमारी ज़रूरत की सभी कार्यक्षमता तक पहुँच सकते हैं।

## चरण 2: डेटा तालिका परिभाषित करें

 इसके बाद, हम इसे लागू करेंगे`ICellsDataTable` एक क्लास बनाने के लिए इंटरफ़ेस जो आयात किए जाने वाले डेटा को प्रदान करता है। यहाँ बताया गया है कि आप कैसे संरचना कर सकते हैं`CellsDataTable` कक्षा:

```csharp
class CellsDataTable : ICellsDataTable
{
    int m_index = -1;
    static String[] colsNames = new String[] { "Pet", "Fruit", "Country", "Color" };
    static String[] col0data = new String[] { "Dog", "Cat", "Duck" };
    static String[] col1data = new String[] { "Apple", "Pear", "Banana" };
    static String[] col2data = new String[] { "UK", "USA", "China" };
    static String[] col3data = new String[] { "Red", "Green", "Blue" };
    static String[][] colsData = new String[][] { col0data, col1data, col2data, col3data };
    
    // ... अन्य सदस्यों को लागू करें ...
}
```

यहां, हम प्रत्येक कॉलम के लिए कॉलम नाम और डेटा परिभाषित कर रहे हैं, जो हमारी आयातित तालिका की संरचना को सुविधाजनक बनाएगा।

## चरण 3: ICellsDataTable इंटरफ़ेस सदस्यों को लागू करें

 के अंदर`CellsDataTable` वर्ग, आपको के सदस्यों को लागू करने की आवश्यकता है`ICellsDataTable` इंटरफ़ेस. यहाँ आवश्यक कार्यान्वयन है:

```csharp
public object this[string columnName]
{
    get
    {
        throw new NotImplementedException();
    }
}

object ICellsDataTable.this[int columnIndex]
{
    get
    {
        return colsData[columnIndex][m_index];
    }
}

string[] ICellsDataTable.Columns
{
    get { return colsNames; }
}

int ICellsDataTable.Count
{
    get { return col0data.Length; }
}

void ICellsDataTable.BeforeFirst()
{
    m_index = -1;
}

bool ICellsDataTable.Next()
{
    m_index++;
    return (m_index < Count);
}
```

क्लास का यह भाग डेटा पुनर्प्राप्ति को संभालता है, यह परिभाषित करता है कि कितनी पंक्तियाँ और कॉलम हैं, और वर्तमान सूचकांक स्थिति का प्रबंधन करता है।

## चरण 4: मुख्य फ़ंक्शन लिखें

 अब, चलिए बनाते हैं`Run`संपूर्ण तालिका आयात प्रक्रिया को व्यवस्थित करने की विधि:

```csharp
public static void Run()
{
    string sourceDir = "Your Document Directory\\";
    string outputDir = "Your Document Directory\\";
    
    CellsDataTable cellsDataTable = new CellsDataTable();
    Workbook wb = new Workbook(sourceDir + "sampleImportTableOptionsShiftFirstRowDown.xlsx");
    Worksheet ws = wb.Worksheets[0];
```

## चरण 5: आयात विकल्प सेट करें

 आयात व्यवहार को नियंत्रित करने के लिए, आपको इसका एक उदाहरण बनाना चाहिए`ImportTableOptions` और उसके अनुसार गुण सेट करें। विशेष रूप से, हम सेट करना चाहते हैं`ShiftFirstRowDown` को`false`.

```csharp
    ImportTableOptions opts = new ImportTableOptions();
    opts.ShiftFirstRowDown = false; // हम पहली पंक्ति को नीचे नहीं ले जाना चाहते
```

## चरण 6: डेटाटेबल आयात करें

 अब हम अपने यहां से डेटा आयात कर सकते हैं`CellsDataTable` कार्यपत्रक में.

```csharp
    ws.Cells.ImportData(cellsDataTable, 2, 2, opts);
}
```

यह कमांड सीधे आपकी डेटा तालिका को निर्दिष्ट पंक्ति और कॉलम से प्रारंभ करके सम्मिलित कर देगा।

## चरण 7: कार्यपुस्तिका सहेजें

अंत में, हम संशोधित कार्यपुस्तिका को वापस एक फ़ाइल में सहेज लेंगे:

```csharp
    wb.Save(outputDir + "outputImportTableOptionsShiftFirstRowDown-False.xlsx");
}
```

## निष्कर्ष

और अब आप समझ गए होंगे! आपने सीखा है कि .NET के लिए Aspose.Cells का उपयोग करके पहली पंक्ति को स्थानांतरित किए बिना Excel शीट में DataTable पंक्तियाँ कैसे डालें। यह प्रक्रिया न केवल Excel के भीतर डेटा हेरफेर को सुव्यवस्थित करती है, बल्कि एक आम तौर पर बोझिल कार्य को स्वचालित करके आपके एप्लिकेशन के प्रदर्शन को भी बढ़ाती है। अपने टूलकिट में इस ज्ञान के साथ, आप Excel स्वचालन कार्यों को संभालने के लिए बेहतर ढंग से सुसज्जित हैं, जिससे आपका समय और प्रयास बचता है।

## अक्सर पूछे जाने वाले प्रश्न

### .NET के लिए Aspose.Cells क्या है?
Aspose.Cells for .NET एक प्रोग्रामिंग लाइब्रेरी है जो डेवलपर्स को .NET अनुप्रयोगों में Excel फ़ाइलों को बनाने, हेरफेर करने और परिवर्तित करने की अनुमति देती है।

### क्या मुझे Aspose.Cells का उपयोग करने के लिए लाइसेंस की आवश्यकता है?
हां, आपको पूर्ण सुविधाओं के लिए वैध लाइसेंस की आवश्यकता होगी। हालांकि, प्रारंभिक परीक्षण के लिए एक निःशुल्क परीक्षण उपलब्ध है।

### क्या मैं वेब अनुप्रयोगों में Aspose.Cells का उपयोग कर सकता हूँ?
बिल्कुल! Aspose.Cells .NET में विकसित डेस्कटॉप, वेब और क्लाउड-आधारित अनुप्रयोगों के लिए एकदम सही है।

### मैं Aspose.Cells के साथ किस प्रकार की Excel फ़ाइलें बना सकता हूँ?
आप XLSX, XLS, CSV आदि सहित विभिन्न प्रकार के एक्सेल फ़ाइल स्वरूप बना सकते हैं।

### मुझे Aspose.Cells के लिए समर्थन कहां मिल सकता है?
 आप प्रश्न पूछ सकते हैं या सहायता पा सकते हैं[Aspose फ़ोरम](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
