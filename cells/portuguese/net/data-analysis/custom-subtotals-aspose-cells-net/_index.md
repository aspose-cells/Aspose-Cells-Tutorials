---
"date": "2025-04-05"
"description": "Aprenda a personalizar subtotais em planilhas do Excel usando o Aspose.Cells para .NET. Este guia aborda configuração, implementação e aplicações práticas."
"title": "Como implementar subtotais personalizados no Excel usando Aspose.Cells para .NET"
"url": "/pt/net/data-analysis/custom-subtotals-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Como implementar subtotais personalizados no Excel com Aspose.Cells para .NET

## Introdução

Deseja gerar relatórios personalizados com rótulos de subtotais específicos em seus arquivos do Excel? Este guia mostrará como fazer isso usando a poderosa biblioteca Aspose.Cells para .NET. Vamos nos concentrar na criação de subtotais médios que atendam às suas necessidades.

**O que você aprenderá:**
- Configurando e usando Aspose.Cells para .NET
- Implementando uma classe personalizada para substituir nomes de subtotais padrão
- Adicionar subtotais personalizados a uma planilha do Excel
- Calculando fórmulas e ajustando larguras de colunas automaticamente

## Pré-requisitos

Antes de começar, certifique-se de ter:
- **Aspose.Cells para .NET** biblioteca instalada em seu projeto (etapas de instalação abaixo)
- Um ambiente de desenvolvimento com Visual Studio ou um IDE similar que suporte projetos C# e .NET
- Conhecimento básico de programação em C# e operações do Excel

## Configurando Aspose.Cells para .NET

Para começar, instale a biblioteca Aspose.Cells para .NET usando o Gerenciador de Pacotes NuGet ou o .NET CLI.

**CLI .NET:**
```bash
dotnet add package Aspose.Cells
```

**Console do gerenciador de pacotes:**
```powershell
PM> Install-Package Aspose.Cells
```

