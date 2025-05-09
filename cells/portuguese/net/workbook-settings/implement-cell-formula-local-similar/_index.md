---
"description": "Descubra como implementar uma fórmula de célula semelhante à funcionalidade local da fórmula de intervalo no Aspose.Cells para .NET. Aprenda a personalizar nomes de funções integradas do Excel e muito mais."
"linktitle": "Implementar fórmula de célula local semelhante à fórmula de intervalo local"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Implementar fórmula de célula local semelhante à fórmula de intervalo local"
"url": "/pt/net/workbook-settings/implement-cell-formula-local-similar/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Implementar fórmula de célula local semelhante à fórmula de intervalo local

## Introdução
O Aspose.Cells para .NET é uma API de manipulação de planilhas poderosa e flexível que permite criar, manipular e converter arquivos do Excel programaticamente. Um dos muitos recursos oferecidos pelo Aspose.Cells é a capacidade de personalizar o comportamento das funções integradas do Excel, incluindo a possibilidade de criar seus próprios nomes de funções locais. Neste tutorial, mostraremos as etapas para implementar uma fórmula de célula semelhante à funcionalidade local da fórmula de intervalo do Aspose.Cells para .NET.
## Pré-requisitos
Antes de começar, certifique-se de ter o seguinte:
1. Microsoft Visual Studio 2010 ou posterior instalado no seu sistema.
2. A versão mais recente da biblioteca Aspose.Cells para .NET instalada em seu projeto. Você pode baixar a biblioteca em [Página de download do Aspose.Cells para .NET](https://releases.aspose.com/cells/net/).
## Pacotes de importação
Para começar, você precisará importar os pacotes necessários para o seu projeto C#. Adicione as seguintes instruções "usando" no início do seu arquivo de código:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Etapa 1: Criar uma classe de configurações de globalização personalizada
O primeiro passo é criar um personalizado `GlobalizationSettings` classe que permitirá que você substitua o comportamento padrão das funções do Excel. Neste exemplo, alteraremos os nomes das funções `SUM` e `AVERAGE` funções para `UserFormulaLocal_SUM` e `UserFormulaLocal_AVERAGE`, respectivamente.
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //Altere o nome da função SOMA conforme suas necessidades.
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //Altere o nome da função MÉDIA conforme suas necessidades.
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## Etapa 2: Crie uma nova pasta de trabalho e atribua as configurações de globalização personalizadas
Em seguida, crie uma nova instância da pasta de trabalho e atribua o personalizado `GlobalizationSettings` classe de implementação para a pasta de trabalho `Settings.GlobalizationSettings` propriedade.
```csharp
//Criar pasta de trabalho
Workbook wb = new Workbook();
//Atribuir classe de implementação GlobalizationSettings
wb.Settings.GlobalizationSettings = new GS();
```
## Etapa 3: Acesse a primeira planilha e uma célula
Agora, vamos acessar a primeira planilha da pasta de trabalho e uma célula específica dentro dessa planilha.
```csharp
//Acesse a primeira planilha
Worksheet ws = wb.Worksheets[0];
//Acesse alguma célula
Cell cell = ws.Cells["C4"];
```
## Etapa 4: Atribuir fórmulas e imprimir o FormulaLocal
Por fim, vamos atribuir o `SUM` e `AVERAGE` fórmulas para a célula e imprimir o resultado `FormulaLocal` valores.
```csharp
//Atribuir fórmula SUM e imprimir sua FormulaLocal
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//Atribuir fórmula MÉDIA e imprimir sua FórmulaLocal
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## Conclusão
Neste tutorial, você aprendeu a implementar uma fórmula de célula semelhante à funcionalidade local da fórmula de intervalo no Aspose.Cells para .NET. Ao criar uma fórmula personalizada `GlobalizationSettings` class, você pode substituir o comportamento padrão das funções do Excel e personalizar os nomes das funções locais para atender às suas necessidades. Isso pode ser particularmente útil ao trabalhar com documentos do Excel localizados ou internacionalizados.
## Perguntas frequentes
### Qual é o propósito do `GlobalizationSettings` classe em Aspose.Cells?
O `GlobalizationSettings` A classe em Aspose.Cells permite que você personalize o comportamento das funções internas do Excel, incluindo a capacidade de alterar os nomes das funções locais.
### Posso substituir o comportamento de outras funções além de `SUM` e `AVERAGE`?
Sim, você pode substituir o comportamento de qualquer função interna do Excel modificando-a `GetLocalFunctionName` método em seu costume `GlobalizationSettings` aula.
### Existe uma maneira de redefinir os nomes das funções de volta aos seus valores padrão?
Sim, você pode redefinir os nomes das funções removendo o personalizado `GlobalizationSettings` classe ou retornando uma string vazia do `GetLocalFunctionName` método.
### Posso usar esse recurso para criar funções personalizadas no Aspose.Cells?
Não, o `GlobalizationSettings` A classe foi projetada para substituir o comportamento das funções internas do Excel, não para criar funções personalizadas. Se precisar criar funções personalizadas, você pode usar a `UserDefinedFunction` classe em Aspose.Cells.
### Este recurso está disponível em todas as versões do Aspose.Cells para .NET?
Sim, o `GlobalizationSettings` classe e a capacidade de personalizar nomes de funções está disponível em todas as versões do Aspose.Cells para .NET.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}