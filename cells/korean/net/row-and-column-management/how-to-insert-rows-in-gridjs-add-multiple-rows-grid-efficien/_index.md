---
category: general
date: 2026-03-29
description: GridJs에서 행을 빠르게 삽입하는 방법을 배워보세요. 이 가이드는 행을 추가하는 방법과 배치 작업으로 여러 행을 한 번에
  추가하는 방법도 다룹니다.
draft: false
keywords:
- how to insert rows
- how to add rows
- add multiple rows grid
- batch row insertion
- large grid performance
language: ko
og_description: GridJs에서 행을 빠르게 삽입하는 방법을 배워보세요. 이 가이드는 행 추가, 여러 행을 한 번에 추가하는 방법, 대량
  배치 삽입을 처리하는 방법을 보여줍니다.
og_title: GridJs에서 행 삽입 방법 – 그리드에 여러 행을 효율적으로 추가하기
tags:
- GridJs
- C#
- data‑grid
title: GridJs에서 행 삽입 방법 – 그리드에 여러 행을 효율적으로 추가하기
url: /ko/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-grid-efficien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GridJs에서 행 삽입하기 – 다중 행을 효율적으로 추가하는 방법

대용량 GridJs 테이블에 **행을 삽입**하면서 UI가 멈추는 상황을 겪어본 적 있나요? **행을** 하나씩 추가하려다 보니 성능이 급격히 떨어지는 경우도 있죠. 좋은 소식은 GridJs가 배치 API를 제공한다는 점입니다. 이 API를 사용하면 **다중 행을 한 번에** 추가할 수 있어 수백만 개의 항목을 다룰 때도 UI가 부드럽게 유지됩니다.

이 튜토리얼에서는 `InsertRowsBatch`를 사용해 **행을 삽입**하는 전체 실행 가능한 예제를 단계별로 살펴봅니다. 배치가 왜 중요한지, 결과를 어떻게 검증하는지, 그리고 대상 인덱스가 매우 클 때 주의해야 할 점을 알려드립니다. 끝까지 따라오면 어떤 GridJs 인스턴스에도 천 개 이상의 새로운 레코드를 자신 있게 삽입할 수 있게 됩니다.

## Prerequisites

시작하기 전에 다음이 준비되어 있어야 합니다:

- .NET 6.0 이상 (코드는 최신 SDK와 호환됩니다)
- `GridJs` NuGet 패키지에 대한 참조 (또는 커스텀 빌드 DLL)
- 기본적인 C# 지식 – 전문가일 필요는 없으며 클래스와 메서드만 이해하면 됩니다
- 원하는 IDE 또는 편집기 (Visual Studio, Rider, VS Code 등 모두 사용 가능)

> **Pro tip:** 실제로 수천만 행 규모의 그리드를 다룰 계획이라면 `gridJs.EnableVirtualization = true;` 를 활성화해 UI 렌더링 부하를 최소화하세요.

## Step 1: Create and Configure the GridJs Instance

먼저 살아있는 `GridJs` 객체가 필요합니다. 이는 행을 그릴 캔버스와 같습니다.

```csharp
using System;
using GridJsLibrary;   // Assume this is the namespace for GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Initialize the grid
            GridJs gridJs = new GridJs();

            // Optional: turn on virtualization for huge data sets
            gridJs.EnableVirtualization = true;

            // Populate the grid with some dummy data so we can see the effect
            SeedInitialData(gridJs);

            // Now we’re ready to insert rows in bulk
            InsertRowsInBatch(gridJs);
        }

        // Helper: add 2 000 000 rows so our batch lands at index 2 000 001
        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }
```

> **Why this step matters:** 그리드를 초기화하고 선택적으로 데이터를 시드하는 과정은 실제 환경에서 그리드가 이미 많은 정보를 보유하고 있는 상황을 모방합니다. 이후 수행할 배치 삽입은 0 기반 인덱스를 기준으로 동작하므로, 정확한 삽입 지점을 보여주기 위해 미리 데이터를 채워두었습니다.

## Step 2: Use `InsertRowsBatch` to **Add Multiple Rows Grid**

튜토리얼의 핵심 – 실제로 **행을** 대량으로 **추가**하는 호출입니다. 메서드 시그니처는 `InsertRowsBatch(int startIndex, int count)` 입니다. 예제에서는 인덱스 2 000 000(2 000 001번째 행)부터 시작해 열 개의 행을 추가합니다.

```csharp
        // Step 2 – Insert a batch of rows
        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based, so this is row 2 000 001
            int rowsToAdd = 10;

            // The batch call creates placeholder rows; you can later populate them
            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Verify by reading back a few rows
            VerifyInsertion(grid, startIndex, rowsToAdd);
        }
```

> **How it works:** `InsertRowsBatch`는 요청된 수만큼의 행을 내부적으로 할당하고 기존 행을 아래로 이동시킵니다. 작업이 하나의 트랜잭션으로 수행되기 때문에 UI는 한 번만 새로 고침되며, 따라서 **행을 효율적으로 추가**하는 권장 방법이 됩니다.

