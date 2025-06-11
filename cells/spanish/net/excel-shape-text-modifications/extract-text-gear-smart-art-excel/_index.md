---
"description": "Aprenda a extraer texto de un SmartArt de tipo engranaje en Excel con Aspose.Cells para .NET. Incluye una guía paso a paso y un ejemplo de código."
"linktitle": "Extraer texto de un Smart Art de tipo engranaje en Excel"
"second_title": "API de procesamiento de Excel Aspose.Cells .NET"
"title": "Extraer texto de un Smart Art de tipo engranaje en Excel"
"url": "/es/net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Extraer texto de un Smart Art de tipo engranaje en Excel

## Introducción
Al trabajar con Excel, puede encontrar gráficos SmartArt que le ayudan a transmitir sus mensajes de forma visualmente atractiva. Entre estos gráficos, el SmartArt de tipo engranaje es uno de los favoritos por sus flujos jerárquicos y direccionales, y se utiliza a menudo en la gestión de proyectos o el modelado de sistemas. Pero ¿qué ocurre si necesita extraer texto de estas formas mediante programación? ¡Aquí es donde Aspose.Cells para .NET resulta muy útil! En esta entrada del blog, le guiaremos paso a paso sobre cómo extraer texto de formas SmartArt de tipo engranaje en Excel con Aspose.Cells para .NET.
## Prerrequisitos
Antes de comenzar, hay algunos requisitos esenciales que debes cumplir. No te preocupes; es sencillo y te guiaré paso a paso.
### Entorno .NET
Asegúrate de tener un entorno de desarrollo .NET configurado en tu ordenador. Puede ser Visual Studio o cualquier IDE compatible con el desarrollo .NET.
### Aspose.Cells para .NET
continuación, deberá instalar la biblioteca Aspose.Cells. Esta es la herramienta clave que le permitirá manipular archivos de Excel sin problemas. Puede descargarla desde [Página de lanzamientos de Aspose](https://releases.aspose.com/cells/net/)Si quieres explorarlo primero, aprovecha la [prueba gratuita](https://releases.aspose.com/).
### Conocimientos básicos de C#
Un conocimiento básico de programación en C# es justo lo que necesitas para seguir este tutorial. Si eres nuevo en esto, no te preocupes: diseñaré los pasos para que sean lo más fáciles de entender posible para principiantes.
### Archivo de Excel de muestra
Para este tutorial, también necesitará un archivo de Excel de ejemplo con formas SmartArt de tipo engranaje. Puede crear uno fácilmente o buscar una plantilla en línea. Solo asegúrese de que el SmartArt incluya al menos una forma de tipo engranaje.
## Importar paquetes
Para empezar a programar, necesitarás importar los paquetes necesarios. Así es como se hace:
### Crear un nuevo proyecto
1. Abra su IDE .NET.
2. Cree un nuevo proyecto. Por ejemplo, seleccione "Aplicación de consola" en las opciones de .NET.
3. Dale un nombre a tu proyecto y establece el marco deseado. 
### Agregar referencias
Para utilizar Aspose.Cells, deberá agregar las referencias de la biblioteca a su proyecto:
1. Haga clic derecho en el nombre de su proyecto en el Explorador de soluciones.
2. Seleccione “Administrar paquetes NuGet”.
3. Busque “Aspose.Cells” e instálelo.
¡Una vez instalado, ya estará listo para comenzar a codificar!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Ahora, analicemos el código que usarás para extraer el texto. Lo haremos paso a paso.
## Paso 1: Configurar el directorio de origen
Comience por definir el directorio donde se encuentra su archivo de Excel:
```csharp
// Directorio de origen
string sourceDir = "Your Document Directory";
```
Asegúrese de reemplazar `"Your Document Directory"` con la ruta real a su archivo Excel.
## Paso 2: Cargue el libro de Excel
A continuación, cargaremos el libro de Excel. Así es como podemos acceder a su contenido:
```csharp
// Cargue un archivo Excel de muestra que contiene una forma de arte inteligente de tipo engranaje.
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
Esta pieza cargará su libro de muestra de Excel.
## Paso 3: Acceda a la primera hoja de trabajo
Ahora que hemos cargado el libro de trabajo, accedamos a la primera hoja de trabajo donde existe nuestro SmartArt:
```csharp
// Acceda a la primera hoja de trabajo.
Worksheet ws = wb.Worksheets[0];
```
Esto recupera la primera hoja de trabajo para una mayor manipulación.
## Paso 4: Accede a la primera forma
A continuación, necesitamos acceder a la primera forma de nuestra hoja de cálculo. De esta manera, podremos navegar por nuestros gráficos SmartArt:
```csharp
// Accede a la primera forma.
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
Aquí, nos centraremos en la primera forma, que suponemos que es el SmartArt que necesitamos.
## Paso 5: Obtener la forma del grupo
Una vez que tenemos nuestra forma, es hora de obtener el resultado de nuestra representación SmartArt:
```csharp
// Obtenga el resultado de la forma de arte inteligente de tipo engranaje en forma de grupo.
Aspose.Cells.Drawing.GroupShape gs = sh.GetResultOfSmartArt();
```
Esto recupera nuestro SmartArt de tipo engranaje como una forma agrupada.
## Paso 6: Extraer formas individuales
Ahora, extraigamos las formas individuales que componen nuestro SmartArt:
```csharp
// Obtenga la lista de formas individuales que consta de una forma de grupo.
Aspose.Cells.Drawing.Shape[] shps = gs.GetGroupedShapes();
```
Esta matriz contendrá todas las formas individuales que necesitamos recorrer en bucle.
## Paso 7: Extraer e imprimir texto
Finalmente, podemos recorrer nuestra matriz de formas y extraer el texto de cualquier forma de tipo engranaje:
```csharp
// Extrae el texto de las formas de tipo engranaje e imprímelas en la consola.
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
Por último, es posible que desees agregar un mensaje de confirmación una vez que el proceso se haya completado correctamente:
```csharp
Console.WriteLine("ExtractTextFromGearTypeSmartArtShape executed successfully.");
```
¡Con esto, la extracción estará completa y deberías ver el texto de salida en la consola!
## Conclusión
¡Felicitaciones! Acaba de aprender a extraer texto de formas SmartArt de tipo engranaje en Excel con Aspose.Cells para .NET. Esta práctica técnica le permite automatizar informes o documentación que se basan en la representación visual de datos. Tanto si es un desarrollador experimentado como si está empezando, controlar y extraer información de SmartArt puede optimizar su flujo de trabajo y aumentar su eficiencia. No olvide explorar la información detallada. [Documentación de Aspose.Cells](https://reference.aspose.com/cells/net/) para mayores capacidades.
## Preguntas frecuentes
### ¿Qué es Aspose.Cells?
Aspose.Cells es una biblioteca .NET que permite a los desarrolladores crear y manipular archivos Excel fácilmente.
### ¿Puedo utilizar Aspose.Cells con otros idiomas?
¡Sí! Aspose.Cells está disponible en varios lenguajes de programación, incluidos Java y Python.
### ¿Necesito comprar Aspose.Cells para .NET?
Aspose.Cells ofrece una prueba gratuita, pero para un uso prolongado, se requiere una compra. Puede encontrar opciones de compra. [aquí](https://purchase.aspose.com/buy).
### ¿Hay soporte disponible para los usuarios de Aspose.Cells?
¡Por supuesto! Puedes encontrar apoyo comunitario en [Foro de Aspose.Cells](https://forum.aspose.com/c/cells/9).
### ¿Puedo extraer otros tipos de SmartArt usando este método?
Sí, con ligeras modificaciones, puedes extraer texto de varias formas SmartArt cambiando las condiciones en tu código.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}