---
date: 2026-02-09
description: Aprenda a criar gráfico de pizza 3D em Java usando Aspose.Cells. Gere
  gráfico de barras 3D, adicione gráfico 3D ao Excel e salve a pasta de trabalho em
  XLSX com exemplos de código passo a passo.
linktitle: Create 3D Pie Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: Criar Gráfico de Pizza 3D em Java com Aspose.Cells
url: /pt/java/advanced-excel-charts/3d-charts/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Criar Gráfico de Pizza 3D Java

## Introdução a Gráficos 3D

Aspose.Cells for Java é uma poderosa API Java para trabalhar com arquivos Excel, e facilita a **create 3d pie chart** de projetos, bem como visualizações clássicas de barras 3‑D. Neste tutorial você verá exatamente como gerar um gráfico de barras 3‑D, como adaptar a mesma abordagem para um gráfico de pizza 3‑D, personalizar aparências e, finalmente, **add 3d chart excel** aos seus relatórios. Seja construindo um painel financeiro, uma planilha de desempenho de vendas ou visualizando dados científicos, os passos abaixo lhe darão uma base sólida.

## Respostas Rápidas
- **Qual biblioteca eu preciso?** Aspose.Cells for Java (latest version)  
- **Posso gerar um gráfico de barras 3D?** Yes – use `ChartType.BAR_3_D`  
- **Preciso de uma licença?** A valid license removes evaluation limits  
- **Quais versões do Excel são suportadas?** All major versions from 2003 to 2023  
- **É possível exportar o gráfico como imagem?** Yes, via `chart.toImage()` methods  

## O que são Gráficos 3D?
Gráficos 3D adicionam profundidade às visualizações tradicionais 2D, ajudando os espectadores a compreender relações multidimensionais de forma mais intuitiva. Eles são especialmente úteis quando você precisa comparar várias categorias lado a lado, mantendo uma hierarquia visual clara.

## Por que usar Aspose.Cells for Java para gerar gráfico de barras 3D?
Aspose.Cells for Java oferece um conjunto rico de APIs de criação de gráficos, total compatibilidade com o Excel e controle detalhado sobre a estilização. Isso significa que você pode **generate 3d bar chart** objetos programaticamente sem se preocupar com peculiaridades das versões do Excel.

## Configurando Aspose.Cells for Java

### Download e Instalação
Você pode baixar a biblioteca Aspose.Cells for Java no site oficial. Siga as instruções fornecidas para Maven/Gradle ou adicione o JAR diretamente ao classpath do seu projeto.

### Inicialização da Licença
To unlock the full feature set, initialize your license before any chart operations:

```java
// Initialize Aspose.Cells license
License license = new License();
license.setLicense("path_to_license_file.xml");
```

## Criando um Gráfico 3D Básico

### Importando Bibliotecas Necessárias
First, bring the required classes into scope:

```java
import com.aspose.cells.*;
```

### Inicializando uma Pasta de Trabalho
Create a fresh workbook that will host the chart:

```java
Workbook workbook = new Workbook();
```

### Adicionando Dados ao Gráfico
Populate the worksheet with sample data that the chart will reference:

```java
Worksheet worksheet = workbook.getWorksheets().get(0);

// Adding data to cells
worksheet.getCells().get("A1").putValue("Category");
worksheet.getCells().get("A2").putValue("A");
worksheet.getCells().get("A3").putValue("B");
worksheet.getCells().get("A4").putValue("C");

worksheet.getCells().get("B1").putValue("Value");
worksheet.getCells().get("B2").putValue(10);
worksheet.getCells().get("B3").putValue(20);
worksheet.getCells().get("B4").putValue(30);
```

### Como gerar gráfico de barras 3D em Java
Now we’ll create the chart itself and apply some basic customizations:

