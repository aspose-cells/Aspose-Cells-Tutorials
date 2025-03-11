---
title: Aspose.Cells를 사용하여 통합 문서 내에서 데이터 복사
linktitle: Aspose.Cells를 사용하여 통합 문서 내에서 데이터 복사
second_title: Aspose.Cells .NET Excel 처리 API
description: 단계별 가이드, 코드 샘플 및 유용한 팁을 통해 Aspose.Cells for .NET을 사용하여 Excel 통합 문서 내에서 데이터를 효율적으로 복사하는 방법을 알아보세요.
weight: 12
url: /ko/net/worksheet-value-operations/copy-data-within-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells를 사용하여 통합 문서 내에서 데이터 복사

## 소개
Excel 통합 문서 내에서 데이터를 관리하는 것은 많은 애플리케이션의 핵심 부분입니다. 필수 데이터로 채워진 템플릿이나 시트가 있고, 나중에 사용하기 위해 동일한 통합 문서 내에서 복제하고 싶다고 상상해 보세요. 여기서 Aspose.Cells for .NET이 빛을 발합니다! 이 가이드에서는 Aspose.Cells를 사용하여 동일한 통합 문서 내에서 데이터를 복사하는 방법을 친절하고 명확한 단계별 자습서와 함께 안내해 드리겠습니다.
## 필수 조건
코딩에 들어가기 전에 이 작업을 완료하는 데 필요한 모든 것이 있는지 확인해 보겠습니다.
1.  .NET 라이브러리용 Aspose.Cells – 최신 버전을 다운로드하세요.[.NET용 Aspose.Cells 다운로드 페이지](https://releases.aspose.com/cells/net/).
2. 개발 환경 – Visual Studio와 같은 .NET 호환 IDE가 필요합니다.
3.  라이센스 – Aspose.Cells에 대한 무료 평가판 또는 구매한 라이센스를 사용합니다. 임시 라이센스를 받을 수 있습니다.[여기](https://purchase.aspose.com/temporary-license/) 또는 구매 옵션을 살펴보세요[여기](https://purchase.aspose.com/buy).
## 패키지 가져오기
코드에서 Aspose.Cells를 가져와서 해당 클래스와 메서드를 활용해야 합니다.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
코드로 들어가 봅시다! Aspose.Cells for .NET을 사용하여 통합 문서 내에서 데이터를 복사하는 작업을 쉽게 따를 수 있는 단계로 나누어 보겠습니다.
## 1단계: 디렉토리 경로 설정
통합 문서를 처리하기 전에 파일의 위치와 출력을 저장할 위치를 정의해 보겠습니다. 디렉토리 경로를 설정하면 모든 것이 체계적으로 정리됩니다.
```csharp
// 문서의 디렉토리 경로를 설정합니다.
string dataDir = "Your Document Directory";
string inputPath = dataDir + "book1.xls";
```
 여기서 교체하세요`"Your Document Directory"` 통합 문서가 저장된 실제 경로와 함께. 이 경로 변수를 사용하면 입력 및 출력 파일을 쉽게 참조할 수 있습니다.
## 2단계: 기존 Excel 파일 열기
Excel 파일을 사용하려면 Aspose.Cells의 workbook 객체에 로드해야 합니다. 이 단계에서는 데이터를 복사할 파일을 엽니다.
```csharp
// 기존 Excel 파일을 엽니다.
Workbook wb = new Workbook(inputPath);
```
 이로써 우리의`Workbook` 물체`wb` 이제 콘텐츠와 상호 작용할 준비가 되었습니다.`book1.xls`.
## 3단계: 워크시트 컬렉션에 액세스
 이제 워크북이 열렸으므로 워크시트 모음에 액세스하겠습니다.`WorksheetCollection` 클래스를 사용하면 통합 문서 내에서 여러 시트를 작업할 수 있습니다.
```csharp
// 통합 문서의 모든 시트를 참조하는 Worksheets 개체를 만듭니다.
WorksheetCollection sheets = wb.Worksheets;
```
 여기,`sheets` 통합 문서의 각 시트를 조작할 수 있게 되며, 기존 시트의 복사본을 추가할 수도 있습니다.
## 4단계: 새 시트에 데이터 복사
작업의 주요 부분은 한 시트의 내용을 같은 통합 문서 내의 새 시트로 복사하는 것입니다. 이 예에서는 "Sheet1"의 데이터를 새 시트로 복사합니다.
```csharp
// 통합 문서 내의 새 시트에 "Sheet1"의 데이터를 복사합니다.
sheets.AddCopy("Sheet1");
```
 그만큼`AddCopy`메서드는 지정된 시트의 정확한 복사본을 만들어 통합 문서에 추가합니다. 여기서는 "Sheet1"을 복제합니다. 복사하려는 시트의 이름을 지정할 수 있습니다.
## 5단계: 새 시트로 통합 문서 저장
시트를 복사한 후에는 변경 내용을 유지하려면 통합 문서를 새 이름이나 새 위치에 저장하세요.
```csharp
// 복사한 데이터로 통합 문서를 저장합니다.
wb.Save(dataDir + "CopyWithinWorkbook_out.xls");
```
 이 줄은 수정된 통합 문서를 다음과 같이 저장합니다.`CopyWithinWorkbook_out.xls` 지정된 디렉토리에 있습니다.
## 결론
그리고 이제 알게 되었습니다! Aspose.Cells for .NET을 사용하여 통합 문서 내에서 데이터를 복사하는 것은 아주 간단합니다. Aspose.Cells를 사용하면 Excel 파일을 간단하게 처리할 수 있으며 복잡한 데이터 관리 작업을 손쉽게 수행할 수 있습니다. 템플릿 사용, 백업 또는 새 버전 생성을 위해 시트를 복제해야 하는 경우, 다룬 단계가 목표를 달성하는 데 도움이 될 것입니다.
 더 자세히 알아보고 싶다면 다음을 확인하세요.[Aspose.Cells 설명서](https://reference.aspose.com/cells/net/) 고급 기능과 성능을 위해.
## 자주 묻는 질문
### 한 번에 여러 장을 복사할 수 있나요?
Aspose.Cells에서는 한 번의 호출로 여러 시트를 복사하는 기능은 지원하지 않지만, 복제하려는 시트를 순환하여 개별적으로 복사할 수 있습니다.
### 복사한 시트의 이름을 바꿀 수 있나요?
 네, 시트를 복사한 후 다음을 사용하여 이름을 바꿀 수 있습니다.`sheets[sheets.Count - 1].Name = "NewSheetName";`.
### Aspose.Cells는 .NET Core와 호환됩니까?
물론입니다! Aspose.Cells는 .NET Framework와 .NET Core 환경을 모두 지원합니다.
### 시트를 복사하는 동안 서식을 어떻게 처리합니까?
 그만큼`AddCopy` 이 방법을 사용하면 모든 내용과 서식이 보존되므로 복사한 시트는 원본과 똑같아 보입니다.
### 시트를 다른 통합 문서에 복사하려면 어떻게 해야 하나요?
당신은 사용할 수 있습니다`Copy` 다른 통합 문서에 대한 참조가 있는 방법, 예:`sheets.Add().Copy(wb.Worksheets["Sheet1"]);`.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
