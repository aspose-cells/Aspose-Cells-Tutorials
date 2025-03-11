---
title: Pare a conversão ou o carregamento usando o Monitor de interrupção
linktitle: Pare a conversão ou o carregamento usando o Monitor de interrupção
second_title: API de processamento do Aspose.Cells .NET Excel
description: Aprenda a interromper a conversão de pastas de trabalho no Aspose.Cells para .NET usando o Interrupt Monitor, com um tutorial detalhado passo a passo.
weight: 26
url: /pt/net/workbook-operations/stop-conversion-or-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pare a conversão ou o carregamento usando o Monitor de interrupção

## Introdução
Trabalhar com arquivos grandes do Excel geralmente envolve processos demorados que podem consumir tempo e recursos. Mas e se você pudesse interromper o processo de conversão no meio do caminho quando percebesse que algo precisa ser alterado? O Aspose.Cells for .NET tem um recurso chamado Interrupt Monitor, que permite interromper a conversão de uma pasta de trabalho para outro formato, como PDF. Isso pode ser um salva-vidas, especialmente ao trabalhar com arquivos de dados substanciais. Neste guia, mostraremos como interromper o processo de conversão usando o Interrupt Monitor no Aspose.Cells for .NET.
## Pré-requisitos
Antes de mergulhar, certifique-se de ter o seguinte em mãos:
1.  Aspose.Cells para .NET - Baixe-o[aqui](https://releases.aspose.com/cells/net/).
2. Ambiente de desenvolvimento .NET - como o Visual Studio.
3. Conhecimento básico de programação em C# - A familiaridade com a sintaxe do C# ajudará você a acompanhar.
## Pacotes de importação
Para começar, vamos importar os pacotes necessários. Essas importações incluem:
- Aspose.Cells: A principal biblioteca para manipulação de arquivos do Excel.
- System.Threading: Para gerenciar threads, pois este exemplo executará dois processos paralelos.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.IO;
```
Vamos dividir o processo em etapas detalhadas. Cada etapa ajudará você a entender a importância de configurar e usar o Interrupt Monitor para gerenciar a conversão de pastas de trabalho do Excel.
## Etapa 1: Crie a classe e defina o diretório de saída
Primeiro, precisamos de uma classe para encapsular nossas funções, juntamente com um diretório onde o arquivo de saída será salvo.
```csharp
class StopConversionOrLoadingUsingInterruptMonitor
{
    static string outputDir = "Your Document Directory";
}
```
 Substituir`"Your Document Directory"` com o caminho real onde você deseja que o arquivo PDF seja salvo.
## Etapa 2: Instanciar o Monitor de Interrupção
Em seguida, crie um objeto InterruptMonitor. Este monitor ajudará a controlar o processo configurando a capacidade de interrompê-lo em qualquer ponto dado.
```csharp
InterruptMonitor im = new InterruptMonitor();
```
Este monitor de interrupção será anexado à nossa pasta de trabalho, permitindo-nos gerenciar o processo de conversão.
## Etapa 3: Configurar a pasta de trabalho para conversão
Agora, vamos criar um objeto de pasta de trabalho, atribuir o InterruptMonitor a ele e, em seguida, acessar a primeira planilha para inserir algum texto de exemplo.
```csharp
void CreateWorkbookAndConvertItToPdfFormat()
{
    Workbook wb = new Workbook();
    wb.InterruptMonitor = im;
    Worksheet ws = wb.Worksheets[0];
    Cell cell = ws.Cells["J1000000"];
    cell.PutValue("This is text.");
}
```
O código acima cria uma pasta de trabalho, define o InterruptMonitor para ela e coloca o texto em uma célula distante (`J1000000`). Colocar texto nessa posição de célula garante que o processamento da pasta de trabalho seja mais demorado, dando ao InterruptMonitor tempo suficiente para intervir.
## Etapa 4: salvar a pasta de trabalho como PDF e lidar com a interrupção
 Agora, vamos tentar salvar a pasta de trabalho como um PDF. Usaremos um`try-catch` bloco para lidar com qualquer interrupção que possa ocorrer.
```csharp
try
{
    wb.Save(outputDir + "output_InterruptMonitor.pdf");
}
catch (Aspose.Cells.CellsException ex)
{
    Console.WriteLine("Process Interrupted - Message: " + ex.Message);
}
```
Se o processo for interrompido, a exceção o capturará e exibirá uma mensagem apropriada. Caso contrário, a pasta de trabalho será salva como PDF.
## Etapa 5: Interrompa o processo de conversão
 A principal característica aqui é a capacidade de interromper o processo. Adicionaremos um atraso usando`Thread.Sleep` e então ligue para o`Interrupt()` método para interromper a conversão após 10 segundos.
```csharp
void WaitForWhileAndThenInterrupt()
{
    Thread.Sleep(1000 * 10);
    im.Interrupt();
}
```
Esse atraso dá tempo para que a pasta de trabalho comece a converter para PDF antes que o sinal de interrupção seja enviado.
## Etapa 6: Execute os threads simultaneamente
Para juntar tudo, precisamos iniciar ambas as funções em threads separadas. Dessa forma, a conversão da pasta de trabalho e a espera de interrupção podem ocorrer simultaneamente.
```csharp
public void TestRun()
{
    ThreadStart ts1 = new ThreadStart(this.CreateWorkbookAndConvertItToPdfFormat);
    Thread t1 = new Thread(ts1);
    t1.Start();
    ThreadStart ts2 = new ThreadStart(this.WaitForWhileAndThenInterrupt);
    Thread t2 = new Thread(ts2);
    t2.Start();
    t1.Join();
    t2.Join();
}
```
 O código acima é executado`CreateWorkbookAndConvertItToPdfFormat` e`WaitForWhileAndThenInterrupt` em threads paralelos, unindo-os quando ambos os processos forem concluídos.
## Etapa 7: Execução final
 Por fim, adicionaremos um`Run()` método para executar o código.
```csharp
public static void Run()
{
    new StopConversionOrLoadingUsingInterruptMonitor().TestRun();
    Console.WriteLine("StopConversionOrLoadingUsingInterruptMonitor executed successfully.");
}
```
 Esse`Run` O método é o ponto de entrada para iniciar e observar a interrupção na ação.
## Conclusão
Neste tutorial, exploramos como interromper o processo de conversão no Aspose.Cells para .NET. O Interrupt Monitor é uma ferramenta útil ao trabalhar com arquivos grandes do Excel, permitindo que você pare processos sem esperar que eles sejam concluídos. Isso é especialmente útil em cenários onde tempo e recursos são preciosos, e feedback rápido é necessário.
## Perguntas frequentes
### O que é um Monitor de Interrupção no Aspose.Cells para .NET?  
Monitor de Interrupção permite que você interrompa a conversão de uma pasta de trabalho ou carregue um processo no meio do caminho.
### Posso usar o Interrupt Monitor para outros formatos além de PDF?  
Sim, você também pode interromper conversões para outros formatos suportados.
### Como Thread.Sleep() afeta o tempo de interrupção?  
Thread.Sleep() cria um atraso antes de acionar a interrupção, dando tempo para a conversão começar.
### Posso interromper o processo antes de 10 segundos?  
 Sim, modifique o atraso em`WaitForWhileAndThenInterrupt()` para um tempo mais curto.
### O processo de interrupção afetará o desempenho?  
O impacto é mínimo e é altamente benéfico para gerenciar processos de longa duração.
 Para mais informações, consulte o[Documentação do Aspose.Cells para .NET](https://reference.aspose.com/cells/net/) . Se precisar de ajuda, confira o[Fórum de suporte](https://forum.aspose.com/c/cells/9)ou pegue um[Teste grátis](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
