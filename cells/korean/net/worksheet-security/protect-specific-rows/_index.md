---
title: Aspose.Cells를 사용하여 워크시트의 특정 행 보호
linktitle: Aspose.Cells를 사용하여 워크시트의 특정 행 보호
second_title: Aspose.Cells .NET Excel 처리 API
description: 이 단계별 가이드를 통해 Aspose.Cells for .NET을 사용하여 Excel 워크시트의 특정 행을 보호하는 방법을 알아보세요. 데이터를 효과적으로 보호하세요.
weight: 16
url: /ko/net/worksheet-security/protect-specific-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells를 사용하여 워크시트의 특정 행 보호

## 소개
이 튜토리얼에서는 Aspose.Cells for .NET을 사용하여 Excel 워크시트에서 특정 행을 보호하는 과정을 안내합니다. 각 단계를 자세히 살펴보고, 필수 구성 요소를 다루고, 필요한 패키지를 가져오고, 코드를 따라하기 쉬운 지침으로 분해합니다. 마지막에는 자신의 애플리케이션에서 행 보호를 적용하는 지식을 갖추게 됩니다.
## 필수 조건
구현에 들어가기 전에 이 튜토리얼을 따라가기 위해 충족해야 할 몇 가지 전제 조건이 있습니다.
1. Aspose.Cells for .NET: Aspose.Cells for .NET을 설치해야 합니다. 아직 설치하지 않았다면 Aspose 웹사이트를 방문하여 최신 버전을 받을 수 있습니다.
2. C# 및 .NET에 대한 기본 이해: 이 튜토리얼은 여러분이 C#에 익숙하고 .NET 프로그래밍에 대한 기본 지식이 있다고 가정합니다. 이러한 것에 익숙하지 않다면 먼저 몇 가지 소개 리소스를 확인해 보는 것이 좋습니다.
3. Visual Studio 또는 .NET IDE: 코드를 실행하려면 Visual Studio와 같은 통합 개발 환경(IDE)이 필요합니다. 여기에는 필요한 모든 도구와 디버깅 기능이 제공됩니다.
4. Aspose.Cells 라이선스: 평가판 버전 제한을 피하려면 유효한 Aspose.Cells 라이선스가 있는지 확인하세요. 방금 시작했다면 임시 라이선스를 사용할 수도 있습니다.
 Aspose.Cells 및 설치에 대한 자세한 내용은 다음을 확인하세요.[선적 서류 비치](https://reference.aspose.com/cells/net/).
## 패키지 가져오기
Aspose.Cells를 사용하려면 C# 프로젝트에서 필요한 네임스페이스를 가져와야 합니다. 이러한 네임스페이스는 Excel 파일을 조작하는 데 필요한 클래스와 메서드에 대한 액세스를 제공합니다.
필요한 네임스페이스를 가져오는 방법은 다음과 같습니다.
```csharp
using System.IO;
using Aspose.Cells;
```
이러한 가져오기는 Aspose.Cells의 기능에 액세스할 수 있게 해주고 .NET 프로젝트에서 Excel 파일과 상호 작용할 수 있게 해주므로 중요합니다.
이제 필수 구성 요소를 설정하고 필요한 가져오기를 제자리에 두었으므로 실제 코드를 살펴볼 시간입니다. 명확성을 보장하기 위해 프로세스를 여러 단계로 나눕니다.
## 1단계: 프로젝트 디렉토리 설정
어떤 프로그램에서든 파일을 정리하는 것이 핵심입니다. 먼저, 워크북을 저장할 수 있는 디렉토리를 만들어 보겠습니다. 디렉토리가 있는지 확인하고 필요하면 만듭니다.
```csharp
// 문서 디렉토리의 경로를 정의합니다.
string dataDir = "Your Document Directory";
// 디렉토리가 없으면 디렉토리를 생성합니다.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
여기서 Excel 파일을 저장할 경로를 정의합니다. 폴더가 없으면 만듭니다. 이 단계는 통합 문서에 저장할 장소가 있는지 확인하는 데 중요합니다.
## 2단계: 새 통합 문서 만들기
 다음으로, 다음을 사용하여 새 통합 문서를 만듭니다.`Workbook` 클래스. 이 클래스는 Excel 파일 작업에 필요한 모든 기능을 제공합니다.
```csharp
// 새로운 통합 문서를 만듭니다.
Workbook wb = new Workbook();
```
이 시점에서 우리는 이제 작업할 새로운 통합 문서가 있습니다.
## 3단계: 워크시트에 액세스
이제 새로 만든 워크북의 첫 번째 워크시트에 액세스합니다. 워크북에는 여러 워크시트가 포함될 수 있지만 이 경우 첫 번째 워크시트에 집중합니다.
```csharp
// 워크시트 개체를 만들고 첫 번째 시트를 가져옵니다.
Worksheet sheet = wb.Worksheets[0];
```
 여기,`Worksheets[0]` 통합 문서의 첫 번째 워크시트를 나타냅니다(0부터 인덱싱됨).
## 4단계: 모든 열 잠금 해제
Excel에서 시트가 보호되면 셀은 기본적으로 잠깁니다. 특정 행을 보호하려면 먼저 열을 잠금 해제해야 합니다. 이 단계에서는 모든 열을 반복하여 잠금을 해제합니다.
```csharp
// 스타일 객체를 정의합니다.
Style style;
// 스타일 플래그 객체를 정의합니다.
StyleFlag flag;
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
여기서 우리는 0에서 255까지의 열(Excel 워크시트의 총 열 수)을 살펴보고 잠금을 해제합니다. 이렇게 하면 보호하려는 행은 여전히 상호 작용할 수 있지만 다른 행은 잠긴 상태로 유지됩니다.
## 5단계: 첫 번째 행 잠금
이제 모든 열이 잠금 해제되었으므로 행을 보호하는 단계로 넘어갈 수 있습니다. 이 단계에서는 첫 번째 행을 잠그고 시트가 보호되면 편집할 수 없게 됩니다.
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
이 코드는 첫 번째 행을 잠그어 시트에 보호 기능을 적용한 후에도 보호 상태가 유지되도록 합니다.
## 6단계: 워크시트 보호
이제 워크시트를 보호할 준비가 되었습니다. 이 단계에서는 보호 설정을 전체 워크시트에 적용하여 잠긴 셀을 편집할 수 없도록 합니다.
```csharp
// 시트를 보호하세요.
sheet.Protect(ProtectionType.All);
```
 사용하여`ProtectionType.All`우리는 명시적으로 잠금 해제된 셀(열과 같은)을 제외한 모든 셀이 보호되도록 합니다. 이것은 워크시트에 보호를 적용하는 단계입니다.
## 7단계: Excel 파일 저장
마지막으로 보호를 적용한 후 통합 문서를 저장합니다. 파일을 저장할 형식을 지정할 수 있습니다. 이 예에서는 통합 문서를 Excel 97-2003 파일로 저장합니다.
```csharp
// Excel 파일을 저장합니다.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
이 단계에서는 지정된 경로에 파일을 저장해서 워크시트의 특정 행을 보호하는 작업을 완료합니다.
## 결론
Aspose.Cells for .NET을 사용하여 Excel 워크시트의 특정 행을 보호하는 것은 단계별로 나누어 보면 간단한 프로세스입니다. 열 잠금 해제, 특정 행 잠금 및 보호 설정 적용을 통해 데이터가 안전하게 유지되고 필요한 경우에만 편집할 수 있습니다. 이 튜토리얼에서는 프로젝트 디렉터리 설정부터 최종 통합 문서 저장까지 모든 주요 단계를 다루었습니다.
템플릿, 보고서 또는 대화형 스프레드시트를 만들든 행 보호를 사용하면 데이터를 제어하는 간단하면서도 효과적인 방법입니다. 자신의 프로젝트에서 이 프로세스를 시도하고 Aspose.Cells for .NET의 모든 잠재력을 살펴보세요.
## 자주 묻는 질문
### 워크시트에서 여러 행을 보호할 수 있나요?  
네, 루프를 수정하거나 다른 행에 스타일을 적용하여 동일한 보호 단계를 여러 행에 적용할 수 있습니다.
### 시트를 보호하기 전에 어떤 열도 잠금 해제하지 않으면 어떻게 되나요?  
열의 잠금을 해제하지 않으면 시트가 보호될 때 열이 잠기고 사용자는 해당 열과 상호 작용할 수 없습니다.
### 전체 열 대신 특정 셀의 잠금을 해제하려면 어떻게 해야 하나요?  
 특정 셀의 스타일을 액세스하고 설정하여 잠금을 해제할 수 있습니다.`IsLocked` 재산에`false`.
### 이 방법을 사용하면 워크시트 전체를 보호할 수 있나요?  
네, 모든 셀에 보호를 적용하고 아무 셀도 잠금 해제하지 않으면 전체 워크시트를 보호할 수 있습니다.
### 워크시트의 보호를 해제하려면 어떻게 해야 하나요?  
 보호를 제거하려면 다음을 호출하세요.`Unprotect`워크시트에 방법을 적용하고 보호 암호(설정된 경우)를 제공합니다.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
