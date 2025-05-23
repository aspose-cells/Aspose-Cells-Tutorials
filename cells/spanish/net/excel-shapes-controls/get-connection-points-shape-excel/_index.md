---
"description": "Aprenda a obtener puntos de conexión de formas en Excel con Aspose.Cells para .NET. Siga nuestra guía paso a paso para extraer y mostrar fácilmente puntos de forma mediante programación."
"linktitle": "Obtener puntos de conexión de formas en Excel"
"second_title": "API de procesamiento de Excel Aspose.Cells .NET"
"title": "Obtener puntos de conexión de formas en Excel"
"url": "/es/net/excel-shapes-controls/get-connection-points-shape-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Obtener puntos de conexión de formas en Excel

## Introducción
Al trabajar con archivos de Excel mediante programación, a menudo necesitamos interactuar con formas incrustadas en las hojas. Una de las tareas más avanzadas que se pueden realizar es extraer puntos de conexión de una forma. Los puntos de conexión se utilizan para conectar formas con conectores y gestionar su diseño con mayor precisión. Si busca obtener los puntos de conexión de una forma en Excel, Aspose.Cells para .NET es la herramienta que necesita. En este tutorial, le guiaremos paso a paso para lograrlo.
## Prerrequisitos
Antes de sumergirse en el código, asegúrese de tener los siguientes requisitos previos:
- Aspose.Cells para .NET: Necesitará tener Aspose.Cells instalado en su entorno de desarrollo. Si aún no lo tiene, puede... [Descargue la última versión aquí](https://releases.aspose.com/cells/net/).
- Entorno de desarrollo: asegúrese de tener una instalación funcional de Visual Studio o cualquier otro IDE compatible con .NET.
- Conocimientos básicos de C#: este tutorial asume que tienes un conocimiento básico de la programación en C# y los principios orientados a objetos.
También puedes inscribirte en un [prueba gratuita de Aspose.Cells](https://releases.aspose.com/) Si aún no lo has hecho, esto te dará acceso a todas las funciones necesarias para esta guía.

## Importar paquetes
Para trabajar con Aspose.Cells en su proyecto, debe incluir los espacios de nombres necesarios. Las siguientes instrucciones de importación deben colocarse al principio del código:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Estos espacios de nombres le brindan acceso a la funcionalidad principal de Aspose.Cells y le permiten manipular hojas de trabajo y formas.

## Guía paso a paso para obtener los puntos de conexión de una figura
En esta sección, le explicaremos cómo extraer los puntos de conexión de una forma en una hoja de cálculo de Excel. Siga cada paso cuidadosamente para comprenderlo.
## Paso 1: Crear una instancia de un nuevo libro de trabajo
Lo primero es lo primero, necesitamos crear una instancia del `Workbook` Clase. Esto representa un archivo de Excel en Aspose.Cells. Si no tiene un archivo, no hay problema: puede empezar con un libro en blanco.
```csharp
// Crear una instancia de un nuevo libro de trabajo
Workbook workbook = new Workbook();
```
En este paso, hemos creado un libro de Excel vacío, pero también puedes cargar uno existente pasando la ruta del archivo al `Workbook` constructor.
## Paso 2: Acceda a la primera hoja de trabajo
A continuación, necesitamos acceder a la hoja de cálculo donde queremos trabajar con las formas. En este caso, usaremos la primera hoja del libro.
```csharp
// Obtenga la primera hoja de trabajo del libro de trabajo
Worksheet worksheet = workbook.Worksheets[0];
```
Esta línea accede a la primera hoja de cálculo del conjunto de hojas de cálculo del libro. Si trabaja con una hoja específica, puede reemplazar el índice. `0` con el índice deseado.
## Paso 3: Agregar un nuevo cuadro de texto (forma)
Ahora, agreguemos una nueva forma a la hoja de cálculo. Crearemos un cuadro de texto, que es un tipo de forma. También puedes agregar otros tipos de formas, pero para simplificar, en este tutorial usaremos un cuadro de texto.
```csharp
// Agregar un nuevo cuadro de texto a la colección
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
Esto es lo que hemos hecho:
- Se agregó un cuadro de texto en la fila `2`, columna `1`.
- Establezca las dimensiones del cuadro de texto en `160` unidades de ancho y `200` unidades de altura.
## Paso 4: Acceda a la forma desde la colección de formas
Una vez que agregamos el cuadro de texto, este pasa a formar parte de la colección de formas de la hoja de cálculo. Ahora accederemos a esa forma usando el `Shapes` recopilación.
```csharp
// Acceda a la forma (cuadro de texto) desde la colección de formas
Shape shape = workbook.Worksheets[0].Shapes[0];
```
En este paso, recuperamos la primera forma (nuestro cuadro de texto) de la colección. Si tiene varias formas, puede especificar el índice o incluso buscar la forma por nombre.
## Paso 5: Recuperar puntos de conexión
Ahora que tenemos nuestra forma, extraigamos sus puntos de conexión. Estos puntos se utilizan para conectar los conectores a la forma. `ConnectionPoints` La propiedad de la forma devuelve todos los puntos de conexión disponibles.
```csharp
// Consigue todos los puntos de conexión en esta forma
var connectionPoints = shape.ConnectionPoints;
```
Esto nos da una colección de todos los puntos de conexión disponibles para esa forma.
## Paso 6: Mostrar puntos de conexión
Finalmente, queremos mostrar las coordenadas de cada punto de conexión. Aquí es donde recorremos los puntos de conexión y los imprimimos en la consola.
```csharp
// Mostrar todos los puntos de forma
foreach (var pt in connectionPoints)
{
    System.Console.WriteLine(string.Format("X = {0}, Y = {1}", pt.X, pt.Y));
}
```
Este bucle itera sobre cada punto de conexión e imprime el `X` y `Y` Coordenadas. Esto puede ser útil para depurar o confirmar visualmente los puntos de conexión de una forma.
## Paso 7: Ejecutar y completar
Una vez configurados todos los pasos anteriores, puedes ejecutar el código. Aquí está la última línea que garantiza que el proceso se complete correctamente:
```csharp
System.Console.WriteLine("GetShapeConnectionPoints executed successfully.");
```
Esta línea simplemente registra un mensaje en la consola indicando que el proceso se ha completado.

## Conclusión
En este tutorial, explicamos cómo recuperar los puntos de conexión de una forma en Excel con Aspose.Cells para .NET. Dividiendo la tarea en pasos pequeños y fáciles de entender, exploramos el proceso de crear un libro, agregar una forma y extraer los puntos de conexión.
Al comprender cómo manipular formas mediante programación, descubrirá un mundo de posibilidades para crear hojas de Excel dinámicas e interactivas. Ya sea que esté creando informes, diseñando paneles o creando diagramas, este conocimiento le resultará muy útil.
## Preguntas frecuentes
### ¿Qué es un punto de conexión en una forma?
Un punto de conexión es un punto específico en una forma donde puedes colocar conectores o vincularlo a otras formas.
### ¿Puedo recuperar puntos de conexión para todas las formas en una hoja de cálculo?
Sí, Aspose.Cells permite recuperar puntos de conexión para cualquier forma que los admita. Simplemente recorra la colección de formas en la hoja de cálculo.
### ¿Necesito una licencia para utilizar Aspose.Cells?
Sí, aunque puedes probarlo gratis, se requiere una licencia para usar todas las funciones. Puedes [compre una licencia aquí](https://purchase.aspose.com/buy) o conseguir uno [licencia temporal](https://purchase.aspose.com/temporary-license/).
### ¿Cómo puedo agregar diferentes tipos de formas en Aspose.Cells?
Puedes utilizar el `Add` Método para formas como rectángulos, elipses y más. Cada forma tiene parámetros específicos que puedes personalizar.
### ¿Cómo cargo un archivo Excel existente en lugar de crear uno nuevo?
Para cargar un archivo existente, pase la ruta del archivo al `Workbook` constructor, así:  
```csharp
Workbook workbook = new Workbook("path_to_file.xlsx");
```

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}