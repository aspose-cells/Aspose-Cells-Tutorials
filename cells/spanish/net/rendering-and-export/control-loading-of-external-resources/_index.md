---
"description": "Descubra cómo controlar recursos externos en la conversión de Excel a PDF usando Aspose.Cells para .NET con nuestra guía fácil de seguir."
"linktitle": "Controlar recursos externos en Excel a PDF en Aspose.Cells"
"second_title": "API de procesamiento de Excel Aspose.Cells .NET"
"title": "Controlar recursos externos en Excel a PDF en Aspose.Cells"
"url": "/es/net/rendering-and-export/control-loading-of-external-resources/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Controlar recursos externos en Excel a PDF en Aspose.Cells

## Introducción
En la era digital actual, convertir hojas de cálculo de Excel a documentos PDF es una tarea común. Ya sea para preparar informes, datos financieros o presentaciones, desea asegurarse de que sus archivos PDF tengan el aspecto deseado. Aspose.Cells para .NET es una biblioteca robusta que le permite controlar este proceso de conversión hasta el último detalle, especialmente al gestionar recursos externos como las imágenes que acompañan a sus archivos de Excel. En esta guía, profundizamos en cómo controlar los recursos externos durante el proceso de conversión de Excel a PDF con Aspose.Cells. ¡Así que, prepare su bebida favorita y comencemos!
## Prerrequisitos
Antes de entrar en detalles, asegurémonos de que tienes todo lo necesario para empezar. Aquí tienes una lista rápida:
1. Visual Studio o cualquier IDE compatible con .NET: necesitará un entorno para escribir y probar su código.
2. Aspose.Cells para .NET: si aún no lo ha instalado, diríjase a la [Descargas de Aspose](https://releases.aspose.com/cells/net/) página y obtenga la última versión.
3. Conocimientos básicos de C#: Estar familiarizado con el lenguaje de programación C# será útil. Si tiene dudas sobre algún concepto, no dude en consultarlo.
4. Archivo de Excel de muestra: Prepare un archivo de Excel con los recursos externos que desee convertir. Puede usar el archivo de muestra "samplePdfSaveOptions_StreamProvider.xlsx".
5. Un archivo de imagen para pruebas: Se usará como recurso externo durante la conversión. El archivo de imagen "newPdfSaveOptions_StreamProvider.png" es un buen marcador de posición.
## Importar paquetes
Para empezar, deberá importar los espacios de nombres necesarios de la biblioteca Aspose.Cells. Esto es crucial para acceder a sus funcionalidades. Asegúrese de agregar las siguientes directivas using al principio del archivo:
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
Estos paquetes le proporcionarán todas las clases y métodos esenciales que necesitará para realizar sus tareas.
## Paso 1: Crea tu clase de proveedor de transmisión
El primer paso es crear una clase de proveedor de transmisión que implemente el `IStreamProvider` Interfaz. Esta clase le permitirá controlar cómo se cargan los recursos externos.
```csharp
class MyStreamProvider : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        Debug.WriteLine("-----Close Stream-----");
    }
    public void InitStream(StreamProviderOptions options)
    {
        string sourceDir = "Your Document Directory";
        Debug.WriteLine("-----Init Stream-----");
        // Lea la nueva imagen en un flujo de memoria y asígnela a la propiedad Flujo
        byte[] bts = File.ReadAllBytes(sourceDir + "newPdfSaveOptions_StreamProvider.png");
        MemoryStream ms = new MemoryStream(bts);
        options.Stream = ms;
    }
}
```
En esta clase:
- CloseStream: Este método se llamará al cerrar la secuencia. Por ahora, solo estamos escribiendo un mensaje de depuración para el seguimiento.
- InitStream: Aquí es donde comienza la magia. Aquí, leerás tu imagen externa como una matriz de bytes, la convertirás en un flujo de memoria y la asignarás a... `options.Stream` propiedad.
## Paso 2: Configurar los directorios de origen y salida
Ahora que su proveedor de transmisión está listo, es momento de establecer dónde se encuentra su archivo Excel y dónde desea guardar su PDF.
```csharp
// Directorio de origen
string sourceDir = "Your Document Directory";
// Directorio de salida
string outputDir = "Your Document Directory";
```
Simplemente reemplace `"Your Document Directory"` Con la ruta de acceso de tus archivos en tu computadora. ¡Mantenerlos organizados es fundamental!
## Paso 3: Cargue su archivo de Excel
A continuación, cargará el archivo Excel desde el que desea crear el PDF.
```csharp
// Cargar archivo fuente de Excel que contiene imágenes externas
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
Estamos usando el `Workbook` Clase de Aspose.Cells, que representa tu archivo de Excel. El archivo puede incluir varios recursos externos, como imágenes, que quieras controlar durante la conversión.
## Paso 4: Establecer las opciones para guardar el PDF
Antes de guardar el libro como PDF, especifique cómo desea guardarlo. Puede ajustar estas opciones según sus necesidades.
```csharp
// Especificar opciones de guardado de PDF - Proveedor de transmisión
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // Guardar cada hoja en una nueva página
```
Aquí, estamos creando una nueva instancia de `PdfSaveOptions`que le permite personalizar cómo se formateará su PDF. El `OnePagePerSheet` Esta opción es útil para garantizar que cada hoja de Excel tenga su propia página en el PDF final.
## Paso 5: Asigna tu proveedor de transmisión
Una vez configuradas las opciones de PDF, debe indicarle a Aspose que utilice su proveedor de transmisión personalizado para recursos externos.
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
Esta línea conecta tu `Workbook` instancia con el `MyStreamProvider` Clase que creó anteriormente. Esto significa que, siempre que se encuentren recursos externos durante la conversión, su proveedor los gestionará según lo especificado.
## Paso 6: Guarde el libro de trabajo como PDF
Con todo configurado, finalmente llega el momento de guardar su libro de Excel como PDF.
```csharp
// Guardar el libro de trabajo en PDF
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
Llamando al `Save` Al utilizar el método en el objeto del libro de trabajo y pasar su directorio de salida junto con las opciones de PDF, está convirtiendo el archivo de Excel en un PDF con un hermoso formato.
## Paso 7: Confirmar la ejecución exitosa
Para finalizar, ¡siempre es bueno confirmar que el proceso ha sido exitoso!
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
Imprimir un mensaje de éxito en la consola le ayuda a mantenerse informado sobre el estado de su operación. Es recomendable incluir estas pequeñas confirmaciones en su código.
## Conclusión
¡Listo! Siguiendo estos sencillos pasos, podrás controlar con precisión la gestión de los recursos externos durante las conversiones de Excel a PDF con Aspose.Cells. Esto significa que tus documentos ahora pueden incluir imágenes y otros elementos externos con precisión, garantizando un resultado final impecable en todo momento.
## Preguntas frecuentes
### ¿Qué es Aspose.Cells?  
Aspose.Cells es una potente biblioteca para desarrolladores .NET que le permite crear, manipular, convertir y renderizar archivos de Excel en varios formatos.
### ¿Cómo descargo Aspose.Cells?  
Puede descargar la última versión de Aspose.Cells desde [Enlace de descarga](https://releases.aspose.com/cells/net/).
### ¿Puedo probar Aspose.Cells gratis?  
¡Sí! Puedes obtener una prueba gratuita visitando el [Página de prueba gratuita](https://releases.aspose.com/).
### ¿Dónde puedo encontrar soporte para Aspose.Cells?  
Para cualquier consulta relacionada con soporte, puede visitar el [Foro de soporte de Aspose](https://forum.aspose.com/c/cells/9).
### ¿Cómo puedo obtener una licencia temporal para Aspose.Cells?  
Puede solicitar una licencia temporal [aquí](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}