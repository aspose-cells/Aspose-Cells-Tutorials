---
"description": "Aspose.Cells for .NET을 사용하여 Excel 워크시트에 타원을 추가하는 방법을 알아보세요. 자세한 코드 설명이 포함된 단계별 가이드입니다."
"linktitle": "Excel 워크시트에 타원 추가"
"second_title": "Aspose.Cells .NET Excel 처리 API"
"title": "Excel 워크시트에 타원 추가"
"url": "/ko/net/excel-shapes-controls/add-oval-to-worksheet-excel/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel 워크시트에 타원 추가

## 소개
멋지고 인터랙티브한 Excel 파일을 만드는 데는 숫자와 수식 외에도 다양한 요소가 포함될 수 있습니다. 타원과 같은 도형은 시각적인 매력을 더하거나 워크시트에 기능적인 요소를 제공할 수 있습니다. 이 튜토리얼에서는 Aspose.Cells for .NET을 사용하여 Excel 워크시트에 프로그래밍 방식으로 타원을 추가하는 방법을 살펴보겠습니다. 특별한 기능이나 기능을 추가하고 싶다면, 단계별 가이드를 통해 모든 것을 자세히 안내해 드립니다.
## 필수 조건
코드를 살펴보기 전에 꼭 준비해야 할 몇 가지 사항이 있습니다.
1. Aspose.Cells for .NET 라이브러리: 여기에서 다운로드할 수 있습니다. [여기](https://releases.aspose.com/cells/net/) 또는 Visual Studio에서 NuGet을 사용하여 설치하세요.
2. 개발 환경: Visual Studio와 같은 AC# IDE.
3. C#에 대한 기본 이해: C#의 기본 코딩 개념에 익숙해야 합니다.
또한 Aspose.Cells for .NET 라이브러리를 설치하여 프로젝트를 설정하는 것을 잊지 마세요. 라이선스가 아직 없다면 [임시 면허](https://purchase.aspose.com/temporary-license/) 또는 사용 [무료 체험](https://releases.aspose.com/) 버전.
## 패키지 가져오기
코드를 작성하기 전에 필요한 네임스페이스를 포함했는지 확인하세요. 다음은 올바른 라이브러리를 사용하고 있는지 확인하기 위한 C# 코드 조각입니다.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## 1단계: 디렉토리 설정
Excel 시트에 타원을 추가하는 첫 번째 단계는 Excel 파일을 저장할 위치를 지정하는 것입니다. 디렉터리 경로를 정의하고 작업을 저장하기 전에 해당 디렉터리가 존재하는지 확인해 보겠습니다.

디렉터리 경로를 생성하고 존재하는지 확인합니다. 폴더가 없으면 자동으로 생성됩니다.
```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "Your Document Directory";
// 디렉토리가 없으면 새로 만듭니다.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
이 단계는 파일이 적절한 위치에 저장되었는지 확인하고 나중에 파일 경로 문제가 발생하지 않도록 하는 데 중요합니다.
## 2단계: 새 통합 문서 초기화
다음으로, 타원 도형을 추가할 새 통합 문서를 만들어야 합니다. 통합 문서는 Excel 파일이며, 여기에 내용이나 도형을 추가할 수 있습니다.

이 단계에서는 새로운 것을 인스턴스화합니다. `Workbook` Excel 파일 컨테이너 역할을 할 객체입니다.
```csharp
// 새로운 통합 문서를 인스턴스화합니다.
Workbook excelbook = new Workbook();
```
## 3단계: 첫 번째 타원 모양 추가
이제 재미있는 부분입니다. 워크시트에 타원 모양을 추가하는 것이죠. 이 타원은 버튼이나 강조 표시와 같은 시각적 요소를 나타낼 수 있습니다. 먼저 워크북의 첫 번째 워크시트에 첫 번째 타원 모양을 추가해 보겠습니다.

여기서 우리는 다음을 사용합니다. `Shapes.AddOval()` 워크시트의 특정 행과 열에 타원을 만드는 방법입니다.
```csharp
// 타원형 모양을 추가합니다.
Aspose.Cells.Drawing.Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```
내부의 매개변수 `AddOval()` 다음과 같습니다.
- 처음 두 숫자는 타원의 왼쪽 상단 모서리에 대한 행과 열을 나타냅니다.
- 다음 두 숫자는 타원의 높이와 너비를 나타냅니다.
## 4단계: 타원의 위치 및 스타일 설정
타원이 생성되면 위치, 선 두께, 대시 스타일을 설정할 수 있습니다. `Placement` 속성은 워크시트에서 셀의 크기를 조정하거나 이동할 때 타원이 어떻게 동작하는지 결정합니다.

타원을 자유롭게 움직이게 만들고 모양을 조정합니다.
```csharp
// 타원의 위치를 설정합니다.
oval1.Placement = PlacementType.FreeFloating;
// 선의 굵기를 설정합니다.
oval1.Line.Weight = 1;
// 타원의 대시 스타일을 설정합니다.
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```
이렇게 하면 타원이 워크시트 내에서 자유롭게 움직일 수 있으며, 시각적 일관성을 위해 선 두께와 스타일이 설정됩니다.
## 5단계: 다른 타원(원) 모양 추가
왜 하나로만 그치나요? 이 단계에서는 또 다른 타원 모양을 추가해 보겠습니다. 이번에는 높이와 너비를 맞춰 완벽한 원을 만들어 보겠습니다.

또 다른 타원을 만들어 다른 위치에 놓고 높이와 너비를 동일하게 설정하여 원형이 되도록 합니다.
```csharp
// 다른 타원(원) 모양을 추가합니다.
Aspose.Cells.Drawing.Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```
## 6단계: 두 번째 타원 스타일 지정
이전과 마찬가지로, 이 두 번째 타원(또는 원)의 배치, 두께, 대시 스타일을 조정해 보겠습니다.

첫 번째 타원의 스타일과 일치하도록 두 번째 타원에도 비슷한 속성을 적용합니다.
```csharp
// 타원의 위치를 설정합니다.
oval2.Placement = PlacementType.FreeFloating;
// 선의 굵기를 설정합니다.
oval2.Line.Weight = 1;
// 타원의 대시 스타일을 설정합니다.
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```
## 7단계: 통합 문서 저장
마지막으로, 방금 추가한 타원이 포함된 통합 문서를 저장해야 합니다. 파일을 저장하면 모든 변경 사항이 저장됩니다.

이전에 정의한 디렉토리 경로에 통합 문서를 저장합니다.
```csharp
// 엑셀 파일을 저장합니다.
excelbook.Save(dataDir + "book1.out.xls");
```
이제 끝입니다! Excel 워크시트에 타원을 추가하고 파일을 저장했습니다.
## 결론
Aspose.Cells for .NET을 사용하여 Excel 시트에 타원과 같은 도형을 추가하는 것은 간단할 뿐만 아니라, 추가적인 시각적 요소로 스프레드시트를 더욱 돋보이게 하는 재미있는 방법입니다. 디자인 목적이든 클릭 가능한 요소 추가든, 도형은 Excel 파일의 디자인과 기능에 중요한 역할을 할 수 있습니다. 따라서 다음에 인터랙티브하거나 시각적으로 매력적인 Excel 시트가 필요한 프로젝트를 진행할 때, 완벽한 타원을 추가하는 방법을 정확히 알고 계실 것입니다!
## 자주 묻는 질문
### Aspose.Cells for .NET을 사용하여 사각형이나 선과 같은 다른 모양을 추가할 수 있나요?
네, 사각형, 선, 화살표 등 다양한 모양을 추가할 수 있습니다. `Shapes` Aspose.Cells에서 컬렉션을 수집합니다.
### 타원을 추가한 후에 크기를 조절할 수 있나요?
물론입니다! 타원을 추가한 후에도 높이와 너비 속성을 수정할 수 있습니다.
### XLS 외에 어떤 파일 형식으로 통합 문서를 저장할 수 있나요?
Aspose.Cells는 XLSX, CSV, PDF 등 다양한 형식을 지원합니다.
### 타원 윤곽선의 색상을 수정할 수 있나요?
예, 다음을 사용하여 타원의 선 색상을 변경할 수 있습니다. `Line.Color` 재산.
### Aspose.Cells를 사용하려면 라이센스가 필요합니까?
무료 평가판을 통해 Aspose.Cells를 사용해 볼 수 있지만 다음이 필요합니다. [특허](https://purchase.aspose.com/buy) 장기 사용이나 고급 기능에 대한 액세스를 위해서입니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}