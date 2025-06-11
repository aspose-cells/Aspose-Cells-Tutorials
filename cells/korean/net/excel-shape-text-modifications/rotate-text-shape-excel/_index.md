---
"description": "Aspose.Cells for .NET을 사용하여 Excel에서 도형과 텍스트를 회전하는 방법을 알아보세요. 완벽한 Excel 프레젠테이션을 위한 단계별 가이드를 따라해 보세요."
"linktitle": "Excel에서 도형으로 텍스트 회전"
"second_title": "Aspose.Cells .NET Excel 처리 API"
"title": "Excel에서 도형으로 텍스트 회전"
"url": "/ko/net/excel-shape-text-modifications/rotate-text-shape-excel/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 도형으로 텍스트 회전

## 소개
Excel 세계에서 시각적 표현은 데이터 자체만큼이나 중요합니다. 보고서를 작성하든 동적 대시보드를 디자인하든, 정보의 배치 방식은 가독성과 전반적인 디자인에 큰 영향을 미칠 수 있습니다. 텍스트를 회전하여 도형에 맞춰 세련되게 정렬하고 싶었던 적이 있으신가요? 행운입니다! 이 튜토리얼에서는 Aspose.Cells for .NET을 사용하여 텍스트를 도형에 맞춰 회전하는 방법을 자세히 살펴보겠습니다. 스프레드시트에 정보를 전달할 뿐만 아니라 인상적인 효과를 더할 수 있습니다.
## 필수 조건
시작하기에 앞서, 필요한 모든 것이 있는지 확인해 보겠습니다.
1. Visual Studio: 코드를 작성할 컴퓨터에 Visual Studio가 설치되어 있는지 확인하세요.
2. Aspose.Cells for .NET: Aspose.Cells 라이브러리가 필요합니다. [최신 버전을 여기에서 다운로드하세요](https://releases.aspose.com/cells/net/) 또는 무료로 사용해 보세요 [무료 체험](https://releases.aspose.com/).
3. C#에 대한 기본 지식: C# 및 .NET 환경에 대한 지식이 있으면 도움이 되지만, 모든 단계를 안내해 드립니다.
4. Excel 파일: 샘플 Excel 파일입니다. `sampleRotateTextWithShapeInsideWorksheet.xlsx`코드를 테스트하려면 , 이 필요합니다. 이 파일은 쉽게 접근할 수 있는 디렉터리에 저장해야 합니다.
다 준비하셨나요? 환상적이에요! 이제 재밌는 부분으로 넘어가 볼까요?
## 패키지 가져오기
시작하려면 필요한 패키지를 프로젝트에 가져와야 합니다. 방법은 다음과 같습니다.
### 새 프로젝트 만들기
1. Visual Studio를 엽니다.
2. "새 프로젝트 만들기"를 선택하세요.
3. "콘솔 앱"을 선택하고 기본 프로그래밍 언어로 C#을 선택하세요.
### Aspose.Cells 설치
이제 프로젝트에 Aspose.Cells를 추가해 보겠습니다. NuGet 패키지 관리자를 사용하면 됩니다.
1. 상단 메뉴에서 "도구"를 엽니다.
2. "NuGet 패키지 관리자"를 선택한 다음 "솔루션용 NuGet 패키지 관리"를 선택합니다.
3. "Aspose.Cells"를 검색하세요.
4. 프로젝트에 추가하려면 "설치"를 클릭하세요.
### 사용 지침 추가
주요 C# 파일의 맨 위에 다음 지시문을 추가해야 합니다.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
이제 코딩을 시작할 준비가 다 되었습니다!
이 과정을 이해하기 쉬운 단계로 나누어 보겠습니다. Excel 파일에서 도형이 있는 텍스트를 회전하는 방법은 다음과 같습니다.
## 1단계: 디렉토리 경로 설정
먼저 Excel 파일을 저장할 원본 및 출력 디렉터리를 설정해야 합니다. 방법은 다음과 같습니다.
```csharp
//소스 디렉토리
string sourceDir = "Your Document Directory"; // 문서 디렉토리 설정
//출력 디렉토리
string outputDir = "Your Document Directory"; // 출력 디렉토리 설정
```
바꾸다 `"Your Document Directory"` 실제 경로와 함께 `sampleRotateTextWithShapeInsideWorksheet.xlsx` 파일이 위치했습니다.
## 2단계: 샘플 Excel 파일 로드
이제 샘플 Excel 파일을 로드해 보겠습니다. 기존 데이터를 조작해야 하므로 이 작업이 매우 중요합니다.
```csharp
//샘플 Excel 파일을 로드합니다.
Workbook wb = new Workbook(sourceDir + "sampleRotateTextWithShapeInsideWorksheet.xlsx");
```
## 3단계: 워크시트에 액세스
파일이 로드되면 수정하려는 특정 워크시트에 접근해야 합니다. 이 경우에는 첫 번째 워크시트입니다.
```csharp
//첫 번째 워크시트에 접근합니다.
Worksheet ws = wb.Worksheets[0];
```
## 4단계: 셀 수정
다음으로, 특정 셀을 수정하여 메시지를 표시해 보겠습니다. 이 예시에서는 B4 셀을 사용하겠습니다.
```csharp
//셀 B4에 접근하여 그 안에 메시지를 추가하세요.
Cell b4 = ws.Cells["B4"];
b4.PutValue("Text is not rotating with shape because RotateTextWithShape is false.");
```
이 단계는 전적으로 의사소통에 관한 것입니다. 이 시트를 여는 사람이 우리가 조정하려는 내용을 이해하도록 하는 것입니다.
## 5단계: 첫 번째 모양에 액세스
텍스트를 회전하려면 작업할 도형이 필요합니다. 여기서는 워크시트의 첫 번째 도형을 사용해 보겠습니다.
```csharp
//첫 번째 모양에 접근합니다.
Shape sh = ws.Shapes[0];
```
## 6단계: 도형 텍스트 정렬 조정
바로 여기서 마법이 일어납니다. 도형의 텍스트 정렬 속성을 조정해 보겠습니다.
```csharp
//모양 텍스트 정렬에 접근합니다.
Aspose.Cells.Drawing.Texts.ShapeTextAlignment shapeTextAlignment = sh.TextBody.TextAlignment;
//RotateTextWithShape를 false로 설정하여 모양과 함께 텍스트를 회전하지 마세요.
shapeTextAlignment.RotateTextWithShape = false;
```
설정하여 `RotateTextWithShape` false로 설정하면 텍스트가 똑바로 세워지고 모양과 함께 회전하지 않으므로 모든 것이 깔끔하고 체계적으로 유지됩니다.
## 7단계: 출력 Excel 파일 저장
마지막으로, 변경 사항을 새 Excel 파일에 저장해 보겠습니다. 이렇게 하면 수정 사항이 손실되지 않고 깔끔한 결과를 얻을 수 있습니다.
```csharp
//출력된 Excel 파일을 저장합니다.
wb.Save(outputDir + "outputRotateTextWithShapeInsideWorksheet.xlsx");
```
이제 B4 셀의 텍스트와 도형에 적용된 조정 내용을 포함한 출력 파일이 저장되었습니다.
## 8단계: 코드 실행
당신의 `Main` 메서드를 사용하여 위의 모든 코드 조각을 래핑하고 프로젝트를 실행하세요. 출력 파일에 변경 사항이 반영되는 것을 확인하세요!
```csharp
Console.WriteLine("RotateTextWithShapeInsideWorksheet executed successfully.");
```
## 결론
Aspose.Cells for .NET을 사용하여 Excel에서 도형과 텍스트를 회전하는 작업은 처음에는 복잡한 과정처럼 보일 수 있지만, 자세히 살펴보면 매우 간단합니다. 이 간단한 단계를 따라 하면 스프레드시트를 더욱 전문적이고 시각적으로 보기 좋게 사용자 지정할 수 있습니다. 이제 고객용이든 개인 프로젝트용이든, 모두가 여러분의 작업 품질에 감탄할 것입니다!
## 자주 묻는 질문
### Aspose.Cells를 무료로 사용할 수 있나요?
네! 사용할 수 있습니다 [무료 체험](https://releases.aspose.com/) 도서관을 이용해 보세요.
### Aspose.Cells는 어떤 버전의 Excel을 지원하나요?
Aspose.Cells는 XLS, XLSX, CSV 등 다양한 Excel 형식을 지원합니다.
### 이전 버전의 Excel에서 도형이 있는 텍스트를 회전할 수 있나요?
네, 이 기능은 Aspose.Cells에서 지원하는 이전 형식에도 적용할 수 있습니다.
### Aspose.Cells에 대한 추가 문서는 어디에서 찾을 수 있나요?
포괄적인 내용을 탐색할 수 있습니다 [선적 서류 비치](https://reference.aspose.com/cells/net/) 더 자세한 정보를 얻으려면.
### Aspose.Cells에 대한 지원은 어떻게 받을 수 있나요?
지원을 요청하려면 다음을 방문하세요. [Aspose 포럼](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}