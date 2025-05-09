---
"description": "Aspose.Cells for .NET을 사용하여 표시 형식을 사용자 지정하는 방법을 알아보세요. 이 단계별 가이드를 사용하여 날짜, 백분율 및 통화 형식을 지정해 보세요."
"linktitle": "사용자 정의 숫자로 표시 형식 사용자 지정"
"second_title": "Aspose.Cells .NET Excel 처리 API"
"title": "사용자 정의 숫자로 표시 형식 사용자 지정"
"url": "/ko/net/number-and-display-formats-in-excel/customizing-display-formats-with-user-defined-numbers/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 사용자 정의 숫자로 표시 형식 사용자 지정

## 소개
Excel 파일을 작업할 때 데이터를 더욱 의미 있고 사용자 친화적으로 표현하기 위해 셀 서식을 사용자 지정해야 하는 경우가 많습니다. 보고서용 Excel 파일을 만든다고 가정해 보겠습니다. 단순히 숫자만 있는 것이 아니라 날짜, 백분율, 통화까지 세련되고 전문적으로 표현하고 싶을 것입니다. 바로 이 부분에서 사용자 지정 표시 형식이 중요한 역할을 합니다. 이 튜토리얼에서는 Aspose.Cells for .NET을 자세히 살펴보고 사용자 정의 설정을 사용하여 숫자 표시 형식을 사용자 지정하는 방법을 보여줍니다.
## 필수 조건
시작하기 전에 이 튜토리얼을 따라 할 수 있는 모든 준비가 되어 있는지 확인하세요. 필요한 준비물은 다음과 같습니다.
- .NET용 Aspose.Cells가 설치되었습니다. [여기에서 다운로드하세요](https://releases.aspose.com/cells/net/).
- C# 및 .NET 프레임워크에 대한 기본 지식.
- Aspose.Cells에 대한 유효한 라이선스가 필요합니다. 라이선스가 없으면 [무료 체험](https://releases.aspose.com/) 또는 요청 [임시 면허](https://purchase.aspose.com/temporary-license/).
- Visual Studio와 같은 IDE.
- .NET Framework 4.0 이상.
혹시 빠진 것이 있다면 걱정하지 마세요. 언제든지 이 링크를 다시 방문하여 필요한 파일을 다운로드하거나 [Aspose 지원 포럼](https://forum.aspose.com/c/cells/9).
## 네임스페이스 가져오기
코드로 들어가기 전에 모든 필수 Aspose.Cells 기능에 액세스하는 데 필요한 네임스페이스를 가져와야 합니다.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
이 두 네임스페이스는 이 튜토리얼의 핵심 도구가 될 것입니다. 이제 재미있는 부분으로 넘어가 보겠습니다.
## 1단계: 프로젝트 디렉토리 설정
먼저, 파일을 저장할 공간이 필요하시죠? 출력된 Excel 파일을 저장할 디렉터리를 만들어 보겠습니다. 이 단계에서는 저장하기 전에 디렉터리가 존재하는지 확인합니다.
```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "Your Document Directory";
// 디렉토리가 없으면 새로 만듭니다.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- 우리는 정의하고 있습니다 `dataDir` 출력 Excel 파일이 저장될 경로를 저장하는 변수입니다.
- 그런 다음 다음을 사용하여 디렉토리가 존재하는지 확인합니다. `System.IO.Directory.Exists()`.
- 디렉토리가 존재하지 않으면 다음을 사용하여 생성됩니다. `System.IO.Directory.CreateDirectory()`.
## 2단계: 새 통합 문서 만들기 및 워크시트 추가
이제 디렉토리가 생겼으니 새로운 Excel 통합 문서를 만들고 여기에 워크시트를 추가해 보겠습니다.
```csharp
// Workbook 개체 인스턴스화
Workbook workbook = new Workbook();
// Excel 개체에 새 워크시트 추가
int i = workbook.Worksheets.Add();
// 새로 추가된 워크시트의 시트 인덱스를 전달하여 해당 워크시트의 참조를 얻습니다.
Worksheet worksheet = workbook.Worksheets[i];
```
- 첫째, 우리는 새로운 것을 만듭니다 `Workbook` 객체입니다. 이것을 Excel 파일이라고 생각해 보세요.
- 이 통합 문서에 새 워크시트를 추가합니다. `Add()` 메서드 및 변수에 인덱스를 저장합니다. `i`.
- 이 워크시트는 다음을 사용하여 참조합니다. `workbook.Worksheets[i]`.
## 3단계: 셀에 날짜 추가 및 형식 사용자 지정
이제 현재 날짜를 셀에 삽입하고 사용자 지정 방식으로 표시되도록 서식을 지정해 보겠습니다. 기본 날짜 형식 대신 다음과 같은 사용자 지정 형식을 설정합니다. `d-mmm-yy`.
```csharp
// "A1" 셀에 현재 시스템 날짜 추가
worksheet.Cells["A1"].PutValue(DateTime.Now);
// A1 셀의 스타일 얻기
Style style = worksheet.Cells["A1"].GetStyle();
// 사용자 지정 표시 형식을 "d-mmm-yy" 형식으로 날짜를 표시하도록 설정합니다.
style.Custom = "d-mmm-yy";
// A1 셀에 스타일 적용하기
worksheet.Cells["A1"].SetStyle(style);
```
- 현재 시스템 날짜를 셀에 추가합니다. `A1` 사용 중 `PutValue(DateTime.Now)`.
- 우리는 셀의 현재 스타일을 검색합니다 `A1` 사용 중 `GetStyle()`.
- 셀의 스타일을 설정하여 수정합니다. `style.Custom = "d-mmm-yy"`날짜를 일, 월, 연도를 약어로 표시해주는 형식입니다.
- 마지막으로 셀에 새 스타일을 적용합니다. `SetStyle()`.
## 4단계: 셀을 백분율로 서식 지정
다음으로 숫자를 다루어 보겠습니다. 다른 셀에 숫자 값을 추가합니다. `A2`, 백분율로 서식을 지정합니다.
```csharp
// "A2" 셀에 숫자 값 추가
worksheet.Cells["A2"].PutValue(20);
// A2 셀의 스타일 얻기
style = worksheet.Cells["A2"].GetStyle();
// 값을 백분율로 표시하도록 사용자 정의 표시 형식 설정
style.Custom = "0.0%";
// A2 셀에 스타일 적용하기
worksheet.Cells["A2"].SetStyle(style);
```
- 우리는 가치를 더합니다 `20` 세포로 `A2`.
- 셀의 스타일을 검색합니다 `A2` 그리고 사용자 정의 형식을 설정하세요 `0.0%` 값을 백분율(예: 20%)로 표시합니다.
- 마지막으로, 우리는 다음을 사용하여 셀에 스타일을 적용합니다. `SetStyle()`.
## 5단계: 셀을 통화로 서식 지정
셀에 다른 값을 추가해 보겠습니다. `A3`을 입력하고 통화로 표시되도록 형식을 지정합니다. 더 흥미롭게 만들기 위해 양수 값을 파운드로, 음수 값을 달러로 표시하는 형식을 사용하겠습니다.
```csharp
// "A3" 셀에 숫자 값 추가
worksheet.Cells["A3"].PutValue(2546);
// A3 셀 스타일 얻기
style = worksheet.Cells["A3"].GetStyle();
// 값을 통화로 표시하도록 사용자 지정 표시 형식 설정
style.Custom = "£#,##0;[Red]$-#,##0";
// A3 셀에 스타일 적용하기
worksheet.Cells["A3"].SetStyle(style);
```
- 우리는 가치를 더합니다 `2546` 세포로 `A3`.
- 사용자 정의 형식을 설정합니다 `£#,##0;[Red]$-#,##0`양수 값은 파운드 기호로 표시되고, 음수 값은 빨간색으로 표시되며 달러 기호가 표시됩니다.
- 우리는 셀에 스타일을 적용합니다. `SetStyle()`.
## 6단계: 통합 문서 저장
마지막 단계는 통합 문서를 Excel 파일로 저장하는 것입니다. 이 튜토리얼에서는 Excel 97-2003 형식을 사용합니다.
```csharp
// Excel 파일 저장
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
- 그만큼 `Save()` 이 방법은 지정된 디렉토리에 통합 문서를 저장합니다.
- 우리는 선택한다 `SaveFormat.Excel97To2003` 이전 버전의 Excel과의 호환성을 보장합니다.
## 결론
자, 이제 Excel 파일을 만들고 Aspose.Cells for .NET을 사용하여 특정 셀에 사용자 지정 날짜, 백분율, 통화 서식을 추가한 후 파일을 저장했습니다. 사용자 지정 서식을 사용하면 Excel 파일의 가독성과 전문성이 훨씬 향상됩니다. Aspose.Cells의 조건부 서식과 같은 다른 서식 옵션을 살펴보고 데이터 표시 방식을 더욱 세부적으로 제어해 보세요.
## 자주 묻는 질문
### Aspose.Cells에서 더 복잡한 서식 옵션을 어떻게 적용할 수 있나요?
글꼴 색상, 테두리, 배경색 등 다양한 서식 스타일을 사용자 정의 숫자 서식과 결합할 수 있습니다.
### 사용자 지정 숫자 서식을 셀 범위에 적용할 수 있나요?
예, Aspose.Cells를 사용하면 다음을 사용하여 셀 범위에 스타일을 적용할 수 있습니다. `Range.SetStyle()` 방법.
### 통합 문서를 어떤 다른 파일 형식으로 저장할 수 있나요?
Aspose.Cells는 XLSX, CSV, PDF 등 다양한 형식을 지원합니다. `SaveFormat` 에서 `Save()` 방법.
### 음수를 다른 형식으로 표현할 수 있나요?
물론입니다! 사용자 지정 숫자 서식을 사용하면 음수를 다양한 색상이나 기호로 표시할 수 있습니다.
### Aspose.Cells for .NET은 무료인가요?
Aspose.Cells는 무료 체험판을 제공하지만, 모든 기능을 사용하려면 유효한 라이선스가 필요합니다. [여기 임시 면허증](https://purchase.aspose.com/temporary-license/).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}