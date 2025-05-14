---
"date": "2025-04-11"
"description": "تعرّف على كيفية إزالة أرقام الصفحات من جدول المحتويات في ملفات PDF باستخدام Aspose.PDF لـ .NET. يقدم هذا الدليل تعليمات خطوة بخطوة وخيارات تكوين رئيسية."
"title": "إخفاء أرقام صفحات جدول المحتويات في ملفات PDF باستخدام Aspose.PDF لـ .NET - دليل خطوة بخطوة"
"url": "/ar/net/document-manipulation/hide-toc-page-numbers-aspose-pdf-dotnet/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# إخفاء أرقام صفحات جدول المحتويات في ملفات PDF باستخدام Aspose.PDF لـ .NET: دليل خطوة بخطوة

## مقدمة

حسّن مظهر مستندات PDF الخاصة بك بإزالة أرقام الصفحات من جدول المحتويات. سيرشدك هذا الدليل إلى كيفية استخدام Aspose.PDF لـ .NET للحصول على مظهر أكثر أناقة، مما يضمن بقاء مستنداتك احترافية وسهلة التصفح.

**ما سوف تتعلمه:**
- إعداد Aspose.PDF لـ .NET
- خطوات تخصيص جدول المحتويات بدون أرقام الصفحات
- خيارات التكوين الرئيسية ونصائح استكشاف الأخطاء وإصلاحها

## المتطلبات الأساسية
قبل أن نبدأ، تأكد من أن لديك:
- **Aspose.PDF لـ .NET**:هذه المكتبة ضرورية للتعامل مع ملفات PDF.
- **بيئة التطوير**:Visual Studio أو أي بيئة متوافقة تدعم تطبيقات .NET.
- **المعرفة الأساسية بلغة C# وبنية PDF**:فهم هذه الأمور سيساعد في التنفيذ.

## إعداد Aspose.PDF لـ .NET
### تثبيت
لتثبيت Aspose.PDF، اختر إحدى الطرق التالية:
**.NET CLI**
```bash
dotnet add package Aspose.PDF
```
**مدير الحزم**
```powershell
Install-Package Aspose.PDF
```
**واجهة مستخدم مدير الحزم NuGet**:ابحث عن "Aspose.PDF" وقم بتثبيت الإصدار الأحدث مباشرةً من خلال بيئة التطوير الخاصة بك.

