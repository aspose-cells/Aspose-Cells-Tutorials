---
title: Insert Image in Header Footer of Worksheet
linktitle: Insert Image in Header Footer of Worksheet
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to easily insert an image into header/footer using Aspose.Cells for .NET in this comprehensive guide.
weight: 15
url: /net/worksheet-page-setup-features/insert-image-in-header-footer/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Insert Image in Header Footer of Worksheet

## Introduction
When it comes to creating professional-looking Excel spreadsheets, little details can make a massive difference. One such detail is adding images to the header or footer of your worksheets. It’s a surefire way to brand your documents and imbue them with a touch of professionalism. While this might sound complicated, especially if you’re not a tech whiz, using Aspose.Cells for .NET simplifies the process significantly. So, let’s dive in and learn how to get this done step-by-step!
## Prerequisites
Before you start your journey of inserting images into header and footer sections, ensure you have a few things in place:
1. Visual Studio: Ensure you have Visual Studio installed on your computer. This IDE is a powerhouse for .NET development.
2. Aspose.Cells for .NET: You can get a free trial or purchase it if you’re serious about maximizing your Excel capabilities. Download it [here](https://releases.aspose.com/cells/net/).
3. Basic Knowledge of C#: A foundational understanding of C# and how to run a .NET application will be beneficial.
4. Image File: Get an image file like a company logo ready. In this example, we’ll refer to it as `aspose-logo.jpg`.
## Import Packages
To get our coding journey started, ensure you have the necessary packages imported in your C# project. You need the Aspose.Cells namespace which contains all the classes and methods you’ll be working with.
Here's how to include it in your code:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Now that we have everything set up, let’s walk through the process with easy-to-follow steps.
## Step 1: Set Up Your Directory
Define where your files will be stored.
First off, we need to specify the path to our documents directory where the Excel file and image are located. You can set any path; just substitute `"Your Document Directory"` with your actual directory path.
```csharp
string dataDir = "Your Document Directory";
```
## Step 2: Create a Workbook Object
Create an instance of your Excel workbook.
With the path set, we now need to create a new instance of a worksheet where we will be inserting our image. 
```csharp
Workbook workbook = new Workbook();
```
## Step 3: Load Your Image
Open and read the image file, converting it into a byte array for processing.
Next, we will set the path for our image (the logo, in this case) and initialize a `FileStream` object to read the image. Here's how to do it:
```csharp
string logo_url = dataDir + "aspose-logo.jpg";
// Declaring a FileStream object
FileStream inFile;
byte[] binaryData;
// Creating the instance of the FileStream object
inFile = new FileStream(logo_url, FileMode.Open, FileAccess.Read);
```
## Step 4: Read the Image into a Byte Array
Convert the image file data into a byte array.
To work with the image, we need to read it into a byte array. This is essential as it allows us to manipulate the image within the application.
```csharp
// Instantiating the byte array of FileStream object's size
binaryData = new byte[inFile.Length];
// Reads a block of bytes from the stream and writes data in a given buffer of byte array.
long bytesRead = inFile.Read(binaryData, 0, (int)inFile.Length);
```
## Step 5: Configure Page Setup for Header/Footer
Access the PageSetup object to manipulate the header and footer sections.
To insert our image, we need to configure the page setup object. This allows us to customize the header of our worksheet:
```csharp
PageSetup pageSetup = workbook.Worksheets[0].PageSetup;
```
## Step 6: Insert the Logo into Header
Embed the image into the header section of the worksheet.
This is the magic moment! We’ll insert our logo into the central section of the header:
```csharp
// Set the logo/picture in the central section of the page header.
pageSetup.SetHeaderPicture(1, binaryData);
// Set the script for the logo/picture
pageSetup.SetHeader(1, "&G");
// Set the Sheet's name in the right section of the page header with the script
pageSetup.SetHeader(2, "&A");
```
## Step 7: Save Your Workbook
Save your changes into a new Excel file.
After configuring everything, it’s time to save our workbook. Make sure to provide a new name for your output file:
```csharp
workbook.Save(dataDir + "InsertImageInHeaderFooter_out.xls");
```
## Step 8: Clean Up Resources
Close the FileStream to release resources.
Finally, after all manipulation, don’t forget to tidy up by closing your `FileStream`!
```csharp
inFile.Close();
```
## Conclusion
And there you have it! You’ve successfully inserted an image into the header/footer of an Excel worksheet using Aspose.Cells for .NET. It’s simple, right? Once you understand the steps, you can customize it further to fit your specific needs. Whether you're looking to brand reports for your business or simply add a personal touch, this technique is incredibly useful. 
## FAQ's
### Can I use any image format?
Yes, Aspose.Cells supports various image formats including JPEG, PNG, and BMP for header and footer images.
### Is Aspose.Cells free to use?
Aspose.Cells offers a free trial, but for continued use, you will need to purchase a license. Find out more about pricing [here](https://purchase.aspose.com/buy).
### How do I access the Aspose.Cells documentation?
You can dive deep into the features and functions of Aspose.Cells by visiting the [documentation](https://reference.aspose.com/cells/net/).
### Can I use Aspose.Cells without Visual Studio?
Yes, as long as you have the .NET runtime environment, you can use Aspose.Cells in any .NET compatible development environment.
### What should I do if I encounter issues?
If you run into any problems or need support, check the [Aspose support forum](https://forum.aspose.com/c/cells/9) for help from the community and developers.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
