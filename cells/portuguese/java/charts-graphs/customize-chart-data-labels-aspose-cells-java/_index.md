---
date: '2026-10-17'
description: Aprenda a definir a forma dos rótulos de dados de gráficos do Excel em
  Java usando Aspose.Cells. Este guia mostra como modificar os rótulos de gráficos
  do Excel de forma rápida e eficiente.
keywords:
- how to set shape
- modify excel chart labels
- customize chart data labels
- add data label shape
lastmod: '2026-10-17'
og_description: Aprenda a definir a forma dos rótulos de dados de gráficos do Excel
  em Java usando Aspose.Cells. Este guia passo a passo ajuda a modificar os rótulos
  de gráficos do Excel rapidamente.
og_image_alt: Guide showing how to set shape of Excel chart data labels using Aspose.Cells
  for Java
og_title: Como definir a forma dos rótulos de dados de gráficos do Excel em Java
schemas:
- author: Aspose
  dateModified: '2026-10-17'
  description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  headline: How to set shape of Excel chart data labels in Java
  type: TechArticle
- description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  name: How to set shape of Excel chart data labels in Java
  steps:
  - name: load your workbook
    text: The `Workbook` class is Aspose.Cells' top‑level object that represents a
      single Excel file in memory. Use `new Workbook("input.xlsx")` to load the file
      you want to modify.
  - name: access the chart
    text: '`Worksheet` represents a single sheet within a workbook. `Worksheet ws
      = workbook.getWorksheets().get(0);` retrieves the first worksheet. `Chart` is
      an object that represents a chart embedded in a worksheet. `Chart chart = ws.getCharts().get(0);`
      obtains the first chart on that sheet.'
  - name: retrieve series and modify data labels
    text: '`Series` represents a data series plotted on a chart. Each `Series` object
      contains a `DataLabel` collection. `DataLabel` controls the appearance of a
      data label for a series. `DataLabelShapeType` is an enumeration of possible
      shapes for data labels. Call `series.getDataLabels().setShapeType(DataLab'
  - name: save your workbook
    text: After applying the shape, invoke `workbook.save("output.xlsx");` to write
      the changes back to disk.
  type: HowTo
- questions:
  - answer: Loop through each series in the chart and call `setShapeType` on the series’
      `DataLabel` object.
    question: How do I change the shape of multiple data labels at once?
  - answer: Yes. With proper memory management, it processes workbooks containing
      hundreds of thousands of rows without loading the entire file into memory.
    question: Can Aspose.Cells for Java handle large Excel files efficiently?
  - answer: Missing Maven dependencies, using an outdated library version, or providing
      an invalid license file are typical pitfalls.
    question: What are common issues when setting up Aspose.Cells?
  - answer: Set the shape type to `DataLabelShapeType.DEFAULT` to restore the original
      appearance.
    question: Is there a way to revert data label shapes to default?
  - answer: Iterate over `ws.getCharts()` and apply the same `setShapeType` logic
      to each chart’s series collection.
    question: How can I apply this customization to multiple charts in a workbook?
  type: FAQPage
tags:
- excel chart
- aspose.cells
- java chart customization
- data label shape
title: Como definir a forma dos rótulos de dados de gráficos do Excel em Java
url: /pt/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Domine a personalização de gráficos em Java com Aspose.Cells: modifique formas de rótulos de dados

## Introdução

Melhorar a aparência visual dos gráficos do Excel é crucial ao preparar relatórios ou dashboards, especialmente se você estiver usando Java. Com Aspose.Cells — uma biblioteca poderosa para gerenciamento e manipulação de planilhas — você pode **how to set shape** de rótulos de dados de gráfico em apenas algumas linhas de código. Este tutorial o guiará na alteração da forma dos rótulos de dados em um gráfico do Excel usando Aspose.Cells para Java. Ao final, você saberá como:

- Acessar e modificar rótulos de dados do gráfico
- Definir formas personalizadas para rótulos de dados
- Salvar alterações no seu workbook

## Respostas rápidas
- **Qual é a classe principal para trabalhar com arquivos Excel?** `Workbook` representa um arquivo Excel completo na memória.  
- **Qual método define a forma do rótulo?** `setShapeType(DataLabelShapeType shape)` em um objeto `DataLabel`.  
- **Preciso de uma licença para desenvolvimento?** Uma licença temporária gratuita funciona para avaliação; uma licença completa é necessária para produção.  
- **Posso aplicar a forma a várias séries?** Sim — itere sobre cada série e chame `setShapeType`.  
- **Esta abordagem é compatível com workbooks grandes?** Aspose.Cells processa workbooks de várias centenas de páginas sem carregar o arquivo inteiro na memória.  

## O que é how to set shape?
A expressão **how to set shape** refere‑se à configuração do contorno visual de um rótulo de dados de um gráfico, como transformar um retângulo simples em um balão ou elipse. Alterar a forma melhora a legibilidade e destaca pontos de dados importantes. Ao selecionar uma forma apropriada, você pode fazer o rótulo sobressair, agrupar pontos relacionados ou corresponder às diretrizes de identidade corporativa, melhorando assim a legibilidade geral do gráfico.

## Por que usar Aspose.Cells para personalização de rótulos de gráfico?
Aspose.Cells suporta **mais de 50 formatos de entrada e saída** — incluindo XLSX, CSV, ODS e PDF — e pode manipular workbooks contendo **até 1 milhão de linhas** sem esgotar a memória. Sua API permite modificar gráficos programaticamente, eliminando a necessidade de edições manuais no Excel e garantindo estilos consistentes em relatórios automatizados.

## Pré-requisitos

- **Aspose.Cells for Java Library**: Versão 25.3 ou posterior é necessária.
- **Java Development Environment**: JDK instalado na sua máquina.
- **IDE Setup**: Use uma IDE como IntelliJ IDEA ou Eclipse para escrever e executar seu código.

### Bibliotecas e dependências necessárias

Para usuários Maven, inclua a seguinte dependência no seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Usuários Gradle devem adicionar isto ao seu arquivo `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Aquisição de licença

Aspose.Cells oferece uma licença de avaliação gratuita, que você pode obter na [página de licença temporária da Aspose](https://purchase.aspose.com/temporary-license/). Isso permite acesso total a todos os recursos sem limitações por um período limitado.

## Configurando Aspose.Cells para Java

Depois que seu ambiente estiver pronto, vamos configurar o Aspose.Cells. Veja como começar:

### Etapas de instalação

1. **Baixar a biblioteca**: Use Maven ou Gradle conforme mostrado acima.
2. **Configuração de licença**:  
   - `License` é uma classe que aplica seu arquivo de licença Aspose.Cells para habilitar a funcionalidade completa.  
   - Baixe e aplique uma licença temporária usando este trecho de código após inicializar o objeto `Workbook`:

    ```java
    License license = new License();
    license.setLicense("path/to/your/license/file");
    ```
3. **Inicialização básica**: Crie uma instância `Workbook` para começar a trabalhar com arquivos Excel.

## Como definir a forma dos rótulos de dados em um gráfico?

Carregue seu workbook, localize o gráfico alvo e aplique a forma desejada aos seus rótulos de dados. As etapas diretas a seguir realizam isso em menos de um minuto.

### Guia passo a passo

#### Etapa 1: carregue seu workbook

A classe `Workbook` é o objeto de nível superior do Aspose.Cells que representa um único arquivo Excel na memória. Use `new Workbook("input.xlsx")` para carregar o arquivo que deseja modificar.

#### Etapa 2: acesse o gráfico

`Worksheet` representa uma única planilha dentro de um workbook.  
`Worksheet ws = workbook.getWorksheets().get(0);` recupera a primeira planilha.  
`Chart` é um objeto que representa um gráfico incorporado em uma planilha.  
`Chart chart = ws.getCharts().get(0);` obtém o primeiro gráfico nessa planilha.

#### Etapa 3: recupere as séries e modifique os rótulos de dados

`Series` representa uma série de dados plotada em um gráfico.  
Cada objeto `Series` contém uma coleção `DataLabel`.  
`DataLabel` controla a aparência de um rótulo de dados para uma série.  
`DataLabelShapeType` é uma enumeração das possíveis formas para rótulos de dados.  
Chame `series.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);` para definir a forma. A enumeração oferece dezenas de opções, como `RECTANGLE`, `CLOUD` e `WEDGE_ELLIPSE_CALLOUT`.

#### Etapa 4: salve seu workbook

Depois de aplicar a forma, invoque `workbook.save("output.xlsx");` para gravar as alterações no disco.

## Dicas de solução de problemas

- **Problemas com caminho de arquivo**: Verifique se o caminho do arquivo é absoluto ou corretamente relativo ao diretório de trabalho do seu projeto.  
- **Incompatibilidade de versão da biblioteca**: Certifique‑se de que está usando Aspose.Cells versão 25.3 ou posterior; versões mais antigas não possuem o método `setShapeType`.  
- **Tipos de gráfico não suportados**: Alguns tipos de gráfico legados (por exemplo, radar) podem não expor propriedades de forma de rótulo de dados; troque para um tipo de gráfico suportado como coluna ou linha.

## Aplicações práticas

1. **Relatórios financeiros** – Destaque margens de lucro chave com rótulos no estilo balão.  
2. **Conteúdo educacional** – Use rótulos em forma de nuvem para chamar atenção a pontos de dados importantes em materiais de ensino.  
3. **Análises de marketing** – Aplique formas personalizadas para diferenciar métricas de desempenho de campanhas em dashboards.

Integrar Aspose.Cells com pipelines de dados ou sistemas CRM permite gerar relatórios totalmente estilizados automaticamente, reduzindo o esforço manual e garantindo visualizações consistentes com a marca.

## Considerações de desempenho

Ao trabalhar com arquivos Excel grandes:

- **Otimizar uso de memória**: Chame `workbook.dispose();` após salvar para liberar recursos nativos prontamente.  
- **Processamento em lote**: Processar gráficos em grupos ao invés de um a um para minimizar a sobrecarga de criação de objetos.  
- **Manipulação eficiente de dados**: Evite cálculos pesados dentro de loops que iteram milhares de linhas; calcule valores previamente.

## Conclusão

Agora você sabe **how to set shape** de rótulos de dados de gráficos Excel em Java usando Aspose.Cells. Essa capacidade não só aprimora a estética dos gráficos, mas também melhora a compreensão dos dados para os usuários finais. Explore opções adicionais de personalização — como cores de rótulo, fontes e linhas de ligação — para refinar ainda mais suas visualizações.

Para quaisquer dúvidas ou assistência, consulte o [fórum de suporte da Aspose](https://forum.aspose.com/c/cells/9).

## Perguntas frequentes

**Q: Como altero a forma de vários rótulos de dados de uma só vez?**  
A: Percorra cada série no gráfico e chame `setShapeType` no objeto `DataLabel` da série.

**Q: O Aspose.Cells para Java pode lidar eficientemente com arquivos Excel grandes?**  
A: Sim. Com gerenciamento adequado de memória, ele processa workbooks contendo centenas de milhares de linhas sem carregar o arquivo inteiro na memória.

**Q: Quais são os problemas comuns ao configurar o Aspose.Cells?**  
A: Dependências Maven ausentes, uso de uma versão de biblioteca desatualizada ou fornecimento de um arquivo de licença inválido são armadilhas típicas.

**Q: Existe uma maneira de reverter as formas dos rótulos de dados para o padrão?**  
A: Defina o tipo de forma para `DataLabelShapeType.DEFAULT` para restaurar a aparência original.

**Q: Como posso aplicar essa personalização a vários gráficos em um workbook?**  
A: Itere sobre `ws.getCharts()` e aplique a mesma lógica `setShapeType` à coleção de séries de cada gráfico.

## Recursos

- [Documentação do Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Baixar Aspose.Cells para Java](https://releases.aspose.com/cells/java/)
- [Comprar uma Licença](https://purchase.aspose.com/buy)
- [Licença de Avaliação Gratuita](https://releases.aspose.com/cells/java/)
- [Licença Temporária](https://purchase.aspose.com/temporary-license/)

---  

**Última atualização:** 2026-10-17  
**Testado com:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose  



```java
Workbook wb = new Workbook("YOUR_DATA_DIRECTORY/sampleSetShapeTypeOfDataLabelsOfChart.xlsx");
```
```java
Worksheet ws = wb.getWorksheets().get(0);
Chart ch = ws.getCharts().get(0);
```
```java
Series srs = ch.getNSeries().get(0);
srs.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);
```
```java
wb.save("YOUR_OUTPUT_DIRECTORY/outputSetShapeTypeOfDataLabelsOfChart.xlsx");
```

## Tutoriais relacionados

- [Modificar rótulos de dados de gráficos Excel usando Aspose.Cells Java](/cells/java/charts-graphs/modify-excel-chart-data-labels-aspose-cells-java/)
- [Como redimensionar rótulos em gráficos Excel com Aspose.Cells para Java](/cells/java/charts-graphs/aspose-cells-java-auto-resize-chart-data-labels/)
- [Adicionar rótulos a gráficos Excel com Aspose Cells para Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}