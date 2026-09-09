---
category: general
date: 2026-09-08
description: Como copiar intervalo em Java usando Aspose.Cells – aprenda a copiar
  tabela dinâmica, duplicar tabela dinâmica e exportar tabela dinâmica preservando
  a formatação.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: pt
lastmod: 2026-09-08
og_description: Como copiar intervalo em Java com Aspose.Cells. Este tutorial mostra
  como copiar tabela dinâmica, duplicar tabela dinâmica e exportar tabela dinâmica
  preservando a formatação.
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: Como copiar intervalo em Java – guia completo do Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Como copiar intervalo em Java com Aspose.Cells
url: /pt/java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como copiar intervalo em Java com Aspose.Cells

Se você precisa **how to copy range** em Java, o Aspose.Cells torna a tarefa simples. Seja movendo um bloco de células comum ou uma tabela dinâmica completa, a biblioteca lida com a operação de cópia mantendo fórmulas, estilos e o cache da tabela dinâmica intactos. Neste guia você aprenderá a **copy pivot table**, **duplicate pivot table**, e até **export pivot table** para uma nova pasta de trabalho com formatação completa.

O tutorial cobre tudo, desde a configuração do projeto até a etapa final de verificação, para que você possa executar o código imediatamente após a leitura. Nenhuma ferramenta externa é necessária além do JAR do Aspose.Cells for Java.

## Pré-requisitos

- Java 17 (ou qualquer JDK suportado) instalado e configurado em sua IDE.
- Maven ou Gradle para gerenciamento de dependências (os exemplos usam Maven).
- Um arquivo Excel de origem (`source.xlsx`) que contém uma tabela dinâmica no intervalo `A1:H20`.
- Familiaridade básica com programação Java.

## Etapa 1: Adicionar Aspose.Cells ao seu projeto

Aspose.Cells é uma biblioteca comercial, mas uma versão de avaliação gratuita está disponível. Adicione a dependência ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **Dica profissional:** Se você preferir Gradle, a entrada equivalente é:
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

Adicionar o JAR fornece acesso às classes `Workbook`, `Worksheet`, `Range` e `CopyOptions` usadas ao longo deste guia.

## Etapa 2: Carregar a pasta de trabalho de origem e selecionar a primeira planilha

A primeira parte de **how to copy range** é abrir a pasta de trabalho que contém os dados que você deseja mover.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **Por que isso importa:** Abrir a pasta de trabalho cria uma representação em memória que a API pode manipular sem tocar no arquivo original no disco.

## Etapa 3: Definir o intervalo que contém a tabela dinâmica

Uma tabela dinâmica reside dentro de um bloco retangular. Você deve especificar esse bloco para que o Aspose.Cells saiba o que copiar.

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **Observação:** O método `createRange` **não** copia nada ainda; ele apenas cria um objeto `Range` que aponta para as células que você pretende duplicar.

## Etapa 4: Criar uma nova pasta de trabalho e obter sua primeira planilha

Agora crie a pasta de trabalho de destino onde o intervalo copiado residirá.

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **Por que uma nova pasta de trabalho?** Usar um arquivo novo garante que nenhum estilo oculto ou intervalo nomeado interfira na operação de cópia, o que é especialmente importante quando você **export pivot table** para um arquivo separado.

## Etapa 5: Copiar o intervalo (incluindo a tabela dinâmica) para a planilha de destino

Este é o núcleo de **how to copy range with formatting**. O objeto `CopyOptions` indica ao Aspose.Cells para preservar tudo: valores, fórmulas, estilos e o cache da tabela dinâmica.

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **Copy pivot table:** Como o intervalo de origem inclui a tabela dinâmica, a API duplica automaticamente o cache da tabela dinâmica, de modo que a nova planilha contém uma tabela dinâmica totalmente funcional que se comporta exatamente como a original.

## Etapa 6: Salvar a pasta de trabalho de destino

Finalmente, grave o resultado no disco.

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

Ao abrir `dest.xlsx`, você verá uma réplica exata da tabela dinâmica original, completa com sua formatação, segmentações e campos calculados.

## Saída esperada

- `dest.xlsx` contém uma planilha chamada **Sheet1**.
- Células `A1:H20` contêm os mesmos dados e a mesma tabela dinâmica da origem.
- Todos os estilos de célula (fontes, cores, bordas) são preservados.
- A tabela dinâmica é totalmente interativa; ao atualizá‑la, ela reflete os dados subjacentes no intervalo copiado.

## Como copiar intervalo com formatação – mergulho mais profundo

O exemplo anterior mostra o cenário mais simples, mas você pode encontrar variações que exigem uma abordagem ligeiramente diferente.

### Copiar tabela dinâmica para uma pasta de trabalho existente

Se você precisar **duplicate pivot table** dentro de uma pasta de trabalho que já contém dados, use a mesma chamada `copyRange` mas aponte para um endereço de destino diferente:

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### Exportar apenas a tabela dinâmica (sem os dados ao redor)

Às vezes você quer apenas a tabela dinâmica, não os dados de origem. Identifique o intervalo de exibição da tabela dinâmica via seu método `getPivotTable`:

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### Preservar formatação condicional

Regras de formatação condicional fazem parte da coleção de estilos. O sinalizador `PasteType.ALL` já as copia, mas você pode ser explícito:

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### Casos limites e solução de problemas

| Situação | O que observar | Correção recomendada |
|-----------|-------------------|-----------------|
| Pastas de trabalho de origem e destino usam versões diferentes do Excel | Alguns recursos mais recentes de tabela dinâmica (ex.: modelo de dados) podem não ser renderizados corretamente | Use a versão mais recente do Aspose.Cells e defina `Workbook.setFileFormatType(FileFormatType.XLSX)` para ambas as pastas de trabalho |
| Tabelas dinâmicas muito grandes ( > 10 000 linhas) causam pressão de memória | Erros de falta de memória durante a cópia | Habilite `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` antes de carregar |
| A planilha de destino já contém um intervalo nomeado com o mesmo nome da origem | Colisão de nomes leva a falha do `CopyOptions` | Chame `copyOptions.setIgnoreNameConflicts(true)` |

## Exemplo completo e executável

Abaixo está o programa completo que você pode copiar‑colar em uma classe Java. Ele inclui todas as importações, tratamento de erros e comentários.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

Execute o programa, então abra `dest.xlsx` para verificar que a tabela dinâmica funciona exatamente como a original.

## Conclusão

Agora você sabe **how to copy range** em Java usando Aspose.Cells, incluindo como **copy pivot table**, **duplicate pivot table** e **export pivot table** enquanto preserva toda a formatação. A biblioteca abstrai os detalhes de baixo nível da estrutura XML do Excel, permitindo que você se concentre na lógica de negócios.

### Próximos passos

- Explore **copy range with formatting** para gráficos e imagens (use `PasteType.PICTURES`).
- Automatize o processamento em lote: faça loop sobre vários arquivos de origem e consolide suas tabelas dinâmicas em uma pasta de trabalho resumida.
- Combine esta técnica com Aspose.Slides para gerar relatórios PowerPoint que incorporam a tabela dinâmica copiada

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como atualizar a fonte da tabela dinâmica do Excel com Aspose.Cells para Java: um guia abrangente](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Otimizar o carregamento de tabelas dinâmicas em Java usando Aspose.Cells – um guia abrangente](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [Como copiar tabela dinâmica em C# – converter Excel para PPTX, copiar intervalo e criar caixa de texto](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}