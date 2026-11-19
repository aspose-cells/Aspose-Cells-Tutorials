---
category: general
date: 2026-11-19
description: Aprenda como copiar uma tabela dinâmica em Java preservando seus dados
  e layout. Este guia passo a passo também mostra como copiar tabelas dinâmicas do
  Excel de forma eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- how to preserve pivot
- preserve pivot table
- copy excel pivot
language: pt
lastmod: 2026-11-19
og_description: Copiar tabela dinâmica em Java com Aspose.Cells. Siga este guia para
  aprender como preservar tabelas dinâmicas e copiar dados de tabelas dinâmicas do
  Excel com precisão.
og_image_alt: Illustration of the copy pivot table workflow in Java
og_title: Copiar tabela dinâmica em Java – guia completo do Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy pivot table in Java while preserving its data and
    layout. This step‑by‑step guide also shows how to copy excel pivot tables efficiently.
  headline: How to copy pivot table in Java with Aspose.Cells
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Pivot tables
title: Como copiar tabela dinâmica em Java com Aspose.Cells
url: /pt/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como copiar tabela dinâmica em Java com Aspose.Cells

Se você precisa **copy pivot table** de uma pasta de trabalho para outra, este guia mostra exatamente como fazer isso em Java. Seja construindo um mecanismo de relatórios ou migrando dados, você verá uma forma confiável de preservar o cache, os campos e a formatação da tabela dinâmica.

Copiar uma tabela dinâmica pode ser complicado porque uma simples cópia de intervalo costuma perder a fonte de dados subjacente. Neste tutorial usaremos o Aspose.Cells para **how to copy pivot** mantendo todos os cálculos intactos, e também abordaremos **how to preserve pivot** tables quando a pasta de trabalho de destino está vazia.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* Java 17 ou superior instalado.  
* Aspose.Cells for Java (versão 23.9 ou posterior) adicionado ao classpath do seu projeto.  
* Dois arquivos Excel: uma pasta de trabalho fonte que contém a tabela dinâmica e uma pasta de trabalho de destino vazia (ou uma pasta de trabalho na qual você deseja mesclar).

Você não precisa de nenhuma licença especial para o exemplo de código, mas uma licença válida do Aspose.Cells remove as marcas d’água de avaliação.

## Etapa 1: Carregar a pasta de trabalho fonte que contém a tabela dinâmica

O primeiro passo é abrir a pasta de trabalho que contém a tabela dinâmica original. Carregar o arquivo lhe dá acesso à planilha, às células e ao cache da tabela dinâmica.

```java
// Step 1: Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Por que isso importa*: O Aspose.Cells lê toda a pasta de trabalho, incluindo os dados de cache ocultos que alimentam a tabela dinâmica. Sem carregar o arquivo completo, a operação de cópia perderia a definição da tabela dinâmica.

## Etapa 2: Preparar a pasta de trabalho de destino

Crie uma nova pasta de trabalho (ou abra uma existente) e obtenha sua primeira planilha. É aqui que a tabela dinâmica será inserida.

```java
// Step 2: Create a new destination workbook and get its first worksheet
Workbook destWb = new Workbook();                     // empty workbook
Worksheet destWs = destWb.getWorksheets().get(0);    // first sheet
```

*Dica*: Se você já tem uma pasta de trabalho de destino, substitua a chamada `new Workbook()` por `new Workbook("target.xlsx")`. Isso permite que você **copy excel pivot** em uma pasta de trabalho já preenchida.

## Etapa 3: Definir a área de células que engloba a tabela dinâmica

É necessário especificar o intervalo exato que cobre a tabela dinâmica. O intervalo inclui a tabela da pivot, a lista de campos e quaisquer dados ao redor que você queira manter.

```java
// Step 3: Define the cell area that covers the pivot table in the source sheet
CellArea area = CellArea.createCellArea("A1", "H30"); // adjust as needed
```

*Por que isso importa*: O `CellArea` informa ao Aspose.Cells o que copiar. Se a área for muito pequena, a tabela dinâmica será truncada; se for muito grande, você copiará dados desnecessários. Ajuste as coordenadas com base no tamanho real da sua tabela dinâmica.

## Etapa 4: Executar a operação de cópia com CopyOptions

Use o método `copy` na coleção de células da planilha fonte. Passar um novo objeto `CopyOptions()` garante que toda a formatação, fórmulas e o cache da pivot sejam transferidos.

```java
// Step 4: Copy the defined range (including the pivot table) to the destination worksheet
srcWb.getWorksheets().get(0).getCells().copy(area, destWs.getCells(), new CopyOptions());
```

### Por que `CopyOptions` preserva a tabela dinâmica

`CopyOptions` indica ao Aspose.Cells que trate o intervalo como um *objeto completo* em vez de um conjunto plano de valores. Essa é a chave para **how to preserve pivot** tables: o cache subjacente da pivot é duplicado, permitindo que a pasta de trabalho de destino recalcule a tabela dinâmica sem intervenção manual.

## Etapa 5: Salvar a pasta de trabalho de destino

Por fim, grave o arquivo de destino no disco. O arquivo salvo conterá uma cópia totalmente funcional da tabela dinâmica original.

```java
// Step 5: Save the destination workbook – the pivot table is preserved
destWb.save("YOUR_DIRECTORY/copied_with_pivot.xlsx");
```

*Resultado esperado*: Abrir `copied_with_pivot.xlsx` no Excel mostra a mesma tabela dinâmica, completa com segmentações, filtros e campos calculados. Você pode atualizá‑la, e a fonte de dados apontará para o intervalo copiado dentro da mesma pasta de trabalho.

---

![Diagrama mostrando o processo de cópia de tabela dinâmica](/images/copy-pivot-table-workflow.png){.align-center width=600 alt="Diagrama ilustrando o fluxo de cópia de tabela dinâmica da pasta de trabalho fonte para a pasta de trabalho destino"}

## Como copiar tabelas dinâmicas entre várias planilhas

Se você precisa **copy excel pivot** tables de várias planilhas, repita as Etapas 3‑4 para cada planilha fonte. Você também pode percorrer `srcWb.getWorksheets()` e copiar cada pivot para uma planilha correspondente em `destWb`. Veja um exemplo conciso de loop:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet srcWs = srcWb.getWorksheets().get(i);
    Worksheet newDestWs = destWb.getWorksheets().add();
    // Assume each pivot occupies A1:H30 – adjust per sheet if needed
    CellArea area = CellArea.createCellArea("A1", "H30");
    srcWs.getCells().copy(area, newDestWs.getCells(), new CopyOptions());
}
destWb.save("YOUR_DIRECTORY/multi_sheet_copy.xlsx");
```

