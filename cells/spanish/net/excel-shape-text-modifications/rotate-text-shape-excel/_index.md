---
title: Girar texto con forma en Excel
linktitle: Girar texto con forma en Excel
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a rotar texto con formas en Excel con Aspose.Cells para .NET. Siga esta guía paso a paso para lograr una presentación perfecta en Excel.
weight: 12
url: /es/net/excel-shape-text-modifications/rotate-text-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Girar texto con forma en Excel

## Introducción
En el mundo de Excel, la representación visual es tan importante como los datos en sí. Ya sea que esté elaborando un informe o diseñando un panel dinámico, la forma en que se presenta la información puede afectar drásticamente su legibilidad y apariencia general. Entonces, ¿alguna vez ha querido rotar texto para alinearlo elegantemente con formas? ¡Está de suerte! En este tutorial, profundizaremos en cómo rotar texto con formas usando Aspose.Cells para .NET, lo que garantizará que sus hojas de cálculo no solo informen sino que también impresionen.
## Prerrequisitos
Antes de comenzar, asegurémonos de que tienes todo lo que necesitas:
1. Visual Studio: asegúrese de tener Visual Studio instalado en su máquina, ya que ahí es donde escribiremos nuestro código.
2.  Aspose.Cells para .NET: Necesitará la biblioteca Aspose.Cells. Puede[Descargue la última versión aquí](https://releases.aspose.com/cells/net/) o pruébalo gratis con un[prueba gratis](https://releases.aspose.com/).
3. Conocimientos básicos de C#: Será útil estar familiarizado con C# y el entorno .NET, aunque lo guiaremos en cada paso del camino.
4.  Archivo Excel: Un archivo Excel de muestra, llamémoslo así`sampleRotateTextWithShapeInsideWorksheet.xlsx`, es necesario para probar nuestro código. Debes colocar este archivo en un directorio al que puedas acceder fácilmente.
¿Ya tienes todo listo? ¡Genial! Pasemos a la parte divertida.
## Importar paquetes
Para empezar, debemos importar los paquetes necesarios a nuestro proyecto. Para ello, siga estos pasos:
### Crear un nuevo proyecto
1. Abra Visual Studio.
2. Seleccione "Crear un nuevo proyecto".
3. Seleccione “Aplicación de consola” y seleccione C# como su lenguaje de programación preferido.
### Instalar Aspose.Cells
Ahora, agreguemos Aspose.Cells a su proyecto. Puede hacerlo mediante el Administrador de paquetes NuGet:
1. Abra “Herramientas” en el menú superior.
2. Seleccione “Administrador de paquetes NuGet” y luego “Administrar paquetes NuGet para la solución”.
3. Busca "Aspose.Cells".
4. Haga clic en "Instalar" para agregarlo a su proyecto.
### Añadir directiva Using
En la parte superior del archivo C# principal, debe agregar la siguiente directiva:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
¡Ahora estamos todos listos para empezar a codificar!
Vamos a dividir el proceso en pasos fáciles de entender. A continuación, se muestra cómo rotar texto con formas en un archivo de Excel:
## Paso 1: Configurar las rutas de directorio
En primer lugar, debe configurar los directorios de origen y salida donde se almacenarán los archivos de Excel. A continuación, le indicamos cómo hacerlo:
```csharp
//Directorio de fuentes
string sourceDir = "Your Document Directory"; // Establezca su directorio de documentos
//Directorio de salida
string outputDir = "Your Document Directory"; // Establezca su directorio de salida
```
 Reemplazar`"Your Document Directory"` con la ruta real donde se encuentra`sampleRotateTextWithShapeInsideWorksheet.xlsx` donde se encuentra el archivo.
## Paso 2: Cargue el archivo Excel de muestra
Ahora, carguemos el archivo Excel de muestra. Esto es fundamental, ya que queremos manipular los datos existentes.
```csharp
//Cargar archivo Excel de muestra.
Workbook wb = new Workbook(sourceDir + "sampleRotateTextWithShapeInsideWorksheet.xlsx");
```
## Paso 3: Acceda a la hoja de trabajo
Una vez cargado el archivo, debemos acceder a la hoja de cálculo específica que queremos modificar. En nuestro caso, es la primera hoja de cálculo.
```csharp
//Acceda a la primera hoja de trabajo.
Worksheet ws = wb.Worksheets[0];
```
## Paso 4: Modificar una celda
A continuación, modificaremos una celda específica para mostrar un mensaje. En nuestro ejemplo, utilizaremos la celda B4.
```csharp
//Acceda a la celda B4 y agregue un mensaje dentro de ella.
Cell b4 = ws.Cells["B4"];
b4.PutValue("Text is not rotating with shape because RotateTextWithShape is false.");
```
Este paso tiene que ver con la comunicación: garantizar que quien abra esta hoja comprenda lo que estamos modificando.
## Paso 5: Accede a la primera forma
Para rotar el texto, necesitamos una forma con la que trabajar. Aquí, accederemos a la primera forma de la hoja de cálculo.
```csharp
//Accede a la primera forma.
Shape sh = ws.Shapes[0];
```
## Paso 6: Ajustar la alineación del texto de la forma
Aquí es donde ocurre la magia. Ajustaremos las propiedades de alineación del texto de la forma.
```csharp
//Acceso a la alineación del texto de la forma.
Aspose.Cells.Drawing.Texts.ShapeTextAlignment shapeTextAlignment = sh.TextBody.TextAlignment;
//No gire el texto con forma estableciendo RotateTextWithShape como falso.
shapeTextAlignment.RotateTextWithShape = false;
```
 Mediante la configuración`RotateTextWithShape` En caso de falso, nos aseguramos de que el texto permanezca en posición vertical y no gire con la forma, manteniendo así todo ordenado y organizado.
## Paso 7: Guarde el archivo de Excel de salida
Por último, guardemos los cambios en un nuevo archivo de Excel. Esto nos asegurará de no perder las modificaciones y de tener un resultado ordenado.
```csharp
//Guarde el archivo Excel de salida.
wb.Save(outputDir + "outputRotateTextWithShapeInsideWorksheet.xlsx");
```
¡Y eso es todo! El archivo de salida ya está guardado, incluido el texto de la celda B4 y los ajustes realizados a la forma.
## Paso 8: Ejecutar el código
 En tu`Main` Método, envuelva todos los fragmentos de código anteriores y ejecute su proyecto. ¡Vea cómo se reflejan los cambios en su archivo de salida!
```csharp
Console.WriteLine("RotateTextWithShapeInsideWorksheet executed successfully.");
```
## Conclusión
Al principio, rotar texto con formas en Excel con Aspose.Cells para .NET puede parecer un proceso complicado, pero una vez que lo analizas, resulta bastante sencillo. Si sigues estos sencillos pasos, puedes personalizar tus hojas de cálculo para que tengan un aspecto más profesional y atractivo visualmente. Ahora bien, ya sea que lo hagas para un cliente o para tus proyectos personales, ¡todos hablarán maravillas de la calidad de tu trabajo!
## Preguntas frecuentes
### ¿Puedo utilizar Aspose.Cells gratis?
 ¡Sí! Puedes utilizar el[prueba gratis](https://releases.aspose.com/) para probar la biblioteca.
### ¿Qué versiones de Excel admite Aspose.Cells?
Aspose.Cells admite una variedad de formatos de Excel, incluidos XLS, XLSX, CSV y más.
### ¿Es posible rotar texto con formas en versiones anteriores de Excel?
Sí, la funcionalidad se puede aplicar a formatos más antiguos compatibles con Aspose.Cells.
### ¿Dónde puedo encontrar más documentación sobre Aspose.Cells?
 Puede explorar la completa[documentación](https://reference.aspose.com/cells/net/) Para obtener más información.
### ¿Cómo puedo obtener soporte para Aspose.Cells?
 Puedes solicitar ayuda visitando el[Foro de Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
