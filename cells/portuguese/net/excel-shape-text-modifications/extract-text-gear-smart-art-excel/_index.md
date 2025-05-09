---
"description": "Aprenda a extrair texto de um SmartArt do tipo engrenagem no Excel usando o Aspose.Cells para .NET. Guia passo a passo e exemplo de código incluídos."
"linktitle": "Extrair texto do tipo de engrenagem Smart Art no Excel"
"second_title": "API de processamento do Excel Aspose.Cells .NET"
"title": "Extrair texto do tipo de engrenagem Smart Art no Excel"
"url": "/pt/net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Extrair texto do tipo de engrenagem Smart Art no Excel

## Introdução
Ao trabalhar com o Excel, você pode encontrar elementos gráficos SmartArt que ajudam a transmitir suas mensagens de uma forma visualmente atraente. Entre esses elementos gráficos, o SmartArt do tipo engrenagem é um favorito por seus fluxos hierárquicos e direcionais, frequentemente usado em gerenciamento de projetos ou modelagem de sistemas. Mas e se você precisar extrair texto dessas formas programaticamente? É aqui que o Aspose.Cells para .NET entra em cena! Nesta publicação do blog, mostraremos um guia passo a passo sobre como extrair texto de formas SmartArt do tipo engrenagem no Excel usando o Aspose.Cells para .NET.
## Pré-requisitos
Antes de começarmos, existem alguns pré-requisitos essenciais que você precisa ter em mente. Não se preocupe; é simples e eu vou te guiar.
### Ambiente .NET
Certifique-se de ter um ambiente de desenvolvimento .NET configurado no seu computador. Pode ser o Visual Studio ou qualquer IDE de sua escolha que suporte desenvolvimento .NET.
### Aspose.Cells para .NET
Em seguida, você precisará instalar a biblioteca Aspose.Cells. Esta é a ferramenta poderosa que permitirá que você manipule arquivos do Excel perfeitamente. Você pode baixá-la do site [Página de lançamentos da Aspose](https://releases.aspose.com/cells/net/). Se você quiser explorá-lo primeiro, aproveite o [teste gratuito](https://releases.aspose.com/).
### Conhecimento básico de C#
Um conhecimento básico de programação em C# é tudo o que você precisa para acompanhar este tutorial. Se você é iniciante, não se preocupe — vou planejar os passos para que sejam o mais fáceis de usar possível para iniciantes.
### Arquivo Excel de exemplo
Para este tutorial, você também precisará de um arquivo de exemplo do Excel contendo formas SmartArt do tipo engrenagem. Você pode criar um facilmente ou encontrar um modelo online. Apenas certifique-se de que o SmartArt inclua pelo menos uma forma do tipo engrenagem.
## Pacotes de importação
Para começar a programar, você precisará importar os pacotes necessários. Veja como fazer:
### Criar um novo projeto
1. Abra seu IDE .NET.
2. Crie um novo projeto. Por exemplo, selecione "Aplicativo de Console" nas opções do .NET.
3. Dê um nome ao seu projeto e defina a estrutura desejada. 
### Adicionar referências
Para usar o Aspose.Cells, você precisará adicionar as referências de biblioteca ao seu projeto:
1. Clique com o botão direito do mouse no nome do seu projeto no Solution Explorer.
2. Selecione “Gerenciar pacotes NuGet”.
3. Procure por "Aspose.Cells" e instale-o.
Depois de instalado, você estará pronto para codificar!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Agora, vamos analisar o código que você usará para extrair o texto. Faremos isso passo a passo.
## Etapa 1: Configurar o diretório de origem
Comece definindo o diretório onde seu arquivo Excel está localizado:
```csharp
// Diretório de origem
string sourceDir = "Your Document Directory";
```
Certifique-se de substituir `"Your Document Directory"` com o caminho real para seu arquivo Excel.
## Etapa 2: Carregar a pasta de trabalho do Excel
Em seguida, carregaremos a pasta de trabalho do Excel. Veja como podemos acessar seu conteúdo:
```csharp
// Carregue um arquivo Excel de exemplo contendo uma forma de arte inteligente do tipo engrenagem.
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
Esta parte carregará sua pasta de trabalho de exemplo do Excel.
## Etapa 3: Acesse a primeira planilha
Agora que carregamos a pasta de trabalho, vamos acessar a primeira planilha onde está nosso SmartArt:
```csharp
// Acesse a primeira planilha.
Worksheet ws = wb.Worksheets[0];
```
Isso recupera a primeira planilha para manipulação posterior.
## Etapa 4: Acesse a primeira forma
Em seguida, precisamos acessar a primeira forma em nossa planilha. Assim, podemos navegar pelos nossos gráficos SmartArt:
```csharp
// Acesse a primeira forma.
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
Aqui, estamos focando na primeira forma, que supomos ser o SmartArt que precisamos.
## Etapa 5: Obtenha a forma do grupo
Depois de termos nossa forma, é hora de obter o resultado da nossa representação SmartArt:
```csharp
// Obtenha o resultado da forma de arte inteligente do tipo engrenagem na forma de grupo.
Aspose.Cells.Drawing.GroupShape gs = sh.GetResultOfSmartArt();
```
Isso recupera nosso SmartArt do tipo engrenagem como uma forma agrupada.
## Etapa 6: Extraia formas individuais
Agora, vamos extrair as formas individuais que compõem nosso SmartArt:
```csharp
// Obtenha a lista de formas individuais consistindo em formas de grupo.
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
Com isso, sua extração está completa e você deverá ver sua saída de texto no console!
## Conclusão
Parabéns! Você acabou de aprender a extrair texto de formas SmartArt do tipo engrenagem no Excel usando o Aspose.Cells para .NET. Essa técnica prática abre portas para a automação de relatórios ou documentação que dependem de representação visual de dados. Seja você um desenvolvedor experiente ou iniciante, controlar e extrair informações do SmartArt pode otimizar seu fluxo de trabalho e torná-lo mais eficiente. Não se esqueça de explorar os detalhes [Documentação do Aspose.Cells](https://reference.aspose.com/cells/net/) para mais recursos.
## Perguntas frequentes
### O que é Aspose.Cells?
Aspose.Cells é uma biblioteca .NET que permite aos desenvolvedores criar e manipular arquivos do Excel facilmente.
### Posso usar o Aspose.Cells com outras linguagens?
Sim! O Aspose.Cells está disponível em diversas linguagens de programação, incluindo Java e Python.
### Preciso comprar o Aspose.Cells para .NET?
O Aspose.Cells oferece um teste gratuito, mas para uso prolongado é necessário efetuar uma compra. Você pode encontrar opções de compra [aqui](https://purchase.aspose.com/buy).
### Há suporte disponível para usuários do Aspose.Cells?
Com certeza! Você pode encontrar suporte da comunidade em [Fórum Aspose.Cells](https://forum.aspose.com/c/cells/9).
### Posso extrair outros tipos de SmartArt usando este método?
Sim, com pequenas modificações, você pode extrair texto de várias formas SmartArt alterando as condições no seu código.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}