### الحصول على الترخيص
- **نسخة تجريبية مجانية**:ابدأ بإصدار تجريبي مجاني لاستكشاف الميزات.
- **رخصة مؤقتة**:احصل على واحد إذا كنت بحاجة إلى وصول موسع أثناء التطوير.
- **شراء**:فكّر في شراء ترخيص للاستخدام طويل الأمد. تفضل بزيارة [شراء Aspose](https://purchase.aspose.com/buy) لمزيد من المعلومات.

### التهيئة الأساسية
بعد التثبيت، قم بتضمين مساحات الأسماء الضرورية:
```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
```
تهيئة `Document` كائن لبدء العمل مع ملفات PDF:
```csharp
document doc = new Document();
```
## دليل التنفيذ
يتناول هذا القسم كيفية إخفاء أرقام الصفحات من جدول المحتويات باستخدام Aspose.PDF لـ .NET.
### الميزة: إخفاء أرقام الصفحات في جدول المحتويات
1. **إنشاء مستند PDF جديد**
   ابدأ بإعداد مستندك وإضافة صفحة جديدة لتكون بمثابة جدول المحتويات:
   ```csharp
   string dataDir = "YOUR_DOCUMENT_DIRECTORY"; // استبدله بمسار دليل المستندات الفعلي لديك.
   string outFile = dataDir + "/HiddenPageNumbers_out.pdf";
   Document doc = new Document();
   Page tocPage = doc.Pages.Add();
   ```
2. **تكوين معلومات جدول المحتويات**
   تعريف أ `TocInfo` الكائن، وتعيين عنوانه، وإخفاء أرقام الصفحات:
   ```csharp
   TocInfo tocInfo = new TocInfo();
   TextFragment title = new TextFragment("Table Of Contents");
   title.TextState.FontSize = 20;
   title.TextState.FontStyle = FontStyles.Bold;
   tocInfo.Title = title;
   tocPage.TocInfo = tocInfo;
   tocInfo.IsShowPageNumbers = false; // إخفاء أرقام الصفحات
   ```
3. **تحديد تنسيق جدول المحتويات**
   تخصيص مظهر إدخالات جدول المحتويات الخاص بك:
   ```csharp
tocInfo.FormatArrayLength = 4؛
   
   // المستوى 1: غامق ومائل، بدون هامش أيمن
   tocInfo.FormatArray[0].Margin.Right = 0؛
   tocInfo.FormatArray[0].TextState.FontStyle = FontStyles.Bold | FontStyles.Italic;
   
   // المستوى 2: مسطر بهامش أيسر محدد
   tocInfo.FormatArray[1].Margin.Left = 30؛
   tocInfo.FormatArray[1].TextState.Underline = true;
   tocInfo.FormatArray[1].TextState.FontSize = 10;
   
   // المستويان 3 و4: أسلوب جريء لكليهما
   tocInfo.FormatArray[2].TextState.FontStyle = FontStyles.Bold;
   tocInfo.FormatArray[3].TextState.FontStyle = FontStyles.Bold;
   ```
4. **Add Headings to Demonstrate TOC Entries**
   Add sample headings to the document to see how they are listed in the TOC:
   ```csharp
   Page page = doc.Pages.Add();
   for (int Level = 1; Level != 5; Level++)
   {
       Heading heading2 = new Heading(Level);
       TextSegment segment2 = new TextSegment();
       heading2.TocPage = tocPage;
       heading2.Segments.Add(segment2);
       heading2.IsAutoSequence = true;
       segment2.Text = "this is heading of level " + Level;
       heading2.IsInList = true;
       page.Paragraphs.Add(heading2);
   }
   ```
5. **حفظ المستند**
   وأخيرًا، احفظ مستندك لمراقبة التغييرات:
   ```csharp
doc.Save(outFile);
   ```
### Troubleshooting Tips
- Ensure all paths and directories are correctly specified.
- Verify that Aspose.PDF is properly installed and referenced in your project.
- Check for any exceptions during execution to troubleshoot issues.
## Practical Applications
This feature can be particularly useful in scenarios such as:
1. **Publishing**: Creating cleaner layouts for digital magazines or books without distracting page numbers.
2. **Internal Reports**: Preparing documents where reordering is frequent, and page numbers are irrelevant initially.
3. **Educational Materials**: Developing study guides where the focus should be on content rather than pagination.
## Performance Considerations
To optimize performance when working with Aspose.PDF:
- **Resource Management**: Dispose of objects appropriately to manage memory usage effectively.
- **Batch Processing**: If processing multiple PDFs, consider doing so in batches to prevent resource exhaustion.
- **Asynchronous Operations**: Use asynchronous methods where available for non-blocking operations.
## Conclusion
By following this guide, you've learned how to hide page numbers from a TOC in your PDF documents using Aspose.PDF for .NET. This feature can enhance the readability and appearance of your documents, making them more professional and user-friendly.
**Next Steps**: Try integrating these techniques into your projects or explore additional features offered by Aspose.PDF to further customize your PDFs.
## FAQ Section
1. **Can I add page numbers later?**
   - Yes, you can update the TOC settings to show page numbers if needed.
2. **Is it possible to change TOC styles dynamically?**
   - Absolutely, adjust `TocFormat` properties based on your requirements.
3. **How do I handle large documents efficiently?**
   - Use Aspose.PDF's efficient memory management features and process in chunks if necessary.
4. **Can this be integrated with other .NET applications?**
   - Yes, Aspose.PDF integrates seamlessly within any .NET application.
5. **What are the licensing options for production use?**
   - Visit [Aspose Purchase](https://purchase.aspose.com/buy) to explore various licensing options suitable for your needs.
## Resources
- [Documentation](https://reference.aspose.com/pdf/net/)
- [Download Aspose.PDF](https://releases.aspose.com/pdf/net/)
- [Purchase License](https://purchase.aspose.com/buy)
- [Free Trial](https://releases.aspose.com/pdf/net/)
- [Temporary License](https://purchase.aspose.com/temporary-license/)
- [Support Forum](https://forum.aspose.com/c/pdf/10)
By understanding and implementing these steps, you'll be well on your way to mastering PDF manipulation with Aspose.PDF for .NET. Happy coding!


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}