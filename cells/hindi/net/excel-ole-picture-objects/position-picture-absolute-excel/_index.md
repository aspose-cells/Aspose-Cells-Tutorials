---
"description": "इस व्यापक चरण-दर-चरण ट्यूटोरियल के साथ .NET के लिए Aspose.Cells का उपयोग करके Excel में छवियों को पूर्णतः स्थानबद्ध करना सीखें।"
"linktitle": "एक्सेल में चित्र की स्थिति (पूर्ण)"
"second_title": "Aspose.Cells .NET एक्सेल प्रोसेसिंग API"
"title": "एक्सेल में चित्र की स्थिति (पूर्ण)"
"url": "/hi/net/excel-ole-picture-objects/position-picture-absolute-excel/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# एक्सेल में चित्र की स्थिति (पूर्ण)

## परिचय
क्या आपने कभी खुद को एक्सेल स्प्रेडशीट में छवियों को सही ढंग से रखने में संघर्ष करते हुए पाया है? आप अकेले नहीं हैं! कई उपयोगकर्ताओं को इस चुनौती का सामना करना पड़ता है, खासकर जब उनके डेटा विज़ुअलाइज़ेशन की ज़रूरतों को बेहतर सौंदर्यशास्त्र या स्पष्टता के लिए पूर्ण स्थिति की आवश्यकता होती है। खैर, आगे मत देखो; यह मार्गदर्शिका आपको .NET के लिए Aspose.Cells का उपयोग करके एक्सेल वर्कशीट में चित्रों को बिल्कुल सही स्थिति में रखने की सीधी प्रक्रिया से गुजारेगी। चाहे आप एक्सेल हेरफेर पर काम करने वाले डेवलपर हों या अपनी रिपोर्ट को बेहतर बनाने के लिए डेटा विश्लेषक, हमारा चरण-दर-चरण ट्यूटोरियल छवियों के साथ आपके एक्सेल अनुभवों को सरल बनाने के लिए यहाँ है!
## आवश्यक शर्तें
कोड और विवरण में जाने से पहले, कुछ चीजें हैं जो आपको तैयार रखनी होंगी:
1. Aspose.Cells लाइब्रेरी: सुनिश्चित करें कि आपके पास .NET लाइब्रेरी के लिए Aspose.Cells का नवीनतम संस्करण है। आप इसे यहाँ से डाउनलोड कर सकते हैं [विज्ञप्ति पृष्ठ](https://releases.aspose.com/cells/net/).
2. विकास पर्यावरण: सुनिश्चित करें कि आपके पास एक कार्यशील .NET विकास पर्यावरण सेटअप है। आप Visual Studio या अपनी पसंद का कोई अन्य IDE उपयोग कर सकते हैं।
3. C# का बुनियादी ज्ञान: कोड स्निपेट को समझने के लिए C# प्रोग्रामिंग भाषा से परिचित होना लाभदायक होगा।
4. छवि फ़ाइल: अपनी निर्दिष्ट दस्तावेज़ निर्देशिका में एक छवि फ़ाइल (जैसे, “logo.jpg”) सहेजें जिसे आप अपनी एक्सेल शीट में सम्मिलित करने की योजना बना रहे हैं।

## पैकेज आयात करें
आरंभ करने के लिए, आइए सुनिश्चित करें कि हम अपने प्रोजेक्ट के लिए आवश्यक पैकेज आयात करें। आपकी प्रोजेक्ट फ़ाइल में निम्नलिखित नामस्थान शामिल होने चाहिए:
```csharp
using System.IO;
using Aspose.Cells;
```
इन नामस्थानों को आयात करके, हम सुनिश्चित करते हैं कि हमारा प्रोग्राम Aspose.Cells द्वारा प्रदान की गई सुविधाओं का लाभ उठा सके।
स्पष्टता के लिए आइए इसे प्रबंधनीय चरणों में विभाजित करें।
## चरण 1: अपनी दस्तावेज़ निर्देशिका सेट करें
इस प्रारंभिक चरण में, आपको वह निर्देशिका निर्धारित करनी होगी जहाँ आपके दस्तावेज़ स्थित हैं। यह प्रोग्राम के लिए यह जानना आवश्यक है कि फ़ाइलों को कहाँ सहेजना या प्राप्त करना है। यहाँ बताया गया है कि आप इसे कैसे सेट कर सकते हैं:
```csharp
string dataDir = "Your Document Directory";
```
बस प्रतिस्थापित करें `"Your Document Directory"` वास्तविक पथ के साथ जहाँ आपकी छवि फ़ाइल स्थित है। यह कुछ इस तरह हो सकता है `"C:\\Users\\YourUsername\\Documents\\"`.
## चरण 2: वर्कबुक ऑब्जेक्ट को इंस्टैंशिएट करना
इसके बाद, आपको एक नया उदाहरण बनाना होगा `Workbook` क्लास. यह ऑब्जेक्ट आपकी एक्सेल फ़ाइल का प्रतिनिधित्व करता है:
```csharp
Workbook workbook = new Workbook();
```
इस बिंदु पर, आपके पास डेटा और छवियों से भरने के लिए एक कार्यपुस्तिका तैयार है।
## चरण 3: नई वर्कशीट जोड़ना
अब जब आपके पास वर्कबुक है, तो आपको इसमें एक वर्कशीट जोड़ने की ज़रूरत है। यहीं पर छवियों को जोड़ने और उनकी स्थिति निर्धारित करने का जादू होगा:
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
यह पंक्ति आपकी कार्यपुस्तिका में एक नई कार्यपत्रिका बनाती है और उसका सूचकांक लौटाती है, जिसे हम चर में संग्रहीत करते हैं `sheetIndex`.
## चरण 4: नई वर्कशीट प्राप्त करना
आइए नई बनाई गई वर्कशीट को संदर्भित करें। हमें अभी जो इंडेक्स मिला है, उसका उपयोग करके हम वर्कशीट तक पहुँच सकते हैं और उसमें बदलाव कर सकते हैं:
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
अब आप इसके साथ काम कर सकते हैं `worksheet` छवियों सहित सामग्री जोड़ने पर आपत्ति।
## चरण 5: चित्र जोड़ना
अब रोमांचक भाग के लिए! यहाँ हम अपनी वर्कशीट में चित्र जोड़ते हैं। हम पंक्ति और स्तंभ सूचकांक निर्दिष्ट करते हैं जहाँ हम चित्र को एंकर करना चाहते हैं (इस मामले में, सेल "F6" पर, जो पंक्ति 5 और स्तंभ 5 है):
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
यह रेखा प्रभावी रूप से संपूर्ण वर्कशीट के सापेक्ष निर्दिष्ट स्थान पर छवि को लॉक कर देती है। हालाँकि, अभी, यह अभी भी कोशिकाओं के साथ आकार बदलने के अधीन है।
## चरण 6: नए जोड़े गए चित्र तक पहुँचना
चित्र में और अधिक परिवर्तन करने के लिए, आपको इसके गुणों तक पहुँचना होगा:
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
इसके साथ, आप उस छवि के गुणों तक पहुंच प्राप्त करेंगे जिसे हमने अभी जोड़ा है!
## चरण 7: चित्र के लिए पूर्ण स्थिति निर्धारित करना
चित्र को पूर्णतः (पिक्सल में) स्थान देने के लिए, आपको इसका उपयोग करके इसकी स्थिति निर्धारित करनी होगी। `Left` और `Top` गुण। यहाँ पर आपको यह नियंत्रण मिलेगा कि छवि कहाँ दिखाई देगी:
```csharp
picture.Left = 60;
picture.Top = 10;
```
आप दोनों मानों को आवश्यकतानुसार समायोजित कर सकते हैं; वे क्रमशः छवि की क्षैतिज और ऊर्ध्वाधर स्थिति को दर्शाते हैं।
## चरण 8: एक्सेल फ़ाइल को सेव करना
अंत में, अपने सभी संशोधन करने के बाद, कार्यपुस्तिका को सहेजने का समय आ गया है:
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
इससे एक एक्सेल फ़ाइल बनेगी जिसका नाम होगा `book1.out.xls` आपके पहले से परिभाषित दस्तावेज़ निर्देशिका में, जिसमें आपकी वर्कशीट शामिल है, जिसमें चित्र बिल्कुल रखा गया है।

## निष्कर्ष
और अब आपका काम हो गया! आपने .NET के लिए Aspose.Cells का उपयोग करके एक्सेल शीट में एक तस्वीर को सफलतापूर्वक पूर्ण स्थिति में रखा है। यह सरल प्रक्रिया न केवल आपके एक्सेल दस्तावेज़ों की दृश्य प्रस्तुति को बढ़ाती है, बल्कि यह भी सुनिश्चित करती है कि छवियाँ ठीक उसी स्थान पर रहें जहाँ आप उन्हें चाहते हैं - सेल आकार और पंक्ति ऊँचाई में किए गए किसी भी बदलाव के बावजूद। अब, चाहे आप कोई रिपोर्ट तैयार कर रहे हों या डैशबोर्ड बना रहे हों, आप सुनिश्चित कर सकते हैं कि आपकी तस्वीरें हर बार बिल्कुल सही तरीके से रखी जाएँ।
## अक्सर पूछे जाने वाले प्रश्न
### .NET के लिए Aspose.Cells क्या है?
Aspose.Cells for .NET एक .NET लाइब्रेरी है जो डेवलपर्स को Microsoft Excel की आवश्यकता के बिना प्रोग्रामेटिक रूप से Excel स्प्रेडशीट बनाने, हेरफेर करने और परिवर्तित करने में सक्षम बनाती है।
### क्या मैं Aspose.Cells का उपयोग करके अन्य छवि हेरफेर कर सकता हूं?
हां, स्थिति निर्धारण के अलावा, आप Aspose.Cells लाइब्रेरी का उपयोग करके एक्सेल स्प्रेडशीट में छवियों का आकार बदल सकते हैं, घुमा सकते हैं और संशोधित भी कर सकते हैं।
### क्या Aspose.Cells का उपयोग निःशुल्क है?
Aspose.Cells एक वाणिज्यिक उत्पाद है, लेकिन आप उनके पास उपलब्ध निःशुल्क परीक्षण के साथ शुरुआत कर सकते हैं [निःशुल्क परीक्षण पृष्ठ](https://releases.aspose.com/).
### मैं Aspose.Cells के लिए अस्थायी लाइसेंस कैसे प्राप्त करूं?
आप अस्थायी लाइसेंस के लिए आवेदन कर सकते हैं [अस्थायी लाइसेंस पृष्ठ](https://purchase.aspose.com/temporary-license/) Aspose द्वारा प्रदान किया गया.
### मैं और अधिक उदाहरण और दस्तावेज कहां पा सकता हूं?
The [Aspose.Cells दस्तावेज़ीकरण](https://reference.aspose.com/cells/net/) इसमें व्यापक संसाधन शामिल हैं, जिनमें कोड उदाहरण और अधिक विस्तृत विशेषताएं शामिल हैं।

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}