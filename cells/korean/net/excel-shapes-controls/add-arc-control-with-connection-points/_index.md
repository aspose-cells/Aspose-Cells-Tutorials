---
title: 연결 지점을 사용하여 아크 제어 추가
linktitle: 연결 지점을 사용하여 아크 제어 추가
second_title: Aspose.Cells .NET Excel 처리 API
description: 이 자세한 가이드에서는 Aspose.Cells for .NET을 사용하여 연결 지점이 있는 아크 컨트롤을 추가하는 방법을 알아봅니다.
weight: 27
url: /ko/net/excel-shapes-controls/add-arc-control-with-connection-points/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 연결 지점을 사용하여 아크 제어 추가

## 소개
시각적으로 매력적인 Excel 보고서를 만드는 데 있어 일러스트레이션은 중요한 역할을 합니다. 재무 보고서나 프로젝트 분석을 작성하든 아크와 같은 모양을 사용하면 데이터 프레젠테이션에 깊이와 명확성을 더할 수 있습니다. 오늘은 Aspose.Cells for .NET을 사용하여 Excel 워크시트에 연결점이 있는 아크 컨트롤을 추가하는 방법을 자세히 알아보겠습니다. 따라서 스프레드시트를 더 매력적으로 만들거나 데이터를 돋보이게 하는 방법을 궁금해하신 적이 있다면 계속 읽어보세요!
## 필수 조건
코딩의 흥분에 뛰어들기 전에, 모든 준비가 완료되었는지 확인해 보겠습니다. 필요한 것은 다음과 같습니다.
1. .NET Framework: 호환되는 버전이 설치되어 있는지 확인하세요. Aspose.Cells는 .NET Core를 포함한 여러 버전과 호환됩니다.
2.  .NET용 Aspose.Cells: Aspose.Cells 라이브러리를 다운로드하여 설치해야 합니다. 쉽게 다음에서 가져올 수 있습니다.[다운로드 링크](https://releases.aspose.com/cells/net/).
3. 좋은 IDE: 모든 .NET 개발자의 충실한 동반자인 Visual Studio는 코딩 경험을 간소화하는 데 도움이 됩니다.
4. C#에 대한 기본 지식: C#를 잘 알고 있다면 이 튜토리얼을 따라하는 데 어려움이 없을 것입니다.
5. 문서 디렉토리에 액세스: Excel 파일을 저장할 위치를 알아두세요. 이는 출력을 효율적으로 구성하는 데 필수적입니다.
## 패키지 가져오기
다음 단계는 프로젝트에 올바른 패키지를 가져왔는지 확인하는 것입니다. Aspose.Cells for .NET에는 다양한 기능이 있으므로 간단하게 설명하겠습니다. 포함해야 할 내용은 다음과 같습니다.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
이러한 네임스페이스를 사용하면 이 가이드 전체에서 사용하게 될 모든 그리기 기능과 셀 관리 기능에 액세스할 수 있습니다.
## 1단계: 문서 디렉토리 설정
우선 먼저—새로 생긴 멋진 Excel 파일을 저장할 디렉토리를 만들어 보겠습니다. 방법은 다음과 같습니다.
```csharp
string dataDir = "Your Document Directory";
// 디렉토리가 없으면 디렉토리를 생성합니다.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
이 코드는 지정한 폴더가 있는지 확인합니다. 없으면 폴더를 만듭니다. 간단하죠? 어수선함을 피하기 위해 파일을 위한 특정 장소를 갖는 것이 항상 좋습니다.
## 2단계: 통합 문서 인스턴스화
이제 디렉토리가 준비되었으니, 새로운 Excel 통합 문서를 만들어 보겠습니다.
```csharp
Workbook excelbook = new Workbook();
```
 전화를 걸어서`Workbook` 생성자는 기본적으로 "이봐, 새로운 Excel 파일을 시작하자!"라고 말하는 것입니다. 이것은 모든 모양과 데이터의 캔버스가 될 것입니다.
## 3단계: 첫 번째 호 모양 추가
여기서부터 재미가 시작됩니다! 첫 번째 호 모양을 추가해 보겠습니다.
```csharp
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
이 코드 줄은 첫 번째 워크시트에 호 모양을 추가합니다. 매개변수는 호의 좌표와 곡률을 정의하는 각도를 지정합니다. 
## 4단계: Arc의 모양 사용자 지정
빈 호 모양은 페인트가 칠해지지 않은 캔버스와 같습니다. 약간의 재치가 필요합니다!
### 아크 채우기 색상 설정
```csharp
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
```
이렇게 하면 아크가 파란색으로 표시됩니다. 원하는 색조로 색상을 변경할 수 있습니다.`Color.Blue` 다른 색상을 위해서.
### 아크 배치 설정
```csharp
arc1.Placement = PlacementType.FreeFloating;
```
배치를 "자유 이동"으로 설정하면 호가 셀 경계에 관계없이 이동할 수 있어 위치를 유연하게 지정할 수 있습니다.
### 선 두께 및 스타일 조정
```csharp
arc1.Line.Weight = 1;      
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
여기에서 선의 굵기와 스타일을 정의하여 더욱 눈에 띄고 시각적으로 매력적으로 만들 수 있습니다.
## 5단계: 다른 호 모양 추가
왜 하나에 그치나요? Excel 비주얼을 풍부하게 하기 위해 또 다른 호 모양을 추가해 봅시다.
```csharp
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
첫 번째 아크와 마찬가지로 이 아크도 다른 위치에 추가되었습니다. 바로 여기에서 디자인의 마법이 일어납니다!
## 6단계: 두 번째 아크 사용자 지정
두 번째 아크에도 개성을 부여해 보겠습니다!
### 아크 선 색상 변경
```csharp
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
```
우리는 파란색을 일관성 있게 유지했지만, 항상 섞어서 매치해서 디자인에 가장 잘 어울리는 색상을 찾을 수 있습니다!
### 첫 번째 호와 유사한 속성 설정
다음과 같은 미적 선택을 반드시 재현하세요.
```csharp
arc2.Placement = PlacementType.FreeFloating;
arc2.Line.Weight = 1;           
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
여기서는 두 번째 호가 첫 번째 호와 일치하는지 확인하여 워크시트 전체에 일관된 모양을 만듭니다.
## 7단계: 통합 문서 저장
저장하지 않고는 걸작이 완성되지 않죠? 이제 아크를 Excel 파일에 쓸 시간입니다.
```csharp
excelbook.Save(dataDir + "book1.out.xls");
```
이 줄은 새로 만든 아크를 지정된 디렉토리에 "book1.out.xls"라는 이름의 Excel 파일에 저장합니다.
## 결론
축하합니다! Aspose.Cells for .NET을 사용하여 Excel 시트에 연결점이 있는 아크 컨트롤을 추가하는 기본 사항을 방금 익혔습니다. 이 기능은 스프레드시트를 아름답게 만들 뿐만 아니라 복잡한 데이터를 더 쉽게 이해할 수 있게 해줍니다. 노련한 개발자이든 초보자이든 이러한 시각적 요소는 보고서를 평범한 것에서 웅장한 것으로 바꿀 수 있습니다.
## 자주 묻는 질문
### Aspose.Cells란 무엇인가요?
Aspose.Cells는 개발자가 Excel 파일을 프로그래밍 방식으로 만들고 조작할 수 있는 강력한 .NET 라이브러리입니다.
### Aspose.Cells를 무료로 사용할 수 있나요?
 네! 무료 체험판을 시도할 수 있습니다. 방문[이 링크](https://releases.aspose.com/) 시작하다.
### 호 외에 다른 모양을 추가하려면 어떻게 해야 하나요?
Aspose.Cells.Drawing 네임스페이스에서 사용 가능한 다양한 클래스를 사용하여 사각형, 원 등 다양한 모양을 추가할 수 있습니다.
### Aspose.Cells로 어떤 유형의 파일을 만들 수 있나요?
XLS, XLSX, CSV 등 다양한 Excel 형식을 만들고 조작할 수 있습니다.
### Aspose.Cells에 대한 기술 지원을 받을 수 있나요?
 물론입니다! 액세스할 수 있습니다.[Aspose 지원 포럼](https://forum.aspose.com/c/cells/9) 도움이 필요하면.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
