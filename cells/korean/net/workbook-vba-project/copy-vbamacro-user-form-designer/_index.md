---
title: Aspose.Cells를 사용하여 VBAMacro 사용자 양식 디자이너 저장소를 통합 문서로 복사
linktitle: Aspose.Cells를 사용하여 VBAMacro 사용자 양식 디자이너 저장소를 통합 문서로 복사
second_title: Aspose.Cells .NET Excel 처리 API
description: 포괄적인 단계별 튜토리얼을 통해 Aspose.Cells for .NET에서 VBA 매크로 사용자 양식 디자이너를 효율적으로 복사하는 방법을 알아보세요! Excel의 잠재력을 잠금 해제하세요.
weight: 11
url: /ko/net/workbook-vba-project/copy-vbamacro-user-form-designer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells를 사용하여 VBAMacro 사용자 양식 디자이너 저장소를 통합 문서로 복사

## 소개
환영합니다! VBA 매크로와 사용자 양식으로 Excel 경험을 향상시키고 싶다면, 당신은 올바른 곳에 있습니다! 이 가이드에서는 Aspose.Cells for .NET을 사용하여 VBA 매크로 사용자 양식 디자이너를 한 통합 문서에서 다른 통합 문서로 원활하게 복사하는 방법을 알아봅니다. 노련한 개발자이든 방금 시작한 개발자이든, 우리는 모든 중요한 단계를 안내해 드립니다. 이 가이드를 Excel 파일을 프로그래밍 방식으로 처리하는 기술을 마스터하기 위한 플레이북으로 생각하세요. 시작할 준비가 되셨나요? 시작해 봅시다!
## 필수 조건
코딩의 핵심을 알아보기 전에 먼저 필요한 모든 것이 있는지 확인해 보겠습니다.
1. C# 개발 환경: C# 개발을 위한 작업 환경이 준비되어 있어야 합니다. Visual Studio를 적극 권장합니다.
2.  .NET 라이브러리용 Aspose.Cells: Aspose.Cells 라이브러리가 프로젝트에 통합되어 있는지 확인하세요. 쉽게[여기서 다운로드하세요](https://releases.aspose.com/cells/net/).
3. VBA와 Excel 매크로에 대한 기본 지식: VBA와 Excel 매크로의 작동 방식을 잘 이해하면 이 튜토리얼을 쉽게 탐색하는 데 도움이 됩니다.
4. 사용자 양식이 포함된 Excel 파일: 사용자 양식이 포함된 Excel 통합 문서를 실험하거나 만들거나 가져오려면 매크로가 활성화된 것이 좋습니다(예:`.xlsm` 파일).
## 패키지 가져오기
C# 프로젝트에서 Aspose.Cells 기능을 활용하려면 파일 맨 위에 특정 네임스페이스를 가져와야 합니다. 방법은 다음과 같습니다.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Vba;
```
이러한 네임스페이스를 포함하면 Aspose.Cells 라이브러리에 내장된 모든 강력한 도구에 액세스할 수 있습니다. 
이제 필수 구성 요소와 패키지를 다루었으니, 이제 재밌는 부분인 코딩으로 넘어갈 시간입니다! 단계별로 나누어 보겠습니다.
## 1단계: 소스 및 출력 디렉토리 정의
먼저, 파일이 어디에 있는지 확인해야 합니다.
```csharp
// 소스 디렉토리
string sourceDir = "Your Document Directory";
// 출력 디렉토리
string outputDir = "Your Document Directory";
```
 여기서 교체하세요`"Your Document Directory"` 파일이 저장된 실제 경로와 함께. 여기서 소스 통합 문서(사용자 양식 포함)를 가져오고 새 통합 문서가 저장되는 곳입니다.
## 2단계: 빈 대상 워크북 만들기
다음으로, 사용자 양식과 매크로를 복사할 대상 통합 문서를 만들어 보겠습니다.
```csharp
// 빈 대상 워크북 만들기
Workbook target = new Workbook();
```
이 코드 줄은 우리가 데이터를 채울 수 있는 새롭고 빈 워크북을 초기화합니다. 걸작을 위한 빈 캔버스라고 생각하세요!
## 3단계: 템플릿 워크북 로드
사용자 양식과 매크로가 포함된 통합 문서를 로드해야 합니다.
```csharp
// VBA-매크로 디자이너 사용자 양식이 포함된 Excel 파일을 로드합니다.
Workbook templateFile = new Workbook(sourceDir + "sampleDesignerForm.xlsm");
```
 변경을 꼭 해주세요`"sampleDesignerForm.xlsm"` 실제 파일 이름으로. 이 워크북은 요리책과 같습니다. 재료를 가져올 곳이죠!
## 4단계: 워크시트를 대상 워크북으로 복사
이제 템플릿에서 대상 통합 문서로 워크시트를 복사해 보겠습니다.
```csharp
// 모든 템플릿 워크시트를 대상 통합 문서로 복사
foreach (Worksheet ws in templateFile.Worksheets)
{
    if (ws.Type == SheetType.Worksheet)
    {
        Worksheet s = target.Worksheets.Add(ws.Name);
        s.Copy(ws);
        // 대상 워크시트의 A2 셀에 메시지를 넣으세요.
        s.Cells["A2"].PutValue("VBA Macro and User Form copied from template to target.");
    }
}
```
이 단계에서는 템플릿의 각 워크시트를 반복해서 살펴보고 대상 워크북에 복사합니다. 생각해 보면, 최고의 레시피를 한 요리책에서 다른 요리책으로 옮기는 것과 같습니다!
## 5단계: 템플릿에서 VBA 매크로 복사
다음으로, UserForm Designer 모듈을 포함한 VBA 매크로를 새 통합 문서에 복사해 보겠습니다.
```csharp
// 템플릿에서 대상으로 VBA-매크로 디자이너 사용자 양식 복사
foreach (VbaModule vbaItem in templateFile.VbaProject.Modules)
{
    if (vbaItem.Name == "ThisWorkbook")
    {
        // 이 워크북 모듈 코드 복사
        target.VbaProject.Modules["ThisWorkbook"].Codes = vbaItem.Codes;
    }
    else
    {
        // 다른 모듈의 코드와 데이터를 복사합니다.
        System.Diagnostics.Debug.Print(vbaItem.Name);
        int vbaMod = 0;
        Worksheet sheet = target.Worksheets.GetSheetByCodeName(vbaItem.Name);
        if (sheet == null)
        {
            vbaMod = target.VbaProject.Modules.Add(vbaItem.Type, vbaItem.Name);
        }
        else
        {
            vbaMod = target.VbaProject.Modules.Add(sheet);
        }
        target.VbaProject.Modules[vbaMod].Codes = vbaItem.Codes;
        if ((vbaItem.Type == VbaModuleType.Designer))
        {
            // 사용자 폼 즉 디자이너 저장소의 데이터를 가져옵니다.
            byte[] designerStorage = templateFile.VbaProject.Modules.GetDesignerStorage(vbaItem.Name);
            // 대상 Vba 프로젝트에 디자이너 저장소 추가
            target.VbaProject.Modules.AddDesignerStorage(vbaItem.Name, designerStorage);
        }
    }
}
```
이 방대한 코드 덩어리는 템플릿 파일에서 각 VBA 모듈을 검사하는 것을 처리합니다. UserForm 디자인과 관련 코드를 복사하고 있습니다. 할머니의 유명한 파이 레시피뿐만 아니라 정확한 베이킹 기술도 얻을 수 있도록 하는 것과 같습니다!
## 6단계: 대상 워크북 저장
모든 사본을 완성한 후에는 열심히 작업한 결과를 저장할 차례입니다.
```csharp
// 대상 통합 문서 저장
target.Save(outputDir + "outputDesignerForm.xlsm", SaveFormat.Xlsm);
```
필요에 따라 출력 파일 이름을 수정해야 합니다. 저장하면 매크로와 사용자 양식이 가득한 통합 문서의 맞춤형 버전을 효과적으로 만드는 것입니다. 얼마나 신나는 일입니까?
## 7단계: 성공 확인
마지막으로 콘솔에 성공 메시지를 출력해 보겠습니다.
```csharp
Console.WriteLine("CopyVBAMacroUserFormDesignerStorageToWorkbook executed successfully.\r\n");
```
이 작은 선은 당신의 과정이 순조롭게 진행되었다는 것을 확신시켜줍니다. 그것은 당신의 코딩 선데이의 꼭대기에 있는 체리입니다!
## 결론
축하합니다! Aspose.Cells for .NET을 사용하여 VBA 매크로 사용자 양식 디자이너를 한 통합 문서에서 다른 통합 문서로 복사하는 단계별 가이드를 완료했습니다. 처음에는 약간 어려울 수 있지만 연습하면 프로처럼 통합 문서 조작을 처리할 수 있습니다. 코딩은 모두 연습에 관한 것이므로 Excel 파일에서 다양한 것을 시도하는 것을 꺼리지 마십시오. 질문이 있거나 문제가 발생하면 Aspose 포럼이나 지원 설명서를 자유롭게 확인하세요!
## 자주 묻는 질문
### Aspose.Cells는 어떤 버전의 Excel을 지원하나요?
Aspose.Cells는 XLSX, XLSM, CSV 등 다양한 Excel 형식을 지원합니다.
### Aspose.Cells를 무료로 사용할 수 있나요?
 네! 무료 체험판으로 시작할 수 있으며, 이를 통해 라이브러리를 평가할 수 있습니다.[무료 체험](https://releases.aspose.com/).
### 이 코드를 실행하려면 Visual Studio가 필요합니까?
사용자 친화적인 기능 때문에 적극 권장되지만, .NET 개발을 지원하는 한 어떤 C# IDE라도 괜찮습니다.
### 더 많은 예와 문서는 어디에서 볼 수 있나요?
 탐색할 수 있습니다[Aspose.Cells 문서](https://reference.aspose.com/cells/net/) 더 많은 예와 자세한 설명은 여기에서 확인하세요.
### Aspose.Cells를 사용하는 동안 문제를 해결하려면 어떻게 해야 하나요?
 당신은 방문해야합니다[Aspose 지원 포럼](https://forum.aspose.com/c/cells/9) 커뮤니티와 Aspose 지원 직원에게 도움을 요청하세요.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