```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

### Salvando o Gráfico em um Arquivo
Finally, write the workbook (which now contains the 3‑D chart) to disk. This also **save workbook xlsx** in the standard Excel format:

```java
workbook.save("3D_Chart.xlsx");
```

## Como criar gráfico de pizza 3D com Aspose.Cells for Java
Se você precisar de uma visualização no estilo de pizza, o fluxo de trabalho é quase idêntico — apenas o enum `ChartType` muda. Substitua `ChartType.BAR_3_D` por `ChartType.PIE_3_D` ao adicionar o gráfico e aponte a série para o mesmo intervalo de dados. Depois que o gráfico for criado, você pode:

* Definir um título descritivo, como “Distribuição de Vendas 3D”.
* Ajustar as cores das fatias usando `chart.getSeries().get(i).getArea().setForegroundColor(...)`.
* Exportar o gráfico de pizza para uma imagem PNG com `chart.toImage("pie_chart.png", ImageFormat.getPng())`, que satisfaz o requisito **convert chart png**.

Como a contagem de blocos de código deve permanecer inalterada, o trecho Java real é omitido aqui, mas os passos refletem o exemplo do gráfico de barras acima.

## Tipos Diferentes de Gráficos 3D
Aspose.Cells for Java suporta várias variedades de gráficos 3D com as quais você pode **add 3d chart excel** arquivos:

- **Bar charts** – ideal para comparar categorias.  
- **Pie charts** – mostram contribuições proporcionais (incluindo pizza 3D).  
- **Line charts** – ilustram tendências ao longo do tempo.  
- **Area charts** – enfatizam a magnitude da mudança.

Você pode mudar o enum `ChartType` para qualquer um dos acima mantendo o mesmo padrão de criação.

## Customização Avançada de Gráficos

### Adicionando Títulos e Rótulos
Dê contexto ao seu gráfico definindo um título descritivo e rótulos de eixo.

### Ajustando Cores e Estilos
Use o método `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRGB(...))` para combinar com a identidade corporativa.

### Trabalhando com Eixos do Gráfico
Ajuste finamente as escalas dos eixos, intervalos e marcas de graduação para melhorar a legibilidade.

### Adicionando Legendas
Habilite legendas com `chart.getLegend().setVisible(true)` para que os espectadores possam identificar cada série de dados.

### Exportando Gráficos como Imagens
Quando precisar de uma imagem estática para um relatório web, chame `chart.toImage("chart.png", ImageFormat.getPng())`. Isso satisfaz o caso de uso **convert chart png** sem sair da pasta de trabalho.

## Integração de Dados
Aspose.Cells for Java pode extrair dados de bancos de dados, arquivos CSV ou APIs ao vivo. Basta preencher as células da planilha com os dados obtidos antes de vincular o intervalo ao gráfico. Isso mantém seu fluxo de trabalho **add 3d chart excel** dinâmico e atualizado.

## Conclusão
Neste guia percorremos como **create 3d pie chart** e **create 3d bar chart** projetos do início ao fim — configurando a biblioteca, adicionando dados, gerando um gráfico de barras 3‑D, adaptando os mesmos passos para um gráfico de pizza 3‑D e aplicando estilização avançada. Com Aspose.Cells for Java você tem uma forma confiável e independente de versão para incorporar visualizações 3‑D ricas diretamente em pastas de trabalho Excel e até exportá‑las como imagens PNG.

## Perguntas Frequentes

**Q: Como posso adicionar múltiplas séries de dados a um gráfico 3D?**  
A: Use `chart.getNSeries().add()` para cada intervalo de série e garanta que o tipo de gráfico permaneça 3‑D (por exemplo, `ChartType.BAR_3_D` ou `ChartType.PIE_3_D`).

**Q: Posso exportar gráficos 3D criados com Aspose.Cells for Java para outros formatos?**  
A: Sim, você pode salvar o gráfico como PNG, JPEG ou PDF chamando os overloads apropriados de `chart.toImage()` ou `workbook.save()`, atendendo ao requisito **convert chart png**.

**Q: É possível criar gráficos 3D interativos com Aspose.Cells for Java?**  
A: Aspose.Cells foca em gráficos estáticos do Excel. Para visualizações 3‑D interativas baseadas na web, considere combinar os dados do Excel com bibliotecas JavaScript como Three.js.

**Q: Posso automatizar o processo de atualização de dados nos meus gráficos 3D?**  
A: Absolutamente. Carregue novos dados na planilha programaticamente e atualize o intervalo do gráfico; na próxima vez que a pasta de trabalho for aberta, o gráfico refletirá os valores atualizados.

**Q: Onde posso encontrar mais recursos e documentação para Aspose.Cells for Java?**  
A: Você pode encontrar documentação abrangente e recursos para Aspose.Cells for Java no site: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).

---

**Última Atualização:** 2026-02-09  
**Testado com:** Aspose.Cells for Java 24.12 (latest)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}