---
date: 2025-12-06
description: Aprenda a alterar o tipo de gráfico do Excel e criar gráficos interativos
  com Java usando Aspose.Cells. Adicione dicas de ferramenta ao gráfico, rótulos de
  dados e drill‑down para uma visualização de dados mais rica.
language: pt
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Alterar o tipo de gráfico do Excel com Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Alterar o Tipo de Gráfico do Excel e Adicionar Interatividade

## Introdução

Gráficos interativos dão aos seus relatórios Excel um novo nível de insight, permitindo que os usuários passem o mouse, cliquem e explorem pontos de dados diretamente. Neste tutorial você **alterará o tipo de gráfico do Excel** e **criará soluções de gráfico interativo em Java** com Aspose.Cells for Java. Vamos percorrer a adição de tooltips ao gráfico, rótulos de dados e um hyperlink simples de drill‑down para que seu público possa aprofundar nos números.

## Respostas Rápidas
- **Qual biblioteca é usada?** Aspose.Cells for Java  
- **Posso mudar o tipo de gráfico?** Sim – basta modificar o enum `ChartType` ao criar o gráfico.  
- **Como adiciono tooltips a um gráfico?** Use a API de rótulo de dados (`setHasDataLabels(true)`) e habilite a exibição de valores.  
- **O drill‑down é suportado?** Você pode anexar hyperlinks a pontos de dados para comportamento básico de drill‑down.  
- **Pré‑requisitos?** IDE Java, Aspose.Cells JAR e um arquivo Excel com dados de exemplo.

## Pré‑requisitos

Antes de começarmos, certifique‑se de que você tem o seguinte:

- Ambiente de Desenvolvimento Java (JDK 8+ recomendado)  
- Biblioteca Aspose.Cells for Java (download de [aqui](https://releases.aspose.com/cells/java/))  
- Uma planilha de exemplo (`data.xlsx`) contendo os dados que você deseja visualizar  

## Passo 1: Configurando Seu Projeto Java

1. Crie um novo projeto Java em sua IDE favorita (IntelliJ IDEA, Eclipse, etc.).  
2. Adicione o JAR Aspose.Cells ao caminho de compilação do seu projeto ou às dependências Maven/Gradle.

## Passo 2: Carregando Dados

Para trabalhar com gráficos, você primeiro precisa de uma planilha carregada na memória.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Passo 3: Criando um Gráfico (e Alterando Seu Tipo)

Você pode escolher qualquer tipo de gráfico que se ajuste à sua análise. Abaixo criamos um **gráfico de colunas**, mas você pode mudar facilmente para um gráfico de linhas, pizza ou barras alterando o enum `ChartType`.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Dica profissional:** Para **alterar o tipo de gráfico do Excel**, substitua `ChartType.COLUMN` por `ChartType.LINE`, `ChartType.PIE`, etc.

## Passo 4: Adicionando Interatividade

### 4.1. Adicionando Tooltips (Adicionar Tooltips ao Gráfico)

Tooltips aparecem quando o usuário passa o mouse sobre um ponto de dados. O código a seguir habilita rótulos de dados e mostra o valor como tooltip.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Adicionando Rótulos de Dados

Rótulos de dados fornecem uma pista visual permanente no próprio gráfico. Você pode exibi‑los como balões para melhor legibilidade.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Implementando Drill‑Down (Hyperlink em um Ponto de Dados)

Uma maneira simples de adicionar capacidade de drill‑down é anexar um hyperlink a um ponto específico. Clicar no ponto abre uma página web com informações detalhadas.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Passo 5: Salvando a Planilha

Depois de configurar o gráfico, persista a planilha para que os recursos interativos sejam armazenados no arquivo de saída.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Problemas Comuns & Soluções

| Problema | Solução |
|----------|---------|
| **Tooltips não aparecem** | Certifique‑se de que `setHasDataLabels(true)` seja chamado antes de configurar `setShowValue(true)`. |
| **Hyperlink não clicável** | Verifique se o formato de saída suporta hyperlinks (por exemplo, XLSX, não CSV). |
| **Tipo de gráfico não muda** | Verifique novamente se você modificou o enum `ChartType` correto ao adicionar o gráfico. |

## Perguntas Frequentes

**Q: Como posso mudar o tipo de gráfico depois que ele foi criado?**  
A: Você precisa criar um novo gráfico com o `ChartType` desejado. Aspose.Cells não fornece conversão de tipo in‑place, então remova o gráfico antigo e adicione um novo.

**Q: Posso personalizar a aparência dos tooltips?**  
A: Sim. Use as propriedades do `DataLabel` como `setFontSize`, `setFontColor` e `setBackgroundColor` para estilizar o texto do tooltip.

**Q: Como eu trato interações do usuário em uma aplicação web?**  
A: Exporte a planilha para um arquivo HTML ou XLSX e use JavaScript no lado do cliente para capturar eventos de clique nos elementos do gráfico.

**Q: Onde posso encontrar mais exemplos e documentação?**  
A: Visite a [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) para uma lista completa de classes e métodos relacionados a gráficos.

## Conclusão

Agora você sabe como **alterar o tipo de gráfico do Excel**, **criar soluções de gráfico interativo em Java** e enriquecê‑las com tooltips, rótulos de dados e hyperlinks de drill‑down usando Aspose.Cells for Java. Essas melhorias tornam seus relatórios Excel muito mais envolventes e perspicazes para os usuários finais.

---

**Última atualização:** 2025-12-06  
**Testado com:** Aspose.Cells for Java 24.12  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}