---
date: 2026-02-09
description: Aprenda a adicionar rótulos de dados a gráficos do Excel e a alterar
  o tipo de gráfico usando Aspose.Cells para Java, além de dicas de ferramenta e interatividade
  de drill‑down.
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Adicionar rótulos de dados ao gráfico do Excel com Aspose.Cells Java
url: /pt/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar Rótulos de Dados ao Gráfico do Excel e Alterar o Tipo de Gráfico – Aspose.Cells Java

Gráficos interativos dão aos seus relatórios Excel um novo nível de insight, e **adicionar rótulos de dados ao gráfico do Excel** torna a informação instantaneamente legível. Neste tutorial você aprenderá como **adicionar rótulos de dados ao gráfico do Excel**, mudar o tipo de gráfico e criar soluções Java interativas com Aspose.Cells. Também mostraremos como adicionar tooltips e um hyperlink simples de drill‑down para que seu público possa explorar os dados em profundidade.

## Respostas Rápidas
- **Qual biblioteca é usada?** Aspose.Cells for Java  
- **Posso mudar o tipo de gráfico?** Sim – basta modificar o enum `ChartType` ao criar o gráfico.  
- **Como adiciono tooltips a um gráfico?** Use a API de rótulos de dados (`setHasDataLabels(true)`) e habilite a exibição de valores.  
- **Drill‑down é suportado?** Você pode anexar hyperlinks a pontos de dados para comportamento básico de drill‑down.  
- **Pré‑requisitos?** IDE Java, JAR do Aspose.Cells e um arquivo Excel com dados de exemplo.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem o seguinte:

- Ambiente de Desenvolvimento Java (JDK 8+ recomendado)  
- Biblioteca Aspose.Cells for Java (download [aqui](https://releases.aspose.com/cells/java/))  
- Uma planilha de exemplo (`data.xlsx`) contendo os dados que você deseja visualizar  

## Etapa 1: Configurando Seu Projeto Java

1. Crie um novo projeto Java na sua IDE favorita (IntelliJ IDEA, Eclipse, etc.).  
2. Adicione o JAR do Aspose.Cells ao caminho de compilação do seu projeto ou às dependências Maven/Gradle.

## Etapa 2: Carregando Dados

Para trabalhar com gráficos, primeiro você precisa de uma planilha carregada na memória.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Etapa 3: Criando um Gráfico (e Alterando Seu Tipo)

Você pode escolher qualquer tipo de gráfico que se ajuste à sua análise. Abaixo criamos um **gráfico de colunas**, mas pode mudar facilmente para linha, pizza ou barra alterando o enum `ChartType`.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Dica profissional:** Para **alterar o tipo de gráfico do Excel**, substitua `ChartType.COLUMN` por `ChartType.LINE`, `ChartType.PIE`, etc.

## Etapa 4: Adicionando Interatividade

### 4.1. Adicionando Tooltips (Adicionar Tooltips ao Gráfico)

Tooltips aparecem quando o usuário passa o mouse sobre um ponto de dados. O código a seguir habilita rótulos de dados e mostra o valor como tooltip.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Adicionando Rótulos de Dados – **add data labels to excel chart**

Rótulos de dados fornecem uma pista visual permanente no próprio gráfico. Você pode exibi‑los como balões para melhorar a legibilidade.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

> **Por que adicionar rótulos de dados?** Incluir rótulos de dados diretamente no gráfico elimina a necessidade de o usuário passar o mouse ou adivinhar valores, melhorando a clareza do relatório.

### 4.3. Implementando Drill‑Down (Hyperlink em um Ponto de Dados)

Uma maneira simples de adicionar capacidade de drill‑down é anexar um hyperlink a um ponto específico. Clicar no ponto abre uma página web com informações detalhadas.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Etapa 5: Salvando a Planilha

Depois de configurar o gráfico, persista a planilha para que os recursos interativos sejam armazenados no arquivo de saída.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Problemas Comuns & Soluções

| Problema | Solução |
|----------|---------|
| **Tooltips não aparecem** | Certifique‑se de que `setHasDataLabels(true)` seja chamado antes de configurar `setShowValue(true)`. |
| **Hyperlink não é clicável** | Verifique se o formato de saída suporta hyperlinks (ex.: XLSX, não CSV). |
| **Tipo de gráfico não muda** | Verifique se você alterou o enum `ChartType` correto ao adicionar o gráfico. |

## Perguntas Frequentes

**P: Como posso mudar o tipo de gráfico depois que ele foi criado?**  
R: Você precisa criar um novo gráfico com o `ChartType` desejado. O Aspose.Cells não oferece conversão in‑place, então remova o gráfico antigo e adicione um novo.

**P: Posso personalizar a aparência dos tooltips?**  
R: Sim. Use as propriedades do `DataLabel` como `setFontSize`, `setFontColor` e `setBackgroundColor` para estilizar o texto do tooltip.

**P: Como trato interações do usuário em uma aplicação web?**  
R: Exporte a planilha para um arquivo HTML ou XLSX e use JavaScript no lado do cliente para capturar eventos de clique nos elementos do gráfico.

**P: Onde posso encontrar mais exemplos e documentação?**  
R: Visite a [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) para uma lista completa de classes e métodos relacionados a gráficos.

## Conclusão

Agora você sabe como **adicionar rótulos de dados ao gráfico do Excel**, **alterar o tipo de gráfico do Excel**, **criar soluções Java de gráficos interativos**, e enriquecer esses gráficos com tooltips, rótulos de dados e hyperlinks de drill‑down usando Aspose.Cells for Java. Essas melhorias tornam seus relatórios Excel muito mais envolventes e informativos para os usuários finais.

---

**Última atualização:** 2026-02-09  
**Testado com:** Aspose.Cells for Java 24.12  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}