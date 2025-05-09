---
"description": "Aspose.Cells for .NET을 사용하여 Excel 워크시트에서 페이지 크기를 가져오는 방법을 알아보세요. A2, A3, A4, Letter 용지 크기를 사용자 지정하는 단계별 가이드입니다."
"linktitle": "워크시트의 페이지 크기 가져오기"
"second_title": "Aspose.Cells .NET Excel 처리 API"
"title": "워크시트의 페이지 크기 가져오기"
"url": "/ko/net/worksheet-page-setup-features/get-page-dimensions/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 워크시트의 페이지 크기 가져오기

## 소개
Aspose.Cells for .NET을 사용하여 Excel 파일을 프로그래밍 방식으로 작업하는 경우, 워크시트의 페이지 크기에 접근하여 설정해야 할 때가 있습니다. 페이지 크기를 알면 특정 용도에 맞게 Excel 시트를 레이아웃, 인쇄 및 사용자 지정하는 데 도움이 될 수 있습니다. 이 글에서는 Aspose.Cells for .NET을 사용하여 Excel에서 다양한 페이지 크기를 가져오고 표시하는 방법을 살펴보겠습니다. 단계별 자습서를 통해 자신 있게 시작하는 데 필요한 모든 정보를 얻을 수 있도록 안내해 드리겠습니다.
## 필수 조건
시작하기에 앞서, 이 튜토리얼을 따라하는 데 필요한 모든 것이 있는지 확인해 보겠습니다.
1. Aspose.Cells for .NET: Aspose.Cells for .NET이 설치되어 있는지 확인하세요. [여기에서 라이브러리를 다운로드하세요](https://releases.aspose.com/cells/net/) 또는 NuGet을 통해 .NET 프로젝트에 설치하세요.
2. .NET 환경: 호환되는 .NET 개발 환경(예: Visual Studio).
3. 라이선스 설정: Aspose.Cells의 모든 기능을 사용하려면 라이선스를 적용하세요. [무료 임시 면허를 요청하세요](https://purchase.aspose.com/temporary-license/) 평가 목적으로.
처음으로 Aspose.Cells를 평가해 보시려면 무료 체험판 버전으로 시작하세요.
## 패키지 가져오기
코드를 시작하기 전에 모든 필수 클래스와 메서드에 액세스하기 위해 Aspose.Cells 네임스페이스를 프로젝트에 가져와야 합니다.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
이 과정을 간단한 단계로 나누어 보겠습니다. 여기에서는 다양한 용지 크기를 확인하고, 워크시트에 적용한 후, 각 용지의 크기를 인쇄해 보겠습니다.
## 1단계: 통합 문서 인스턴스 만들기
첫 번째 단계는 인스턴스를 만드는 것입니다. `Workbook` 클래스입니다. 이 객체는 우리가 조작할 수 있는 워크시트를 포함하는 기본 워크북 역할을 합니다.
```csharp
Workbook book = new Workbook();
```
생각하다 `Workbook` Excel 파일의 기본 컨테이너로 사용합니다. 개별 워크시트에 액세스하고 제어하는 데 필요합니다.
## 2단계: 첫 번째 워크시트에 액세스
다음으로, 통합 문서의 첫 번째 워크시트에 접근해 보겠습니다. 기본적으로 새 통합 문서에는 시트가 하나 포함되어 있으므로 인덱스를 사용하여 직접 참조할 수 있습니다. `0`.
```csharp
Worksheet sheet = book.Worksheets[0];
```
그만큼 `Worksheets` 컬렉션에서 `Workbook` 각 워크시트에 색인별로 접근할 수 있습니다. 여기서는 첫 번째 시트를 가져와 페이지 크기를 설정합니다.
## 3단계: 용지 크기를 A2로 설정하고 치수를 표시합니다.
이제 워크시트에 접근할 수 있으니 용지 크기를 A2로 설정해 보겠습니다. 용지 크기를 설정하면 인쇄하거나 내보내기 전에 페이지 서식을 지정하는 데 유용합니다. 용지 크기를 설정한 후에는 페이지 크기를 인치 단위로 인쇄합니다.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
여기서 우리는 변경합니다 `PaperSize` 재산에 `PaperA2`. 크기를 설정한 후, `PageSetup.PaperWidth` 그리고 `PageSetup.PaperHeight` 시트의 너비와 높이를 인치 단위로 검색합니다. 이를 통해 페이지 크기를 빠르게 파악할 수 있습니다.
## 4단계: 용지 크기를 A3로 설정하고 치수를 표시합니다.
위와 같은 단계를 따라 페이지 크기를 A3 크기로 조정해 보겠습니다. 이 변경 사항은 약간 더 큰 인쇄물이나 한 페이지에 더 많은 내용을 넣을 때 유용합니다.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
A3 크기는 A4 크기의 두 배이므로 큰 표나 자세한 차트를 만드는 데 적합합니다. 용지 크기를 변경하면 워크시트 레이아웃도 그에 맞게 조정됩니다.
## 5단계: 용지 크기를 A4로 설정하고 치수를 표시합니다.
이제 용지 크기를 A4로 설정해 보겠습니다. A4는 문서 인쇄에 가장 일반적으로 사용되는 용지 크기입니다. 업데이트된 크기는 나중에 표시하겠습니다.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
표준 문서 형식을 사용하는 경우 일반적으로 A4 크기가 가장 적합합니다. 크기를 알면 콘텐츠 레이아웃을 조정하여 인쇄 문제를 방지하는 데 도움이 될 수 있습니다.
## 6단계: 용지 크기를 Letter로 설정하고 표시 크기를 설정합니다.
마지막으로, 용지 크기를 북미에서 일반적으로 사용되는 Letter 형식으로 설정합니다. 마지막으로 치수를 인쇄해 보겠습니다.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Letter 크기는 북미 지역에서 문서에 널리 사용되므로, 해당 지역에 있는 팀이나 고객과 협업할 때 이 크기를 설정하면 도움이 됩니다.
## 결론
이 튜토리얼에서는 Aspose.Cells for .NET을 사용하여 다양한 용지 크기에 대한 페이지 크기를 설정하고 가져오는 방법을 살펴보았습니다. A2, A3, A4, Letter 등의 페이지 크기를 구성하여 특정 인쇄 및 레이아웃 요구 사항에 맞게 Excel 워크시트 서식을 지정할 수 있습니다. 이러한 페이지 크기 제어 기능은 콘텐츠가 각 페이지 크기에 완벽하게 맞도록 보장하므로 전문적인 보고 및 프레젠테이션에 특히 유용합니다.
## 자주 묻는 질문
### Aspose.Cells에서 페이지 방향을 어떻게 바꿀 수 있나요?  
다음을 사용하여 방향을 변경할 수 있습니다. `PageSetup.Orientation` 속성을 다음 중 하나로 설정합니다. `PageOrientationType.P또는trait` or `PageOrientationType.Landscape`.
### Aspose.Cells에서 사용자 정의 페이지 크기를 설정할 수 있나요?  
예, 여백과 크기 조정 옵션을 조정하여 사용자 지정 페이지 크기를 설정할 수 있습니다. `PageSetup` 더 많은 통제를 위해.
### Aspose.Cells의 기본 용지 크기는 무엇입니까?  
기본 용지 크기는 일반적으로 A4입니다. 하지만 지역 설정에 따라 달라질 수 있으며, 필요에 따라 조정할 수 있습니다.
### Aspose.Cells에서 페이지 레이아웃을 미리 볼 수 있나요?  
Aspose.Cells는 그래픽 미리보기를 제공하지 않지만, Excel에서 레이아웃을 프로그래밍 방식으로 설정하고 인쇄 미리보기를 사용할 수 있습니다.
### .NET용 Aspose.Cells를 어떻게 설치하나요?  
Visual Studio에서 NuGet 패키지 관리자를 사용하여 Aspose.Cells를 설치하거나 다음에서 DLL을 다운로드할 수 있습니다. [Aspose.Cells 다운로드 페이지](https://releases.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}