---
date: 2026-02-16
description: Aprenda como definir o intervalo de dados do gráfico e criar um gráfico
  de cascata em Java usando Aspose.Cells. Guia passo a passo para adicionar série
  de dados ao gráfico, personalizá‑lo e exportar para XLSX.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Definir intervalo de dados do gráfico – Aspose.Cells for Java Gráfico de Cascata
url: /pt/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Gráficos Cascata

## Introdução aos Gráficos Cascata usando Aspose.Cells for Java

Neste tutorial, você aprenderá como **set chart data range** e criar um **waterfall chart** com Aspose.Cells for Java. Gráficos cascata são uma ferramenta essencial na visualização de dados porque permitem ver o efeito cumulativo de uma série de valores positivos e negativos. Seja preparando um demonstrativo financeiro, um relatório de desempenho de vendas ou qualquer outra análise orientada por dados, um gráfico cascata pode transformar números brutos em insights claros e acionáveis.

## Respostas Rápidas
- **What is a waterfall chart?** Um visual que mostra como um valor inicial é aumentado e diminuído por uma série de valores intermediários, terminando com um total final.  
- **Which library is used?** Aspose.Cells for Java.  
- **Do I need a license?** Um teste gratuito funciona para desenvolvimento; uma licença comercial é necessária para produção.  
- **Can I save the file as XLSX?** Sim – use `workbook.save("FileName.xlsx")`.  
- **Is it suitable for Java data visualization?** Absolutamente; Aspose.Cells fornece recursos avançados de gráficos sem precisar do Office instalado.

## O que é um Gráfico Cascata?
Um gráfico cascata exibe contribuições positivas e negativas sequenciais a um valor inicial, ajudando a entender como cada componente impacta o resultado geral.

## Por que usar Aspose.Cells for Java para adicionar um Gráfico Cascata?
- **No Microsoft Excel required** – gere gráficos em qualquer servidor ou pipeline de CI.  
- **Full control over formatting** – cores, rótulos de dados e eixos podem ser personalizados programaticamente.  
- **Supports multiple output formats** – XLSX, PDF, HTML e mais.  
- **High performance** – ideal para grandes pastas de trabalho e relatórios automatizados.

## Pré-requisitos

Antes de mergulharmos no código, certifique‑se de que você tem os seguintes pré-requisitos configurados:

- Aspose.Cells for Java: Você precisará ter o Aspose.Cells for Java instalado. Você pode baixá‑lo [aqui](https://releases.aspose.com/cells/java/).

- Ambiente de Desenvolvimento Java: Certifique‑se de que o Java está instalado em seu sistema.

Agora, vamos começar a criar o gráfico cascata passo a passo.

## Como definir o intervalo de dados do gráfico para um Gráfico Cascata em Java

### Etapa 1: Importar Aspose.Cells

```java
import com.aspose.cells.*;
```

Primeiro, você precisa importar a biblioteca Aspose.Cells para seu projeto Java. Esta biblioteca oferece funcionalidade extensa para trabalhar com arquivos Excel, incluindo a criação de gráficos.

### Etapa 2: Inicializar Workbook e Worksheet

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Crie uma nova workbook e adicione uma worksheet a ela. Usaremos esta worksheet para inserir nossos dados e **add chart to worksheet**.

### Etapa 3: Inserir Dados

Agora, vamos preencher a worksheet com os dados que queremos representar no gráfico cascata.

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

Neste exemplo, temos categorias na coluna A e valores correspondentes na coluna B. Você pode substituir esses dados pelo seu próprio conjunto de dados.

### Etapa 4: Criar o Gráfico Cascata

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Adicionamos um gráfico cascata à nossa worksheet, especificamos a série de dados e os dados de categoria. Esta é a etapa central que **adds waterfall chart** à sua planilha. Observe como o método `add` usa o intervalo `"B2:B6"` – é aqui que **set chart data range** para a série. Você pode personalizar ainda mais a aparência do gráfico (cores, rótulos de dados, etc.) usando as propriedades do objeto `Chart`.

### Etapa 5: Salvar a Workbook

```java
workbook.save("WaterfallChart.xlsx");
```

Salve a workbook em um arquivo. O exemplo usa o formato XLSX, mas o Aspose.Cells também permite que você **export excel pdf java**‑compatible arquivos como PDF, CSV e muitos outros formatos. Isso atende ao requisito **save workbook xlsx**.

## Problemas Comuns e Soluções

- **Chart appears blank** – Verifique se as referências de intervalo de dados (`B2:B6` e `A2:A6`) correspondem às células reais que contêm seus valores e categorias.  
- **Negative values not displayed correctly** – Certifique‑se de que o tipo de série está definido como `ChartType.WATERFALL`; outros tipos de gráfico tratam os negativos de forma diferente.  
- **File not opening in Excel** – Certifique‑se de que está usando uma versão recente do Aspose.Cells (a última versão) e que a extensão do arquivo corresponde ao formato (`.xlsx` para Excel).

## Perguntas Frequentes

### Como posso personalizar a aparência do meu gráfico cascata?

Você pode personalizar a aparência do seu gráfico cascata modificando propriedades como cores, rótulos de dados e rótulos de eixo. Consulte a documentação do Aspose.Cells para orientações detalhadas.

### Posso criar múltiplos gráficos cascata na mesma worksheet?

Sim, você pode criar múltiplos gráficos cascata na mesma worksheet seguindo as mesmas etapas com diferentes intervalos de dados.

### O Aspose.Cells é compatível com diferentes ambientes de desenvolvimento Java?

Sim, o Aspose.Cells for Java é compatível com vários ambientes de desenvolvimento Java, incluindo Eclipse, IntelliJ IDEA e NetBeans.

### Posso adicionar séries de dados adicionais ao meu gráfico cascata?

Certamente, você pode adicionar mais séries de dados ao seu gráfico cascata para representar cenários de dados complexos de forma eficaz. Este é um exemplo de como você pode **add data series chart** programaticamente.

### Onde posso encontrar mais recursos e exemplos para Aspose.Cells for Java?

Você pode explorar a documentação do Aspose.Cells for Java em [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) para informações detalhadas e exemplos de código.

## FAQ

**Q: Como definir o intervalo de dados do gráfico para um gráfico cascata financeiro?**  
A: Use o método `add` na série do gráfico, passando o intervalo de células que contém seus valores, por exemplo, `"B2:B6"`.

**Q: Posso exportar a workbook para PDF em vez de XLSX?**  
A: Sim, chame `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` para obter saída **export excel pdf java**‑compatible.

**Q: E se eu precisar criar um gráfico cascata financeiro com mais categorias?**  
A: Expanda o intervalo de dados tanto na coluna de valores quanto na coluna de categorias, então atualize as chamadas `add` e `setCategoryData` de acordo.

**Q: Existe uma maneira de formatar automaticamente as barras positivas e negativas?**  
A: Você pode iterar através da coleção `Series` e definir a cor `FillFormat` com base no sinal de cada valor.

**Q: O Aspose.Cells suporta atualizações dinâmicas de dados para gráficos?**  
A: Sim, você pode modificar os valores das células após o gráfico ser criado; o gráfico refletirá as alterações quando a workbook for salva.

---

**Last Updated:** 2026-02-16  
**Tested With:** Aspose.Cells for Java (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}