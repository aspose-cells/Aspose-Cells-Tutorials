---
title: Aspose.Cells를 사용하여 워크시트의 특정 셀 보호
linktitle: Aspose.Cells를 사용하여 워크시트의 특정 셀 보호
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET을 사용하여 Excel 워크시트에서 특정 셀을 보호하는 방법을 알아보세요. 몇 단계만으로 민감한 데이터를 보호하고 실수로 변경되는 것을 방지하세요.
weight: 14
url: /ko/net/worksheet-security/protect-specific-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells를 사용하여 워크시트의 특정 셀 보호

## 소개
이 튜토리얼에서는 Excel 워크시트에서 특정 셀을 보호하는 과정을 안내해 드리겠습니다. 마지막에는 전문가처럼 자신 있게 셀을 잠그고, 필요한 경우 워크시트를 유연하게 유지하면서도 승인되지 않은 변경을 방지할 수 있습니다.
## 필수 조건
자세한 내용을 살펴보기 전에 이 튜토리얼을 원활하게 따라갈 수 있도록 필요한 모든 것이 있는지 확인해 보겠습니다.
1. Visual Studio – 아직 설치하지 않았다면 Visual Studio를 다운로드하여 설치하세요. .NET 애플리케이션을 실행하는 기본 환경이 됩니다.
2.  .NET용 Aspose.Cells – .NET 애플리케이션에서 Excel 파일을 사용하려면 Aspose.Cells 라이브러리가 필요합니다. 아직 설치하지 않았다면 다음에서 최신 버전을 가져올 수 있습니다.[Aspose 웹사이트](https://releases.aspose.com/cells/net/).
3. .NET Framework 또는 .NET Core – 이 튜토리얼은 .NET Framework와 .NET Core 모두에서 작동합니다. 프로젝트가 Aspose.Cells와 호환되는지 확인하세요.
이러한 사항들이 준비되면 시작할 준비가 된 것입니다.
## 패키지 가져오기
단계별 가이드로 넘어가기 전에 Aspose.Cells에서 작업하는 데 필요한 네임스페이스를 가져와야 합니다. 프로젝트에서 파일 맨 위에 다음 가져오기 문을 포함합니다.
```csharp
using System.IO;
using Aspose.Cells;
```
이러한 네임스페이스를 사용하면 Excel 파일과 상호 작용하고 워크시트 셀에 스타일을 지정하고 보호하는 데 필요한 클래스를 사용할 수 있습니다.
이제 Aspose.Cells for .NET을 사용하여 워크시트의 특정 셀을 보호하는 간단한 단계로 나누어 보겠습니다. 셀 A1, B1, C1을 보호하고 나머지 워크시트는 편집할 수 있도록 열어 둡니다.
## 1단계: 새 통합 문서 및 워크시트 만들기
먼저, 새 통합 문서(Excel 파일)와 그 안에 워크시트를 만들어야 합니다. 여기서 셀 보호를 적용할 것입니다.
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
 이 단계에서는 아직 존재하지 않는 경우 결과 Excel 파일을 저장할 디렉토리도 만듭니다.`Workbook` 클래스는 새 Excel 파일을 초기화하고`Worksheets[0]` 통합 문서의 첫 번째 시트에서 작업할 수 있습니다.
## 2단계: 모든 열 잠금 해제
다음으로 워크시트의 모든 열을 잠금 해제합니다. 이렇게 하면 기본적으로 워크시트의 모든 셀을 편집할 수 있습니다. 나중에 보호하려는 셀만 잠급니다.
```csharp
// 스타일 객체를 정의합니다.
Style style;
// 스타일 플래그 객체를 정의합니다
StyleFlag styleflag;
// 워크시트의 모든 열을 반복하여 잠금을 해제합니다.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    styleflag = new StyleFlag();
    styleflag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, styleflag);
}
```
 이 코드 블록에서는 모든 열(최대 255개)을 반복하고 다음을 설정합니다.`IsLocked` 재산에`false` 이렇게 하면 기본적으로 해당 열의 모든 셀이 잠금 해제되어 기본적으로 편집할 수 있습니다. 그런 다음 스타일을 열에 적용합니다.`ApplyStyle()` 방법.
## 3단계: 특정 셀 잠금(A1, B1, C1)
 이제 모든 열이 잠금 해제되었으므로 A1, B1 및 C1과 같은 특정 셀을 잠그는 데 집중하겠습니다. 셀 스타일을 수정하고 해당 셀을 설정합니다.`IsLocked` 재산에`true`.
```csharp
// 3개의 셀을 잠그세요... 즉, A1, B1, C1.
style = sheet.Cells["A1"].GetStyle();
style.IsLocked = true;
sheet.Cells["A1"].SetStyle(style);
style = sheet.Cells["B1"].GetStyle();
style.IsLocked = true;
sheet.Cells["B1"].SetStyle(style);
style = sheet.Cells["C1"].GetStyle();
style.IsLocked = true;
sheet.Cells["C1"].SetStyle(style);
```
이 단계는 셀 A1, B1 및 C1이 잠겼는지 확인합니다. 이는 보호되는 셀이며 워크시트 보호가 적용되면 편집할 수 없습니다.
## 4단계: 워크시트 보호
필요한 셀을 잠그면 다음 단계는 전체 워크시트를 보호하는 것입니다. 이 단계는 잠긴 셀(A1, B1, C1)을 편집할 수 없게 만들고, 다른 셀은 편집을 위해 열려 있는 상태로 유지합니다.
```csharp
// 마지막으로 이제 시트를 보호하세요.
sheet.Protect(ProtectionType.All);
```
 그만큼`Protect` 워크시트에서 메서드가 호출되어 시트의 모든 측면을 보호해야 함을 지정합니다. 이렇게 하면 표시된 특정 셀이 잠깁니다.`IsLocked = true` 사용자가 변경할 수 없도록 보장합니다.
## 5단계: 통합 문서 저장
셀이 잠기고 시트가 보호되면 통합 문서를 원하는 위치에 저장할 수 있습니다.
```csharp
// Excel 파일을 저장합니다.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
이 단계에서는 통합 문서를 저장합니다.`dataDir` 파일 이름이 있는 폴더`output.out.xls`. 필요에 맞게 파일 이름과 디렉토리를 수정할 수 있습니다. 파일은 Excel 97-2003 형식으로 저장되지만 요구 사항에 따라 조정할 수 있습니다.
## 결론
Aspose.Cells for .NET을 사용하여 Excel 워크시트의 특정 셀을 보호하는 것은 간단한 프로세스입니다. 위의 단계를 따르면 다른 셀은 편집 가능한 상태로 유지하면서 특정 셀을 잠글 수 있습니다. 이 기능은 다른 사람과 통합 문서를 공유할 때 매우 유용한데, 어떤 데이터를 수정할 수 있고 어떤 데이터를 보호해야 하는지 제어하는 데 도움이 되기 때문입니다. 민감한 데이터를 작업하든 실수로 변경하는 것을 방지하든 Aspose.Cells는 유연하고 강력한 솔루션을 제공합니다.
## 자주 묻는 질문
### 몇 개의 셀 대신 특정 범위의 셀만 보호하려면 어떻게 해야 하나요?
개별 셀을 수동으로 잠그는 대신, 특정 범위의 셀이나 열에 대해 반복 작업을 수행하고 잠그도록 코드를 수정할 수 있습니다.
### 워크시트를 보호하기 위해 비밀번호를 추가할 수 있나요?
네, 전화할 때 비밀번호를 지정할 수 있습니다.`Protect()` 사용자가 올바른 비밀번호 없이 시트 보호를 해제하는 것을 제한하는 방법입니다.
### 셀 대신 특정 행이나 열을 보호할 수 있나요?
 예, Aspose.Cells를 사용하면 행 또는 열을 수정하여 전체 행이나 열을 잠글 수 있습니다.`IsLocked` 행이나 열에 대한 속성은 셀을 잠그는 방법과 유사합니다.
### 워크시트의 보호를 해제하려면 어떻게 해야 하나요?
 워크시트 보호를 해제하려면 다음을 사용하세요.`Unprotect()` 보호 중에 비밀번호가 설정된 경우 선택적으로 비밀번호를 제공하는 방법입니다.
### Aspose.Cells를 수식이나 차트 추가 등 다른 Excel 조작에도 사용할 수 있나요?
물론입니다! Aspose.Cells는 수식 추가, 차트 생성 등을 포함한 광범위한 Excel 작업을 수행할 수 있는 강력한 라이브러리입니다.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
