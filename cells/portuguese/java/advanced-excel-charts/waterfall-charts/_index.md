---
date: 2025-12-10
description: Aprenda a criar um gráfico de cascata em Java usando Aspose.Cells. Guia
  passo a passo para adicionar o gráfico à planilha, personalizá‑lo e salvar a pasta
  de trabalho como XLSX.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Como criar um gráfico de cascata com Aspose.Cells para Java
url: /pt/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Gráficos de Cascata

## Introdução aos Gráficos de Cascata usando Aspose.Cells para Java

Neste tutorial você aprenderá como **criar um gráfico de cascata** com Aspose.Cells para Java. Gráficos de cascata são uma ferramenta essencial na visualização de dados porque permitem ver o efeito cumulativo de uma série de valores positivos e negativos. Seja preparando um demonstrativo financeiro, um relatório de desempenho de vendas ou qualquer outra análise orientada a dados, um gráfico de cascata pode transformar números brutos em insights claros e acionáveis.

## Respostas Rápidas
- **O que é um gráfico de cascata?** Uma visualização que mostra como um valor inicial é aumentado e diminuído por uma série de valores intermediários, terminando com um total final.  
- **Qual biblioteca é usada?** Aspose.Cells para Java.  
- **Preciso de uma licença?** Uma versão de avaliação gratuita funciona para desenvolvimento; uma licença comercial é necessária para produção.  
- **Posso salvar o arquivo como XLSX?** Sim – use `workbook.save("FileName.xlsx")`.  
- **É adequado para visualização de dados em Java?** Absolutamente; Aspose.Cells fornece recursos avançados de gráficos sem necessidade do Office instalado.

## O que é um Gráfico de Cascata?
Um gráfico de cascata exibe contribuições positivas e negativas sequenciais a um valor inicial, ajudando a entender como cada componente impacta o resultado geral.

## Por que usar Aspose.Cells para Java para adicionar um Gráfico de Cascata?
- **Não requer Microsoft Excel** – gere gráficos em qualquer servidor ou pipeline de CI.  
- **Controle total sobre a formatação** – cores, rótulos de dados e eixos podem ser personalizados programaticamente.  
- **Suporta múltiplos formatos de saída** – XLSX, PDF, HTML e mais.  
- **Alto desempenho** – ideal para pastas de trabalho grandes e relatórios automatizados.

## Pré-requisitos

Antes de mergulharmos no código, certifique‑se de que você tem os seguintes pré‑requisitos em vigor:

- Aspose.Cells para Java: Você precisará ter o Aspose.Cells para Java instalado. Você pode baixá-lo [aqui](https://releases.aspose.com/cells/java/).

- Ambiente de Desenvolvimento Java: Certifique‑se de que o Java está instalado em seu sistema.

Agora, vamos começar a criar o gráfico de casc passo a passo.

## Como Criar um Gráfico de Cascata em Java

### Etapa 1: Importar Aspose.Cells

```java
import com.aspose.cells.*;
```

Primeiro, você precisa importar a biblioteca Aspose.Cells para seu projeto Java. Essa biblioteca fornece funcionalidade extensa para trabalhar com arquivos Excel, incluindo a criação de gráficos.

### Etapa 2: Inicializar Workbook e Worksheet

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Crie um novo workbook e adicione uma worksheet a ele. Usaremos essa worksheet para inserir nossos dados e **add chart to worksheet**.

### Etapa 3: Inserir Dados

Agora, vamos preencher a worksheet com os dados que queremos representar no gráfico de cascata.

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

### Etapa 4: Criar o Gráfico de Cascata

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Adicionamos um gráfico de cascata à nossa worksheet, especificamos a série de dados e os dados de categoria. Esta é a etapa central que **adds waterfall chart** à sua planilha. Você pode personalizar ainda mais a aparência do gráfico (cores, rótulos de dados, etc.) usando as propriedades do objeto `Chart`.

### Etapa 5: Salvar o Workbook

```java
workbook.save("WaterfallChart.xlsx");
```

Salve o workbook em um arquivo. O exemplo usa o formato XLSX, mas o Aspose.Cells também permite exportar para PDF, CSV e muitos outros formatos. Isso satisfaz o requisito **save workbook xlsx**.

## Problemas Comuns e Soluções

- **O gráfico aparece em branco** – Verifique se as referências de intervalo de dados (`B2:B6` e `A2:A6`) correspondem às células reais que contêm seus valores e categorias.  
- **Valores negativos não são exibidos corretamente** – Certifique‑se de que o tipo de série está definido como `ChartType.WATERFALL`; outros tipos de gráfico tratam negativos de forma diferente.  
- **Arquivo não abre no Excel** – Certifique‑se de que está usando uma versão recente do Aspose.Cells (a última versão) e que a extensão do arquivo corresponde ao formato (`.xlsx` para Excel).

## Perguntas Frequentes

### Como posso personalizar a aparência do meu gráfico de cascata?

Você pode personalizar a aparência do seu gráfico de cascata modificando propriedades como cores, rótulos de dados e rótulos dos eixos. Consulte a documentação do Aspose.Cells para orientações detalhadas.

### Posso criar múltiplos gráficos de cascata na mesma planilha?

Sim, você pode criar múltiplos gráficos de cascata na mesma planilha seguindo os mesmos passos com diferentes intervalos de dados.

### O Aspose.Cells é compatível com diferentes ambientes de desenvolvimento Java?

Sim, o Aspose.Cells para Java é compatível com vários ambientes de desenvolvimento Java, incluindo Eclipse, IntelliJ IDEA e NetBeans.

### Posso adicionar séries de dados adicionais ao meu gráfico de cascata?

Certamente, você pode adicionar mais séries de dados ao seu gráfico de cascata para representar cenários de dados complexos de forma eficaz.

### Onde posso encontrar mais recursos e exemplos para Aspose.Cells para Java?

Você pode explorar a documentação do Aspose.Cells para Java em [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) para informações aprofundadas e exemplos de código.

---

**Última atualização:** 2025-12-10  
**Testado com:** Aspose.Cells para Java 24.12 (mais recente)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}