## Step 3: Verify the Insertion – Did the Rows Land Where Expected?

배치 작업 후에는 행이 예상한 위치에 삽입됐는지 확인해야 합니다. 아래 헬퍼 코드는 새로 추가된 블록의 첫 번째와 마지막 행을 읽어 콘솔에 출력합니다.

```csharp
        // Step 3 – Simple verification
        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

**Expected output**

```
Initial seed completed – 2 000 000 rows present.
Inserted 10 rows starting at index 2000001.
Verifying inserted rows:
Row 2000001: , 
Row 2000002: , 
...
Row 2000010: , 
```

빈 셀은 해당 행이 아직 데이터가 채워지지 않은 자리표시자임을 의미합니다. 이제 개별적으로 데이터를 채우거나 또 다른 배치 업데이트를 수행할 수 있습니다.

> **Edge case note:** `startIndex`가 현재 행 수를 초과하면 GridJs는 자동으로 새 행을 끝에 추가합니다. 반대로 음수 인덱스를 전달하면 `ArgumentOutOfRangeException`이 발생하므로 사용자 입력 인덱스는 반드시 검증해야 합니다.

## Step 4: Populate the New Rows (Optional but Common)

대부분 빈 행만 만들고 싶지는 않으며, 의미 있는 값으로 채워야 합니다. 새로 만든 범위를 순회하면서 `SetCell` 등 적절한 API를 호출하면 됩니다.

```csharp
        // Optional: fill the newly added rows with sample data
        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }
```

배치 삽입 직후에 행을 즉시 화면에 표시해야 한다면 `PopulateNewRows(gridJs, startIndex, rowsToAdd);` 를 호출하면 됩니다.

## Step 5: Performance Tips for Very Large Grids

수백만 행 규모의 **다중 행을 추가**할 때 기억해 두면 좋은 팁:

1. **배치 크기가 중요** – 한 번에 10 000행을 삽입하는 것이 1 000행 배치를 10번 하는 것보다 빠를 수 있습니다. 각 배치는 UI 새로 고침을 한 번만 발생시키기 때문입니다.
2. **UI 업데이트 끄기** – 일부 GridJs 버전에서는 `grid.SuspendLayout()` / `grid.ResumeLayout()` 를 제공한다. 지연이 눈에 띄면 배치를 이 호출 사이에 감싸세요.
3. **가상화 사용** – 앞서 언급한 `EnableVirtualization` 은 메모리 사용량과 렌더링 시간을 크게 줄여줍니다.
4. **깊은 복사 피하기** – 그리드에 전달하는 객체는 단순한 값 타입이나 가벼운 객체여야 합니다. 무거운 객체는 복제 과정에서 성능을 저하시킵니다.

## Full Working Example

모든 내용을 하나로 합치면 다음과 같은 완전한 프로그램이 됩니다. 새 콘솔 프로젝트에 복사‑붙여넣기 하면 바로 실행할 수 있습니다.

```csharp
using System;
using GridJsLibrary;   // Replace with the actual namespace of your GridJs library

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            GridJs gridJs = new GridJs
            {
                EnableVirtualization = true
            };

            SeedInitialData(gridJs);
            InsertRowsInBatch(gridJs);
        }

        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }

        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based index for row 2 000 001
            int rowsToAdd = 10;

            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Optional: fill them with data
            PopulateNewRows(grid, startIndex, rowsToAdd);

            VerifyInsertion(grid, startIndex, rowsToAdd);
        }

        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }

        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

프로그램을 실행하면 콘솔에 열 개의 행이 정확한 위치에 삽입되고 채워졌음을 확인하는 출력이 나타납니다.

## Conclusion

우리는 배치 API를 활용해 GridJs에서 **행을 삽입**하는 방법을 살펴보고, **행을 효율적으로 추가**하는 요령을 시연했으며, UI가 멈추지 않도록 **다중 행을 추가**하는 다양한 전략을 소개했습니다. 핵심 정리:

- 대량 작업에는 `InsertRowsBatch(startIndex, count)` 를 사용하세요.
- 인덱스를 검증하고, 대규모 데이터셋에는 가상화를 고려하세요.
- 즉시 내용이 필요하면 배치 후에 행을 채우세요.

다음 단계로 **행 삭제 방법**을 탐구하거나, 배치 편집을 위한 **undo/redo** 구현, 혹은 데이터를 스트리밍으로 제공하는 백엔드 서비스와 GridJs를 연동해 보는 것을 권장합니다. 모두 이번에 배운 개념을 기반으로 합니다.

코드를 자유롭게 실험해 보세요—배치 크기를 바꾸거나, 그리드 시작 부분에 삽입해 보거나, 여러 배치를 하나의 트랜잭션으로 결합해 보는 등 다양한 시도를 통해 대용량 그리드 작업에 익숙해질 수 있습니다.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}