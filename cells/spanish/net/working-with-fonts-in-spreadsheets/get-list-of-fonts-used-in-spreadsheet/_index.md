---
title: Obtener lista de fuentes utilizadas en la hoja de cálculo
linktitle: Obtener lista de fuentes utilizadas en la hoja de cálculo
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a obtener y enumerar fuentes de hojas de cálculo de Excel usando Aspose.Cells para .NET con este tutorial fácil de seguir.
weight: 10
url: /es/net/working-with-fonts-in-spreadsheets/get-list-of-fonts-used-in-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obtener lista de fuentes utilizadas en la hoja de cálculo

## Introducción
¿Alguna vez se ha encontrado desplazándose por una hoja de cálculo de Excel y preguntándose qué fuentes se usaron en sus distintas celdas? ¿Quizás se ha encontrado con un documento antiguo y le encantaría saber qué opciones tipográficas se tomaron? ¡Pues está de suerte! Con Aspose.Cells para .NET, es como tener una caja de herramientas que le permite examinar y descubrir los secretos de las fuentes ocultas en sus hojas de cálculo. En esta guía, le mostraremos cómo recuperar fácilmente una lista de todas las fuentes utilizadas en un archivo de Excel. ¡Abróchese el cinturón y sumerjámonos en el mundo de las hojas de cálculo!
## Prerrequisitos
Antes de comenzar con el código, hay algunas cosas que necesitarás para comenzar. No te preocupes, es muy sencillo. Aquí tienes una lista de verificación de lo que necesitas:
1. Visual Studio: Asegúrate de tener una versión de Visual Studio instalada en tu equipo. Aquí es donde escribiremos nuestro código.
2. Aspose.Cells para .NET: Necesita tener disponible la biblioteca Aspose.Cells. Si aún no la ha descargado, puede descargarla desde el sitio web[sitio](https://releases.aspose.com/cells/net/).
3. Conocimientos básicos de C#: un poco de comprensión de la programación en C# definitivamente te ayudará a navegar por el código fácilmente.
4. Un archivo de Excel de muestra: necesitará un archivo de Excel de muestra, como "sampleGetFonts.xlsx", con el que trabajar. Aquí es donde aplicaremos nuestra exploración de fuentes.
¡Una vez que tengas todo resuelto, estarás listo para comenzar a codificar!
## Importar paquetes
Para empezar, importemos los espacios de nombres necesarios. En .NET, importar paquetes es como invitar a los invitados adecuados a una fiesta: sin ellos, las cosas no funcionarán bien.
A continuación se explica cómo importar Aspose.Cells:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Con esta sencilla línea, estamos incorporando la funcionalidad principal de Aspose.Cells a nuestro proyecto. Ahora, pasemos a cargar el libro de trabajo.
## Paso 1: Establezca el directorio del documento
Lo primero es lo primero: antes de adentrarnos en el código, debes establecer la ruta al directorio de tu documento. Aquí es donde se encuentra tu archivo de Excel. 
```csharp
string dataDir = "Your Document Directory";
```
Reemplazarás “Tu directorio de documentos” por la ruta real donde se encuentra tu archivo de Excel. Piensa en esto como si le estuvieras diciendo al programa: “Oye, aquí es donde guardé mi archivo de Excel; ¡ve a verlo!”.
## Paso 2: Cargue el libro de trabajo de origen
 Es hora de cargar el archivo de Excel. Crearemos una nueva instancia del`Workbook` clase y pasar la ruta del archivo. 
```csharp
Workbook wb = new Workbook(dataDir + "sampleGetFonts.xlsx");
```
 ¿Qué está pasando aquí? Básicamente, estamos abriendo la puerta a nuestra hoja de cálculo.`Workbook` La clase nos permite interactuar con el contenido del archivo Excel. 
## Paso 3: Obtener todas las fuentes
 Ahora llega el momento mágico: ¡recuperemos las fuentes!`GetFonts()` El método es nuestro boleto dorado.
```csharp
Aspose.Cells.Font[] fnts = wb.GetFonts();
```
 Aquí, le pedimos al libro de trabajo que nos explique todas las fuentes que se utilizan en él.`fnts` La matriz contendrá nuestros tesoros.
## Paso 4: Imprima las fuentes
Por último, tomemos esas fuentes e imprimámoslas. Esto nos ayudará a verificar lo que hemos encontrado.
```csharp
for (int i = 0; i < fnts.Length; i++)
{
	Console.WriteLine(fnts[i]);
}
```
 Este bucle recorre cada fuente en nuestro`fnts` matriz y los envía a la consola uno por uno. ¡Es como mostrar todas las opciones de tipografía geniales que tienes en tu archivo de Excel!
## Conclusión
¡Y ya está! Con solo unas pocas líneas de código, ha recuperado e impreso con éxito la lista de fuentes utilizadas en su hoja de cálculo de Excel mediante Aspose.Cells para .NET. No se trata solo de fuentes; se trata de comprender las sutilezas de sus documentos, mejorar sus presentaciones y dominar el arte de la tipografía en sus hojas de cálculo. Ya sea que sea un desarrollador o alguien a quien simplemente le encanta jugar con Excel, este pequeño fragmento podría cambiar las reglas del juego. 
## Preguntas frecuentes
### ¿Necesito instalar Aspose.Cells por separado?
Sí, necesitas descargar y referenciar la biblioteca en tu proyecto. 
### ¿Puedo utilizar Aspose.Cells para otros formatos?
¡Por supuesto! Aspose.Cells funciona con varios formatos de Excel, como XLSX, XLS y CSV.
### ¿Hay una prueba gratuita disponible?
 Sí, puedes obtener una prueba gratuita desde[enlace de descarga](https://releases.aspose.com/).
### ¿Cómo puedo obtener soporte técnico?
 Si necesita ayuda, el[Foro de soporte de Aspose](https://forum.aspose.com/c/cells/9) Es un gran recurso.
### ¿Aspose.Cells es compatible con .NET Core?
Sí, Aspose.Cells también es compatible con proyectos .NET Core.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
