---
title: Excel에서 모양의 연결점 가져오기
linktitle: Excel에서 모양의 연결점 가져오기
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET을 사용하여 Excel에서 모양 연결점을 가져오는 방법을 알아보세요. 단계별 가이드를 따라 모양점을 쉽게 추출하고 프로그래밍 방식으로 표시하세요.
weight: 11
url: /ko/net/excel-shapes-controls/get-connection-points-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 모양의 연결점 가져오기

## 소개
Excel 파일을 프로그래밍 방식으로 작업할 때 종종 시트에 포함된 모양과 상호 작용해야 합니다. 수행할 수 있는 보다 고급 작업 중 하나는 모양에서 연결점을 추출하는 것입니다. 연결점은 커넥터로 모양을 연결하고 레이아웃을 보다 정확하게 관리하는 데 사용됩니다. Excel에서 모양의 연결점을 가져오려는 경우 Aspose.Cells for .NET이 필요한 도구입니다. 이 자습서에서는 이를 달성하기 위한 단계별 프로세스를 안내합니다.
## 필수 조건
코드를 살펴보기 전에 다음 전제 조건이 충족되었는지 확인하세요.
- .NET용 Aspose.Cells: 개발 환경에 Aspose.Cells가 설치되어 있어야 합니다. 아직 설치되어 있지 않으면 다음을 수행할 수 있습니다.[최신 버전을 여기에서 다운로드하세요](https://releases.aspose.com/cells/net/).
- 개발 환경: Visual Studio나 다른 .NET 호환 IDE가 제대로 설치되어 있는지 확인하세요.
- C#에 대한 기본 지식: 이 튜토리얼에서는 사용자가 C# 프로그래밍과 객체 지향 원칙에 대한 기본적인 이해가 있다고 가정합니다.
 또한 다음에 가입할 수도 있습니다.[Aspose.Cells 무료 체험](https://releases.aspose.com/) 아직 하지 않았다면. 그러면 이 가이드에 필요한 모든 기능에 액세스할 수 있습니다.

## 패키지 가져오기
프로젝트에서 Aspose.Cells를 사용하려면 필요한 네임스페이스를 포함해야 합니다. 다음 import 문은 코드 맨 위에 있어야 합니다.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
이러한 네임스페이스를 사용하면 Aspose.Cells의 핵심 기능에 액세스할 수 있으며 워크시트와 도형을 조작할 수 있습니다.

## 모양의 연결점을 얻기 위한 단계별 가이드
이 섹션에서는 Excel 워크시트 내에서 도형의 연결점을 추출하는 방법을 안내해 드리겠습니다. 명확하게 이해하려면 각 단계를 주의 깊게 따르세요.
## 1단계: 새 통합 문서 인스턴스화
 우선, 우리는 인스턴스를 생성해야 합니다.`Workbook` 클래스. 이것은 Aspose.Cells의 Excel 파일을 나타냅니다. 기존 파일이 없어도 문제 없습니다. 빈 통합 문서로 시작할 수 있습니다.
```csharp
// 새 통합 문서 인스턴스화
Workbook workbook = new Workbook();
```
 이 단계에서는 빈 Excel 통합 문서를 만들었지만 파일 경로를 전달하여 기존 통합 문서를 로드할 수도 있습니다.`Workbook` 건설자.
## 2단계: 첫 번째 워크시트에 액세스
다음으로, 도형을 작업할 워크시트에 액세스해야 합니다. 이 경우, 워크북의 첫 번째 워크시트를 사용하겠습니다.
```csharp
// 워크북의 첫 번째 워크시트를 받으세요
Worksheet worksheet = workbook.Worksheets[0];
```
 이 줄은 통합 문서의 워크시트 모음에서 첫 번째 워크시트에 액세스합니다. 특정 시트로 작업하는 경우 인덱스를 바꿀 수 있습니다.`0` 원하는 인덱스로.
## 3단계: 새 텍스트 상자(도형) 추가
이제 워크시트에 새 도형을 추가해 보겠습니다. 도형의 한 유형인 텍스트 상자를 만들 것입니다. 다른 유형의 도형을 추가할 수도 있지만, 이 튜토리얼에서는 단순성을 위해 텍스트 상자를 고수하겠습니다.
```csharp
// 컬렉션에 새 텍스트 상자 추가
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
우리가 한 일은 다음과 같습니다.
-  행에 텍스트 상자를 추가했습니다`2` , 열`1`.
-  텍스트 상자의 크기를 설정하세요`160` 폭의 단위 및`200` 높이의 단위.
## 4단계: Shapes 컬렉션에서 Shape에 액세스
 텍스트 상자를 추가하면 워크시트의 도형 컬렉션의 일부가 됩니다. 이제 다음을 사용하여 해당 도형에 액세스합니다.`Shapes`수집.
```csharp
// shapes 컬렉션에서 모양(텍스트 상자)에 액세스합니다.
Shape shape = workbook.Worksheets[0].Shapes[0];
```
이 단계에서는 컬렉션에서 첫 번째 모양(텍스트 상자)을 검색합니다. 모양이 여러 개 있는 경우 인덱스를 지정하거나 이름으로 모양을 찾을 수도 있습니다.
## 5단계: 연결 지점 검색
이제 모양이 생겼으니 연결점을 추출해 보겠습니다. 이 점은 모양에 커넥터를 부착하는 데 사용됩니다.`ConnectionPoints` 모양의 속성은 사용 가능한 모든 연결 지점을 반환합니다.
```csharp
// 이 모양의 모든 연결점을 얻으세요
var connectionPoints = shape.ConnectionPoints;
```
이를 통해 해당 모양에 사용할 수 있는 모든 연결 지점의 컬렉션을 얻을 수 있습니다.
## 6단계: 연결 지점 표시
마지막으로, 각 연결 지점의 좌표를 표시하고 싶습니다. 여기서 연결 지점을 반복하고 콘솔에 출력합니다.
```csharp
// 모든 모양 포인트 표시
foreach (var pt in connectionPoints)
{
    System.Console.WriteLine(string.Format("X = {0}, Y = {1}", pt.X, pt.Y));
}
```
 이 루프는 각 연결 지점을 반복하고 다음을 인쇄합니다.`X` 그리고`Y` 좌표. 이는 디버깅이나 모양의 연결 지점을 시각적으로 확인하는 데 유용할 수 있습니다.
## 7단계: 실행 및 완료
위의 모든 단계를 설정했으면 코드를 실행할 수 있습니다. 프로세스가 성공적으로 완료되도록 하는 마지막 줄은 다음과 같습니다.
```csharp
System.Console.WriteLine("GetShapeConnectionPoints executed successfully.");
```
이 줄은 단순히 프로세스가 완료되었다는 것을 나타내는 메시지를 콘솔에 기록합니다.

## 결론
이 튜토리얼에서는 Aspose.Cells for .NET을 사용하여 Excel에서 도형의 연결점을 검색하는 방법을 다루었습니다. 작업을 소화하기 쉬운 작은 단계로 나누어 통합 문서를 만들고, 도형을 추가하고, 연결점을 추출하는 과정을 살펴보았습니다.
모양을 프로그래밍 방식으로 조작하는 방법을 이해하면 동적이고 대화형 Excel 시트를 구축할 수 있는 가능성의 세계가 열립니다. 보고서를 작성하든, 대시보드를 디자인하든, 다이어그램을 만들든 이 지식은 유용할 것입니다.
## 자주 묻는 질문
### 도형의 연결점이란 무엇인가요?
연결점은 모양의 특정 지점으로, 여기에 커넥터를 부착하거나 다른 모양에 연결할 수 있습니다.
### 워크시트에 있는 모든 도형의 연결점을 검색할 수 있나요?
네, Aspose.Cells를 사용하면 지원하는 모든 도형에 대한 연결점을 검색할 수 있습니다. 워크시트에서 도형 컬렉션을 반복하기만 하면 됩니다.
### Aspose.Cells를 사용하려면 라이선스가 필요한가요?
네, 무료로 사용해 볼 수는 있지만 전체 기능을 사용하려면 라이선스가 필요합니다.[여기서 라이센스를 구매하세요](https://purchase.aspose.com/buy)또는 얻을[임시 면허](https://purchase.aspose.com/temporary-license/).
### Aspose.Cells에서 다양한 유형의 모양을 추가하려면 어떻게 해야 하나요?
당신은 사용할 수 있습니다`Add` 직사각형, 타원 등의 모양에 대한 방법입니다. 각 모양에는 사용자 정의할 수 있는 특정 매개변수가 있습니다.
### 새 Excel 파일을 만드는 대신 기존 Excel 파일을 로드하려면 어떻게 해야 합니까?
 기존 파일을 로드하려면 파일 경로를 전달하세요.`Workbook` 생성자는 다음과 같습니다.  
```csharp
Workbook workbook = new Workbook("path_to_file.xlsx");
```
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
