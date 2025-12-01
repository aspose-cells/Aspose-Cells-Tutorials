---
date: 2025-12-01
description: Aprenda a mudar o tipo de gráfico do Excel e adicionar recursos interativos
  como dicas de ferramenta, rótulos de dados e drill‑down usando Aspose.Cells para
  Java.
language: pt
linktitle: Change Excel chart type and add interactivity
second_title: Aspose.Cells Java Excel Processing API
title: Alterar o tipo de gráfico do Excel e adicionar interatividade – Aspose.Cells
  Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Alterar o tipo de gráfico do Excel e adicionar interatividade

## Introdução

Gráficos interativos permitem que seu público explore os dados em tempo real, enquanto a capacidade de **alterar o tipo de gráfico do Excel** oferece flexibilidade para apresentar informações no formato visual mais eficaz. Neste tutorial você aprenderá a usar Aspose.Cells para Java para mudar o tipo de um gráfico, adicionar tooltips, incorporar rótulos de dados e até criar links de drill‑down — tudo sem sair do seu código Java. Ao final, você terá uma pasta de trabalho do Excel totalmente interativa, que pode ser incorporada em relatórios, dashboards ou aplicações web.

## Respostas rápidas
- **Posso alterar o tipo de gráfico programaticamente?** Sim – use o enum `ChartType` ao criar ou atualizar um gráfico.  
- **Como adiciono tooltips a um gráfico?** Habilite rótulos de dados e defina `ShowValue` como true.  
- **Qual a maneira mais fácil de adicionar links de drill‑down?** Anexe um hyperlink a um ponto de dados via `getHyperlinks().add(url)`.  
- **Preciso de licença para o Aspose.Cells?** Uma avaliação gratuita funciona para desenvolvimento; uma licença é necessária para produção.  
- **Qual versão do Java é suportada?** Java 8 ou superior são totalmente suportados.

## O que significa “alterar o tipo de gráfico do Excel”?

Alterar o tipo de gráfico significa trocar a representação visual (por exemplo, de um gráfico de colunas para um gráfico de linhas) mantendo os dados subjacentes intactos. Isso é útil quando você percebe que um tipo de gráfico diferente comunica melhor tendências, comparações ou distribuições.

## Por que adicionar interatividade aos gráficos do Excel?

- **Melhor insight dos dados:** Tooltips e rótulos de dados permitem que os usuários vejam valores exatos sem precisar rolar.  
- **Apresentações envolventes:** Elementos interativos mantêm o público interessado.  
- **Capacidade de drill‑down:** Hyperlinks permitem que os usuários naveguem para planilhas detalhadas ou recursos externos.  
- **Ativos reutilizáveis:** Uma única pasta de trabalho pode atender a múltiplos cenários de relatório simplesmente trocando o tipo de gráfico.

## Pré‑requisitos

- Ambiente de desenvolvimento Java (JDK 8+)  
- Biblioteca Aspose.Cells para Java (download em [here](https://releases.aspose.com/cells/java/))  
- Um arquivo Excel de exemplo (`data.xlsx`) contendo os dados que você deseja visualizar

## Guia passo a passo

### Etapa 1: Configurar seu projeto Java

1. Crie um novo projeto Java na sua IDE favorita (IntelliJ IDEA, Eclipse, VS Code, etc.).  
2. Adicione o JAR do Aspose.Cells ao classpath do seu projeto.

### Etapa 2: Carregar a pasta de trabalho de origem

Começamos carregando uma pasta de trabalho existente que contém os dados para o nosso gráfico.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Etapa 3: Criar um gráfico e **alterar seu tipo**

A seguir criamos um gráfico de colunas e, imediatamente, demonstramos como você pode trocá‑lo para um gráfico de linhas, se necessário.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// OPTIONAL: Change the chart type to LINE
chart.setChartType(ChartType.LINE);
```

> **Dica profissional:** Alterar o tipo de gráfico após a criação é tão simples quanto chamar `setChartType(...)`. Isso atende à palavra‑chave principal **alterar o tipo de gráfico do Excel** sem precisar criar um novo objeto de gráfico.

### Etapa 4: Adicionar interatividade

#### 4.1 Adicionar tooltips ao gráfico

Tooltips são exibidos quando o usuário passa o mouse sobre um ponto de dados. No Aspose.Cells eles são implementados via rótulos de dados.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

#### 4.2 Adicionar rótulos de dados (**add data labels chart**)

Rótulos de dados podem mostrar o valor exato, o nome da categoria ou ambos. Aqui usamos um estilo de balão.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

#### 4.3 Implementar drill‑down (**add drill down excel**)

Um link de drill‑down permite que os usuários cliquem em um ponto e naveguem para uma visualização detalhada, seja dentro da pasta de trabalho ou em uma página web.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

### Etapa 5: Salvar a pasta de trabalho

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Problemas comuns e soluções

| Problema | Motivo | Solução |
|----------|--------|---------|
| Tooltips não aparecem | `HasDataLabels` não está habilitado | Certifique‑se de chamar `setHasDataLabels(true)` antes de configurar `ShowValue`. |
| Link de drill‑down não funciona | URL do hyperlink está malformada | Verifique se a URL começa com `http://` ou `https://`. |
| Tipo de gráfico não muda | Versão antiga do Aspose.Cells | Atualize para a versão mais recente (testada com 24.12). |

## Perguntas frequentes

**P: Como posso mudar o tipo de gráfico depois que ele foi criado?**  
R: Chame `chart.setChartType(ChartType.SUA_ESCOLHA)` no objeto `Chart` existente. Isso atende diretamente ao requisito **alterar o tipo de gráfico do Excel**.

**P: Posso personalizar a aparência dos tooltips?**  
R: Sim. Use `chart.getNSeries().get(0).getPoints().getDataLabels()` para definir tamanho da fonte, cor e plano de fundo.

**P: É possível adicionar vários links de drill‑down em um único gráfico?**  
R: Absolutamente. Percorra os pontos e chame `getHyperlinks().add(url)` para cada ponto que desejar vincular.

**P: O Aspose.Cells suporta outros tipos de gráfico, como pizza ou radar?**  
R: Todos os tipos de gráfico definidos no enum `ChartType` são suportados, incluindo `PIE`, `RADAR`, `AREA`, etc.

**P: Onde posso encontrar mais exemplos?**  
R: Visite a [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) oficial para a lista completa de métodos relacionados a gráficos.

## Conclusão

Agora você sabe como **alterar o tipo de gráfico do Excel**, incorporar **tooltips**, adicionar **rótulos de dados** e criar links de **drill‑down** usando Aspose.Cells para Java. Esses recursos interativos transformam planilhas estáticas em ferramentas dinâmicas de exploração de dados, perfeitas para dashboards, relatórios e análises baseadas na web.

---

**Última atualização:** 2025-12-01  
**Testado com:** Aspose.Cells 24.12 para Java  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}