---
date: '2026-02-22'
description: CopyOptions와 PasteOptions를 사용해 수식을 정확히 유지하고 보이는 값만 붙여넣는 방식으로 Java에서 Aspose.Cells를
  활용한 Excel 보고서 자동화 방법을 배우세요.
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
title: Excel 보고서 자동화 – Aspose.Cells와 Java에서 CopyOptions 및 PasteOptions 마스터하기
url: /ko/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 Aspose.Cells를 사용한 Excel 보고 자동화: CopyOptions 및 PasteOptions

Java를 사용해 **Excel 보고 자동화**를 원하시나요? Aspose.Cells를 이용하면 프로그래밍 방식으로 복사·붙여넣기 및 수식 조정이 가능해 보고서의 정확성을 유지하면서 필요한 데이터만 전송할 수 있습니다. 이 튜토리얼에서는 **CopyOptions.ReferToDestinationSheet**와 **PasteOptions**라는 두 가지 핵심 기능을 살펴보며, 수식 참조를 보존하고 표시된 셀만 값을 붙여넣는 방법을 안내합니다.

## Quick Answers
- **`CopyOptions.ReferToDestinationSheet`는 무엇을 하나요?** 복사 시 수식이 대상 시트로 향하도록 조정합니다.  
- **표시된 셀만 붙여넣으려면?** `PasteOptions.setOnlyVisibleCells(true)`와 `PasteType.VALUES`를 사용합니다.  
- **필요한 라이브러리 버전은?** Aspose.Cells 25.3 이상.  
- **프로덕션에 라이선스가 필요합니까?** 예, 영구 또는 임시 라이선스를 적용하면 평가 제한이 해제됩니다.  
- **Maven 또는 Gradle을 사용할 수 있나요?** 두 빌드 도구 모두 지원됩니다. 아래 의존성 스니펫을 참고하세요.

## “Excel 보고 자동화”란?
Excel 보고 자동화는 워크북을 프로그래밍으로 생성·통합·서식 지정하여 수동 복사·붙여넣기 작업을 없애고 오류를 줄이는 것을 의미합니다. Aspose.Cells는 Java 개발자가 대규모 스프레드시트를 조작할 수 있도록 풍부한 API를 제공합니다.

## 보고서에 CopyOptions와 PasteOptions를 사용하는 이유
- **수식 무결성 유지** – 시트 간 데이터 이동 시 수식이 깨지지 않음.  
- **숨김 행/열 제외** – 보고서를 깔끔하고 집중된 형태로 유지.  
- **성능 향상** – 전체 범위가 아니라 필요한 데이터만 복사하여 처리 속도 개선.

## Prerequisites
- Java 8 이상.  
- Maven 또는 Gradle을 이용한 의존성 관리.  
- Aspose.Cells 25.3+ (평가판, 임시 라이선스 또는 영구 라이선스).  

## Setting Up Aspose.Cells for Java

프로젝트에 라이브러리를 추가하려면 다음 중 하나를 사용하세요:

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

### License Acquisition
- **Free Trial** – 전체 기능을 평가용으로 제공.  
- **Temporary License** – 테스트 중에 평가 제한을 해제.  
- **Permanent License** – 프로덕션 워크로드에 권장.

Java 코드에서 Aspose.Cells를 초기화합니다:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Step‑By‑Step Guide

### 1. CopyOptions with ReferToDestinationSheet

#### Overview
`CopyOptions.ReferToDestinationSheet`를 `true`로 설정하면 복사 후 수식 참조가 새 시트를 가리키도록 재작성됩니다.

#### Step 1: Initialize Workbook and Worksheets
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Step 2: Configure CopyOptions
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Step 3: Execute Copy Operation
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Why this matters*: 원래 `Sheet1`을 참조하던 수식이 이제 `DestSheet`를 올바르게 가리키게 되어 자동화된 보고서의 신뢰성이 확보됩니다.

**Troubleshooting Tip**: 수식이 여전히 이전 시트를 가리킨다면 복사 전에 `setReferToDestinationSheet(true)`가 호출되었는지 확인하세요.

### 2. PasteOptions for Values‑Only from Visible Cells

#### Overview
`PasteOptions`를 사용하면 붙여넣을 내용을 정의할 수 있습니다. `PasteType.VALUES`와 `onlyVisibleCells=true`를 함께 지정하면 숨겨진 행·열과 서식을 무시하고 표시된 값만 복사됩니다.

#### Step 1: Initialize Workbook and Worksheets
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Step 2: Configure PasteOptions
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Step 3: Execute Paste Operation
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Why this matters*: 필터링된 데이터 추출이나 숨겨진 행·열이 없는 깔끔한 보고서 생성에 이상적입니다.

**Troubleshooting Tip**: 복사하기 전에 Excel에서 행·열이 실제로 숨겨져 있는지 확인하세요. 숨겨져 있지 않다면 복사에 포함됩니다.

## Practical Applications
1. **Financial Consolidation** – 월별 시트를 마스터 워크북으로 병합하면서 모든 수식을 정확히 유지.  
2. **Filtered Data Export** – 필터된 테이블에서 표시된 행만 추출해 요약 시트에 넣기.  
3. **Scheduled Report Generation** – 정확한 셀 값과 올바른 참조를 갖춘 야간 자동 Excel 보고서 생성.

## Performance Considerations
- **Dispose of Workbooks** when done (`wb.dispose();`) to free native resources.  
- **Batch Operations** – 여러 복사·붙여넣기 호출을 하나로 묶어 오버헤드 감소.  
- **Monitor Memory** – 대용량 워크북은 힙 크기 증가(`-Xmx2g`)가 필요할 수 있음.

## Frequently Asked Questions

**Q1: `CopyOptions.ReferToDestinationSheet`는 무엇에 사용되나요?**  
A: 복사 후 수식 참조를 대상 시트로 재작성하여 보고서 수식이 올바르게 유지되도록 합니다.

**Q2: 표시된 셀만 붙여넣으려면 어떻게 하나요?**  
A: `PasteOptions.setOnlyVisibleCells(true)`를 설정하고 `PasteType.VALUES`를 선택합니다.

**Q3: Aspose.Cells를 라이선스 없이 사용할 수 있나요?**  
A: 평가판 또는 임시 라이선스로 평가용은 가능하지만, 프로덕션에서는 영구 라이선스가 필요합니다.

**Q4: 복사 후에도 일부 참조가 잘못된 경우는 왜인가요?**  
A: 복사 전에 `ReferToDestinationSheet`가 활성화되었는지, 그리고 원본 수식에 외부 워크북 링크가 포함되어 있지 않은지 다시 확인하세요.

**Q5: 메모리 관리 모범 사례는 무엇인가요?**  
A: 사용이 끝난 `Workbook` 객체를 반드시 `dispose()`하고, 큰 파일은 청크 단위로 처리하며, JVM 힙 사용량을 모니터링합니다.

**Q6: 하나의 작업에서 CopyOptions와 PasteOptions를 함께 사용할 수 있나요?**  
A: 예, 먼저 `CopyOptions`로 복사한 뒤 대상 범위에 `PasteOptions`를 적용하면 됩니다.

## Resources
- **Documentation**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download**: [Aspose.Cells Releases for Java](https://releases.aspose.com/cells/java/)  
- **Purchase**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Free Trial**: [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **Temporary License**: [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Support Forum**: [Aspose Support](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2026-02-22  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose