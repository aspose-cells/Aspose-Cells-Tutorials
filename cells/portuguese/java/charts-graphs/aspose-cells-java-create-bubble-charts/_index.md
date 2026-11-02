---
date: '2026-04-02'
description: Aprenda como criar gráficos e gerar gráficos de bolhas no Excel usando
  Aspose.Cells para Java. Este guia orienta você na configuração, nos dados e na gravação
  do gráfico.
keywords:
- how to create chart
- generate excel bubble chart
- set bubble chart data
title: 'Como criar gráfico: Gráfico de bolhas do Excel com Aspose.Cells Java'
url: /pt/java/charts-graphs/aspose-cells-java-create-bubble-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Como Criar Gráfico: Gráfico de Bolhas do Excel com Aspose.Cells Java

Aprimore seus relatórios do Excel com gráficos de bolhas dinâmicos usando Aspose.Cells para Java. Neste tutorial, você aprenderá **como criar objetos de gráfico** que visualizam dados como gráficos de bolhas, tornando suas apresentações mais perspicazes e interativas. Percorreremos cada passo — desde a configuração do ambiente de desenvolvimento até a configuração dos dados do gráfico e, finalmente, a gravação da pasta de trabalho.

## Respostas Rápidas
- **Qual biblioteca é a melhor para gráficos do Excel em Java?** Aspose.Cells for Java.
- **Posso gerar um gráfico de bolhas do Excel programaticamente?** Sim, usando a API de gráficos mostrada abaixo.
- **Preciso de uma licença para executar o código?** Uma avaliação gratuita funciona, mas uma licença completa desbloqueia todos os recursos.
- **Quais ferramentas de construção Java são suportadas?** Maven e Gradle são suportados.
- **Qual é o método principal para definir os dados do gráfico de bolhas?** Use `setBubbleSizes`, `setXValues` e `setValues` na série.

## O que é um Gráfico de Bolhas?
Um gráfico de bolhas é uma variação de um diagrama de dispersão onde cada ponto de dados é representado por uma bolha. O eixo X e o eixo Y determinam a posição, enquanto o tamanho da bolha transmite uma terceira dimensão de informação — perfeito para visualizar dados financeiros, de vendas ou científicos.

## Por que Usar Aspose.Cells para Java?
- **Motor Excel sem instalação** – não é necessário o Microsoft Office no servidor.
- **API de gráficos avançada** – suporta todos os tipos modernos de gráficos, incluindo gráficos de bolhas.
- **Multiplataforma** – funciona no Windows, Linux e macOS.
- **Alto desempenho** – otimizado para grandes conjuntos de dados e geração de relatórios em alto volume.

## Pré-requisitos
Para criar gráficos de bolhas usando Aspose.Cells para Java, certifique‑se de atender aos seguintes pré‑requisitos:

### Bibliotecas e Dependências Necessárias
- **Aspose.Cells for Java**: Instale a versão mais recente (por exemplo, 25.3).

### Requisitos de Configuração do Ambiente
- Kit de Desenvolvimento Java (JDK) compatível instalado.
- Configure seu projeto para usar Maven ou Gradle.

### Pré-requisitos de Conhecimento
- Compreensão básica de programação Java.
- Familiaridade com estruturas de arquivos Excel e tipos de gráficos.

## Configurando Aspose.Cells para Java
Configurar seu ambiente é crucial. Veja como começar:

### Instalando via Maven
Adicione a seguinte dependência ao seu `pom.xml`:
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Instalando via Gradle
Para quem usa Gradle, adicione isto ao seu `build.gradle`:
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Aquisição de Licença
Aspose.Cells oferece uma avaliação gratuita com funcionalidade limitada. Para recursos completos:
- **Compra**: Visite a [página de compra](https://purchase.aspose.com/buy) para opções de licenciamento.
- **Licença Temporária**: Obtenha uma licença temporária [aqui](https://purchase.aspose.com/temporary-license/) para testar totalmente.

### Inicialização Básica
Antes de usar Aspose.Cells, inicialize-o em seu projeto Java:
```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook object
Workbook workbook = new Workbook();
```

## Guia de Implementação
Vamos dividir o processo de criação e configuração de gráficos de bolhas com Aspose.Cells.

### Como Criar Gráfico: Inicializando um Objeto Workbook
Um `Workbook` representa um arquivo Excel completo, permitindo que você manipule planilhas, células e mais. Inicialize-o da seguinte forma:
```java
import com.aspose.cells.Workbook;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

### Como Definir Dados do Gráfico de Bolhas: Acessando e Manipulando Planilhas
Prepare os dados que alimentarão o gráfico de bolhas:
```java
import com.aspose.cells.WorksheetCollection;
import com.aspose.cells.Cells;
import com.aspose.cells.Cell;

// Get the collection of worksheets
WorksheetCollection worksheets = workbook.getWorksheets();
Worksheet sheet = worksheets.get(0);
Cells cells = sheet.getCells();

// Set values in specific cells to prepare data for charting
cells.get("A1").setValue(50);
cells.get("A2").setValue(100);
cells.get("A3").setValue(150);
cells.get("B1").setValue(4);
cells.get("B2").setValue(20);
cells.get("B3").setValue(180);
cells.get("C1").setValue(320);
cells.get("C2").setValue(110);
cells.get("C3").setValue(180);
cells.get("D1").setValue(40);
cells.get("D2").setValue(120);
cells.get("D3").setValue(250);
```

### Como Gerar Gráfico de Bolhas do Excel: Criando e Configurando o Gráfico
Crie um gráfico de bolhas adicionando-o à planilha e definindo suas fontes de dados:
```java
import com.aspose.cells.ChartCollection;
import com.aspose.cells.Chart;
import com.aspose.cells.SeriesCollection;
import com.aspose.cells.ChartType;

// Access the collection of charts in the sheet
ChartCollection charts = sheet.getCharts();
int chartIndex = charts.add(ChartType.BUBBLE, 5, 0, 15, 5);
Chart chart = charts.get(chartIndex);

// Add series to the chart and set data sources
SeriesCollection serieses = chart.getNSeries();
serieses.add("A1:B3", true);

// Set bubble sizes, X values, and Y values for the chart
chart.getNSeries().get(0).setBubbleSizes("B2:D2");
chart.getNSeries().get(0).setXValues("B3:D3");
chart.getNSeries().get(0).setValues("B1:D1");
```

### Como Salvar o Gráfico: Salvando a Pasta de Trabalho
Persista a pasta de trabalho (e o gráfico incorporado) no disco:
```java
import com.aspose.cells.SaveFormat;

// Define the directory to save the file
String dataDir = "YOUR_DATA_DIRECTORY";
workbook.save(dataDir + "/HToCrBChart_out.xls", SaveFormat.EXCEL_97_TO_2003);
```

## Aplicações Práticas
- **Relatórios Financeiros** – Visualize receita, lucro e participação de mercado em uma única visualização.
- **Análise de Dados de Vendas** – Destaque o desempenho de vendas regional onde o tamanho da bolha indica volume.
- **Pesquisa Científica** – Exiba resultados experimentais com três variáveis simultaneamente.

## Considerações de Desempenho
- Libere objetos não utilizados prontamente para liberar memória.
- Mantenha os intervalos de dados o mais restritos possível; intervalos grandes e desnecessários podem desacelerar a renderização.
- Use as melhores práticas de gerenciamento de memória do Java ao processar conjuntos de dados massivos.

## Problemas Comuns e Soluções
| Problema | Causa | Solução |
|----------|-------|----------|
| **Gráfico vazio** | Intervalos de dados não correspondem às séries | Verifique se `setBubbleSizes`, `setXValues` e `setValues` referenciam as células corretas. |
| **Tamanhos de bolha incorretos** | Comprimentos de intervalo incompatíveis | Garanta que todos os três intervalos contenham o mesmo número de pontos. |
| **Exceção de licença** | Executando sem uma licença válida | Aplique uma licença temporária ou comprada antes de criar a pasta de trabalho. |

## Perguntas Frequentes

**Q: Qual é a versão mínima do Aspose.Cells necessária?**  
A: A versão 25.3 é recomendada para este tutorial para garantir compatibilidade com todos os recursos demonstrados.

**Q: Como posso personalizar as cores do gráfico de bolhas?**  
A: Use os métodos de formatação da série, como `chart.getNSeries().get(0).getArea().getFillFormat().setForeColor(Color.getRed())`.

**Q: Posso executar este código em servidores Linux?**  
A: Sim, Aspose.Cells para Java é totalmente multiplataforma e funciona em qualquer SO com um JDK compatível.

**Q: O que devo fazer se receber um erro “Data source size mismatch”?**  
A: Verifique novamente se os intervalos para tamanhos de bolhas, valores X e valores Y contêm o mesmo número de células.

**Q: Onde posso obter uma licença temporária para testes?**  
A: Visite a [página de licença temporária da Aspose](https://purchase.aspose.com/temporary-license/) para solicitar uma licença de avaliação.

## Recursos
- **Documentação**: Para mais detalhes, consulte a [documentação oficial](https://reference.aspose.com/cells/java/).
- **Download**: Obtenha a versão mais recente na [página de lançamentos](https://releases.aspose.com/cells/java/).
- **Compra**: Explore opções de licenciamento nesta [página](https://purchase.aspose.com/buy).
- **Teste Gratuito**: Comece com um teste gratuito para testar recursos na [seção de lançamentos da Aspose](https://releases.aspose.com/cells/java/).
- **Fórum de Suporte**: Para quaisquer dúvidas, o [fórum de suporte](https://forum.aspose.com/c/cells/9) está disponível.

---

**Última atualização:** 2026-04-02  
**Testado com:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}