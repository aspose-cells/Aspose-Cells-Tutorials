---
title: Extraer texto de un Smart Art de tipo engranaje en Excel
linktitle: Extraer texto de un Smart Art de tipo engranaje en Excel
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a extraer texto de un SmartArt de tipo engranaje en Excel con Aspose.Cells para .NET. Incluye una guía paso a paso y un ejemplo de código.
weight: 10
url: /es/net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraer texto de un Smart Art de tipo engranaje en Excel

## Introducción
Al trabajar con Excel, puede encontrar gráficos SmartArt que le ayuden a transmitir sus mensajes de una manera visualmente atractiva. Entre estos gráficos, el SmartArt de tipo engranaje es uno de los favoritos por sus flujos jerárquicos y direccionales, que se utilizan a menudo en la gestión de proyectos o el modelado de sistemas. Pero, ¿qué sucede si necesita extraer texto de estas formas mediante programación? ¡Aquí es donde Aspose.Cells para .NET resulta útil! En esta publicación del blog, le guiaremos paso a paso a través de una guía sobre cómo extraer texto de formas SmartArt de tipo engranaje en Excel utilizando Aspose.Cells para .NET.
## Prerrequisitos
Antes de comenzar, hay algunos requisitos previos esenciales que debes cumplir. No te preocupes, es sencillo y te guiaré en el proceso.
### Entorno .NET
Asegúrate de tener un entorno de desarrollo .NET configurado en tu computadora. Puede ser Visual Studio o cualquier IDE de tu elección que admita el desarrollo .NET.
### Aspose.Cells para .NET
 A continuación, deberá instalar la biblioteca Aspose.Cells. Esta es la herramienta que le permitirá manipular archivos de Excel sin problemas. Puede descargarla desde[Página de lanzamientos de Aspose](https://releases.aspose.com/cells/net/) Si quieres explorarlo primero, aprovecha la[prueba gratis](https://releases.aspose.com/).
### Conocimientos básicos de C#
Un conocimiento básico de programación en C# es justo lo que necesitas para seguir este tutorial. Si eres nuevo en esto, no te preocupes: diseñaré los pasos para que sean lo más fáciles de entender posible para principiantes.
### Archivo de Excel de muestra
Para este tutorial, también necesitará un archivo de Excel de muestra que contenga formas SmartArt de tipo engranaje. Puede crear uno fácilmente o buscar una plantilla en línea. Solo asegúrese de que el SmartArt incluya al menos una forma de tipo engranaje.
## Importar paquetes
Para comenzar a codificar, deberá importar los paquetes necesarios. A continuación, le indicamos cómo hacerlo:
### Crear un nuevo proyecto
1. Abra su IDE .NET.
2. Cree un nuevo proyecto. Por ejemplo, seleccione "Aplicación de consola" en las opciones de .NET.
3. Dale un nombre a tu proyecto y establece el marco deseado. 
### Agregar referencias
Para utilizar Aspose.Cells, deberá agregar las referencias de la biblioteca a su proyecto:
1. Haga clic derecho en el nombre de su proyecto en el Explorador de soluciones.
2. Seleccione “Administrar paquetes NuGet”.
3. Busque “Aspose.Cells” e instálelo.
¡Una vez instalado, ya estará listo para codificar!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Ahora, desglosemos el código que usarás para extraer el texto. Lo haremos paso a paso.
## Paso 1: Configurar el directorio de origen
Comience por definir el directorio donde se encuentra su archivo de Excel:
```csharp
// Directorio de fuentes
string sourceDir = "Your Document Directory";
```
 Asegúrese de reemplazar`"Your Document Directory"` con la ruta real a su archivo Excel.
## Paso 2: Cargue el libro de trabajo de Excel
A continuación, cargaremos el libro de Excel. Así podremos acceder a su contenido:
```csharp
// Cargue un archivo Excel de muestra que contiene la forma de arte inteligente de tipo engranaje.
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
Esta pieza cargará su libro de trabajo de Excel de muestra.
## Paso 3: Acceda a la primera hoja de trabajo
Ahora que hemos cargado el libro de trabajo, accedamos a la primera hoja de trabajo donde existe nuestro SmartArt:
```csharp
// Acceda a la primera hoja de trabajo.
Worksheet ws = wb.Worksheets[0];
```
Esto recupera la primera hoja de trabajo para una mayor manipulación.
## Paso 4: Accede a la primera forma
continuación, debemos acceder a la primera forma de nuestra hoja de cálculo. De esta manera, podremos navegar por nuestros gráficos SmartArt:
```csharp
// Accede a la primera forma.
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
Aquí, nos centraremos en la primera forma, que suponemos que es el SmartArt que necesitamos.
## Paso 5: Obtener la forma del grupo
Una vez que tenemos nuestra forma, es hora de obtener el resultado de nuestra representación SmartArt:
```csharp
// Obtenga el resultado de la forma de arte inteligente de tipo engranaje en forma de forma de grupo.
Aspose.Cells.Drawing.GroupShape gs = sh.GetResultOfSmartArt();
```
Esto recupera nuestro SmartArt de tipo engranaje como una forma agrupada.
## Paso 6: Extraer formas individuales
Ahora, extraigamos las formas individuales que componen nuestro SmartArt:
```csharp
// Obtenga la lista de formas individuales que consta de formas de grupo.
Aspose.Cells.Drawing.Shape[] shps = gs.GetGroupedShapes();
```
Esta matriz contendrá todas las formas individuales que necesitamos recorrer en un bucle.
## Paso 7: Extraer e imprimir texto
Finalmente, podemos recorrer nuestra matriz de formas y extraer el texto de cualquier forma de tipo engranaje:
```csharp
// Extraiga el texto de las formas de tipo engranaje e imprímalos en la consola.
for (int i = 0; i < shps.Length; i++)
{
    Aspose.Cells.Drawing.Shape s = shps[i];
    if (s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear9 || s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear6)
    {
        Console.WriteLine("Gear Type Shape Text: " + s.Text);
    }
}
```
En este bucle, verificamos el tipo de forma e imprimimos el texto si es una forma de tipo engranaje.
## Paso 8: Confirmación de ejecución
Por último, es posible que desees agregar un mensaje de confirmación una vez que el proceso se haya completado con éxito:
```csharp
Console.WriteLine("ExtractTextFromGearTypeSmartArtShape executed successfully.");
```
¡Con esto, tu extracción estará completa y deberías ver el texto de salida en la consola!
## Conclusión
 ¡Felicitaciones! Acaba de aprender a extraer texto de formas SmartArt de tipo engranaje en Excel con Aspose.Cells para .NET. Esta práctica técnica abre las puertas a la automatización de informes o documentación que se basan en la representación visual de datos. Ya sea que sea un desarrollador experimentado o recién esté comenzando, controlar y extraer información de SmartArt puede agilizar su flujo de trabajo y hacerlo más eficiente. No olvide explorar la información detallada[Documentación de Aspose.Cells](https://reference.aspose.com/cells/net/) para mayores capacidades.
## Preguntas frecuentes
### ¿Qué es Aspose.Cells?
Aspose.Cells es una biblioteca .NET que permite a los desarrolladores crear y manipular archivos de Excel fácilmente.
### ¿Puedo utilizar Aspose.Cells con otros idiomas?
¡Sí! Aspose.Cells está disponible en varios lenguajes de programación, incluidos Java y Python.
### ¿Necesito comprar Aspose.Cells para .NET?
 Aspose.Cells ofrece una prueba gratuita, pero para un uso prolongado es necesario realizar una compra. Puede encontrar opciones de compra[aquí](https://purchase.aspose.com/buy).
### ¿Hay soporte disponible para los usuarios de Aspose.Cells?
 ¡Por supuesto! Puedes encontrar soporte de la comunidad en[Foro Aspose.Cells](https://forum.aspose.com/c/cells/9).
### ¿Puedo extraer otros tipos de SmartArt usando este método?
Sí, con ligeras modificaciones, puedes extraer texto de varias formas SmartArt cambiando las condiciones en tu código.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
