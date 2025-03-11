---
title: कार्यपुस्तिका डिज़ाइनर के लिए ICellsDataTableDataSource का उपयोग करें
linktitle: कार्यपुस्तिका डिज़ाइनर के लिए ICellsDataTableDataSource का उपयोग करें
second_title: Aspose.Cells .NET एक्सेल प्रोसेसिंग API
description: एक्सेल शीट को गतिशील रूप से पॉप्युलेट करने के लिए .NET के लिए Aspose.Cells के साथ ICellsDataTableDataSource का उपयोग करना सीखें। कार्यपुस्तिकाओं में ग्राहक डेटा को स्वचालित करने के लिए बिल्कुल सही।
weight: 21
url: /hi/net/workbook-operations/use-icells-datatable-data-source/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# कार्यपुस्तिका डिज़ाइनर के लिए ICellsDataTableDataSource का उपयोग करें

## परिचय
 स्वचालित डेटा एकीकरण के साथ उन्नत स्प्रेडशीट बनाना एक गेम-चेंजर हो सकता है, खासकर व्यावसायिक अनुप्रयोगों में। इस ट्यूटोरियल में, हम इसका उपयोग करने के तरीके के बारे में जानेंगे`ICellsDataTableDataSource`Aspose.Cells for .NET में वर्कबुक डिज़ाइनर के लिए। हम आपको कस्टम डेटा को गतिशील रूप से Excel फ़ाइल में लोड करने के लिए एक सरल, मानव-पठनीय समाधान बनाने में मदद करेंगे। इसलिए, यदि आप ग्राहक सूचियों, बिक्री डेटा या इसी तरह की किसी भी चीज़ के साथ काम कर रहे हैं, तो यह गाइड आपके लिए है!
