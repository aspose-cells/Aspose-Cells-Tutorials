---
title: Enviar forma al frente o al dorso en Excel
linktitle: Enviar forma al frente o al dorso en Excel
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Descubra cómo enviar formas al frente o al fondo en Excel con Aspose.Cells para .NET. Esta guía ofrece un tutorial paso a paso con sugerencias.
weight: 16
url: /es/net/excel-shape-text-modifications/send-shape-front-back-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Enviar forma al frente o al dorso en Excel

## Introducción
Al trabajar con archivos de Excel, es posible que necesite más control sobre los elementos visuales de su hoja de cálculo. Las formas, como las imágenes y los gráficos, pueden mejorar la presentación de sus datos. Pero, ¿qué sucede cuando estas formas se superponen o es necesario reordenarlas? Aquí es donde Aspose.Cells para .NET brilla. En este tutorial, le guiaremos por los pasos para manipular formas en una hoja de cálculo de Excel, específicamente para enviar formas al frente o al dorso de otras formas. Si está listo para mejorar su rendimiento en Excel, ¡comencemos!
## Prerrequisitos
Antes de comenzar, necesitarás tener algunas cosas en cuenta:
1.  Instalación de la biblioteca Aspose.Cells: Asegúrese de tener instalada la biblioteca Aspose.Cells para .NET. Puede encontrarla[aquí](https://releases.aspose.com/cells/net/).
2. Entorno de desarrollo: asegúrese de tener un entorno de desarrollo configurado con soporte .NET, como Visual Studio.
3. Conocimientos básicos de C#: la familiaridad con la programación en C# le ayudará a comprender mejor los fragmentos de código.
Muy bien, ¿has marcado todos los requisitos previos? ¡Genial! Pasemos a la parte divertida: ¡escribir código!
## Importar paquetes
Antes de sumergirnos en la codificación propiamente dicha, importemos los paquetes necesarios. Solo tienes que añadir la siguiente directiva using en la parte superior del archivo C#:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
Estos espacios de nombres son cruciales ya que contienen las clases y los métodos que usaremos para manipular archivos y formas de Excel.
## Paso 1: Defina las rutas de sus archivos
En este primer paso, debemos establecer los directorios de origen y de salida. Aquí es donde se encuentra el archivo de Excel y donde desea guardar el archivo modificado.
```csharp
//Directorio de fuentes
string sourceDir = "Your Document Directory";
//Directorio de salida
string outputDir = "Your Document Directory";
```
 Reemplazar`"Your Document Directory"` con la ruta real donde se almacenan sus archivos de Excel.
## Paso 2: Cargue el libro de trabajo
Ahora que tenemos nuestros directorios configurados, carguemos el libro de trabajo (el archivo de Excel) que contiene las formas que queremos manipular.
```csharp
//Cargar archivo fuente de Excel
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
 Esta línea de código inicializa un nuevo`Workbook` objeto, cargando el archivo Excel especificado en la memoria para que podamos trabajar con él.
## Paso 3: Acceda a la hoja de trabajo 
continuación, debemos acceder a la hoja de cálculo específica donde se encuentran nuestras formas. Para este ejemplo, utilizaremos la primera hoja de cálculo.
```csharp
//Acceda a la primera hoja de trabajo
Worksheet ws = wb.Worksheets[0];
```
 Haciendo referencia`Worksheets[0]`Estamos apuntando a la primera hoja de nuestro libro de trabajo. Si las formas están en una hoja diferente, ajuste el índice en consecuencia.
## Paso 4: Accede a las formas
Con el acceso a la hoja de trabajo listo, tomemos las formas que nos interesan. Para este ejemplo, accederemos a la primera y cuarta forma.
```csharp
//Accede a la primera y cuarta forma
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
Estas líneas obtienen las formas específicas de la hoja de trabajo según su índice.
## Paso 5: Imprima la posición de orden Z de las formas
Antes de mover cualquier figura, imprimamos su posición actual en orden Z. Esto nos ayuda a rastrear su posicionamiento antes de realizar cambios.
```csharp
//Imprima la posición de orden Z de la forma
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
 llamando`ZOrderPosition`, podemos ver dónde se ubica cada forma en el orden del dibujo.
## Paso 6: Envía la primera forma al frente
¡Ahora es momento de actuar! Enviemos la primera figura al frente del orden Z.
```csharp
//Envía esta forma al frente
sh1.ToFrontOrBack(2);
```
 Al pasar`2` a`ToFrontOrBack`Le estamos indicando a Aspose.Cells que traiga esta forma al frente. 
## Paso 7: Imprima la posición de orden Z de la segunda forma
Antes de enviar la segunda forma hacia atrás, verifiquemos dónde está posicionada.
```csharp
//Imprima la posición de orden Z de la forma
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
Esto nos da una idea de la posición de la cuarta forma antes de realizar cualquier cambio.
## Paso 8: Envía la cuarta forma hacia atrás
Finalmente, vamos a enviar la cuarta forma al final de la pila de orden Z.
```csharp
//Envía esta forma hacia atrás
sh4.ToFrontOrBack(-2);
```
 Usando`-2` ya que el parámetro envía la forma hacia el final de la pila, lo que garantiza que no obstruirá otras formas o textos.
## Paso 9: Guardar el libro de trabajo 
El último paso es guardar el libro de trabajo con las formas recién posicionadas.
```csharp
//Guardar el archivo de salida de Excel
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
Este comando guarda el libro de trabajo modificado en el directorio de salida especificado.
## Paso 10: Mensaje de confirmación
Por último, proporcionemos una confirmación simple para informarnos que nuestra tarea se completó exitosamente.
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
¡Y esto concluye el código de nuestro tutorial!
## Conclusión
Manipular formas en Excel con Aspose.Cells para .NET no solo es sencillo, sino también eficaz. Si sigue esta guía, ahora podrá enviar formas al frente o al fondo con facilidad, lo que le permitirá tener un mejor control de sus presentaciones de Excel. Con estas herramientas a su disposición, estará listo para mejorar el atractivo visual de sus hojas de cálculo.
## Preguntas frecuentes
### ¿Qué lenguaje de programación necesito para Aspose.Cells?  
Debe utilizar C# o cualquier lenguaje compatible con .NET para trabajar con Aspose.Cells.
### ¿Puedo probar Aspose.Cells gratis?  
 Sí, puedes comenzar con una prueba gratuita de Aspose.Cells[aquí](https://releases.aspose.com/).
### ¿Qué tipos de formas puedo manipular en Excel?  
Puede manipular varias formas como rectángulos, círculos, líneas e imágenes.
### ¿Cómo puedo obtener soporte para Aspose.Cells?  
 Puede visitar su foro comunitario para cualquier ayuda o consulta.[aquí](https://forum.aspose.com/c/cells/9).
### ¿Existe una licencia temporal disponible para Aspose.Cells?  
 Sí, puedes solicitar una licencia temporal[aquí](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
