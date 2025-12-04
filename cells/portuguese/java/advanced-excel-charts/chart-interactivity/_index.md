---
date: 2025-12-04
description: Aprenda a criar gráficos interativos em Java usando Aspose.Cells, adicione
  dicas de ferramenta ao gráfico e inclua gráficos de detalhamento para uma visualização
  de dados mais rica.
language: pt
linktitle: Create Interactive Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: Criar Gráfico Interativo Java com Aspose.Cells
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Criar Gráfico Interativo Java

## Introdução

Gráficos interativos dão aos seus usuários a capacidade de explorar pontos de dados, ver detalhes ao passar o mouse e até aprofundar em conjuntos de dados maiores — tudo sem sair da planilha. Neste tutorial você aprenderá **como criar gráficos interativos Java** usando Aspose.Cells. Vamos percorrer a adição de tooltips, rótulos de dados e a implementação de uma experiência de drill‑down, para que seus gráficos se tornem mais envolventes e informativos.

## Respostas Rápidas
- **Qual biblioteca é usada?** Aspose.Cells for Java  
- **Posso adicionar tooltips ao gráfico?** Sim, usando a API de rótulo de dados NSeries  
- **O drill‑down é suportado?** Sim, anexando hyperlinks aos pontos de dados  
- **Qual formato de arquivo é produzido?** Pasta de trabalho XLSX padrão com gráficos incorporados  
- **Preciso de licença?** Uma avaliação gratuita funciona para testes; uma licença comercial é necessária para produção  

## Pré‑requisitos

Antes de começarmos, certifique‑se de que você tem:

- Um ambiente de desenvolvimento Java (JDK 8+ recomendado)  
- Biblioteca Aspose.Cells for Java (download na página oficial de [lançamento da Aspose](https://releases.aspose.com/cells/java/))  
- Um arquivo Excel de exemplo chamado **data.xlsx** contendo os dados que você deseja visualizar  

## Etapa 1: Configurando Seu Projeto Java

1. Crie um novo projeto Java na sua IDE favorita (IntelliJ IDEA, Eclipse, VS Code, etc.).  
2. Adicione o JAR do Aspose.Cells ao classpath do seu projeto — seja colocando o JAR na pasta `libs` ou adicionando a dependência Maven/Gradle.

## Etapa 2: Carregando Dados

Para construir um gráfico interativo você primeiro precisa de uma planilha com dados. O trecho abaixo abre uma pasta de trabalho existente e obtém a primeira planilha.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Dica:** Certifique‑se de que o intervalo de dados que você pretende graficar seja contíguo; o Aspose.Cells detectará automaticamente o intervalo ao vincular a série.

## Etapa 3: Criando um Gráfico

Agora criamos um gráfico de colunas e o posicionamos na planilha. Você pode mudar `ChartType.COLUMN` para qualquer outro tipo (por exemplo, `ChartType.LINE`) se preferir um estilo visual diferente.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Por que isso importa:** Adicionar o gráfico programaticamente lhe dá controle total sobre seu tamanho, posição e fonte de dados, o que é essencial para construir experiências interativas.

## Etapa 4: Adicionando Interatividade

### Como adicionar tooltips ao gráfico

Tooltips (ou rótulos de dados que mostram valores) ajudam os usuários a ver instantaneamente a figura exata por trás de cada barra. O código a seguir habilita rótulos de dados e os configura para exibir o valor.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### Como adicionar rótulos de dados (callouts)

Se você quiser que os rótulos apareçam como callouts em vez de texto simples, altere a propriedade `ShowLabelAsDataCallout`.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### Como adicionar gráfico drill‑down

Drill‑down permite que o usuário clique em um ponto de dados e vá para uma visualização detalhada relacionada — tipicamente implementado com um hyperlink. Abaixo anexamos uma URL ao primeiro ponto da série.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **Armadilha comum:** Lembre‑se de definir o destino do hyperlink para uma página que possa renderizar os dados detalhados (por exemplo, um relatório web ou outra planilha Excel). Caso contrário, o clique levará a um link morto.

## Etapa 5: Salvando a Pasta de Trabalho

Depois de configurar o gráfico, persista a pasta de trabalho. O arquivo resultante contém o gráfico interativo pronto para ser aberto no Excel ou em qualquer visualizador compatível.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Conclusão

Neste guia você aprendeu **como criar gráficos interativos Java** com Aspose.Cells, abordando:

- Carregamento de dados de uma pasta de trabalho existente  
- Criação programática de um gráfico de colunas  
- Adição de tooltips e rótulos de dados em formato callout  
- Implementação de funcionalidade drill‑down via hyperlinks  
- Salvamento da pasta de trabalho final  

Essas técnicas transformam planilhas estáticas em dashboards dinâmicos e amigáveis que aumentam a compreensão dos dados e facilitam a tomada de decisão.

## Perguntas Frequentes

**P: Como posso mudar o tipo de gráfico?**  
R: Modifique o enum `ChartType` no método `add` (por exemplo, `ChartType.LINE` para um gráfico de linhas).

**P: Posso personalizar a aparência dos tooltips?**  
R: Sim, você pode ajustar tamanho da fonte, cor, plano de fundo e outras propriedades de estilo através do objeto `DataLabels`.

**P: Como lidar com a interatividade do gráfico em uma aplicação web?**  
R: Exporte a pasta de trabalho para XLSX, então use uma biblioteca de gráficos JavaScript (por exemplo, Highcharts) para renderizar os dados no cliente, ou incorpore o arquivo Excel em um Office Web Viewer que respeite hyperlinks.

**P: Onde posso encontrar mais exemplos?**  
R: Visite a [Referência da API Aspose.Cells Java](https://reference.aspose.com/cells/java/) oficial para uma lista completa de classes e métodos relacionados a gráficos.

**P: Preciso de licença para uso em produção?**  
R: Sim, uma licença comercial é necessária para implantação; uma licença de avaliação gratuita está disponível para testes.

---

**Última atualização:** 2025-12-04  
**Testado com:** Aspose.Cells for Java 24.12 (mais recente na data de escrita)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}