## आवश्यक शर्तें
आरंभ करने के लिए, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:
-  Aspose.Cells for .NET लाइब्रेरी – आप इसे यहाँ से डाउनलोड कर सकते हैं[यहाँ](https://releases.aspose.com/cells/net/) या निःशुल्क परीक्षण संस्करण प्राप्त करें.
- .NET डेवलपमेंट एनवायरनमेंट - विजुअल स्टूडियो एक बढ़िया विकल्प है।
- C# की बुनियादी समझ - क्लासेस और डेटा हैंडलिंग से परिचित होने से आपको आगे बढ़ने में मदद मिलेगी।
आगे बढ़ने से पहले, सुनिश्चित करें कि आपका विकास वातावरण आवश्यक पैकेजों के साथ स्थापित है।
## पैकेज आयात करें
Aspose.Cells को प्रभावी ढंग से उपयोग करने के लिए, आपको आवश्यक पैकेज आयात करने की आवश्यकता है। नीचे आवश्यक नामस्थानों के लिए एक त्वरित संदर्भ दिया गया है:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## चरण 1: ग्राहक डेटा वर्ग परिभाषित करें
 आरंभ करने के लिए, एक सरल बनाएं`Customer` वर्ग। इस वर्ग में बुनियादी ग्राहक विवरण जैसे`FullName` और`Address`इसे अपने डेटा के "आकार" को परिभाषित करने के तरीके के रूप में सोचें।
```csharp
public class Customer
{
    public Customer(string aFullName, string anAddress)
    {
        FullName = aFullName;
        Address = anAddress;
    }
    public string FullName { get; set; }
    public string Address { get; set; }
}
```
## चरण 2: ग्राहक सूची वर्ग सेट करें
 इसके बाद, एक परिभाषित करें`CustomerList` वह वर्ग जो विस्तृत होता है`ArrayList` . यह अनुकूलित सूची निम्नलिखित के उदाहरण रखेगी`Customer` और प्रत्येक प्रविष्टि तक अनुक्रमित पहुंच की अनुमति दें।
```csharp
public class CustomerList : ArrayList
{
    public new Customer this[int index]
    {
        get { return (Customer)base[index]; }
        set { base[index] = value; }
    }
}
```
इस चरण में, हम अपने डेटा को एक ऐसे प्रारूप में लपेट रहे हैं जिसे Aspose.Cells पहचान और संसाधित कर सकता है।
## चरण 3: ग्राहक डेटा स्रोत वर्ग बनाएँ
 यहाँ से चीजें दिलचस्प हो जाती हैं। हम एक बनाएंगे`CustomerDataSource` वर्ग कार्यान्वयन`ICellsDataTable` हमारे डेटा को Aspose.Cells के कार्यपुस्तिका डिजाइनर के साथ संगत बनाने के लिए।
```csharp
public class CustomerDataSource : ICellsDataTable
{
    internal string[] m_Columns;
    internal ICollection m_DataSource;
    private Hashtable m_PropHash;
    private IEnumerator m_IEnumerator;
    private PropertyInfo[] m_Properties;
    public CustomerDataSource(CustomerList customers)
    {
        this.m_DataSource = customers;
        this.m_Properties = customers[0].GetType().GetProperties();
        this.m_Columns = new string[this.m_Properties.Length];
        this.m_PropHash = new Hashtable(this.m_Properties.Length);
        for (int i = 0; i < m_Properties.Length; i++)
        {
            this.m_Columns[i] = m_Properties[i].Name;
            this.m_PropHash.Add(m_Properties[i].Name, m_Properties[i]);
        }
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public string[] Columns => this.m_Columns;
    public int Count => this.m_DataSource.Count;
    public void BeforeFirst()
    {
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public object this[int index] => this.m_Properties[index].GetValue(this.m_IEnumerator.Current, null);
    public object this[string columnName] => ((PropertyInfo)this.m_PropHash[columnName]).GetValue(this.m_IEnumerator.Current, null);
    public bool Next()
    {
        if (this.m_IEnumerator == null)
            return false;
        return this.m_IEnumerator.MoveNext();
    }
}
```
 यह प्रथा`CustomerDataSource` क्लास Aspose.Cells के लिए प्रत्येक की व्याख्या करना संभव बनाता है`Customer` एक्सेल फ़ाइल में एक पंक्ति के रूप में ऑब्जेक्ट बनाएँ।
## चरण 4: ग्राहक डेटा आरंभ करें
अब, आइए अपनी सूची में कुछ ग्राहकों को जोड़ें। यहाँ हम कार्यपुस्तिका में लिखे जाने वाले डेटा को लोड करते हैं। आवश्यकतानुसार और प्रविष्टियाँ जोड़ने के लिए स्वतंत्र महसूस करें।
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
इस उदाहरण में, हम एक छोटे डेटासेट के साथ काम कर रहे हैं। हालाँकि, आप डेटाबेस या अन्य स्रोतों से डेटा लोड करके आसानी से इस सूची का विस्तार कर सकते हैं।
## चरण 5: कार्यपुस्तिका लोड करें
अब, आइए एक मौजूदा एक्सेल वर्कबुक खोलें जिसमें आवश्यक स्मार्ट मार्कर शामिल हैं। यह वर्कबुक हमारे टेम्पलेट के रूप में काम करेगी, और Aspose.Cells गतिशील रूप से स्मार्ट मार्कर को ग्राहक डेटा से बदल देगा।
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
 यह सुनिश्चित करें कि`"SmartMarker1.xlsx"` जैसे प्लेसहोल्डर्स शामिल हैं`&=Customer.FullName` और`&=Customer.Address` जहां डेटा भरा जाना चाहिए.
## चरण 6: वर्कबुक डिज़ाइनर सेट करें
अब, आइए कार्यपुस्तिका डिज़ाइनर को हमारे ग्राहक डेटा स्रोत को कार्यपुस्तिका के स्मार्ट मार्करों से लिंक करने के लिए कॉन्फ़िगर करें।
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
`SetDataSource` विधि हमारे बांधता है`CustomerDataSource` कार्यपुस्तिका में स्मार्ट मार्करों के लिए। प्रत्येक मार्कर लेबल`&=Customer` एक्सेल में अब संबंधित ग्राहक डेटा द्वारा प्रतिस्थापित किया जाएगा।
## चरण 7: कार्यपुस्तिका को प्रोसेस करें और सेव करें
अंत में, आइए कार्यपुस्तिका में डेटा भरने और परिणामों को सहेजने की प्रक्रिया शुरू करें।
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
यह कोड स्मार्ट मार्कर प्रोसेसिंग को ट्रिगर करता है, सभी प्लेसहोल्डर्स को डेटा से बदल देता है, और परिणाम को इस रूप में सहेजता है`dest.xlsx`.
## निष्कर्ष
 बधाई हो! आपने सफलतापूर्वक कार्यान्वयन कर लिया है`ICellsDataTableDataSource` .NET के लिए Aspose.Cells का उपयोग करने वाले वर्कबुक डिज़ाइनर के लिए। यह दृष्टिकोण स्प्रेडशीट में डेटा पॉपुलेशन को स्वचालित करने के लिए आदर्श है, खासकर जब ग्राहक सूचियों या उत्पाद सूची जैसे गतिशील डेटा से निपटना हो। इन कौशलों के साथ, आप डेटा-संचालित एप्लिकेशन बनाने के अपने रास्ते पर हैं जो एक्सेल-आधारित रिपोर्टिंग को आसान बनाते हैं!
## अक्सर पूछे जाने वाले प्रश्न
###  क्या है`ICellsDataTable` in Aspose.Cells?  
यह एक इंटरफ़ेस है जो गतिशील डेटा जनसंख्या के लिए कस्टम डेटा स्रोतों को Aspose.Cells स्मार्ट मार्करों के साथ जोड़ने की अनुमति देता है।
### मैं कार्यपुस्तिका टेम्पलेट में डेटा को कैसे अनुकूलित कर सकता हूँ?  
 स्मार्ट मार्कर नामक प्लेसहोल्डर, जैसे`&=Customer.FullName`, का उपयोग किया जाता है। प्रसंस्करण के दौरान इन मार्करों को वास्तविक डेटा से बदल दिया जाता है।
### क्या .NET के लिए Aspose.Cells निःशुल्क है?  
 Aspose.Cells निःशुल्क परीक्षण प्रदान करता है, लेकिन पूर्ण पहुँच के लिए सशुल्क लाइसेंस की आवश्यकता होती है। उनकी जाँच करें[मुफ्त परीक्षण](https://releases.aspose.com/) या[खरीदना](https://purchase.aspose.com/buy) विकल्प.
### क्या मैं गतिशील रूप से अधिक ग्राहक डेटा जोड़ सकता हूँ?  
 बिलकुल! बस भरें`CustomerList`प्रोग्राम चलाने से पहले अतिरिक्त प्रविष्टियों के साथ।
### अगर मैं फंस जाऊं तो मुझे सहायता कहां से मिल सकती है?  
 Aspose के पास एक[सहयता मंच](https://forum.aspose.com/c/cells/9) जहां उपयोगकर्ता प्रश्न पूछ सकते हैं और समुदाय और Aspose टीम से सहायता प्राप्त कर सकते हैं।
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
