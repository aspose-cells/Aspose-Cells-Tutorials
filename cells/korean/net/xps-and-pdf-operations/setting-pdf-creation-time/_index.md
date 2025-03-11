---
title: .NET에서 PDF 생성 시간 설정
linktitle: .NET에서 PDF 생성 시간 설정
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells를 사용하여 .NET에서 PDF 생성 시간을 설정하는 방법을 알아보세요. Excel에서 PDF로의 원활한 변환을 위한 단계별 가이드를 따르세요.
weight: 11
url: /ko/net/xps-and-pdf-operations/setting-pdf-creation-time/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET에서 PDF 생성 시간 설정

## 소개
오늘날의 디지털 시대에 문서를 다양한 형식으로 변환하는 기능은 많은 애플리케이션에 필수적입니다. 일반적인 요구 사항 중 하나는 Excel 스프레드시트를 PDF 파일로 변환하는 것입니다. 이렇게 하면 서식이 유지될 뿐만 아니라 공유 및 인쇄가 훨씬 쉬워집니다. .NET으로 작업하는 개발자라면 Aspose.Cells는 이 프로세스를 단순화하는 환상적인 라이브러리입니다. 이 튜토리얼에서는 Aspose.Cells for .NET을 사용하여 Excel 파일을 PDF로 변환할 때 PDF 생성 시간을 설정하는 방법을 살펴보겠습니다.
## 필수 조건
코드의 세부 사항을 살펴보기에 앞서, 시작하는 데 필요한 모든 것이 있는지 확인해 보겠습니다.
### 당신에게 필요한 것
1. Visual Studio: 컴퓨터에 Visual Studio가 설치되어 있는지 확인하세요. 이것이 개발 환경이 됩니다.
2.  .NET용 Aspose.Cells: Aspose.Cells 라이브러리를 다음에서 다운로드하세요.[웹사이트](https://releases.aspose.com/cells/net/). 무료 체험판을 통해 기능을 테스트해 볼 수도 있습니다.
3. C#에 대한 기본 지식: C# 프로그래밍에 익숙하면 코드 조각을 더 잘 이해하는 데 도움이 됩니다.
4.  Excel 파일: 변환할 Excel 파일을 준비하세요. 이 예에서는 다음 이름의 파일을 사용하겠습니다.`Book1.xlsx`.
이제 필수 구성 요소를 정리했으니, 재밌는 부분, 즉 필요한 패키지를 가져오고 코드를 작성해 보겠습니다!
## 패키지 가져오기
시작하려면 C# 파일에 필요한 네임스페이스를 가져와야 합니다. 이는 Aspose.Cells 라이브러리에서 제공하는 클래스와 메서드에 액세스할 수 있게 해주므로 매우 중요합니다.
### C# 프로젝트 열기
Visual Studio를 열고 PDF 변환 기능을 구현할 새 프로젝트를 만들거나 기존 프로젝트를 엽니다.
### Aspose.Cells 참조 추가
솔루션 탐색기에서 프로젝트를 마우스 오른쪽 버튼으로 클릭하고 "NuGet 패키지 관리"를 선택한 다음 "Aspose.Cells"를 검색하여 Aspose.Cells 라이브러리를 프로젝트에 추가할 수 있습니다. 패키지를 설치합니다.
### 네임스페이스 가져오기
C# 파일의 맨 위에 다음 네임스페이스를 포함하세요.
```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Charts;
```
이러한 네임스페이스를 사용하면 Workbook 클래스와 기타 필수 기능에 액세스할 수 있습니다.

이제 패키지를 가져왔으니, 생성 시간을 설정하면서 Excel 파일을 PDF로 변환하는 과정을 분석해 보겠습니다.
## 1단계: 문서 디렉토리 정의
먼저, 문서가 저장된 디렉토리를 지정해야 합니다. 이는 Excel 파일이 있는 위치이며 출력 PDF가 저장되는 위치입니다.
```csharp
string dataDir = "Your Document Directory"; // 문서 디렉토리를 지정하세요
```
 바꾸다`"Your Document Directory"` 실제 경로와 함께`Book1.xlsx` 파일이 위치해 있습니다. 이 경로는 애플리케이션이 처리할 파일을 찾는 데 도움이 됩니다.
## 2단계: Excel 파일 로드
 다음으로 Excel 파일을 로드합니다.`Workbook` 객체. Aspose.Cells가 빛나는 부분은 Excel 파일을 손쉽게 작업할 수 있게 해주기 때문입니다.
```csharp
string inputPath = dataDir + "Book1.xlsx"; // Excel 파일에 대한 경로
Workbook workbook = new Workbook(inputPath); // Excel 파일을 로드합니다
```
 그만큼`Workbook` 클래스는 Excel 파일을 로드하고 조작하는 데 사용됩니다. 입력 경로를 전달하면 애플리케이션에 어떤 파일을 작업할지 알려주는 것입니다.
## 3단계: PdfSaveOptions 만들기
 이제 인스턴스를 생성할 시간입니다.`PdfSaveOptions`이 클래스를 사용하면 생성 시간을 포함하여 통합 문서를 PDF로 저장하기 위한 다양한 옵션을 지정할 수 있습니다.
```csharp
PdfSaveOptions options = new PdfSaveOptions(); // PdfSaveOptions 인스턴스 생성
options.CreatedTime = DateTime.Now; // 생성 시간을 지금으로 설정하세요
```
 설정하여`options.CreatedTime` 에게`DateTime.Now`, PDF가 생성된 현재 날짜와 시간이 반영되도록 하는 것입니다.
## 4단계: 통합 문서를 PDF로 저장
마지막으로, 방금 정의한 옵션을 사용하여 통합 문서를 PDF 파일로 저장합니다.
```csharp
workbook.Save(dataDir + "output.pdf", options); //PDF로 저장
```
 이 코드 줄은 통합 문서를 가져와 지정된 위치에 PDF 형식으로 저장합니다.`options` 매개변수는 PDF 메타데이터에 생성 시간을 포함하기 위해 전달됩니다.

## 결론
이제 다 됐습니다! Aspose.Cells for .NET을 사용하여 Excel 파일을 PDF로 성공적으로 변환했습니다. 생성 타임스탬프도 포함되었습니다. 이 기능은 문서 버전을 추적해야 하거나 수신자에게 문서가 생성된 시점에 대한 정보를 제공해야 할 때 매우 유용할 수 있습니다.
 Aspose.Cells의 더 많은 기능을 탐색하려면 주저하지 말고 다음을 확인하세요.[선적 서류 비치](https://reference.aspose.com/cells/net/).
## 자주 묻는 질문
### Aspose.Cells란 무엇인가요?
Aspose.Cells는 개발자가 Excel 파일을 만들고, 조작하고, 변환할 수 있는 강력한 .NET용 라이브러리입니다.
### Aspose.Cells를 무료로 사용할 수 있나요?
 네, 무료 체험판을 통해 시작할 수 있습니다.[Aspose 웹사이트](https://releases.aspose.com/).
### 다른 PDF 속성은 어떻게 설정하나요?
 다양한 PDF 속성을 설정할 수 있습니다.`PdfSaveOptions` 페이지 크기, 압축 등과 같은 클래스입니다.
### 한 번에 여러 개의 Excel 파일을 변환할 수 있나요?
네, 파일 목록을 순환하여 각 파일에 동일한 변환 프로세스를 적용할 수 있습니다.
### Aspose.Cells에 대한 지원은 어디서 받을 수 있나요?
 Aspose 커뮤니티에서 지원을 받을 수 있습니다.[지원 포럼](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
