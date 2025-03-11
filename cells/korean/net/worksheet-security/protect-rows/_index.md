---
title: Aspose.Cells를 사용하여 워크시트의 행 보호
linktitle: Aspose.Cells를 사용하여 워크시트의 행 보호
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET을 사용하여 Excel 워크시트의 행을 보호하는 방법을 알아보세요. 행 수준 보호로 데이터를 보호하고 실수로 변경하는 것을 방지하세요.
weight: 18
url: /ko/net/worksheet-security/protect-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells를 사용하여 워크시트의 행 보호

## 소개
Excel 파일을 프로그래밍 방식으로 작업하는 것은 종종 데이터 조작뿐만 아니라 데이터 보호도 필요한 작업입니다. 중요한 데이터를 보호하거나 실수로 편집하는 것을 방지해야 하는 경우 워크시트의 행을 보호하는 것은 중요한 단계가 될 수 있습니다. 이 튜토리얼에서는 Aspose.Cells for .NET을 사용하여 Excel 워크시트의 특정 행을 보호하는 방법을 자세히 살펴보겠습니다. 환경을 준비하는 것부터 간단하고 쉽게 따라할 수 있는 방식으로 보호 기능을 구현하는 것까지 필요한 모든 단계를 살펴보겠습니다.
## 필수 조건
워크시트에서 행을 보호하기 전에 먼저 준비해야 할 몇 가지 사항이 있습니다.
1.  Aspose.Cells for .NET: 개발 머신에 Aspose.Cells for .NET이 설치되어 있는지 확인하세요. 아직 설치하지 않았다면 다음에서 쉽게 다운로드할 수 있습니다.[Aspose Cells 다운로드 페이지](https://releases.aspose.com/cells/net/).
2. Visual Studio 또는 .NET IDE: 솔루션을 구현하려면 개발 환경을 설정해야 합니다. Visual Studio는 좋은 옵션이지만 .NET 호환 IDE라면 무엇이든 작동합니다.
3. 기본 C# 지식: C# 프로그래밍의 기본을 이해하면 튜토리얼을 따라가고 자신의 필요에 맞게 예제 코드를 수정하는 데 도움이 됩니다.
4.  Aspose.Cells API 문서: 다음을 숙지하세요.[.NET용 Aspose.Cells 설명서](https://reference.aspose.com/cells/net/) 라이브러리에서 사용되는 클래스 구조와 메서드에 대한 개요를 알아보세요.
모든 필수 구성 요소를 갖추었다면 바로 구현을 시작해 보겠습니다.
## 패키지 가져오기
시작하려면 필요한 패키지를 가져와야 합니다. 이러한 라이브러리는 C# 프로젝트에서 Excel 파일과 상호 작용하는 데 필수적입니다.
```csharp
using System.IO;
using Aspose.Cells;
```
필요한 패키지를 가져오면 코딩을 시작할 수 있습니다. 
이제, 여러분이 따라하기 매우 쉬운 과정을 더 작은 단계로 나누어 보겠습니다. 각 단계는 구현의 특정 부분에 초점을 맞추어 여러분이 빠르게 이해하고 적용할 수 있도록 합니다. 
## 1단계: 새 통합 문서 및 워크시트 만들기
보호 설정을 적용하기 전에 새 통합 문서를 만들고 작업할 워크시트를 선택해야 합니다. 이것이 작업 문서가 됩니다.
```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "Your Document Directory";
// 디렉토리가 없으면 디렉토리를 생성합니다.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// 새로운 통합 문서를 만듭니다.
Workbook wb = new Workbook();
// 워크시트 개체를 만들고 첫 번째 시트를 가져옵니다.
Worksheet sheet = wb.Worksheets[0];
```
이 예에서 우리는 단일 워크시트로 새 워크북을 만듭니다(Aspose.Cells를 사용하여 새 워크북을 만들 때의 기본 설정입니다). 그런 다음 워크북에서 첫 번째 워크시트를 가져오는데, 이것이 행 보호의 대상이 됩니다.
## 2단계: Style 및 StyleFlag 객체 정의
다음 단계는 스타일 및 스타일 플래그 객체를 정의하는 것입니다. 이러한 객체를 사용하면 셀의 속성(예: 잠긴 상태 또는 잠금 해제 상태)을 수정할 수 있습니다.
```csharp
// 스타일 객체를 정의합니다.
Style style;
// 스타일 플래그 객체를 정의합니다.
StyleFlag flag;
```
이후 단계에서 이러한 개체를 사용하여 셀 속성을 사용자 지정하고 워크시트에 적용하게 됩니다.
## 3단계: 워크시트의 모든 열 잠금 해제
기본적으로 Excel 워크시트의 모든 셀은 잠겨 있습니다. 그러나 워크시트를 보호하면 잠금 상태가 적용됩니다. 특정 행이나 셀만 보호되도록 하려면 먼저 모든 열을 잠금 해제할 수 있습니다. 이 단계는 특정 행만 보호하려는 경우 필수적입니다.
```csharp
// 워크시트의 모든 열을 반복하여 잠금을 해제합니다.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
 이 코드에서 우리는 워크시트의 모든 256개 열을 반복합니다(Excel 워크시트는 최대 256개 열을 가지며 0에서 255까지 인덱싱됨)`IsLocked` 재산에`false`. 이 작업을 수행하면 모든 열이 잠금 해제되지만 나중에 특정 행은 잠깁니다.
## 4단계: 첫 번째 행 잠금
열을 잠금 해제한 후 다음 단계는 보호하려는 특정 행을 잠그는 것입니다. 이 예에서는 첫 번째 행을 잠급니다. 이렇게 하면 다른 행이 잠금 해제된 상태에서 사용자가 해당 행을 수정할 수 없습니다.
```csharp
//첫 번째 행 스타일을 가져옵니다.
style = sheet.Cells.Rows[0].Style;
// 잠그세요.
style.IsLocked = true;
//플래그를 인스턴스화합니다.
flag = new StyleFlag();
// 잠금설정을 합니다.
flag.Locked = true;
// 첫 번째 행에 스타일을 적용합니다.
sheet.Cells.ApplyRowStyle(0, style, flag);
```
여기서 우리는 첫 번째 행의 스타일에 접근하고 이를 설정합니다.`IsLocked` 재산에`true` . 그 후, 우리는 다음을 사용합니다.`ApplyRowStyle()` 전체 행에 잠금 스타일을 적용하는 방법입니다. 보호하려는 다른 행을 잠그려면 이 단계를 반복할 수 있습니다.
## 5단계: 시트 보호
이제 필요한 행을 잠금 해제하고 잠그었으므로 워크시트를 보호할 차례입니다. 보호는 보호 암호(제공된 경우)를 제거하지 않는 한 아무도 잠긴 행이나 셀을 수정할 수 없도록 보장합니다.
```csharp
// 시트를 보호하세요.
sheet.Protect(ProtectionType.All);
```
 이 단계에서는 다음을 사용하여 전체 시트에 보호를 적용합니다.`ProtectionType.All`. 이 유형의 보호는 잠긴 행과 셀을 포함한 시트의 모든 측면이 보호됨을 의미합니다. 필요한 경우 다른 보호 유형을 지정하여 이 보호를 사용자 정의할 수도 있습니다.
## 6단계: 통합 문서 저장
마지막으로, 필요한 스타일과 보호를 적용한 후 통합 문서를 저장해야 합니다. 통합 문서는 Excel 97-2003, Excel 2010 등 다양한 형식으로 저장할 수 있습니다.
```csharp
// Excel 파일을 저장합니다.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
이 코드 줄은 변경 사항을 적용하여 Excel 97-2003 형식으로 통합 문서를 저장합니다. 다양한 파일 형식을 선택하여 필요에 따라 파일 형식을 변경할 수 있습니다.`SaveFormat` 옵션.
## 결론
이제 Aspose.Cells for .NET을 사용하여 워크시트의 행을 보호하는 방법을 성공적으로 배웠습니다. 위의 단계를 따르면 필요에 따라 행이나 열을 잠금 해제하거나 잠그고 보호를 적용하여 데이터 무결성을 보장할 수 있습니다.
## 자주 묻는 질문
### 한 번에 여러 행을 보호하려면 어떻게 해야 하나요?  
 여러 행을 반복하고 각 행에 잠금 스타일을 개별적으로 적용할 수 있습니다. 간단히 다음을 바꾸세요.`0` 잠그려는 행 인덱스를 사용합니다.
### 시트 보호에 비밀번호를 설정할 수 있나요?  
 네! 비밀번호를 전달할 수 있습니다.`sheet.Protect()` 비밀번호 보호를 강제하는 방법입니다.
### 열 전체가 아닌 셀만 잠금 해제할 수 있나요?  
네! 열 잠금을 해제하는 대신 스타일 속성을 수정하여 개별 셀의 잠금을 해제할 수 있습니다.
### 보호된 행을 편집하려고 하면 어떻게 되나요?  
행이 보호되면 Excel에서는 시트의 보호를 해제하지 않는 한 잠긴 셀을 편집할 수 없습니다.
### 특정 범위를 연속해서 보호할 수 있나요?  
 네! 개별 범위를 행으로 잠글 수 있습니다.`IsLocked` 범위 내의 특정 셀에 대한 속성입니다.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
