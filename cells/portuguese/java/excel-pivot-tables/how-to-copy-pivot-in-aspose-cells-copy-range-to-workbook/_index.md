---
category: general
date: 2026-08-08
description: Como copiar uma tabela dinâmica no Aspose.Cells e copiar um intervalo
  para a pasta de trabalho usando Java. Aprenda os passos exatos para duplicar uma
  tabela dinâmica com CopyOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: pt
lastmod: 2026-08-08
og_description: Como copiar uma tabela dinâmica no Aspose.Cells e copiar um intervalo
  para a pasta de trabalho com Java. Siga este guia completo para duplicar uma tabela
  dinâmica usando CopyOptions.
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: Como copiar tabela dinâmica no Aspose.Cells – copiar intervalo para a pasta
  de trabalho
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: Como copiar tabela dinâmica no Aspose.Cells – copiar intervalo para a pasta
  de trabalho
url: /pt/java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como copiar pivot no Aspose.Cells – copiar intervalo para a pasta de trabalho

Se você precisa **how to copy pivot** em um arquivo Excel usando Aspose.Cells, este guia mostra o processo exato. Ao final do tutorial você será capaz de **copy range to workbook** preservando a definição da tabela dinâmica.

O exemplo usa Java, mas os mesmos conceitos se aplicam a qualquer linguagem .NET que trabalhe com Aspose.Cells. Nenhuma ferramenta externa é necessária—apenas a biblioteca Aspose.Cells for Java e um ambiente de desenvolvimento básico.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* Java Development Kit (JDK) 8 ou posterior.
* Maven ou Gradle para gerenciar dependências (o exemplo usa Maven).
* Aspose.Cells for Java 23.9 (ou a versão mais recente) adicionada ao seu projeto.
* Uma pasta de trabalho de entrada (`input.xlsx`) que contenha ao menos uma tabela dinâmica na primeira planilha.

Ter esses itens prontos evita erros de tempo de execução quando o código acessa a pasta de trabalho.

## Como copiar pivot com Aspose.Cells

Esta seção percorre cada passo necessário para **how to copy pivot** de uma parte de uma planilha para outra, usando a classe `CopyOptions`.

### Etapa 1: Adicionar Aspose.Cells ao seu projeto

Se você usa Maven, adicione a dependência a seguir ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*Por que esta etapa importa*: A biblioteca fornece as classes `Workbook`, `CopyOptions` e outras necessárias para operações **aspose.cells copy range**. Sem a dependência o compilador não pode resolver esses tipos.

### Etapa 2: Carregar a pasta de trabalho de origem

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Carregar o arquivo cria uma representação em memória da planilha. O objeto `Workbook` fornece acesso a planilhas, células e tabelas dinâmicas.

### Etapa 3: Configurar opções de cópia para incluir a tabela dinâmica

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

`CopyOptions.setCopyPivotTable(true)` informa ao Aspose.Cells que a operação deve preservar os metadados da tabela dinâmica. Se você omitir essa flag, a tabela dinâmica será reduzida a dados estáticos, perdendo sua interatividade.

### Etapa 4: Copiar o intervalo desejado com a tabela dinâmica

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

O método `copyRange` copia células, formatação e—devido às opções definidas na etapa anterior—qualquer tabela dinâmica que intersecte o intervalo. Este é o núcleo da funcionalidade **copy range to workbook**.

### Etapa 5: Salvar a pasta de trabalho modificada

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Salvar grava as alterações em um novo arquivo (`output.xlsx`). Agora você pode abrir este arquivo no Excel e ver que a tabela dinâmica foi duplicada exatamente onde o intervalo foi copiado.

## Exemplo completo e executável

Juntando todas as peças, aqui está o programa completo que você pode compilar e executar:

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### Resultado esperado

* `output.xlsx` contém os mesmos dados que `input.xlsx`.
* A tabela dinâmica que originalmente ocupava o intervalo de origem aparece nas células de destino, totalmente funcional (filtros, capacidade de atualização, etc.).
* Toda a formatação de células, fórmulas e larguras de coluna são preservadas porque `copyRange` copia todo o bloco de células.

## Perguntas comuns e casos extremos

**E se o intervalo de destino sobrepuser uma tabela dinâmica existente?**  
Aspose.Cells sobrescreverá as células de destino. Para evitar perda de dados, garanta que a área de destino esteja vazia ou mova a tabela dinâmica existente primeiro.

**Posso copiar uma tabela dinâmica entre planilhas?**  
Sim. Use `workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);` onde `targetSheetIndex` aponta para a planilha de destino.

**`setCopyPivotTable(true)` copia a fonte de dados subjacente?**  
O método copia apenas a referência ao cache da tabela dinâmica. Se os dados de origem residirem na mesma pasta de trabalho, a tabela dinâmica de destino apontará para o mesmo cache. Para duplicar o cache, você deve criar um novo cache de tabela dinâmica manualmente.

**Como copiar um intervalo grande de forma eficiente?**  
Ao copiar intervalos muito grandes, considere usar `CopyOptions.setCopyFormula(true)` e `setCopyDataValidation(true)` somente se necessário. Reduzir o número de opções pode melhorar o desempenho.

## Dicas para uso confiável de **aspose.cells copy range**

* **Dica profissional:** Sempre chame `workbook.calculateFormula()` após a cópia se o intervalo contiver fórmulas que dependam do cache da tabela dinâmica.
* **Cuidado com:** Planilhas ocultas. `copyRange` funciona apenas em planilhas visíveis, a menos que você faça referência explícita à planilha oculta por índice.
* **Verificação de versão:** A flag `setCopyPivotTable` está disponível a partir do Aspose.Cells 20.9. Certifique‑se de que sua versão da biblioteca a suporte.

## Conclusão

Agora você sabe **how to copy pivot** no Aspose.Cells e como **copy range to workbook** preservando a funcionalidade completa da tabela dinâmica. As etapas—adicionar a biblioteca, carregar a pasta de trabalho, configurar `CopyOptions`, executar a cópia e salvar—formam um padrão repetível que você pode adaptar a outros cenários de copiar‑e‑colar.

Em seguida, explore tópicos relacionados como **aspose.cells copy range** para gráficos, formatação condicional e validação de dados. Experimente copiar entre diferentes formatos de arquivo (XLSX → XLS) para ampliar suas capacidades de automação. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como criar tabelas dinâmicas no Excel usando Aspose.Cells para Java: Um guia abrangente](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Como atualizar a fonte da tabela dinâmica do Excel com Aspose.Cells para Java: Um guia abrangente](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Como implementar segmentações em tabelas dinâmicas usando Aspose.Cells para Java: Um guia abrangente](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}