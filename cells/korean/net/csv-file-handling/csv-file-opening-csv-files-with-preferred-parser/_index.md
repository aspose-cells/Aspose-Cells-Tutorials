---
title: 선호하는 파서로 CSV 파일 열기
linktitle: 선호하는 파서로 CSV 파일 열기
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET에서 사용자 정의 파서로 CSV 파일을 열고 파싱하는 방법을 알아보세요. 텍스트와 날짜를 손쉽게 처리하세요. 개발자에게 완벽합니다.
weight: 11
url: /ko/net/csv-file-handling/csv-file-opening-csv-files-with-preferred-parser/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 선호하는 파서로 CSV 파일 열기

## 소개
CSV 파일을 다룰 때, 때로는 사용자 정의 파서로 다양한 데이터 유형을 처리하고 싶을 것입니다. 이 튜토리얼은 Aspose.Cells for .NET을 사용하여 선호하는 파서로 CSV 파일을 여는 방법을 안내합니다. 텍스트, 날짜 또는 기타 사용자 정의 형식을 처리하든, 이 가이드는 명확한 설명과 함께 각 단계를 안내합니다.
## 필수 조건
코드에 대해 알아보기 전에, 시작하는 데 필요한 필수 항목을 살펴보겠습니다.
1.  Aspose.Cells for .NET 라이브러리: Aspose.Cells 라이브러리가 설치되어 있는지 확인하세요. 다운로드할 수 있습니다.[여기](https://releases.aspose.com/cells/net/) . 무료 체험판을 이용할 수도 있습니다.[여기](https://releases.aspose.com/).
2. .NET 개발 환경: Visual Studio가 권장되지만, .NET과 호환되는 IDE라면 무엇이든 작동합니다.
3. C#에 대한 기본 지식: 이 튜토리얼에서는 독자가 C# 및 객체 지향 프로그래밍에 익숙하다고 가정합니다.
## 패키지 가져오기
Aspose.Cells를 사용하려면 C# 파일 맨 위에 필요한 네임스페이스를 가져와야 합니다.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
이제 준비가 되었으니, 선호하는 파서로 CSV 파일을 여는 방법을 살펴보겠습니다. 이 파서는 텍스트와 날짜 등 다양한 데이터 형식을 처리합니다.
## 1단계: 사용자 정의 파서 정의
 텍스트나 특정 날짜 형식과 같은 다양한 데이터 유형을 처리하려면 사용자 정의 파서를 정의해야 합니다. Aspose.Cells에서 사용자 정의 파서는 다음을 구현합니다.`ICustomParser` 인터페이스.
### 1.1 텍스트 파서 생성
이 파서는 일반 텍스트 값을 처리합니다. 형식을 수정하지 않으므로 값은 그대로 반환됩니다.
```csharp
class TextParser : ICustomParser
{
    public object ParseObject(string value)
    {
        return value;
    }
    public string GetFormat()
    {
        return "";
    }
}
```
 그만큼`ParseObject` 이 메서드는 단순히 입력 값을 반환합니다. "아무것도 변경하지 말고 텍스트만 주세요!"라고 말하는 것과 같습니다.
### 1.2 날짜 파서 생성
 날짜의 경우 CSV 데이터가 올바르게 구문 분석되었는지 확인해야 합니다.`DateTime` 객체. 날짜 파서를 만드는 방법은 다음과 같습니다.
```csharp
class DateParser : ICustomParser
{
    public object ParseObject(string value)
    {
        DateTime myDate = DateTime.ParseExact(value, "dd/MM/yyyy", 
            System.Globalization.CultureInfo.InvariantCulture);
        return myDate;
    }
    public string GetFormat()
    {
        return "dd/MM/yyyy";
    }
}
```
 이 파서에서는 다음을 사용합니다.`ParseExact` 미리 정의된 형식에 따라 날짜가 올바르게 해석되도록 보장합니다.`"dd/MM/yyyy"`). 이렇게 하면 이 형식을 따르는 CSV의 모든 날짜가 문제 없이 처리됩니다.
## 2단계: 로드 옵션 구성
 다음으로 CSV 파일을 로드하는 방법을 구성해야 합니다. 이는 다음을 사용하여 수행됩니다.`TxtLoadOptions` 인코딩 및 사용자 정의 파서를 포함한 파싱 옵션을 지정할 수 있는 클래스입니다.
### 2.1 로드 옵션 설정
 우리는 초기화로 시작할 것입니다`TxtLoadOptions` 구분 기호 및 인코딩과 같은 주요 매개변수 정의:
