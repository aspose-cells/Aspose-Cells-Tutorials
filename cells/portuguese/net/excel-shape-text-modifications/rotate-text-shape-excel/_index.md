---
title: Girar texto com forma no Excel
linktitle: Girar texto com forma no Excel
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda a girar texto com formas no Excel usando Aspose.Cells para .NET. Siga este guia passo a passo para uma apresentação perfeita no Excel.
weight: 12
url: /pt/net/excel-shape-text-modifications/rotate-text-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Girar texto com forma no Excel

## Introdução
No mundo do Excel, a representação visual é tão importante quanto os dados em si. Não importa se você está elaborando um relatório ou projetando um painel dinâmico, a maneira como as informações são dispostas pode impactar drasticamente sua legibilidade e aparência geral. Então, você já quis girar texto para alinhá-lo com estilo com formas? Você está com sorte! Neste tutorial, vamos nos aprofundar em como girar texto com formas usando o Aspose.Cells para .NET, garantindo que suas planilhas não apenas informem, mas também impressionem.
## Pré-requisitos
Antes de começar, vamos garantir que você tenha tudo o que precisa:
1. Visual Studio: certifique-se de ter o Visual Studio instalado em sua máquina, pois é onde escreveremos nosso código.
2.  Aspose.Cells para .NET: Você precisará da biblioteca Aspose.Cells. Você pode[baixe a última versão aqui](https://releases.aspose.com/cells/net/) ou experimente gratuitamente com um[teste gratuito](https://releases.aspose.com/).
3. Conhecimento básico de C#: familiaridade com C# e ambiente .NET será útil, embora nós o guiaremos em cada etapa do caminho.
4.  Arquivo Excel: Um arquivo Excel de exemplo, vamos chamá-lo`sampleRotateTextWithShapeInsideWorksheet.xlsx`, é necessário para testar nosso código. Você deve colocar esse arquivo em um diretório que você possa acessar facilmente.
Tem tudo pronto? Fantástico! Vamos pular para a parte divertida.
## Pacotes de importação
Para começar, precisamos importar os pacotes necessários para o nosso projeto. Veja como fazer isso:
### Criar um novo projeto
1. Abra o Visual Studio.
2. Selecione "Criar um novo projeto".
3. Escolha "Console App" e selecione C# como sua linguagem de programação preferida.
### Instalar Aspose.Cells
Agora, vamos adicionar Aspose.Cells ao seu projeto. Você pode fazer isso usando o NuGet Package Manager:
1. Abra "Ferramentas" no menu superior.
2. Selecione "Gerenciador de Pacotes NuGet" e depois "Gerenciar Pacotes NuGet para Solução".
3. Pesquise por "Aspose.Cells".
4. Clique em "Instalar" para adicioná-lo ao seu projeto.
### Adicionar diretiva Using
No topo do seu arquivo C# principal, você precisa adicionar a seguinte diretiva:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Agora estamos prontos para começar a programar!
Vamos dividir o processo em etapas fáceis de digerir. Veja como girar texto com formas em um arquivo Excel:
## Etapa 1: configure seus caminhos de diretório
Primeiro, você precisa configurar seus diretórios de origem e saída onde seus arquivos Excel serão armazenados. Veja como:
```csharp
//Diretório de origem
string sourceDir = "Your Document Directory"; // Defina seu diretório de documentos
//Diretório de saída
string outputDir = "Your Document Directory"; // Defina seu diretório de saída
```
 Substituir`"Your Document Directory"` com o caminho real onde seu`sampleRotateTextWithShapeInsideWorksheet.xlsx` o arquivo está localizado.
## Etapa 2: Carregue o arquivo Excel de amostra
Agora, vamos carregar o arquivo Excel de exemplo. Isso é crucial, pois queremos manipular os dados existentes.
```csharp
//Carregue um arquivo Excel de exemplo.
Workbook wb = new Workbook(sourceDir + "sampleRotateTextWithShapeInsideWorksheet.xlsx");
```
## Etapa 3: Acesse a planilha
Depois que o arquivo for carregado, precisamos acessar a planilha específica que queremos modificar. No nosso caso, é a primeira planilha.
```csharp
//Acesse a primeira planilha.
Worksheet ws = wb.Worksheets[0];
```
## Etapa 4: Modificar uma célula
Em seguida, modificaremos uma célula específica para exibir uma mensagem. Em nosso exemplo, usaremos a célula B4.
```csharp
//Acesse a célula B4 e adicione uma mensagem dentro dela.
Cell b4 = ws.Cells["B4"];
b4.PutValue("Text is not rotating with shape because RotateTextWithShape is false.");
```
Esta etapa tem tudo a ver com comunicação: garantir que quem abrir esta planilha entenda o que estamos ajustando.
## Etapa 5: Acesse a primeira forma
Para girar o texto, precisamos de uma forma para trabalhar. Aqui, acessaremos a primeira forma na planilha.
```csharp
//Acesse a primeira forma.
Shape sh = ws.Shapes[0];
```
## Etapa 6: ajuste o alinhamento do texto da forma
É aqui que a mágica acontece. Ajustaremos as propriedades de alinhamento de texto da forma.
```csharp
//Acessar alinhamento de texto de forma.
Aspose.Cells.Drawing.Texts.ShapeTextAlignment shapeTextAlignment = sh.TextBody.TextAlignment;
//Não gire o texto com a forma definindo RotateTextWithShape como falso.
shapeTextAlignment.RotateTextWithShape = false;
```
 Ao definir`RotateTextWithShape` para falso, garantimos que o texto permaneça na vertical e não gire com o formato, mantendo assim tudo limpo e organizado.
## Etapa 7: Salve o arquivo de saída do Excel
Por fim, vamos salvar nossas alterações em um novo arquivo Excel. Isso garante que não perderemos nossas edições e teremos uma saída organizada.
```csharp
//Salve o arquivo de saída do Excel.
wb.Save(outputDir + "outputRotateTextWithShapeInsideWorksheet.xlsx");
```
E é isso! Seu arquivo de saída agora está salvo, incluindo o texto na célula B4 e os ajustes feitos na forma.
## Etapa 8: Execute o código
 Em seu`Main` método, envolva todos os trechos de código acima e execute seu projeto. Veja as mudanças refletidas em seu arquivo de saída!
```csharp
Console.WriteLine("RotateTextWithShapeInsideWorksheet executed successfully.");
```
## Conclusão
Girar texto com formas no Excel usando o Aspose.Cells para .NET pode parecer um processo elaborado no começo, mas é bem direto quando você o decompõe. Seguindo essas etapas simples, você pode personalizar suas planilhas para parecerem mais profissionais e visualmente atraentes. Agora, não importa se você está fazendo isso para um cliente ou para seus projetos pessoais, todos vão ficar delirando com a qualidade do seu trabalho!
## Perguntas frequentes
### Posso usar o Aspose.Cells gratuitamente?
 Sim! Você pode usar o[teste gratuito](https://releases.aspose.com/) para experimentar a biblioteca.
### Quais versões do Excel o Aspose.Cells suporta?
O Aspose.Cells suporta uma variedade de formatos do Excel, incluindo XLS, XLSX, CSV e muito mais.
### É possível girar texto com formas em versões mais antigas do Excel?
Sim, a funcionalidade pode ser aplicada a formatos mais antigos suportados pelo Aspose.Cells.
### Onde posso encontrar mais documentação sobre o Aspose.Cells?
 Você pode explorar o abrangente[documentação](https://reference.aspose.com/cells/net/) para mais informações.
### Como obtenho suporte para o Aspose.Cells?
 Você pode solicitar suporte visitando o[Fórum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
