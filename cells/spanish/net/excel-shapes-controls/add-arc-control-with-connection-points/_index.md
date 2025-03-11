---
title: Añadir control de arco con puntos de conexión
linktitle: Añadir control de arco con puntos de conexión
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Descubra cómo agregar controles de arco con puntos de conexión usando Aspose.Cells para .NET en esta guía detallada.
weight: 27
url: /es/net/excel-shapes-controls/add-arc-control-with-connection-points/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Añadir control de arco con puntos de conexión

## Introducción
Cuando se trata de crear informes de Excel visualmente atractivos, las ilustraciones desempeñan un papel fundamental. Ya sea que esté elaborando un informe financiero o un desglose de un proyecto, el uso de formas como arcos puede agregar profundidad y claridad a la presentación de sus datos. Hoy, profundizaremos en cómo utilizar Aspose.Cells para .NET para agregar controles de arco con puntos de conexión en sus hojas de cálculo de Excel. Entonces, si alguna vez se preguntó cómo darle vida a sus hojas de cálculo o hacer que sus datos se destaquen, ¡siga leyendo!
## Prerrequisitos
Antes de sumergirnos en la emoción de la codificación, asegurémonos de que todo esté listo. Esto es lo que necesitas:
1. .NET Framework: asegúrate de tener instalada una versión compatible. Aspose.Cells funciona con varias versiones, incluida .NET Core.
2.  Aspose.Cells para .NET: deberá descargar e instalar la biblioteca Aspose.Cells. Puede descargarla fácilmente desde el sitio web[enlace de descarga](https://releases.aspose.com/cells/net/).
3. Un buen IDE: Visual Studio, ese fiel compañero de cualquier desarrollador .NET, le ayudará a agilizar su experiencia de codificación.
4. Conocimientos básicos de C#: si conoces C#, este tutorial te resultará muy sencillo.
5. Acceso a su directorio de documentos: sepa dónde guardará sus archivos de Excel. Es fundamental para organizar su producción de manera eficiente.
## Importar paquetes
El siguiente paso es asegurarse de haber importado los paquetes correctos en el proyecto. Aspose.Cells para .NET tiene varias funcionalidades, por lo que lo simplificaremos. Esto es lo que deberá incluir:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Estos espacios de nombres le darán acceso a todas las funciones de dibujo y funcionalidades de administración de celdas que utilizará a lo largo de esta guía.
## Paso 1: Configurar el directorio de documentos
Primero lo primero: vamos a crear un directorio donde guardaremos esos nuevos y atractivos archivos de Excel. Así es como lo hacemos:
```csharp
string dataDir = "Your Document Directory";
// Crear directorio si aún no está presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Este fragmento de código comprueba si la carpeta especificada existe. Si no existe, crea una. Sencillo, ¿verdad? Siempre es bueno tener un lugar específico para los archivos para evitar el desorden.
## Paso 2: Crear una instancia de un libro de trabajo
Ahora que tenemos nuestro directorio listo, creemos un nuevo libro de Excel.
```csharp
Workbook excelbook = new Workbook();
```
 Al llamar al`Workbook` constructor, básicamente estás diciendo: "¡Oye, comencemos un nuevo archivo de Excel!" Este será el lienzo para todas tus formas y datos.
## Paso 3: Agregar la primera forma de arco
¡Aquí es donde comienza la diversión! Agreguemos nuestra primera forma de arco.
```csharp
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
Esta línea de código agrega una forma de arco a la primera hoja de cálculo. Los parámetros especifican las coordenadas del arco y los ángulos que definen su curvatura. 
## Paso 4: Personaliza la apariencia del arco
Un arco en blanco es como un lienzo sin pintura: ¡necesita un poco de estilo!
### Establecer el color de relleno del arco
```csharp
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
```
Esto hace que el arco sea de un azul sólido. Puedes cambiar el color a cualquier tono que te guste intercambiando`Color.Blue` para otro color.
### Establecer la colocación del arco
```csharp
arc1.Placement = PlacementType.FreeFloating;
```
Establecer la ubicación en "Flotante libre" permite que el arco se mueva independientemente de los límites de la celda, lo que le brinda flexibilidad en el posicionamiento.
### Ajustar el grosor y el estilo de la línea
```csharp
arc1.Line.Weight = 1;      
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Aquí se define el peso y el estilo de la línea, haciéndola más prominente y visualmente atractiva.
## Paso 5: Agregar otra forma de arco
¿Por qué detenernos en una sola? Agreguemos otra forma de arco para enriquecer nuestro elemento visual de Excel.
```csharp
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Al igual que el primer arco, este se agrega en una posición diferente: ¡aquí es donde ocurre la magia del diseño!
## Paso 6: Personaliza el segundo arco
¡Démosle personalidad también a nuestro segundo arco!
### Cambiar el color de la línea del arco
```csharp
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
```
Mantendremos la consistencia con el color azul, pero siempre puedes mezclar y combinar para ver qué se adapta mejor a tu diseño.
### Establecer propiedades similares al primer arco
Asegúrese de replicar esas opciones estéticas:
```csharp
arc2.Placement = PlacementType.FreeFloating;
arc2.Line.Weight = 1;           
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Aquí, simplemente te aseguras de que el segundo arco coincida con el primero, creando una apariencia cohesiva en toda la hoja de trabajo.
## Paso 7: Guarda tu libro de trabajo
Ninguna obra maestra está completa sin ser guardada, ¿no? Es hora de escribir los arcos en un archivo de Excel.
```csharp
excelbook.Save(dataDir + "book1.out.xls");
```
Esta línea guarda los arcos recién creados en un archivo Excel llamado "book1.out.xls" en su directorio designado.
## Conclusión
¡Felicitaciones! Acaba de dominar los conceptos básicos de cómo agregar controles de arco con puntos de conexión en sus hojas de Excel mediante Aspose.Cells para .NET. Esta funcionalidad no solo embellece sus hojas de cálculo, sino que también puede hacer que los datos complejos sean más fáciles de digerir. Ya sea que sea un desarrollador experimentado o recién esté comenzando, estos elementos visuales pueden transformar sus informes de insulsos a grandiosos.
## Preguntas frecuentes
### ¿Qué es Aspose.Cells?
Aspose.Cells es una potente biblioteca .NET que permite a los desarrolladores crear y manipular archivos de Excel mediante programación.
### ¿Puedo utilizar Aspose.Cells gratis?
 ¡Sí! Puedes probar una versión de prueba gratuita. Visita[Este enlace](https://releases.aspose.com/) Para empezar.
### ¿Cómo agrego otras formas además de arcos?
Puede utilizar diferentes clases disponibles en el espacio de nombres Aspose.Cells.Drawing para agregar varias formas como rectángulos, círculos y más.
### ¿Qué tipos de archivos puedo crear con Aspose.Cells?
Puede crear y manipular varios formatos de Excel, incluidos XLS, XLSX, CSV y más.
### ¿Hay soporte técnico disponible para Aspose.Cells?
 ¡Por supuesto! Puedes acceder a la[Foro de soporte de Aspose](https://forum.aspose.com/c/cells/9) para solicitar ayuda.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