```csharp
TxtLoadOptions oTxtLoadOptions = new TxtLoadOptions(LoadFormat.Csv);
oTxtLoadOptions.Separator = Convert.ToChar(",");
oTxtLoadOptions.Encoding = Encoding.UTF8;
oTxtLoadOptions.ConvertDateTimeData = true;
```
- 구분 기호: 이는 CSV 파일에서 값을 구분하는 데 사용되는 문자를 정의합니다(이 경우 쉼표).
- 인코딩: 다양한 문자를 처리하기 위해 UTF-8 인코딩을 사용합니다.
-  ConvertDateTimeData: 이것을 true로 설정하면 날짜 값이 자동으로 변환됩니다.`DateTime` 가능하면 객체를 사용합니다.
### 2.2 사용자 정의 파서 적용
다음으로, 앞서 생성한 파서를 CSV의 값을 처리하도록 할당합니다.
```csharp
oTxtLoadOptions.PreferredParsers = new ICustomParser[] 
{ 
    new TextParser(), 
    new DateParser() 
};
```
 이것은 Aspose.Cells에 다음을 사용하도록 지시합니다.`TextParser` 일반 텍스트 값 및`DateParser`CSV 파일에서 발견되는 모든 날짜 필드에 대해.
## 3단계: CSV 파일 로드 및 읽기
 이제 로드 옵션이 구성되었으므로 CSV 파일을 로드할 수 있습니다.`Aspose.Cells.Workbook` 물체.
### 3.1 CSV 파일 로드
 파일 경로와 구성된 내용을 전달하여 CSV 파일을 로드합니다.`TxtLoadOptions` 에게`Workbook` 건설자:
```csharp
string sourceDir = "Your Document Directory";
Workbook oExcelWorkBook = new Aspose.Cells.Workbook(sourceDir + "samplePreferredParser.csv", oTxtLoadOptions);
```
이 단계에서는 CSV 데이터를 완벽한 기능을 갖춘 Excel 통합 문서로 변환하고, 각 값은 선호하는 규칙에 따라 구문 분석합니다.
## 4단계: 셀 데이터 액세스 및 표시
CSV가 통합 문서에 로드되면 데이터 작업을 시작할 수 있습니다. 예를 들어, 특정 셀의 유형과 값을 인쇄하고 싶을 수 있습니다.
### 4.1 셀 A1 검색 및 표시
첫 번째 셀(A1)을 검색하여 해당 값과 유형을 표시해 보겠습니다.
```csharp
Cell oCell = oExcelWorkBook.Worksheets[0].Cells["A1"];
Console.WriteLine("A1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
 여기서,`Type` 속성은 데이터 유형을 보여줍니다(예:`String` 또는`DateTime` ), 그리고`DisplayStringValue` 형식화된 값을 제공합니다.
### 4.2 셀 B1 검색 및 표시
마찬가지로 B1과 같은 다른 셀을 검색하여 표시할 수 있습니다.
```csharp
oCell = oExcelWorkBook.Worksheets[0].Cells["B1"];
Console.WriteLine("B1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
이 과정은 필요한 만큼의 셀에 대해 반복할 수 있습니다.
## 5단계: 통합 문서 저장
 데이터 작업을 마친 후에는 통합 문서를 새 파일에 저장하고 싶을 수 있습니다. Aspose.Cells는 간단한`Save` 방법:
```csharp
string outputDir = "Your Document Directory";
oExcelWorkBook.Save(outputDir + "outputsamplePreferredParser.xlsx");
```
이렇게 하면 통합 문서가 Excel 파일로 저장되고 모든 서식과 데이터 구문 분석이 그대로 유지됩니다.
## 결론
Aspose.Cells for .NET에서 선호하는 파서로 CSV 파일을 여는 것은 다양한 데이터 유형을 처리하는 유연하고 강력한 방법입니다. 사용자 정의 파서를 만들고 로드 옵션을 구성하면 텍스트, 날짜 또는 기타 사용자 정의 형식을 처리하든 CSV 파일이 필요한 대로 정확히 파싱되도록 할 수 있습니다. 이 튜토리얼을 통해 이제 프로젝트에서 더 복잡한 데이터 파싱 시나리오를 처리할 수 있게 되었습니다.
## 자주 묻는 질문
### .NET용 Aspose.Cells의 사용자 정의 파서의 목적은 무엇입니까?
사용자 정의 파서를 사용하면 CSV 파일을 로드할 때 텍스트나 날짜와 같은 특정 데이터 유형을 어떻게 파싱해야 하는지 정의할 수 있습니다.
### CSV 파일에서 다른 구분 문자를 사용할 수 있나요?
 예, 구분 기호로 원하는 문자를 지정할 수 있습니다.`TxtLoadOptions.Separator` 재산.
### CSV를 로드할 때 Aspose.Cells에서 인코딩을 어떻게 처리합니까?
 설정할 수 있습니다`Encoding` 의 속성`TxtLoadOptions` UTF-8, ASCII 등 모든 인코딩 방식에 적용 가능
### CSV의 날짜 형식이 다르면 어떻게 되나요?
사용자 정의 파서를 사용하여 특정 날짜 형식을 정의하고 날짜 값을 올바르게 구문 분석할 수 있습니다.
### 통합 문서를 다른 형식으로 저장할 수 있나요?
네, Aspose.Cells를 사용하면 XLSX, CSV, PDF 등 다양한 형식으로 통합 문서를 저장할 수 있습니다.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
