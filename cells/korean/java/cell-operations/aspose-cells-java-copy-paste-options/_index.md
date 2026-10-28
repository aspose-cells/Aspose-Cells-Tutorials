---
date: '2026-10-28'
description: Java에서 Aspose.Cells 복사 및 붙여넣기 옵션을 사용하여 값을 붙여넣는 방법을 단계별 코드, Maven 의존성
  설정 및 라이선스 팁과 함께 배웁니다.
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: Java에서 Aspose.Cells 복사 및 붙여넣기 옵션을 사용하여 값을 붙여넣는 방법을 단계별 코드, Maven 의존성
  설정 및 라이선스 팁과 함께 배웁니다.
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: Aspose.Cells 복사 및 붙여넣기 옵션으로 값 붙여넣는 방법
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: Aspose.Cells 복사 및 붙여넣기 옵션으로 값 붙여넣는 방법
url: /ko/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells 복사 및 붙여넣기 옵션으로 값 붙여넣는 방법

Java에서 Excel 보고서를 자동화한다는 것은 Excel을 직접 열지 않고도 워크북을 생성, 통합 및 서식 지정할 수 있음을 의미합니다. **Aspose.Cells**를 사용하면 수식, 숨겨진 행 및 셀 값에 대한 완전한 제어가 가능하므로 보고서가 정확하고 가볍게 유지됩니다. 이 튜토리얼에서는 **CopyOptions.ReferToDestinationSheet**를 사용하여 수식을 올바르게 유지하고 **PasteOptions**를 사용해 필요한 표시된 값만 붙여넣는 방법을 배웁니다.

## 빠른 답변
- **`CopyOptions.ReferToDestinationSheet`가 무엇을 하나요?** 복사 작업 후 수식이 대상 시트로 가리키도록 수식을 다시 작성합니다.  
- **보이는 셀만 어떻게 붙여넣나요?** `PasteOptions.setOnlyVisibleCells(true)`를 `PasteType.VALUES`와 함께 호출합니다.  
- **필요한 라이브러리 버전은 무엇인가요?** Aspose.Cells 25.3 이상.  
- **프로덕션에 라이선스가 필요합니까?** 예 – 영구 또는 임시 라이선스를 사용하면 평가 제한이 해제됩니다.  
- **Maven 또는 Gradle을 사용할 수 있나요?** 두 가지 모두 지원되며, 아래의 의존성 스니펫을 참조하세요.

## “Excel 보고서 자동화”란 무엇인가요?
Excel 보고서 자동화는 프로그래밍 방식으로 Excel 워크북을 생성 및 업데이트하는 것을 의미하며, 수동 복사‑붙여넣기 없이 보고서를 만들고, 병합하고, 서식 지정할 수 있어 오류를 줄이고 반복 작업 시간을 절약합니다. 이 접근 방식은 예약 배치 작업, 데이터 기반 대시보드 및 재무 통합 파이프라인에 이상적입니다.

## 보고서에 CopyOptions와 PasteOptions를 사용하는 이유는 무엇인가요?
이 두 클래스는 데이터를 복사하면서 수식 참조를 그대로 유지하고 **그리고** 필터링하거나 행을 숨긴 후에 표시되는 셀만 추출할 수 있게 해줍니다. 함께 사용하면 일반적인 필터링된 테이블 시나리오에서 전송되는 데이터 양을 최대 80 %까지 줄이고, 대상 시트에서 수식이 올바르게 계산되도록 보장합니다.

## 전제 조건
- Java 8 이상.  
- 의존성 관리를 위한 Maven 또는 Gradle.  
- Aspose.Cells 25.3 이상 (평가판, 임시 또는 영구 라이선스).  

## Java용 Aspose.Cells 설정
다음 중 하나를 사용하여 라이브러리를 프로젝트에 추가하세요:

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### 라이선스 획득
- **Free trial** – 평가를 위한 전체 기능 제공.  
- **Temporary license** – 테스트 중에 평가 제한을 해제합니다.  
- **Permanent license** – 프로덕션 작업에 권장됩니다.

Java 코드에서 Aspose.Cells를 초기화합니다:  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## 단계별 가이드

### 1. referToDestinationSheet와 함께 copyOptions

#### 개요
`CopyOptions`는 복사 작업 중 수식 및 셀 참조가 처리되는 방식을 제어하는 Aspose.Cells의 구성 객체입니다. `CopyOptions.ReferToDestinationSheet`를 `true`로 설정하면 복사 작업 후 수식 참조가 새 시트를 가리키도록 다시 작성됩니다.

#### Step 1: 워크북 및 워크시트 초기화  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Step 2: copyOptions 구성  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Step 3: 복사 작업 실행  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*왜 중요한가*: 원래 `Sheet1`을 참조하던 수식이 이제 `DestSheet`를 올바르게 참조하게 되어 자동화된 보고서가 신뢰성을 유지합니다.

