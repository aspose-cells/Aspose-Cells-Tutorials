---
title: 워크북에서 내장된 Mol 파일 추출
linktitle: 워크북에서 내장된 Mol 파일 추출
second_title: Aspose.Cells .NET Excel 처리 API
description: 이 자세한 단계별 튜토리얼을 통해 Aspose.Cells for .NET을 사용하여 Excel 통합 문서에서 포함된 MOL 파일을 추출하는 방법을 알아보세요.
weight: 18
url: /ko/net/workbook-operations/extract-embedded-mol-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 워크북에서 내장된 Mol 파일 추출

## 소개
Excel 통합 문서 내에서 데이터를 관리할 때 표준 형식이 아닌 다양한 내장 개체를 마주치는 경우가 있습니다. 그러한 형식 중 하나는 MOL(Molecular Structure File)로, 화학에서 분자 정보를 나타내는 데 일반적으로 사용됩니다. Aspose.Cells for .NET을 사용하여 Excel 통합 문서에서 이러한 MOL 파일을 추출하려는 경우 올바른 가이드를 찾은 것입니다. 이 문서에서는 단계별로 프로세스를 안내하고 각 부분을 이해하기 쉽게 설명합니다.
## 필수 조건
코드에 뛰어들기 전에 필요한 기술과 도구가 있는지 확인하는 것이 중요합니다. 필요한 것은 다음과 같습니다.
1. .NET 프로그래밍에 대한 기본적인 이해: C# 및 .NET 프레임워크에 대해 알고 있어야 합니다.
2.  .NET용 Aspose.Cells: Aspose.Cells 라이브러리가 있는지 확인하세요.[여기서 다운로드하세요](https://releases.aspose.com/cells/net/).
3. IDE: Visual Studio나 기타 .NET 호환 IDE를 사용할 수 있습니다.
4. MOL 파일이 포함된 Excel 워크북: 이 튜토리얼에서는 MOL 개체가 포함된 Excel 파일이 필요합니다. 직접 만들거나 샘플 파일을 사용할 수 있습니다.
## 패키지 가져오기
시작하려면 프로젝트에 필요한 네임스페이스를 가져와야 합니다. 이는 Aspose.Cells 기능에 액세스하는 데 중요합니다. 다음은 이를 수행하는 방법입니다.

```csharp
using Aspose.Cells.Drawing;
using Aspose.Cells.WebExtensions;
using System;
using System.IO;
```

이러한 네임스페이스를 사용하면 통합 문서를 조작하고, 워크시트에 액세스하고, 일반적으로 파일을 작업할 수 있습니다.
이제 필수 구성 요소가 정리되었으니 코드를 살펴보고 Excel 통합 문서에서 내장된 MOL 파일을 추출하는 데 필요한 각 단계를 알아보겠습니다. 
## 1단계: 디렉토리 설정
첫 번째 단계는 소스 문서가 있는 위치와 추출된 MOL 파일을 저장할 위치를 정의하는 것입니다. 해당 디렉토리를 설정해 보겠습니다.
```csharp
string SourceDir = "Your Document Directory"; // 디렉토리 경로로 바꾸세요
string outputDir = "Your Document Directory"; // 출력 경로로 바꾸세요
```
 여기서, 당신은 대체합니다`"Your Document Directory"`실제 디렉토리로의 경로와 함께. 소스 및 출력 디렉토리가 모두 애플리케이션에서 액세스할 수 있는 것이 중요합니다.
## 2단계: 통합 문서 로드
디렉토리를 설정했으면 다음 작업은 Excel 통합 문서를 로드하는 것입니다. 지금 해보겠습니다.

```csharp
Workbook workbook = new Workbook(SourceDir + "EmbeddedMolSample.xlsx");
```

 우리는 인스턴스를 생성하고 있습니다`Workbook` 클래스와 Excel 파일 이름을 경로로 전달합니다.`EmbeddedMolSample.xlsx`. 이 단계에서는 통합 문서를 초기화하여 내용에 액세스할 수 있도록 합니다.
## 3단계: 워크시트 반복
이제 통합 문서가 로드되었으므로 통합 문서 내의 각 워크시트를 반복해야 합니다. 이렇게 하면 각 시트에서 내장된 개체를 검사할 수 있습니다.

```csharp
var index = 1; // 추출된 MOL 파일의 이름을 지정하는 데 사용됩니다.
foreach (Worksheet sheet in workbook.Worksheets)
{
    OleObjectCollection oles = sheet.OleObjects;
    // 추가 추출 논리는 여기에 있습니다.
}
```

 여기서는 다음을 사용하고 있습니다.`foreach` 워크시트를 탐색하려면 루프를 사용합니다. 각 워크시트에 대해 액세스합니다.`OleObjects` 모든 내장 객체를 포함하는 컬렉션입니다.
## 4단계: MOL 파일 추출
이제 중요한 부분인 OLE 개체에서 MOL 파일을 추출하는 단계입니다. 여기에는 워크시트 루프 내부에 또 다른 루프가 필요합니다.

```csharp
foreach (OleObject ole in oles)
{
    string fileName = outputDir + "OleObject" + index + ".mol ";
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
    index++;
}
```

 찾은 각 OLE 개체에 대해 출력 디렉토리에 새 파일을 만듭니다.`ObjectData` 의 속성`OleObject` 새로 만든 파일에 쓸 수 있는 내장 객체의 데이터를 보관합니다.`FileStream`. 파일 이름은 순차적으로 지정됩니다.`OleObject1.mol`, `OleObject2.mol` 등)을 기반으로`index` 변하기 쉬운.
## 5단계: 프로세스 완료 확인
마지막으로, 모든 MOL 파일이 추출되면 프로세스가 성공적으로 완료되었음을 사용자에게 알리는 것이 좋습니다.

```csharp
Console.WriteLine("ExtractEmbeddedMolFile executed successfully.");
```

이 줄은 단순히 콘솔에 메시지를 인쇄하여 추출이 성공했음을 알려줍니다. 사용자 피드백을 위한 좋은 터치입니다.
## 결론
이제 Aspose.Cells for .NET을 사용하여 Excel 통합 문서에서 임베디드 MOL 파일을 성공적으로 추출했습니다. 이 프로세스는 몇 가지 핵심 단계를 통합하여 임베디드 객체를 처리하는 데 구조화된 접근 방식을 보장합니다. 과학 연구, 화학 분석 또는 단순히 복잡한 데이터 세트를 처리하든 이러한 파일 유형을 추출하고 조작할 수 있다면 정보를 관리하는 방법에 상당한 차이를 만들 수 있습니다. 
## 자주 묻는 질문
### Excel에서 MOL 외에도 다른 파일 형식을 추출할 수 있나요?
네, 비슷한 기술을 사용해 다양한 다른 내장 파일 유형을 추출할 수 있습니다.
### Aspose.Cells는 무료로 사용할 수 있나요?
 Aspose.Cells는 상용 라이브러리이지만[기간 한정으로 무료로 체험해보세요](https://releases.aspose.com/).
### 이 방법이 모든 Excel 버전에서 적용되나요?
네, Aspose.Cells에서 파일 형식을 지원한다면 가능합니다.
### 이 추출 과정을 자동화할 수 있나요?
물론입니다! 예약된 작업이나 스크립트에 코드를 배치하여 이 프로세스를 자동화할 수 있습니다.
### Aspose.Cells에 대한 추가 문서는 어디에서 찾을 수 있나요?
 당신은 확인할 수 있습니다[Aspose.Cells 설명서](https://reference.aspose.com/cells/net/) 자세한 내용과 예를 확인하세요.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
