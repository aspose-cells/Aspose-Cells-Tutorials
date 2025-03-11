---
title: Especificar fuentes del Lejano Oriente y latín en Excel
linktitle: Especificar fuentes del Lejano Oriente y latín en Excel
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a especificar fuentes latinas y del Lejano Oriente en Excel usando Aspose.Cells para .NET en este tutorial completo y fácil de seguir.
weight: 17
url: /es/net/excel-shape-text-modifications/specify-far-east-latin-font-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Especificar fuentes del Lejano Oriente y latín en Excel

## Introducción
¿Está buscando mejorar sus informes o documentos de Excel con requisitos de fuentes específicos? Ya sea que trabaje con varios idiomas o simplemente busque una estética única en sus hojas de cálculo, comprender cómo especificar fuentes del Lejano Oriente y latinas en Excel es una habilidad crucial. ¡Por suerte para usted, tenemos una solución! En este tutorial, exploramos cómo usar Aspose.Cells para .NET para implementar esta función sin problemas. ¡Vamos a profundizar!
## Prerrequisitos
Antes de entrar en materia, hay algunas cosas que deberás configurar antes de comenzar a utilizar Aspose.Cells:
### .NET Framework o .NET Core
Asegúrate de tener .NET Framework o .NET Core instalado en tu equipo. Esta biblioteca funciona bien con ambos.
### Instalación de Aspose.Cells
 Necesitarás descargar la biblioteca Aspose.Cells. Puedes[Descárgalo desde aquí](https://releases.aspose.com/cells/net/) Si no está familiarizado con la instalación de paquetes NuGet, siga[Esta guía](https://www.nuget.org/).
### Entorno de desarrollo integrado (IDE)
Tener un IDE como Visual Studio o JetBrains Rider puede simplificar la codificación, la depuración y la ejecución de su proyecto.
### Conocimientos básicos de C#
Estar familiarizado con la programación en C# será muy beneficioso para seguir este tutorial.
## Importar paquetes
Antes de poder trabajar con Aspose.Cells, debemos importar los paquetes necesarios a nuestro proyecto. A continuación, le indicamos cómo hacerlo:
### Crear un nuevo proyecto
1. Abra su IDE y cree un nuevo proyecto de aplicación de consola.
2.  Ponle un nombre descriptivo a tu proyecto, como`FontSpecifyingApp`.
### Agregar paquete NuGet Aspose.Cells
1. Haga clic derecho en su proyecto en el Explorador de soluciones.
2.  Seleccionar`Manage NuGet Packages...`.
3.  Buscar`Aspose.Cells` e instalarlo.
¡Al finalizar estos pasos, deberías tener todo listo para comenzar a codificar!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Una vez realizada la configuración, es hora de ponerse manos a la obra y comenzar a codificar. En concreto, crearemos un nuevo libro de Excel y especificaremos las fuentes de Extremo Oriente y latín para los cuadros de texto. A continuación, se explica cómo hacerlo paso a paso:
## Paso 1: Configurar el directorio de salida
Comenzamos por especificar dónde queremos guardar nuestro archivo de Excel. Esto es fundamental porque queremos asegurarnos de que nuestro archivo de salida se almacene en una ubicación a la que se pueda acceder fácilmente.
```csharp
// Directorio de salida
string outputDir = "Your Document Directory";
```
## Paso 2: Crear un libro de trabajo vacío
Ahora que tenemos nuestro directorio configurado, vamos a crear un nuevo libro de trabajo donde agregaremos nuestro contenido. Esto es similar a comenzar con un lienzo en blanco antes de pintar.
```csharp
// Crear un libro de trabajo vacío.
Workbook wb = new Workbook();
```
## Paso 3: Acceda a la primera hoja de trabajo
A continuación, queremos trabajar con una hoja de trabajo de nuestro libro de ejercicios. Piense en una hoja de trabajo como una página de su libro donde ocurre toda la magia.
```csharp
// Acceda a la primera hoja de trabajo.
Worksheet ws = wb.Worksheets[0];
```
## Paso 4: Agregar un cuadro de texto
Ahora, agregaremos un cuadro de texto a nuestra hoja de cálculo. Aquí es donde escribiremos nuestro texto. Imagine que esto es como crear un cuadro de texto dentro de una diapositiva de una presentación.
```csharp
// Agregar cuadro de texto dentro de la hoja de cálculo.
int idx = ws.TextBoxes.Add(5, 5, 50, 200);
Aspose.Cells.Drawing.TextBox tb = ws.TextBoxes[idx];
```
## Paso 5: Establezca el texto del cuadro de texto
Escribamos un texto. En este ejemplo, vamos a ingresar caracteres japoneses para demostrar la fuente Far East. ¡Es tan sencillo como escribir en un cuadro de texto en su computadora!
```csharp
// Establezca el texto del cuadro de texto.
tb.Text = "こんにちは世界"; //Esto significa "Hola mundo" en japonés.
```
## Paso 6: Especificar las fuentes
¡Ahora viene la parte emocionante! Configuraremos las fuentes latinas y del Lejano Oriente para el texto. ¡Esto es como elegir la fuente perfecta para una elegante invitación de boda!
```csharp
// Especifique el nombre del Lejano Oriente y del latín de la fuente.
tb.TextOptions.LatinName = "Comic Sans MS"; // Esta es nuestra fuente latina elegida.
tb.TextOptions.FarEastName = "KaiTi"; // Esta es nuestra fuente deseada del Lejano Oriente.
```
## Paso 7: Guarde el archivo de Excel de salida
Por último, guardemos nuestro libro de trabajo. Este paso pone fin a nuestra tarea y garantiza que todo el trabajo duro que hemos realizado se guarde correctamente. 
```csharp
// Guarde el archivo Excel de salida.
wb.Save(outputDir + "outputSpecifyFarEastAndLatinNameOfFontInTextOptionsOfShape.xlsx", SaveFormat.Xlsx);
```
## Paso 8: Mensaje de confirmación
Para informarnos que todo se ha ejecutado correctamente, imprimiremos un mensaje de confirmación en la consola:
```csharp
Console.WriteLine("SpecifyFarEastAndLatinNameOfFontInTextOptionsOfShape executed successfully.");
```
## Conclusión
¡Y ya está! Has especificado correctamente fuentes del Lejano Oriente y latinas en un libro de Excel con Aspose.Cells para .NET. Esta habilidad no solo le da a tus documentos un toque profesional, sino que también enriquece la experiencia de lectura para los usuarios de distintos idiomas.
Experimente con diferentes fuentes y estilos para encontrar una combinación que se adapte a sus necesidades específicas. ¡Que disfrute programando!
## Preguntas frecuentes
### ¿Qué es Aspose.Cells?
Aspose.Cells es una biblioteca .NET para crear y administrar hojas de cálculo de Excel sin necesidad de tener Microsoft Excel instalado en su máquina. 
### ¿Puedo utilizar Aspose.Cells para aplicaciones web?
¡Sí! Aspose.Cells se puede utilizar tanto para aplicaciones de escritorio como para aplicaciones web creadas con .NET.
### ¿Existe una versión gratuita de Aspose.Cells?
 Sí, Aspose ofrece una prueba gratuita. Puedes[Descárgalo aquí](https://releases.aspose.com/).
### ¿Cómo puedo obtener soporte para Aspose.Cells?
 Puede solicitar apoyo y encontrar recursos valiosos en el[Foros de Aspose](https://forum.aspose.com/c/cells/9).
### ¿Dónde puedo comprar Aspose.Cells?
 Puedes comprar Aspose.Cells directamente desde[Sitio web de Aspose](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
