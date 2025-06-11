---
"date": "2025-04-05"
"description": "Aprenda a criar gráficos de pizza dinâmicos com linhas de chamada usando o Aspose.Cells para .NET. Siga este guia para aprimorar suas habilidades de visualização de dados."
"title": "Criando gráficos de pizza com linhas de chamada no Aspose.Cells .NET - Um guia completo"
"url": "/pt/net/charts-graphs/create-pie-charts-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Criando gráficos de pizza com linhas de chamada usando Aspose.Cells .NET

## Introdução
Aprimore sua visualização de dados criando gráficos de pizza mais informativos com o Aspose.Cells para .NET. Este guia passo a passo mostra como adicionar linhas de chamada a segmentos de gráficos de pizza, facilitando a identificação rápida das categorias de dados correspondentes. Seguindo este tutorial, suas visualizações ficarão visualmente atraentes e altamente funcionais.

**O que você aprenderá:**
- Configurando Aspose.Cells para .NET em seu ambiente
- Criação de gráficos de pizza de linha de liderança personalizados usando C#
- Salvando o gráfico como uma imagem ou em uma pasta de trabalho do Excel

Certifique-se de ter tudo pronto para acompanhar de forma eficaz.

## Pré-requisitos
Antes de começar, certifique-se de atender a estes pré-requisitos:

- **Bibliotecas e Versões**: Instale o Aspose.Cells para .NET. Certifique-se de que seu projeto esteja configurado com a versão mais recente.
- **Configuração do ambiente**: Este guia pressupõe um ambiente .NET compatível para Aspose.Cells.
- **Pré-requisitos de conhecimento**Familiaridade básica com programação em C# e operações do Excel é benéfica.

## Configurando Aspose.Cells para .NET
Para começar, instale o Aspose.Cells no seu projeto via:

**.NET CLI**
```bash
dotnet add package Aspose.Cells
```

**Gerenciador de Pacotes**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

