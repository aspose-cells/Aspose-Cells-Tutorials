---
title: Excel 워크시트에 사각형 컨트롤 추가
linktitle: Excel 워크시트에 사각형 컨트롤 추가
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET을 사용하여 Excel 워크시트에 사각형 컨트롤을 추가하는 방법을 자세하고 단계별 가이드를 통해 알아보세요.
weight: 25
url: /ko/net/excel-shapes-controls/add-rectangle-control-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 워크시트에 사각형 컨트롤 추가

## 소개
Excel 작업을 자동화하는 데 있어 Aspose.Cells for .NET은 워크시트에 직사각형과 같은 모양을 추가하는 것을 포함한 다양한 목표를 달성하는 데 도움이 되는 강력한 도구입니다. 이 가이드에서는 Aspose.Cells for .NET을 사용하여 Excel 워크시트에 직사각형 컨트롤을 추가하는 방법을 살펴보겠습니다. 마지막에는 직사각형 컨트롤이 포함된 워크시트를 만들고, 사용자 지정하고, 저장할 수 있게 됩니다.
하지만 이에 앞서 전제 조건부터 살펴보겠습니다.
## 필수 조건
이 튜토리얼을 따라가려면 다음 필수 조건이 충족되었는지 확인하세요.
1.  .NET 라이브러리용 Aspose.Cells: 아직 없다면,[라이브러리를 다운로드하다](https://releases.aspose.com/cells/net/) 또는 Visual Studio에서 NuGet을 사용하여 설치하세요.
2. .NET Framework: 컴퓨터에 .NET 개발 환경을 설정해야 합니다.
3. C#에 대한 기본 지식: 단계별로 안내해 드리지만, C#와 객체 지향 프로그래밍에 대한 기본적인 지식이 있으면 좋습니다.
4.  라이센스: Aspose.Cells를 평가 모드에서 사용하면 기본 작업에 적합하지만 전체 기능을 사용하려면 다음을 고려하세요.[임시 면허](https://purchase.aspose.com/temporary-license/)또는 다음에서 구매[여기](https://purchase.aspose.com/buy).
이제 코드를 살펴보겠습니다!
## 패키지 가져오기
Aspose.Cells를 시작하려면 프로젝트에 필요한 네임스페이스를 가져왔는지 확인하세요. 이러한 가져오기를 통해 Excel 파일과 상호 작용하는 데 필요한 다양한 클래스와 메서드에 액세스할 수 있습니다.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
이러한 줄은 프로젝트가 파일 디렉토리와 상호 작용할 수 있도록 보장합니다.`System.IO`), Excel 통합 문서(`Aspose.Cells`), 그리고 모양 그리기(`Aspose.Cells.Drawing`).
이제 여러분이 쉽게 따라할 수 있고 여러분의 프로젝트에도 복제할 수 있도록 과정을 간단한 단계로 나누어 보겠습니다.
## 1단계: 디렉토리 경로 설정
가장 먼저 해야 할 일은 Excel 파일을 저장할 디렉토리를 정의하는 것입니다. 이 단계는 프로젝트가 출력 파일을 만들고 저장할 위치를 알 수 있도록 합니다.
### 데이터 디렉토리 정의
```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "Your Document Directory";
```
 여기서 Excel 파일이 저장될 디렉토리 경로를 지정합니다. 다음을 바꿀 수 있습니다.`"Your Document Directory"` 컴퓨터의 실제 경로를 사용하거나, 폴더가 없으면 동적으로 만듭니다.
### 디렉토리 확인 및 생성
```csharp
// 디렉토리가 없으면 디렉토리를 생성합니다.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
이 블록은 디렉토리가 존재하는지 확인합니다. 존재하지 않으면 디렉토리를 만듭니다. 문서를 저장하기 전에 파일 캐비닛을 준비하는 것과 같습니다.
## 2단계: 새 통합 문서 인스턴스화
 이 단계에서는 다음을 사용하여 새 Excel 통합 문서를 만듭니다.`Aspose.Cells.Workbook` 클래스. 이것은 워크시트와 도형을 담는 용기 역할을 할 것입니다.
```csharp
// 새 통합 문서를 인스턴스화합니다.
Workbook excelbook = new Workbook();
```
 전화를 걸어서`Workbook` 생성자를 사용하면 이제 사용자 정의할 수 있는 빈 Excel 통합 문서가 준비됩니다.
## 3단계: 사각형 컨트롤 추가
마법이 일어나는 곳은 바로 여기입니다. 워크북의 첫 번째 워크시트에 직사각형 모양을 추가합니다.
```csharp
// 사각형 컨트롤을 추가합니다.
Aspose.Cells.Drawing.RectangleShape rectangle = excelbook.Worksheets[0].Shapes.AddRectangle(3, 0, 2, 0, 70, 130);
```
이것을 자세히 살펴보겠습니다.
- `excelbook.Worksheets[0]`: 통합 문서의 첫 번째 워크시트에 액세스합니다.
- `.Shapes.AddRectangle(3, 0, 2, 0, 70, 130)`: 이것은 워크시트에 직사각형 모양을 추가합니다. 여기의 매개변수는 직사각형의 위치(행과 열)와 너비와 높이를 정의합니다.
## 4단계: 사각형 사용자 지정
사각형을 추가하는 것만으로는 충분하지 않습니다. 사용자 지정해야 합니다. 이 단계에서는 사각형의 배치, 선 두께, 대시 스타일을 설정합니다.
### 배치 설정
```csharp
// 사각형의 위치를 설정합니다.
rectangle.Placement = PlacementType.FreeFloating;
```
이렇게 하면 사각형이 자유롭게 움직일 수 있으므로 셀 크기에 구애받지 않습니다.
### 선 두께 설정
```csharp
// 선의 굵기를 설정합니다.
rectangle.Line.Weight = 4;
```
여기서 우리는 사각형의 선 두께를 4포인트로 설정했습니다. 숫자가 높을수록 선이 두꺼워집니다.
### 대시 스타일 설정
```csharp
// 사각형의 대시 스타일을 설정합니다.
rectangle.Line.DashStyle = MsoLineDashStyle.Solid;
```
 이 줄은 사각형 테두리의 대시 스타일을 단색으로 설정합니다. 다음과 같은 다양한 스타일을 실험할 수 있습니다.`Dash` 또는`Dot` 귀하의 요구 사항에 따라 다릅니다.
## 5단계: 통합 문서 저장
사각형을 추가하고 사용자 지정한 후 마지막 단계는 지정된 디렉토리에 통합 문서를 저장하는 것입니다.
```csharp
// Excel 파일을 저장합니다.
excelbook.Save(dataDir + "book1.out.xls");
```
 이렇게 하면 통합 문서가 다음과 같이 저장됩니다.`.xls` 이전에 정의한 폴더에 있는 파일입니다. 확장자를 변경하여 파일 형식을 수정할 수 있습니다(예:`.xlsx` 최신 Excel 형식을 선호하는 경우
## 결론
그리고 이제 알게 되었습니다! Aspose.Cells for .NET을 사용하여 Excel 워크시트에 사각형 컨트롤을 추가하는 것은 단계별로 분해하면 간단한 프로세스입니다. 시각적인 매력을 위해 모양을 추가하거나, 데이터 섹션을 강조 표시하거나, 보고서를 사용자 지정해야 하는 경우 Aspose.Cells는 프로그래밍 방식으로 이를 수행할 수 있는 유연성을 제공합니다.
이 가이드는 Aspose.Cells를 사용하여 Excel 시트에 직사각형과 같은 모양을 추가하는 데 필요한 모든 지식을 제공했을 것입니다. 이제 이 강력한 라이브러리로 무엇을 더 달성할 수 있는지 실험하고 확인할 시간입니다!
## 자주 묻는 질문
### Aspose.Cells for .NET을 사용하여 원이나 선과 같은 다른 모양을 추가할 수 있나요?  
네, Aspose.Cells를 사용하면 원, 선, 화살표 등 다양한 모양을 추가할 수 있습니다.
### 사각형 컨트롤에 대해 어떤 다른 속성을 설정할 수 있나요?  
사각형 안에 채우기 색상, 선 색상, 투명도를 사용자 지정할 수 있으며, 심지어 텍스트도 추가할 수 있습니다.
### Aspose.Cells는 .NET Core와 호환됩니까?  
네, Aspose.Cells는 .NET Core는 물론 .NET Framework와 기타 .NET 기반 플랫폼을 지원합니다.
### 사각형을 특정 셀을 기준으로 배치할 수 있나요?  
 예, 특정 행과 열에 사각형을 배치하거나 다음을 사용할 수 있습니다.`PlacementType` 고정 방법을 제어합니다.
### Aspose.Cells의 무료 평가판이 있나요?  
 네, 당신은 얻을 수 있습니다[무료 체험](https://releases.aspose.com/) 구매하기 전에 웹사이트에서 도서관의 기능을 테스트해 보세요.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
