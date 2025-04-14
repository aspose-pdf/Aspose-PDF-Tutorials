---
title: "How to Access and Modify PDF Properties with Aspose.PDF for Java&#58; A Comprehensive Guide"
description: "Learn how to access and modify PDF properties using Aspose.PDF for Java. This guide covers document metadata, window settings, reading order, and more."
date: "2025-04-14"
weight: 1
url: "/java/metadata-document-info/aspose-pdf-java-access-modify-properties/"
keywords:
- Access PDF Properties Java
- PDF metadata manipulation
- PDF document info

---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}
# How to Access and Modify PDF Properties with Aspose.PDF for Java

## Introduction

Enhance your application's interaction with PDF files by accessing and modifying their properties effortlessly using **Aspose.PDF for Java**. This comprehensive guide will walk you through utilizing Aspose.PDF to manage various document properties, including window position, reading order, display title settings, and more.

**What You'll Learn:**
- Setting up Aspose.PDF for Java in your project.
- Accessing various document properties using Aspose.PDF methods.
- Configuring window display settings and reading order.
- Troubleshooting common issues when working with PDFs.

Let's explore the prerequisites you need to get started!

## Prerequisites

Before we begin, ensure your setup includes:

### Required Libraries
- **Aspose.PDF for Java**: Version 25.3 or later is recommended. Add it via Maven or Gradle as detailed in this tutorial.

### Environment Setup
- A Java Development Kit (JDK) installed on your machine.
- An Integrated Development Environment (IDE) like IntelliJ IDEA, Eclipse, or NetBeans.

### Knowledge Prerequisites
- Basic understanding of Java programming.
- Familiarity with project management tools such as Maven or Gradle for dependency management.

With the prerequisites in place, let's move forward to setting up Aspose.PDF for Java.

## Setting Up Aspose.PDF for Java

To start using **Aspose.PDF for Java**, you need to include it in your project. Here’s how:

### Maven
Add the following dependency to your `pom.xml` file:
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Include this line in your `build.gradle` file:
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### License Acquisition