*Pro dica*: Use `srcWs.getPivotTables().getCount()` para detectar se uma planilha realmente contém uma pivot antes de copiar. Isso evita a cópia de dados irrelevantes.

## Armadilhas comuns e como evitá‑las

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| **Pivot perde seu cache** | Uso de `Worksheet.copy()` sem `CopyOptions` copia apenas valores das células. | Sempre use `srcWs.getCells().copy(..., new CopyOptions())`. |
| **Destino mostra erros #REF!** | A pivot copiada ainda referencia a fonte de dados externa da pasta de trabalho original. | Após copiar, chame `destWs.getPivotTables().get(0).refresh();` para reatribuir o cache ao novo intervalo. |
| **Segmentações desaparecem** | Segmentações são armazenadas fora da área principal de células. | Expanda o `CellArea` para incluir os intervalos das segmentações, ou copie a planilha inteira (`srcWs.copy(destWs, new CopyOptions())`). |
| **Desempenho lento em pivots grandes** | Copiar intervalos enormes com formatação pode ser demorado. | Use `CopyOptions.setOnlyData(true)` se não precisar da formatação, e reaplique estilos manualmente. |

## Como preservar a formatação da tabela dinâmica ao atualizar os dados

Às vezes você precisa **how to preserve pivot** layout após alterações nos dados de origem. Depois de copiar, você pode bloquear o estilo da pivot:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.setPreserveFormatting(true);   // keeps colors, fonts, and layout
pt.refresh();                     // recalculates with new data
```

Definir `PreserveFormatting` garante que quaisquer estilos personalizados aplicados na origem sobrevivam à cópia.

## Verificando a cópia

Uma maneira rápida de confirmar que a cópia foi bem‑sucedida é comparar as definições das pivots:

```java
PivotTable srcPt = srcWb.getWorksheets().get(0).getPivotTables().get(0);
PivotTable destPt = destWs.getPivotTables().get(0);

System.out.println("Source fields: " + srcPt.getFields().size());
System.out.println("Destination fields: " + destPt.getFields().size());
// Both numbers should match
```

Se as contagens coincidirem e a pasta de trabalho de destino abrir sem erros, você copiou a **copy pivot table** com sucesso.

## Conclusão

Agora você sabe como **copy pivot table** de uma pasta de trabalho Excel para outra usando Aspose.Cells para Java, e viu os passos exatos para **how to copy pivot** garantindo que o cache, a formatação e as segmentações da pivot permaneçam intactos. O mesmo padrão funciona para cenários **copy excel pivot** em várias planilhas, e você pode adaptar o código para casos extremos, como preservar a formatação da pivot ou lidar com conjuntos de dados grandes.

### Próximos passos

* Explore as opções **preserve pivot table** como `setPreserveFormatting` e `refresh` para fontes de dados dinâmicas.  
* Experimente copiar tabelas dinâmicas entre pastas de trabalho com diferentes ordens de colunas — ajuste o `CellArea` conforme necessário.  
* Combine esta técnica com Aspose.Slides para inserir instantâneos de pivots em apresentações PowerPoint.

Feliz codificação, e sinta‑se à vontade para experimentar variações que se adequem ao seu pipeline de automação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Como copiar intervalo e preservar uma tabela dinâmica em Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [Como copiar uma tabela dinâmica entre planilhas em Java](/cells/english/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/)
- [Como copiar tabela dinâmica para uma nova pasta de trabalho em Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}