**문제 해결 팁**: 수식이 여전히 이전 시트를 참조한다면 `setReferToDestinationSheet(true)`가 복사 **전**에 호출되었는지 확인하세요.

### 2. 표시된 셀에서 값만 붙여넣기 위한 pasteOptions

#### 개요
`PasteOptions`는 무엇을 붙여넣을지 정의하는 Aspose.Cells의 설정 객체입니다. `PasteType.VALUES`와 `onlyVisibleCells=true`를 함께 사용하면 숨겨진 행/열 및 서식을 무시하고 표시된 값만 복사합니다.

#### Step 1: 워크북 및 워크시트 초기화  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Step 2: pasteOptions 구성  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Step 3: 붙여넣기 작업 실행  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*왜 중요한가*: 필터링된 데이터를 추출하거나 숨겨진 행이나 서식 잡음 없이 깔끔한 보고서를 생성하는 데 이상적입니다.

**문제 해결 팁**: 복사하기 전에 Excel에서 행/열이 실제로 숨겨져 있는지 확인하세요; 그렇지 않으면 포함됩니다.

## 실용적인 적용 사례
1. **Financial consolidation** – 월별 시트를 마스터 워크북으로 병합하면서 모든 수식을 정확하게 유지합니다.  
2. **Filtered data export** – 필터링된 테이블에서 표시된 행만 요약 시트로 가져옵니다.  
3. **Scheduled report generation** – 정확한 셀 값과 올바른 참조를 사용하여 매일 밤 Excel 보고서 생성을 자동화합니다.

## 성능 고려 사항
- **워크북 해제**를 완료 시(`wb.dispose();`) 호출하여 네이티브 리소스를 해제합니다.  
- **Batch operations** – 여러 복사/붙여넣기 호출을 그룹화하여 오버헤드를 줄입니다.  
- **Monitor memory** – 큰 워크북은 힙을 늘려야 할 수 있습니다 (`-Xmx2g`).  
- Aspose.Cells는 **50개 이상의 입력 및 출력 포맷**을 지원하며, **최대 200만 행**까지 전체 파일을 메모리에 로드하지 않고 워크북을 처리할 수 있어 엔터프라이즈 작업에 고처리량 성능을 제공합니다.

## 자주 묻는 질문

**Q: `CopyOptions.ReferToDestinationSheet`는 무엇에 사용되나요?**  
A: 복사 후 수식 참조를 대상 시트로 가리키도록 다시 작성하여 보고서 수식이 올바르게 유지되도록 합니다.

**Q: 보이는 셀만 어떻게 붙여넣나요?**  
A: `PasteOptions.setOnlyVisibleCells(true)`를 설정하고 `PasteType.VALUES`를 선택합니다.

**Q: 라이선스를 구매하지 않고 Aspose.Cells를 사용할 수 있나요?**  
A: 예, 평가를 위한 무료 체험 또는 임시 라이선스를 제공하지만, 프로덕션에는 영구 라이선스가 필요합니다.

**Q: 복사 후에도 일부 참조가 여전히 잘못된 이유는 무엇인가요?**  
A: 복사 작업 **전**에 `ReferToDestinationSheet`가 활성화되어 있는지, 그리고 원본 수식에 외부 워크북 링크가 포함되지 않았는지 다시 확인하세요.

**Q: 어떤 메모리 관리 모범 사례를 따라야 하나요?**  
A: 작업이 끝나면 `Workbook` 객체를 해제하고, 큰 파일은 청크로 처리하며, JVM 힙 사용량을 모니터링합니다.

**Q: 하나의 작업에서 CopyOptions와 PasteOptions를 결합할 수 있나요?**  
A: 예, 먼저 `CopyOptions`로 복사한 다음 대상 범위에 `PasteOptions`를 적용하여 연쇄적으로 사용할 수 있습니다.

## 리소스
- **문서**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **다운로드**: [Aspose.Cells releases for Java](https://releases.aspose.com/cells/java/)  
- **구매**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **무료 체험**: [Aspose.Cells free trial](https://releases.aspose.com/cells/java/)  
- **임시 라이선스**: [Apply for a temporary license](https://purchase.aspose.com/temporary-license/)  
- **지원 포럼**: [Aspose support](https://forum.aspose.com/c/cells)

---

**마지막 업데이트:** 2026-10-28  
**테스트 환경:** Aspose.Cells 25.3 for Java  
**작성자:** Aspose

## 관련 튜토리얼

- [Excel 파일 읽기 Java – Aspose.Cells를 사용한 워크북 셀 조작 마스터](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [Aspose.Cells for Java를 사용하여 Excel 셀에 데이터 추가](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Aspose.Cells Java로 Excel 셀 행 열 인덱스 변환](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}