You can obtain a **free trial** of Aspose.PDF by downloading it from the [release page](https://releases.aspose.com/pdf/java/). For ongoing use, you may need to purchase a license or apply for a temporary one via the [purchase page](https://purchase.aspose.com/buy).

### Basic Initialization

Once your project is set up with Aspose.PDF, initialize it as follows:
```java
import com.aspose.pdf.Document;

public class PdfPropertiesExample {
    public static void main(String[] args) {
        String dataDir = "YOUR_DOCUMENT_DIRECTORY";
        
        // Initialize a Document object
        Document pdfDocument = new Document(dataDir + "/Original.pdf");
        
        // Proceed to access document properties
    }
}
```

With Aspose.PDF configured, we can now explore how to access and configure PDF document properties.

## Implementation Guide

This section will guide you through accessing various properties of a PDF document using Aspose.PDF.

### Center Window Property

**Overview**: This property determines if the PDF window should be centered upon opening. By default, it is set to `false`.

#### Steps
1. **Accessing the Property**
   ```java
   boolean centerWindow = pdfDocument.isCenterWindow();
   System.out.println("Is center window enabled? " + centerWindow);
   ```

2. **Setting the Property**
   To enable centering:
   ```java
   pdfDocument.setCenterWindow(true);
   ```

### Reading Order

**Overview**: The `Direction` property specifies the reading order, such as left-to-right (L2R) or right-to-left (R2L).

#### Steps
1. **Accessing the Property**
   ```java
   String direction = pdfDocument.getDirection();
   System.out.println("Reading direction: " + direction);
   ```

2. **Setting the Reading Order**
   Change it to right-to-left:
   ```java
   pdfDocument.setDirection(com.aspose.pdf.Document.DirectionType.R2L);
   ```

### Display Document Title

**Overview**: Controls whether the window's title bar displays the document title or file name.

#### Steps
1. **Accessing the Property**
   ```java
   boolean displayDocTitle = pdfDocument.isDisplayDocTitle();
   System.out.println("Is document title displayed? " + displayDocTitle);
   ```

2. **Modifying the Setting**
   To enable displaying the document title:
   ```java
   pdfDocument.setDisplayDocTitle(true);
   ```

### Fit Window

**Overview**: This property resizes the window to fit the first page when opened.

#### Steps
1. **Accessing the Property**
   ```java
   boolean fitWindow = pdfDocument.isFitWindow();
   System.out.println("Is fit window enabled? " + fitWindow);
   ```

2. **Adjusting the Setting**
   Enable resizing:
   ```java
   pdfDocument.setFitWindow(true);
   ```

### Hide Menubar and Toolbars

**Overview**: These properties control the visibility of UI elements like the menu bar and toolbars.

#### Steps
1. **Accessing Properties**
   ```java
   boolean hideMenuBar = pdfDocument.isHideMenubar();
   System.out.println("Is menu bar hidden? " + hideMenuBar);

   boolean hideToolBar = pdfDocument.isHideToolBar();
   System.out.println("Is tool bar hidden? " + hideToolBar);
   ```

2. **Configuring Visibility**
   To hide both:
   ```java
   pdfDocument.setHideMenubar(true);
   pdfDocument.setHideToolBar(true);
   ```

### Hide Window UI

**Overview**: When set to true, this property hides all UI elements except the page contents.

#### Steps
1. **Accessing the Property**
   ```java
   boolean hideWindowUI = pdfDocument.isHideWindowUI();
   System.out.println("Is window UI hidden? " + hideWindowUI);
   ```

2. **Enabling the Setting**
   ```java
   pdfDocument.setHideWindowUI(true);
   ```

### Non-Full-Screen Page Mode

**Overview**: Determines the page mode when exiting full-screen display.

#### Steps
1. **Accessing the Property**
   ```java
   String nonFullScreenPageMode = pdfDocument.getNonFullScreenPageMode();
   System.out.println("Non-full screen page mode: " + nonFullScreenPageMode);
   ```

2. **Setting Page Mode**
   Change to thumbnails:
   ```java
   pdfDocument.setNonFullScreenPageMode(com.aspose.pdf.Document.PageModeType.Thumbnails);
   ```

### Page Layout

**Overview**: Defines how pages are laid out, such as single page or two columns.

#### Steps
1. **Accessing the Property**
   ```java
   String pageLayout = pdfDocument.getPageLayout();
   System.out.println("Page layout: " + pageLayout);
   ```

2. **Configuring Layout**
   Set to two columns:
   ```java
   pdfDocument.setPageLayout(com.aspose.pdf.Document.PageLayoutType.TwoColumnLeft);
   ```

### Page Mode

**Overview**: Controls how the document is displayed upon opening, with options like thumbnails and outlines.

#### Steps
1. **Accessing the Property**
   ```java
   String pageMode = pdfDocument.getPageMode();
   System.out.println("Page mode: " + pageMode);
   ```

2. **Setting Page Mode**
   Display as bookmarks:
   ```java
   pdfDocument.setPageMode(com.aspose.pdf.Document.PageModeType.Outlines);
   ```

## Practical Applications

Understanding and manipulating PDF properties can be immensely useful in various scenarios:

1. **Automated Report Generation**: Customize window settings for client presentations.
2. **Digital Publishing**: Control reading order for multilingual documents.
3. **User Interface Customization**: Enhance user experience by adjusting UI elements like toolbars.
4. **Presentation Mode**: Use non-full-screen page modes and layout adjustments for better viewing experiences.

## Conclusion

This guide has walked you through the process of accessing and modifying PDF properties using Aspose.PDF for Java. By leveraging these capabilities, you can enhance your applications' interaction with PDF files, providing a more tailored experience for users.

For further exploration, consider diving into Aspose.PDF's extensive documentation and exploring additional features that could benefit your projects.
{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}