Obtenha uma licença para funcionalidade completa selecionando entre as seguintes opções:
- **Teste grátis**: Comece seu teste gratuito no [Página de download do Aspose](https://releases.aspose.com/cells/net/).
- **Licença Temporária**: Obter uma licença temporária [aqui](https://purchase.aspose.com/temporary-license/).
- **Comprar**: Para obter todos os recursos, adquira uma licença [aqui](https://purchase.aspose.com/buy).

Inicialize Aspose.Cells em seu projeto criando uma instância do `Workbook` aula.

## Guia de Implementação

### Criando a pasta de trabalho e a planilha
1. **Inicializar a pasta de trabalho**
   Crie uma nova pasta de trabalho no formato XLSX:
   ```csharp
   Workbook workbook = new Workbook(FileFormatType.Xlsx);
   ```

2. **Acessando a Primeira Planilha**
   Use a primeira planilha para inserir dados:
   ```csharp
   Worksheet worksheet = workbook.Worksheets[0];
   ```

3. **Adicionando dados para gráfico de pizza**
   Preencha sua planilha com categorias e valores:
   ```csharp
   worksheet.Cells["A1"].PutValue("Retail");
   // Adicione os nomes das categorias restantes...
   worksheet.Cells["B1"].PutValue(10.4);
   // Adicione os valores correspondentes...
   ```

### Adicionando um gráfico de pizza à planilha
1. **Crie o gráfico de pizza**
   Gere um gráfico de pizza e adicione-o à coleção de gráficos da sua planilha:
   ```csharp
   int id = worksheet.Charts.Add(ChartType.Pie, 3, 3, 23, 13);
   ```

2. **Configurar dados de séries e categorias**
   Vincule os dados das séries e categorias:
   ```csharp
   Chart chart = worksheet.Charts[id];
   chart.NSeries.Add("B1:B16", true);
   chart.NSeries.CategoryData = "A1:A16";
   ```

3. **Personalizar rótulos de dados**
   Desative a exibição de legendas e defina rótulos de dados para mostrar nomes de categorias e porcentagens:
   ```csharp
   chart.ShowLegend = false;
   DataLabels dataLabels = chart.NSeries[0].DataLabels;
   dataLabels.ShowCategoryName = true;
   dataLabels.ShowPercentage = true;
   dataLabels.Position = LabelPositionType.OutsideEnd;
   ```

### Implementando Linhas de Líder
1. **Ativar linhas de liderança**
   Habilite linhas de liderança para conexões visuais mais claras:
   ```csharp
   chart.NSeries[0].HasLeaderLines = true;
   ```

2. **Ajustar a posição dos rótulos de dados**
   Garanta a visibilidade ajustando as posições dos rótulos:
   ```csharp
   int DELTA = 100;
   foreach (var point in chart.NSeries[0].Points)
   {
       int X = point.DataLabels.X;
       if (X > 2000) 
           point.DataLabels.X += DELTA;
       else 
           point.DataLabels.X -= DELTA;
   }
   ```

### Salvando o gráfico e a pasta de trabalho
1. **Salvar como imagem**
   Renderize o gráfico em um arquivo de imagem:
   ```csharp
   ImageOrPrintOptions options = new ImageOrPrintOptions { ImageType = Drawing.ImageType.Png, HorizontalResolution = 200, VerticalResolution = 200 };
   chart.ToImage("output_out.png", options);
   ```

2. **Salvar pasta de trabalho**
   Salve a pasta de trabalho para visualizar o gráfico no Excel:
   ```csharp
   workbook.Save("output_out.xlsx");
   ```

## Aplicações práticas
- **Relatórios Financeiros**:Represente claramente as alocações orçamentárias.
- **Análise de Marketing**: Visualize dados de participação de mercado de forma eficaz em apresentações ou relatórios.
- **Análise de Vendas**Exiba a distribuição de vendas entre diferentes regiões/produtos com facilidade.

As possibilidades de integração incluem exportar essas visualizações para aplicativos da web ou incorporá-las em ferramentas de relatórios automatizadas.

## Considerações de desempenho
Ao usar Aspose.Cells, considere o seguinte para um desempenho ideal:
- Minimize grandes conjuntos de dados carregados na memória de uma só vez.
- Use loops eficientes e evite cálculos desnecessários dentro deles.
- Limpe regularmente recursos, como objetos de pasta de trabalho, para evitar vazamentos de memória.

## Conclusão
Você aprendeu a criar gráficos de pizza com linhas de chamada usando o Aspose.Cells para .NET. Essa funcionalidade aprimora a clareza das suas visualizações de dados, tornando-as mais acessíveis e impactantes. 

**Próximos passos:**
Explore mais personalizações na aparência dos gráficos ou experimente outros tipos de gráficos disponíveis no Aspose.Cells.

## Seção de perguntas frequentes
1. **O que é uma linha líder em um gráfico de pizza?**
   As linhas de liderança conectam rótulos de dados aos seus respectivos segmentos, melhorando a legibilidade.

2. **Posso usar o Aspose.Cells gratuitamente?**
   Sim, você pode começar com uma avaliação gratuita, mas os recursos completos exigem uma licença.

3. **É possível exportar gráficos como imagens?**
   Com certeza! Use `ImageOrPrintOptions` para salvar seu gráfico em formatos de imagem como PNG ou JPEG.

4. **Como ajusto manualmente as posições dos rótulos de dados?**
   Modifique as coordenadas X e Y dos rótulos de dados dentro do loop de pontos da série.

5. **O Aspose.Cells pode ser integrado a outros sistemas?**
   Sim, ele pode ser usado em conjunto com bancos de dados, serviços web e muito mais para soluções de relatórios automatizados.

## Recursos
- [Documentação do Aspose.Cells](https://reference.aspose.com/cells/net/)
- [Baixar Aspose.Cells](https://releases.aspose.com/cells/net/)
- [Licença de compra](https://purchase.aspose.com/buy)
- [Teste grátis](https://releases.aspose.com/cells/net/)
- [Licença Temporária](https://purchase.aspose.com/temporary-license/)
- [Fórum de Suporte](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}