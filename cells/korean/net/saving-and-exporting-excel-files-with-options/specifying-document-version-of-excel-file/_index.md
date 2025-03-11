---
title: .NET에서 Excel 파일의 문서 버전을 프로그래밍 방식으로 지정
linktitle: .NET에서 Excel 파일의 문서 버전을 프로그래밍 방식으로 지정
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET을 사용하여 단계별 지침을 통해 Excel 파일에서 버전, 작성자, 제목과 같은 문서 속성을 프로그래밍 방식으로 지정하는 방법을 알아보세요.
weight: 12
url: /ko/net/saving-and-exporting-excel-files-with-options/specifying-document-version-of-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET에서 Excel 파일의 문서 버전을 프로그래밍 방식으로 지정

## 소개
Aspose.Cells for .NET은 개발자가 Excel 파일을 쉽게 프로그래밍 방식으로 조작할 수 있는 강력한 라이브러리입니다. 처음부터 Excel 파일을 만들거나 기존 파일을 수정하려는 경우 Aspose.Cells는 목표를 달성하기 위한 포괄적인 API를 제공합니다. 그러한 기능 중 하나는 버전, 작성자 또는 제목과 같은 문서 속성을 지정하는 것입니다. 이 튜토리얼에서는 Aspose.Cells for .NET을 사용하여 Excel 파일의 문서 버전을 프로그래밍 방식으로 지정하는 방법을 안내합니다.
## 필수 조건
자세한 내용을 살펴보기 전에 이 튜토리얼을 따라가는 데 필요한 모든 것이 있는지 확인해 보겠습니다.
1. .NET용 Aspose.Cells: 최신 버전을 다운로드할 수 있습니다.[여기](https://releases.aspose.com/cells/net/) 아직 라이센스를 구매하지 않은 경우 다음을 선택할 수 있습니다.[임시 면허](https://purchase.aspose.com/temporary-license/) 기능을 탐색해보세요.
2. .NET 개발 환경: Visual Studio나 .NET과 호환되는 IDE를 사용할 수 있습니다.
3. C#에 대한 기본 지식: C# 프로그래밍에 대한 이해가 있으면 따라하기가 더 쉽습니다.
## 패키지 가져오기
코딩을 시작하기 전에 Aspose.Cells 라이브러리에서 필요한 네임스페이스를 가져와야 합니다. 그러면 Excel 파일 조작에 필요한 클래스와 메서드에 액세스할 수 있습니다.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
이 두 네임스페이스는 통합 문서와 기본 제공 문서 속성과 상호 작용하는 데 필수적입니다.
이제 버전, 제목, 작성자를 비롯한 Excel 파일에서 문서 속성을 지정하는 과정을 살펴보겠습니다.
## 1단계: 통합 문서 개체 초기화
 첫 번째 단계는 새 인스턴스를 만드는 것입니다.`Workbook` 객체. 이 객체는 작업할 전체 Excel 파일을 나타냅니다.
```csharp
Workbook wb = new Workbook();
```
 그만큼`Workbook`클래스는 Excel 파일의 표현을 제공합니다. 이를 인스턴스화하여 조작할 수 있는 빈 Excel 통합 문서를 만듭니다.
## 2단계: 내장 문서 속성에 액세스
 Aspose.Cells는 제목, 작성자, 문서 버전과 같은 필드를 포함하는 내장 문서 속성을 제공합니다. 이러한 속성은 다음을 통해 액세스할 수 있습니다.`BuiltInDocumentProperties`수집.
```csharp
Aspose.Cells.Properties.BuiltInDocumentPropertyCollection bdpc = wb.BuiltInDocumentProperties;
```
 그만큼`BuiltInDocumentPropertyCollection` 클래스는 제목, 작성자 및 일반적으로 문서와 관련된 다른 메타데이터와 같은 기본 제공 문서 속성 컬렉션에 대한 액세스를 제공합니다.
## 3단계: Excel 문서 제목 설정
다음으로, Excel 문서의 제목을 설정합니다. 이 메타데이터는 나중에 파일을 식별하고 관리하는 데 도움이 됩니다.
```csharp
bdpc.Title = "Aspose File Format APIs";
```
제목을 설정하는 것은 문서 구성에 중요합니다. 이 메타데이터는 파일 속성에서 볼 수 있으며 외부 시스템에서 문서를 더 효과적으로 카탈로그화하거나 식별하는 데 사용할 수 있습니다.
## 4단계: 작성자 지정
문서 작성자는 파일을 만든 사람이나 수정한 사람을 나타내도록 지정할 수도 있습니다.
```csharp
bdpc.Author = "Aspose APIs Developers";
```
이 단계는 문서 관리나 협업 시나리오에 대한 추가 메타데이터를 제공하여 문서를 작성자에게 귀속시키는 데 도움이 됩니다.
## 5단계: 문서 버전 지정
이 튜토리얼에서 다루는 가장 중요한 속성 중 하나는 문서 버전입니다. 이 단계에서는 문서 버전을 지정할 수 있으며, 이는 버전 제어가 필요한 환경에서 작업할 때 유용합니다.
```csharp
bdpc.DocumentVersion = "Aspose.Cells Version - 18.3";
```
문서 버전을 설정하면 파일을 만드는 데 사용된 문서 또는 라이브러리 버전에 대한 명확성을 제공합니다. 이는 특히 파일 개정 또는 다른 라이브러리 버전과의 호환성을 추적해야 하는 환경에서 중요합니다.
## 6단계: Excel 파일 저장
 마지막으로 방금 설정한 모든 속성과 함께 Excel 파일을 저장할 수 있습니다. Aspose.Cells를 사용하면 다양한 형식으로 파일을 저장할 수 있지만 이 예에서는 다음을 사용합니다.`.xlsx` 체재.
```csharp
wb.Save("outputSpecifyDocumentVersionOfExcelFile.xlsx", SaveFormat.Xlsx);
```
 그만큼`Save` 이 방법은 파일을 지정된 디렉토리에 저장하는 데 사용됩니다. 여기서는 Excel 파일로 저장합니다.`.xlsx`형식. 필요한 경우 Aspose.Cells는 다음과 같은 형식도 지원합니다.`.xls`, `.csv` , 그리고`.pdf`귀하의 프로젝트 요구 사항에 따라 유연성을 제공합니다.
## 결론
이 튜토리얼에서는 Aspose.Cells for .NET을 사용하여 Excel 파일에서 문서 속성, 특히 문서 버전을 지정하는 방법을 살펴보았습니다. Aspose.Cells는 Excel 파일을 프로그래밍 방식으로 조작할 수 있는 매우 유연하고 강력한 도구로, 스프레드시트로 작업하는 모든 .NET 개발자에게 큰 자산이 됩니다.
## 자주 묻는 질문
### Aspose.Cells를 사용하여 다른 기본 제공 속성을 수정할 수 있나요?  
네, 주제, 키워드, 댓글 등 다른 기본 제공 속성도 수정할 수 있습니다.
### Aspose.Cells는 어떤 파일 형식을 지원하나요?  
 Aspose.Cells는 다음을 포함한 다양한 형식을 지원합니다.`.xls`, `.xlsx`, `.csv`, `.pdf`, 그리고 더 많은 것들.
### Aspose.Cells for .NET을 사용하려면 라이선스가 필요합니까?  
 Aspose.Cells를 탐색할 수 있습니다.[무료 체험](https://releases.aspose.com/) 또는 신청하세요[임시 면허](https://purchase.aspose.com/temporary-license/) 확장된 테스트를 위해.
### 웹 애플리케이션에서 Aspose.Cells를 사용할 수 있나요?  
네, Aspose.Cells는 데스크톱과 웹 애플리케이션 모두에서 사용할 수 있습니다. 매우 다재다능하며 .NET 웹 프레임워크와 잘 통합됩니다.
### Aspose.Cells에 대한 지원은 어디서 받을 수 있나요?  
 커뮤니티와 지원에 액세스할 수 있습니다.[Aspose.Cells 지원 포럼](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
