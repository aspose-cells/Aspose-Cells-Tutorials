---
title: Excel에서 내장 숫자 형식을 프로그래밍 방식으로 사용하기
linktitle: Excel에서 내장 숫자 형식을 프로그래밍 방식으로 사용하기
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET을 사용하여 Excel에서 숫자 서식을 자동화합니다. 날짜, 백분율 및 통화 서식을 프로그래밍 방식으로 적용하는 방법을 알아보세요.
weight: 10
url: /ko/net/number-and-display-formats-in-excel/using-built-in-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 내장 숫자 형식을 프로그래밍 방식으로 사용하기

## 소개
이 튜토리얼에서는 Aspose.Cells for .NET을 사용하여 Excel에서 기본 제공 숫자 서식을 사용하는 방법을 안내합니다. 환경 설정부터 날짜, 백분율, 통화와 같은 다양한 서식을 적용하는 것까지 모든 것을 다룹니다. 노련한 프로이든 .NET 생태계에 발을 들인 사람이든 이 가이드를 통해 Excel 셀을 아주 쉽게 서식 지정할 수 있습니다.
## 필수 조건
시작하기 전에 다음 사항이 있는지 확인하세요.
-  .NET 라이브러리용 Aspose.Cells가 설치되었습니다.[여기서 다운로드하세요](https://releases.aspose.com/cells/net/).
- C# 및 기본 .NET 프로그래밍에 대한 실무 지식이 있습니다.
- 컴퓨터에 Visual Studio나 .NET IDE가 설치되어 있어야 합니다.
-  유효한 Aspose 라이센스 또는[임시 면허](https://purchase.aspose.com/temporary-license/).
- .NET framework가 설치되었습니다(버전 4.0 이상).
  
위에 있는 것 중 하나라도 빠진 것이 있다면 제공된 링크를 따라 모든 것을 설정하세요. 준비되셨나요? 재밌는 부분으로 넘어가 볼까요!
## 패키지 가져오기
튜토리얼을 시작하기 전에 .NET용 Aspose.Cells 작업에 필요한 네임스페이스를 가져와야 합니다.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
이것들을 가져온 후에는 Excel 파일을 프로그래밍 방식으로 조작할 준비가 되었습니다. 이제 단계별 가이드로 들어가 봅시다!
## 1단계: Excel 통합 문서 만들기 또는 액세스
이 단계에서는 새 통합 문서를 만듭니다. 이것은 새 Excel 파일을 여는 것과 같지만, 코드를 통해 하는 것입니다!
```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "Your Document Directory";
// 디렉토리가 없으면 디렉토리를 생성합니다.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Workbook 개체 인스턴스화
Workbook workbook = new Workbook();
```
 여기서 우리는 단순히 새로운 것을 인스턴스화하고 있습니다.`Workbook` 객체. 이것은 데이터 조작을 위해 준비된 Excel 파일 역할을 합니다. 경로를 제공하여 기존 파일을 로드할 수도 있습니다.
## 2단계: 워크시트에 액세스
Excel 워크북에는 여러 워크시트가 포함될 수 있습니다. 이 단계에서는 워크북의 첫 번째 워크시트에 액세스합니다.
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
이제 워크북의 첫 번째 워크시트에 액세스하고 있습니다. 추가 시트를 조작해야 하는 경우 인덱스나 이름을 사용하여 참조할 수 있습니다.
## 3단계: 셀에 데이터 추가
특정 셀에 데이터를 추가해 보겠습니다. 먼저 현재 시스템 날짜를 셀 "A1"에 삽입합니다.
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
이 줄은 현재 날짜를 셀 A1에 삽입합니다. 꽤 멋지죠? 수백 개의 셀에 대해 이것을 수동으로 한다고 상상해보세요. 악몽이겠죠. 이제 서식 지정으로 넘어가겠습니다!
## 4단계: 셀 "A1"의 날짜 서식 지정
다음으로, 그 날짜를 "15-Oct-24"와 같이 더 읽기 쉬운 형식으로 포맷해 보겠습니다. 여기서 Aspose.Cells가 정말 빛을 발합니다.
1. 셀의 스타일 검색:
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
여기서 우리는 셀 A1의 스타일을 잡고 있습니다. 이것은 조정하기 전에 셀의 "패션"을 잡는 것으로 생각하세요.
2. 날짜 형식 설정:
```csharp
style.Number = 15;
```
 설정하기`Number` 속성을 15로 설정하면 원하는 날짜 형식이 적용됩니다. 이것은 날짜를 "d-mmm-yy" 형식으로 표시하기 위한 내장 숫자 형식 코드입니다.
3. 셀에 스타일 적용:
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
이 줄은 셀에 스타일 변경 사항을 적용합니다. 이제 기본 날짜 형식 대신 "15-Oct-24"와 같이 훨씬 더 사용자 친화적인 형식을 볼 수 있습니다.
## 5단계: 셀 "A2"에 백분율 추가 및 서식 지정
이제 백분율 서식 지정으로 넘어가겠습니다. 값을 삽입하여 백분율로 표시하고 싶다고 가정해 보겠습니다. 이 단계에서는 셀 "A2"에 숫자 값을 추가하고 백분율로 서식을 지정합니다.
1. 숫자 값 삽입:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
이렇게 하면 셀 A2에 숫자 20이 삽입됩니다. "그냥 평범한 숫자일 뿐인데, 어떻게 백분율로 바꿀 수 있을까?"라고 생각하실 수도 있습니다. 글쎄요, 이제 그 부분에 대해 알아보겠습니다.
2. 스타일 검색 및 백분율 형식 설정:
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // 백분율로 형식 지정
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
여기서는 셀 A3에 2546을 더합니다. 다음으로, 이 숫자를 통화로 표시되도록 포맷합니다.
2. 스타일 검색 및 통화 형식 설정:
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // 통화로 형식 지정
worksheet.Cells["A3"].SetStyle(style);
```
 설정하기`Number` 속성을 6으로 설정하면 통화 형식이 적용됩니다. 이제 셀 A3의 값은 쉼표와 소수점 두 자리까지 포함된 "2,546.00"으로 표시됩니다.
## 7단계: Excel 파일 저장
이제 모든 서식 지정을 적용했으니 파일을 저장할 시간입니다.
```csharp
// Excel 파일 저장하기
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
 이 줄은 Excel 파일을 Excel 97-2003 형식으로 저장합니다. 다음을 변경할 수 있습니다.`SaveFormat`귀하의 필요에 맞게. 그리고 그렇게 하면, 당신은 Excel 파일을 프로그래밍 방식으로 만들고 포맷했습니다!
## 결론
축하합니다! Aspose.Cells for .NET을 사용하여 Excel 파일의 셀에 기본 제공 숫자 서식을 적용하는 방법을 성공적으로 배웠습니다. 날짜부터 백분율과 통화까지 Excel 데이터 처리에 가장 일반적인 서식 지정 요구 사항 중 일부를 다루었습니다. 이제 셀을 수동으로 서식 지정하는 대신 전체 프로세스를 자동화하여 시간을 절약하고 오류를 줄일 수 있습니다.
## 자주 묻는 질문
### .NET용 Aspose.Cells를 사용하여 사용자 지정 숫자 서식을 적용할 수 있나요?
 네! 기본 제공 형식 외에도 Aspose.Cells는 사용자 지정 숫자 형식도 지원합니다. 다음을 사용하여 매우 구체적인 형식을 만들 수 있습니다.`Custom` 에 있는 재산`Style` 수업.
### 셀을 특정 기호를 사용하여 통화로 서식을 지정하려면 어떻게 해야 하나요?
 특정 통화 기호를 적용하려면 사용자 지정 서식을 설정하여 사용할 수 있습니다.`Style.Custom` 재산.
### 행이나 열 전체를 서식 지정할 수 있나요?
 물론입니다! 다음을 사용하여 전체 행이나 열에 스타일을 적용할 수 있습니다.`Rows` 또는`Columns`컬렉션에서`Worksheet` 물체.
### 한 번에 여러 셀의 서식을 지정하려면 어떻게 해야 하나요?
당신은 사용할 수 있습니다`Range` 여러 셀을 선택하여 스타일을 한 번에 적용합니다.
### Aspose.Cells를 사용하려면 Microsoft Excel을 설치해야 합니까?
아니요, Aspose.Cells는 Microsoft Excel과 독립적으로 작동하므로 컴퓨터에 Excel을 설치할 필요가 없습니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