### Aquisição de Licença
A Aspose oferece uma licença de teste gratuita por 30 dias, permitindo que você teste todos os recursos sem limitações. Obtenha esta [aqui](https://purchase.aspose.com/temporary-license/). Para uso contínuo, considere comprar uma licença completa ou explorar opções de assinatura em seu [página de compra](https://purchase.aspose.com/buy).

### Inicialização e configuração
Uma vez instalado, importe os namespaces necessários:
```csharp
using Aspose.Cells;
```

## Guia de Implementação

Dividiremos essa implementação em etapas para ajudar você a entender cada parte do processo.

### Etapa 1: Crie uma classe de configurações personalizadas
Primeiro, crie uma classe personalizada que estenda `GlobalizationSettings`:
```csharp
class CustomSettings : GlobalizationSettings
{
    public override string GetTotalName(ConsolidationFunction functionType)
    {
        switch (functionType)
        {
            case ConsolidationFunction.Average:
                return "AVG";
            default:
                return base.GetTotalName(functionType);
        }
    }

    public override string GetGrandTotalName(ConsolidationFunction functionType)
    {
        switch (functionType)
        {
            case ConsolidationFunction.Average:
                return "GRD AVG";
            default:
                return base.GetGrandTotalName(functionType);
        }
    }
}
```
**Explicação:** Esta classe personaliza como os subtotais são nomeados para diferentes funções, como Média.

### Etapa 2: carregue sua pasta de trabalho
Carregue sua pasta de trabalho do Excel existente contendo os dados que você deseja manipular:
```csharp
Workbook book = new Workbook("sampleCustomLabelsSubtotals.xlsx");
```
**Explicação:** Substituir `"sampleCustomLabelsSubtotals.xlsx"` com o caminho do seu arquivo. Isso inicializa o `Workbook` objeto.

### Etapa 3: definir configurações de globalização personalizadas
Atribua nossas configurações personalizadas à pasta de trabalho:
```csharp
book.Settings.GlobalizationSettings = new CustomSettings();
```
**Explicação:** Isso garante que qualquer cálculo de subtotal use nossos rótulos personalizados de `CustomSettings`.

### Etapa 4: Adicionar funcionalidade de subtotal
Adicione um subtotal à sua planilha dentro de um intervalo especificado usando a função média:
```csharp
Worksheet sheet = book.Worksheets[0];
sheet.Cells.Subtotal(CellArea.CreateCellArea("A2", "B9"), 0, ConsolidationFunction.Average, new int[] { 1 });
```
**Explicação:** Isso tem como alvo as células de A2 a B9 e adiciona um subtotal médio com base na primeira coluna (índice 1).

### Etapa 5: Calcular fórmulas e ajustar colunas
Depois de adicionar os subtotais, calcule todas as fórmulas e ajuste automaticamente as colunas:
```csharp
book.CalculateFormula();
sheet.AutoFitColumns();
```
**Explicação:** `CalculateFormula()` garante que todos os cálculos estejam atualizados. `AutoFitColumns()` ajusta a largura da coluna para caber no conteúdo.

### Etapa 6: Salve sua pasta de trabalho
Salve suas alterações em um novo arquivo:
```csharp
book.Save("outputCustomLabelsSubtotals.xlsx");
```
**Explicação:** Isso salva sua pasta de trabalho modificada com subtotais personalizados e colunas ajustadas.

## Aplicações práticas
Aqui estão alguns cenários do mundo real em que subtotais personalizados podem ser inestimáveis:
1. **Relatórios financeiros**Personalize rótulos de subtotal para refletir termos financeiros específicos, como "Média líquida" ou "Receita total ajustada".
2. **Gestão de Estoque**: Use subtotais personalizados para diferentes categorias ou fornecedores em seus relatórios de inventário.
3. **Análise de dados de vendas**: Implemente cálculos médios que sejam atualizados automaticamente com novas entradas de dados de vendas.
4. **Sistemas de classificação educacional**: Personalize rótulos para representar as médias das pontuações dos alunos em todas as disciplinas.
5. **Painéis de Business Intelligence**: Adapte os rótulos de subtotal para corresponder a KPIs ou métricas específicas para maior clareza.

## Considerações de desempenho
Ao trabalhar com Aspose.Cells, considere estas dicas para otimizar o desempenho:
- **Uso eficiente da memória**: Descarte os objetos que não são mais necessários usando o `Dispose()` método.
- **Processamento em lote**: Se estiver processando várias pastas de trabalho, realize operações em lote para minimizar a sobrecarga.
- **Operações Assíncronas**:Para arquivos grandes, implemente métodos assíncronos sempre que possível.

## Conclusão
Este tutorial explorou como implementar subtotais personalizados com Aspose.Cells para .NET. Ao criar uma derivada `GlobalizationSettings` classe e manipulando dados do Excel programaticamente, você pode aprimorar seus recursos de geração de relatórios.

**Próximos passos:** Experimente ainda mais adicionando outras funções de consolidação ou integrando essas funcionalidades em aplicativos maiores.

## Seção de perguntas frequentes
1. **O que é Aspose.Cells para .NET?**
   - É uma biblioteca que permite aos desenvolvedores trabalhar com arquivos do Excel programaticamente sem precisar instalar o Microsoft Office.
2. **Como lidar com erros ao calcular fórmulas?**
   - Certifique-se de que todos os intervalos de células estejam especificados corretamente e verifique se há referências circulares na sua pasta de trabalho.
3. **Posso aplicar rótulos de subtotal personalizados para diferentes funções?**
   - Sim, estenda o `GetTotalName` método para lidar com vários tipos de funções de consolidação além de apenas médias.
4. **O Aspose.Cells é gratuito?**
   - Uma versão de teste está disponível com acesso a todos os recursos por 30 dias. Para uso contínuo, é necessário adquirir uma licença.
5. **Posso processar várias pastas de trabalho ao mesmo tempo usando esta biblioteca?**
   - Sim, iterando sobre cada pasta de trabalho em um loop e aplicando operações semelhantes às demonstradas acima.

## Recursos
- [Documentação do Aspose.Cells](https://reference.aspose.com/cells/net/)
- [Baixe Aspose.Cells para .NET](https://releases.aspose.com/cells/net/)
- [Licença de compra](https://purchase.aspose.com/buy)
- [Versão de teste gratuita](https://releases.aspose.com/cells/net/)
- [Pedido de Licença Temporária](https://purchase.aspose.com/temporary-license/)
- [Fórum de Suporte à Comunidade](https://forum.aspose.com/c/cells/9)

Seguindo este guia, você estará preparado para aproveitar o poder do Aspose.Cells para .NET na criação de subtotais personalizados e muito mais. Boa programação!


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}