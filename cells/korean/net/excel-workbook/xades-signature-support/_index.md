---
title: Xades 서명 지원
linktitle: Xades 서명 지원
second_title: .NET API 참조를 위한 Aspose.Cells
description: 이 단계별 가이드를 통해 Aspose.Cells for .NET을 사용하여 Excel 파일에 Xades 서명을 추가하는 방법을 알아보세요. 문서를 보호하세요.
weight: 190
url: /ko/net/excel-workbook/xades-signature-support/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xades 서명 지원

## 소개

오늘날의 디지털 세계에서 문서 보안은 그 어느 때보다 중요합니다. 민감한 비즈니스 정보나 개인 데이터를 다루든 파일의 무결성과 신뢰성을 보장하는 것이 가장 중요합니다. 이를 달성하는 한 가지 방법은 디지털 서명, 특히 Xades 서명을 사용하는 것입니다. 애플리케이션에서 Xades 서명 지원을 구현하려는 .NET 개발자라면 올바른 위치에 있습니다! 이 가이드에서는 Aspose.Cells for .NET을 사용하여 Excel 파일에 Xades 서명을 추가하는 과정을 안내합니다. 그럼 바로 시작해 볼까요!

## 필수 조건

시작하기 전에 꼭 준비해야 할 몇 가지 사항이 있습니다.

