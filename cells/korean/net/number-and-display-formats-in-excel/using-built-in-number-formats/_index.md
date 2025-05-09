---
"description": "Aspose.Cells for .NET을 사용하여 Excel에서 숫자 서식을 자동화합니다. 날짜, 백분율 및 통화 서식을 프로그래밍 방식으로 적용하는 방법을 알아봅니다."
"linktitle": "Excel에서 내장 숫자 형식을 프로그래밍 방식으로 사용하기"
"second_title": "Aspose.Cells .NET Excel 처리 API"
"title": "Excel에서 내장 숫자 형식을 프로그래밍 방식으로 사용하기"
"url": "/ko/net/number-and-display-formats-in-excel/using-built-in-number-formats/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 내장 숫자 형식을 프로그래밍 방식으로 사용하기

## 소개
이 튜토리얼에서는 Aspose.Cells for .NET을 사용하여 Excel에서 기본 숫자 서식을 사용하는 방법을 안내합니다. 환경 설정부터 날짜, 백분율, 통화 등 다양한 서식 적용까지 모든 것을 다룹니다. 숙련된 전문가든 .NET 생태계를 이제 막 경험해 본 초보자든, 이 가이드를 통해 Excel 셀 서식을 손쉽게 지정할 수 있습니다.
## 필수 조건
시작하기 전에 다음 사항이 있는지 확인하세요.
- Aspose.Cells for .NET 라이브러리가 설치되었습니다. [여기서 다운로드하세요](https://releases.aspose.com/cells/net/).
- C# 및 기본 .NET 프로그래밍에 대한 실무 지식.
- 컴퓨터에 Visual Studio나 .NET IDE가 설치되어 있어야 합니다.
- 유효한 Aspose 라이센스 또는 [임시 면허](https://purchase.aspose.com/temporary-license/).
- .NET framework가 설치되어 있어야 합니다(버전 4.0 이상).
  
위에 나열된 내용 중 누락된 것이 있다면, 제공된 링크를 따라 모든 것을 설정하세요. 준비되셨나요? 이제 재미있는 단계로 넘어가 볼까요!
## 패키지 가져오기
튜토리얼을 시작하기 전에 Aspose.Cells for .NET 작업에 필요한 네임스페이스를 가져와야 합니다.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
이것들을 가져오면 Excel 파일을 프로그래밍 방식으로 조작할 준비가 된 것입니다. 이제 단계별 가이드를 살펴보겠습니다!
## 1단계: Excel 통합 문서 만들기 또는 액세스
이 단계에서는 새 통합 문서를 만듭니다. 마치 새 Excel 파일을 여는 것처럼 생각하시면 됩니다. 단, 코드를 통해 작업해야 합니다!
```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "Your Document Directory";
// 디렉토리가 없으면 새로 만듭니다.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Workbook 개체 인스턴스화
Workbook workbook = new Workbook();
```
여기서 우리는 단순히 새로운 것을 인스턴스화하고 있습니다. `Workbook` 객체입니다. 이 객체는 데이터 조작이 가능한 Excel 파일 역할을 합니다. 경로를 제공하여 기존 파일을 로드할 수도 있습니다.
## 2단계: 워크시트에 액세스
Excel 통합 문서에는 여러 개의 워크시트가 포함될 수 있습니다. 이 단계에서는 통합 문서의 첫 번째 워크시트에 액세스합니다.
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
이제 통합 문서의 첫 번째 워크시트에 접근하고 있습니다. 추가 시트를 조작해야 하는 경우, 해당 시트의 색인이나 이름을 사용하여 참조할 수 있습니다.
## 3단계: 셀에 데이터 추가
특정 셀에 데이터를 추가해 보겠습니다. 먼저 현재 시스템 날짜를 "A1" 셀에 삽입합니다.
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
이 줄은 현재 날짜를 A1 셀에 삽입합니다. 멋지지 않나요? 수백 개의 셀에 대해 이렇게 직접 입력한다고 생각해 보세요. 정말 악몽일 겁니다. 이제 서식을 설정해 보겠습니다!
## 4단계: 셀 "A1"의 날짜 서식 지정
다음으로, 해당 날짜를 "2024년 10월 15일"처럼 더 읽기 쉬운 형식으로 지정해 보겠습니다. Aspose.Cells의 진가가 발휘되는 부분이 바로 여기입니다.
1. 셀의 스타일을 검색하세요:
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
여기서는 A1 셀의 스타일을 가져옵니다. 셀을 조정하기 전에 셀의 "스타일"을 가져오는 것이라고 생각하면 됩니다.
2. 날짜 형식 설정:
```csharp
style.Number = 15;
```
설정 `Number` 속성을 15로 설정하면 원하는 날짜 형식이 적용됩니다. 이는 날짜를 "d-mmm-yy" 형식으로 표시하기 위한 기본 제공 숫자 형식 코드입니다.
3. 셀에 스타일 적용:
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
이 줄은 셀에 스타일 변경 사항을 적용합니다. 이제 기본 날짜 형식 대신 "2024년 10월 15일"과 같이 훨씬 더 사용자 친화적인 형식이 표시됩니다.
## 5단계: 셀 "A2"에 백분율 추가 및 서식 지정
백분율 서식을 설정해 보겠습니다. 값을 삽입하고 백분율로 표시하려고 한다고 가정해 보겠습니다. 이 단계에서는 "A2" 셀에 숫자 값을 추가하고 백분율 서식을 지정합니다.
1. 숫자 값 삽입:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
이렇게 하면 A2 셀에 숫자 20이 삽입됩니다. "그냥 숫자일 뿐인데, 어떻게 백분율로 변환하지?"라고 생각하실 수도 있겠네요. 이제 그 부분을 살펴보겠습니다.
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
여기서는 A3 셀에 2546을 더합니다. 다음으로, 이 숫자를 통화로 표시되도록 서식을 지정하겠습니다.
2. 스타일 검색 및 통화 형식 설정:
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // 통화로 형식 지정
worksheet.Cells["A3"].SetStyle(style);
```
설정 `Number` 속성을 6으로 설정하면 통화 형식이 적용됩니다. 이제 A3 셀의 값은 쉼표와 소수점 이하 두 자리까지 포함된 "2,546.00"으로 표시됩니다.
## 7단계: Excel 파일 저장
이제 모든 서식 지정을 적용했으므로 파일을 저장할 차례입니다.
```csharp
// Excel 파일 저장
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
이 줄은 Excel 파일을 Excel 97-2003 형식으로 저장합니다. `SaveFormat` 필요에 맞게. 이렇게 하면 프로그래밍 방식으로 Excel 파일을 만들고 서식을 지정할 수 있습니다!
## 결론
축하합니다! Aspose.Cells for .NET을 사용하여 Excel 파일의 셀에 기본 숫자 서식을 적용하는 방법을 성공적으로 익혔습니다. 날짜부터 백분율, 통화까지 Excel 데이터 처리에 가장 자주 사용되는 서식 지정 방법을 살펴보았습니다. 이제 셀 서식을 직접 지정하는 대신 전체 프로세스를 자동화하여 시간을 절약하고 오류를 줄일 수 있습니다.
## 자주 묻는 질문
### Aspose.Cells for .NET을 사용하여 사용자 지정 숫자 형식을 적용할 수 있나요?
네! Aspose.Cells는 기본 제공 형식 외에도 사용자 지정 숫자 형식도 지원합니다. `Custom` 에 있는 재산 `Style` 수업.
### 셀을 특정 기호를 사용하여 통화로 서식을 지정하려면 어떻게 해야 하나요?
특정 통화 기호를 적용하려면 사용자 지정 서식을 설정하여 사용할 수 있습니다. `Style.Custom` 재산.
### 행이나 열 전체를 서식 지정할 수 있나요?
물론입니다! 다음을 사용하여 전체 행이나 열에 스타일을 적용할 수 있습니다. `Rows` 또는 `Columns` 컬렉션 `Worksheet` 물체.
### 여러 셀을 한 번에 서식 지정하려면 어떻게 해야 하나요?
당신은 사용할 수 있습니다 `Range` 여러 셀을 선택하고 모든 셀에 스타일을 한 번에 적용합니다.
### Aspose.Cells를 사용하려면 Microsoft Excel을 설치해야 합니까?
아니요, Aspose.Cells는 Microsoft Excel과 독립적으로 작동하므로 컴퓨터에 Excel을 설치할 필요가 없습니다.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}