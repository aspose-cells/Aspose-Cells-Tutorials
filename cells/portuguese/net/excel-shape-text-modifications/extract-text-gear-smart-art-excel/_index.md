---
title: Extrair texto do tipo de engrenagem Smart Art no Excel
linktitle: Extrair texto do tipo de engrenagem Smart Art no Excel
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda a extrair texto do SmartArt do tipo engrenagem no Excel usando o Aspose.Cells para .NET. Guia passo a passo e exemplo de código incluídos.
weight: 10
url: /pt/net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair texto do tipo de engrenagem Smart Art no Excel

## Introdução
Ao trabalhar com o Excel, você pode encontrar gráficos SmartArt que ajudam a transmitir suas mensagens de uma forma visualmente atraente. Entre esses gráficos, o SmartArt do tipo engrenagem é um favorito por seus fluxos hierárquicos e direcionais, frequentemente usado em gerenciamento de projetos ou modelagem de sistemas. Mas e se você precisar extrair texto dessas formas programaticamente? É aqui que o Aspose.Cells para .NET é útil! Nesta postagem do blog, mostraremos um guia passo a passo sobre como extrair texto de formas SmartArt do tipo engrenagem no Excel usando o Aspose.Cells para .NET.
## Pré-requisitos
Antes de mergulharmos, há alguns pré-requisitos essenciais que você precisa ter em mãos. Não se preocupe; é simples, e eu vou te guiar por isso.
### Ambiente .NET
Certifique-se de ter um ambiente de desenvolvimento .NET configurado no seu computador. Pode ser o Visual Studio ou qualquer IDE de sua escolha que suporte desenvolvimento .NET.
### Aspose.Cells para .NET
 Em seguida, você precisará instalar a biblioteca Aspose.Cells. Esta é a potência que permitirá que você manipule arquivos do Excel perfeitamente. Você pode baixá-la do[Página de lançamentos da Aspose](https://releases.aspose.com/cells/net/) . Se você quiser explorá-lo primeiro, aproveite o[teste gratuito](https://releases.aspose.com/).
### Conhecimento básico de C#
Um entendimento básico de programação em C# é exatamente o que você precisa para acompanhar este tutorial. Se você é novo nisso, não se preocupe — eu vou projetar os passos para serem o mais amigáveis possível para iniciantes.
### Exemplo de arquivo Excel
Para este tutorial, você também precisará de um arquivo Excel de exemplo que contenha formas SmartArt do tipo engrenagem. Você pode criar um facilmente ou encontrar um modelo online. Apenas garanta que o SmartArt inclua pelo menos uma forma do tipo engrenagem.
## Pacotes de importação
Para começar a codificar, você precisará importar os pacotes necessários. Veja como fazer isso:
### Criar um novo projeto
1. Abra seu IDE .NET.
2. Crie um novo projeto. Por exemplo, selecione 'Console Application' nas opções .NET.
3. Dê um nome ao seu projeto e defina a estrutura desejada. 
### Adicionar referências
Para usar o Aspose.Cells, você precisará adicionar as referências de biblioteca ao seu projeto:
1. Clique com o botão direito do mouse no nome do seu projeto no Solution Explorer.
2. Escolha “Gerenciar pacotes NuGet”.
3. Procure por "Aspose.Cells" e instale-o.
Depois de instalado, você estará pronto para codificar!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Agora, vamos decompor o código que você usará para extrair o texto. Faremos isso passo a passo.
## Etapa 1: Configurar o diretório de origem
Comece definindo o diretório onde seu arquivo Excel está localizado:
```csharp
// Diretório de origem
string sourceDir = "Your Document Directory";
```
 Certifique-se de substituir`"Your Document Directory"` com o caminho real para seu arquivo Excel.
## Etapa 2: Carregue a pasta de trabalho do Excel
Em seguida, carregaremos a pasta de trabalho do Excel. É assim que podemos acessar seu conteúdo:
```csharp
// Carregue um arquivo Excel de exemplo contendo uma forma de arte inteligente do tipo engrenagem.
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
Esta parte carregará sua pasta de trabalho de exemplo do Excel.
## Etapa 3: Acesse a primeira planilha
Agora que carregamos a pasta de trabalho, vamos acessar a primeira planilha onde nosso SmartArt está:
```csharp
// Acesse a primeira planilha.
Worksheet ws = wb.Worksheets[0];
```
Isso recupera a primeira planilha para manipulação posterior.
## Etapa 4: Acesse a primeira forma
Em seguida, precisamos acessar a primeira forma dentro da nossa planilha. Ao fazer isso, podemos navegar pelos nossos gráficos SmartArt:
```csharp
// Acesse a primeira forma.
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
Aqui, estamos nos concentrando na primeira forma, que assumimos ser o SmartArt que precisamos.
## Etapa 5: Obtenha a forma do grupo
Depois de termos nossa forma, é hora de obter o resultado da nossa representação SmartArt:
```csharp
// Obtenha o resultado da forma de arte inteligente do tipo engrenagem na forma de forma de grupo.
Aspose.Cells.Drawing.GroupShape gs = sh.GetResultOfSmartArt();
```
Isso recupera nosso SmartArt do tipo engrenagem como uma forma agrupada.
## Etapa 6: Extraia formas individuais
Agora, vamos extrair as formas individuais que compõem nosso SmartArt:
```csharp
// Obtenha a lista de formas individuais consistindo de formas de grupo.
Aspose.Cells.Drawing.Shape[] shps = gs.GetGroupedShapes();
```
Esta matriz conterá todas as formas individuais que precisamos percorrer.
## Etapa 7: Extrair e imprimir texto
Por fim, podemos percorrer nosso array de formas e extrair o texto de qualquer forma do tipo engrenagem:
```csharp
// Extraia o texto das formas do tipo engrenagem e imprima-as no console.
for (int i = 0; i < shps.Length; i++)
{
    Aspose.Cells.Drawing.Shape s = shps[i];
    if (s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear9 || s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear6)
    {
        Console.WriteLine("Gear Type Shape Text: " + s.Text);
    }
}
```
Neste loop, verificamos o tipo de forma e imprimimos o texto se for do tipo engrenagem.
## Etapa 8: Confirmação de execução
Por fim, você pode adicionar uma mensagem de confirmação quando o processo for concluído com sucesso:
```csharp
Console.WriteLine("ExtractTextFromGearTypeSmartArtShape executed successfully.");
```
Com isso, sua extração está concluída e você deverá ver sua saída de texto no console!
## Conclusão
 Parabéns! Você acabou de aprender como extrair texto de formas SmartArt do tipo engrenagem no Excel usando Aspose.Cells para .NET. Essa técnica útil abre portas para automatizar relatórios ou documentação que dependem de representação visual de dados. Seja você um desenvolvedor experiente ou apenas iniciante, controlar e extrair informações do SmartArt pode agilizar seu fluxo de trabalho e torná-lo mais eficiente. Não se esqueça de explorar os detalhes[Documentação do Aspose.Cells](https://reference.aspose.com/cells/net/) para mais recursos.
## Perguntas frequentes
### O que é Aspose.Cells?
Aspose.Cells é uma biblioteca .NET que permite aos desenvolvedores criar e manipular arquivos do Excel facilmente.
### Posso usar o Aspose.Cells com outros idiomas?
Sim! Aspose.Cells está disponível em várias linguagens de programação, incluindo Java e Python.
### Preciso comprar o Aspose.Cells para .NET?
 O Aspose.Cells oferece um teste gratuito, mas para uso prolongado, é necessária uma compra. Você pode encontrar opções de compra[aqui](https://purchase.aspose.com/buy).
### Há suporte disponível para usuários do Aspose.Cells?
 Absolutamente! Você pode encontrar suporte da comunidade em[Fórum Aspose.Cells](https://forum.aspose.com/c/cells/9).
### Posso extrair outros tipos de SmartArt usando este método?
Sim, com pequenas modificações, você pode extrair texto de várias formas SmartArt alterando as condições no seu código.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