1.  .NET용 Aspose.Cells: Aspose.Cells 라이브러리가 설치되어 있는지 확인하세요. 다음에서 쉽게 다운로드할 수 있습니다.[Aspose 웹사이트](https://releases.aspose.com/cells/net/).
2. 개발 환경: 코드를 작성하고 실행할 수 있는 .NET 개발 환경(Visual Studio와 유사)
3. 디지털 인증서: 비밀번호가 있는 유효한 디지털 인증서(PFX 파일)가 필요합니다. 이 인증서는 디지털 서명을 만드는 데 필수적입니다.
4. C#에 대한 기본 지식: C# 프로그래밍에 익숙하면 예제를 더 잘 이해하는 데 도움이 됩니다.

이러한 필수 구성 요소를 정리하면 Excel 파일에서 Xades 서명을 구현할 준비가 된 것입니다!

## 패키지 가져오기

Aspose.Cells for .NET을 사용하려면 필요한 네임스페이스를 가져와야 합니다. 방법은 다음과 같습니다.

```csharp
using Aspose.Cells.DigitalSignatures;
using System;
using System.IO;
```

이러한 네임스페이스는 Excel 파일을 사용하고 디지털 서명을 관리하는 데 필요한 클래스와 메서드에 대한 액세스를 제공합니다.

이제 모든 것이 설정되었으니 Excel 파일에 Xades 서명을 추가하는 과정을 명확하고 관리하기 쉬운 단계로 나누어 보겠습니다.

## 1단계: 소스 및 출력 디렉토리 설정

먼저, 우리는 소스 Excel 파일이 어디에 있는지, 그리고 서명된 출력 파일을 어디에 저장할지 정의해야 합니다. 이것은 파일을 효율적으로 구성하는 데 도움이 되기 때문에 중요한 단계입니다.

```csharp
// 소스 디렉토리
string sourceDir = "Your Document Directory";
// 출력 디렉토리
string outputDir = "Your Output Directory";
```

## 2단계: 통합 문서 로드

다음으로, 서명하려는 Excel 통합 문서를 로드해 보겠습니다. 여기서 기존 Excel 파일을 로드합니다.

```csharp
Workbook workbook = new Workbook(sourceDir + "sourceFile.xlsx");
```

 여기서 우리는 새로운 인스턴스를 생성합니다`Workbook` 클래스, 소스 Excel 파일의 경로를 전달합니다. 파일 이름이 소스 디렉토리에 있는 파일 이름과 일치하는지 확인하세요.

## 3단계: 디지털 인증서 준비

디지털 서명을 만들려면 디지털 인증서를 로드해야 합니다. 여기에는 PFX 파일을 읽고 암호를 제공하는 것이 포함됩니다.

```csharp
string password = "pfxPassword"; // PFX 비밀번호로 바꾸세요
string pfx = "pfxFile"; // PFX 파일 경로로 바꾸세요
```

 이 단계에서는 다음을 교체합니다.`pfxPassword` 실제 비밀번호와 함께`pfxFile` PFX 파일 경로와 함께. 이것이 문서에 서명하는 열쇠입니다!

## 4단계: 디지털 서명 만들기

 이제 다음을 사용하여 디지털 서명을 만들어 보겠습니다.`DigitalSignature` 수업. 마법이 일어나는 곳이 바로 여기예요!

```csharp
DigitalSignature signature = new DigitalSignature(File.ReadAllBytes(pfx), password, "testXAdES", DateTime.Now);
signature.XAdESType = XAdESType.XAdES;
```

 이 스니펫에서는 PFX 파일을 바이트 배열로 읽고 새 파일을 만듭니다.`DigitalSignature` 객체입니다. 또한 우리는 다음을 설정합니다.`XAdESType` 에게`XAdES`이는 우리의 서명에 필수적입니다.

## 5단계: 통합 문서에 서명 추가

디지털 서명이 생성되면 다음 단계는 이를 통합 문서에 추가하는 것입니다.

```csharp
DigitalSignatureCollection dsCollection = new DigitalSignatureCollection();
dsCollection.Add(signature);
workbook.SetDigitalSignature(dsCollection);
```

 여기서 우리는 다음을 생성합니다.`DigitalSignatureCollection`, 서명을 추가한 다음 이 컬렉션을 통합 문서로 설정합니다. 이렇게 하면 서명을 Excel 파일에 첨부할 수 있습니다.

## 6단계: 서명된 통합 문서 저장

마지막으로, 서명된 통합 문서를 출력 디렉토리에 저장할 때입니다. 이 단계는 프로세스를 마무리합니다.

```csharp
workbook.Save(outputDir + "XAdESSignatureSupport_out.xlsx");
Console.WriteLine("XAdESSignatureSupport executed successfully.");
```

 이 코드에서는 통합 문서를 새 이름으로 저장합니다.`XAdESSignatureSupport_out.xlsx`, 출력 디렉토리에 있습니다. 이 단계가 완료되면 콘솔에 성공 메시지가 표시됩니다.

## 결론

이제 아시죠! Aspose.Cells for .NET을 사용하여 Excel 파일에 Xades 서명을 성공적으로 추가했습니다. 이 프로세스는 문서의 보안을 강화할 뿐만 아니라 파일의 신뢰성을 보장하여 사용자와의 신뢰를 구축합니다. 
디지털 서명은 현대 문서 관리에 필수적인 부분이며, Aspose.Cells의 기능을 사용하면 애플리케이션에서 디지털 서명을 쉽게 구현할 수 있습니다.

## 자주 묻는 질문

### Xades 시그니처는 무엇인가요?
Xades(XML Advanced Electronic Signatures)는 전자 문서의 무결성과 진위성을 보장하기 위한 추가 기능을 제공하는 디지털 서명 표준입니다.

### Xades 서명을 만들려면 디지털 인증서가 필요합니까?
네, Xades 서명을 만들려면 유효한 디지털 인증서(PFX 파일)가 필요합니다.

### 구매하기 전에 Aspose.Cells for .NET을 테스트해 볼 수 있나요?
 물론입니다! 무료 체험판을 받으실 수 있습니다.[Aspose 웹사이트](https://releases.aspose.com/).

### Aspose.Cells는 모든 버전의 .NET과 호환됩니까?
 Aspose.Cells는 다양한 버전의 .NET 프레임워크를 지원합니다.[선적 서류 비치](https://reference.aspose.com/cells/net/) 호환성에 대한 자세한 내용은 다음을 참조하세요.

### 문제가 발생하면 어디에서 지원을 받을 수 있나요?
 방문할 수 있습니다[Aspose 포럼](https://forum.aspose.com/c/cells/9) 지역사회의 지원과 도움을 위해.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
