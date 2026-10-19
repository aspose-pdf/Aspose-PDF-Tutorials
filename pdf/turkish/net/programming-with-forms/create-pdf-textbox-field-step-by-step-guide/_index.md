---
category: general
date: 2026-06-21
description: C# ile PDF metin kutusu alanı oluşturun ve sadece birkaç satır kodla
  PDF form alanını kopyalamayı veya PDF formuna metin kutusu eklemeyi öğrenin.
draft: false
keywords:
- create pdf textbox field
- duplicate pdf form field
- add textbox to pdf form
- pdf form automation
- c# pdf library
language: tr
og_description: PDF metin kutusu alanını hızlıca oluşturun. Bu kılavuz, modern bir
  C# PDF kütüphanesi kullanarak PDF form alanını nasıl çoğaltacağınızı ve PDF formuna
  metin kutusu ekleyeceğinizi gösterir.
og_title: PDF Metin Kutusu Alanı Oluşturma – Tam C# Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  headline: Create PDF Textbox Field – Step‑by‑Step Guide
  type: TechArticle
- description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  name: Create PDF Textbox Field – Step‑by‑Step Guide
  steps:
  - name: What if I need the field on *more* than two pages?
    text: Just repeat the clone‑and‑add steps for each additional page. The underlying
      data object stays the same, so all widgets stay in sync.
  - name: How do I change the appearance (font, border, background)?
    text: Each `Widget` has a `SetBorderColor`, `SetBorderWidth`, and `SetBackgroundColor`
      method. You can also assign a default appearance string (`DA`) to control the
      font and size.
  - name: Can I make the field read‑only after the user fills it?
    text: Yes. Set the `ReadOnly` flag on the field after you’ve collected the data,
      or toggle it based on your workflow.
  - name: What about PDFs that already contain a form?
    text: If the document already has an AcroForm, `doc.GetForm()` simply returns
      it. You can then add new fields without disturbing existing ones. Just be careful
      to use unique field names.
  type: HowTo
tags:
- PDF
- C#
- FormFields
title: PDF Metin Kutusu Alanı Oluşturma – Adım Adım Rehber
url: /tr/net/programming-with-forms/create-pdf-textbox-field-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF Textbox Field Oluşturma – Tam C# Öğreticisi

Hiç **PDF textbox field** oluşturmanız gerektiğinde hangi API çağrılarını kullanacağınızdan emin olmadınız mı? Yalnız değilsiniz. İster bir sözleşme‑imzalama portalı, ister basit bir veri‑toplama sayfası oluşturuyor olun, PDF'ye etkileşimli metin kutuları eklemek, herhangi bir form‑otomasyon geliştiricisi için temel bir beceridir.  

Bu rehberde, sadece **PDF formuna metin kutusu ekleme**yi değil, aynı zamanda **PDF form alanını çoğaltma** sayesinde aynı girdinin birden fazla sayfada görünmesini sağlayan pratik bir örnek üzerinden ilerleyeceğiz. Sonunda, herhangi bir .NET projesine ekleyebileceğiniz çalıştırılabilir bir program elde edeceksiniz.

## Gereksinimler

- .NET 6.0 veya daha yenisi (kod .NET Core ile de çalışır)  
- Modern bir C# PDF kütüphanesi – aşağıdaki kod parçacığı **PDFTron SDK**'yı kullanıyor, ancak kavramlar iText 7, PdfSharp veya diğer kütüphanelere de uygulanabilir.  
- Visual Studio 2022 (veya tercih ettiğiniz herhangi bir IDE)  

Hepsi bu – ekstra hizmete, gizli bağımlılıklara gerek yok. Zaten eklemek istediğiniz bir PDF'niz varsa, kodu ona yönlendirin.

---

## Adım 1: Projeyi Oluşturun ve SDK'yı İçe Aktarın

İlk olarak bir konsol uygulaması oluşturun:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
```

PDFTron NuGet paketini ekleyin:

```bash
dotnet add package PDFTron.NET
```

Şimdi `Program.cs` dosyasını açın ve ihtiyacımız olan ad alanlarını ekleyelim:

```csharp
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;
```

> **Pro ipucu:** Farklı bir kütüphane kullanıyorsanız, `using` ifadelerini eşdeğerleriyle değiştirin (ör. iText 7 için `iText.Kernel.Pdf`).

## Adım 2: PDF Belgesini ve Formu Başlatın

İlk sayfada orijinal metin kutusu, ikinci sayfada ise kopya olacak iki sayfalı yeni bir PDF ile başlayacağız.

```csharp
PDFNet.Initialize();                     // Initialize the PDFTron runtime

// Create a new PDF document
using (PDFDoc doc = new PDFDoc())
{
    // Add two blank pages (letter size)
    Page sourcePage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(sourcePage);
    Page targetPage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(targetPage);

    // Get (or create) the AcroForm object
    Form form = doc.GetForm();
```

`Form` nesnesi, tüm etkileşimli alanların bulunduğu yerdir. Belge zaten bir form içermiyorsa, `GetForm()` bizim için bir tane oluşturur.

## Adım 3: **Create PDF Textbox Field** – İlk Sayfada Metin Kutusu Oluşturma

İşte öğreticimizin kalbi – bir metin kutusu alanı oluşturma. Dikdörtgen koordinatları nokta biriminde ifade edilir (1 inç = 72 nokta). Örnek, kutuyu ilk sayfanın üst‑ortasına yerleştirir.

```csharp
    // Step 1: Create a text box field on the first page and set its initial value
    TextBoxField textBoxField = new TextBoxField(sourcePage, new Rect(100, 500, 300, 520))
    {
        Value = "Sample"
    };
```

`Value` değerini hemen neden ayarlıyoruz? Alanı önceden doldurmak, kullanıcılara beklenen giriş hakkında ipucu verir ve alanın tamamen işlevsel olduğunu gösterir.

## Adım 4: Alanı Forma Ekleyin – **Add Textbox to PDF Form**

Şimdi alanı mantıksal bir adla forma kaydediyoruz. Bu ad, alanın verilerini programatik olarak okurken veya değiştirirken referans alacağınız isimdir.

```csharp
    // Step 2: Add the field to the form with a logical name
    form.Add(textBoxField, "multiBox");
```

Açık bir ad seçmek (ör. `"multiBox"`) sonraki kodun anlaşılmasını kolaylaştırır, özellikle onlarca alanınız olduğunda.

## Adım 5: **Duplicate PDF Form Field** – Başka Bir Sayfada Kopyalama

Sık karşılaşılan bir ihtiyaç, aynı alanı birden çok sayfada göstermek‑ örneğin her fatura sayfasında görünen bir “Müşteri Adı” kutusu. PDFTron, alanın görsel temsili olan widget anotasyonunu klonlamamıza izin verir.

```csharp
    // Step 3: Clone the field's widget annotation so it can appear on another page
    Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

    // Step 4: Place the cloned widget on the second page
    targetPage.Annotations.Add(clonedWidget);
```

Klonlanan widget, aynı temel veri nesnesini paylaşır. Kullanıcı bir örneğe yazı yazdığında diğeri otomatik olarak güncellenir – işte **duplicate PDF form field** sihirli kısmı.

## Adım 6: Belgeyi Kaydedin ve Temizleyin

Son olarak PDF'yi diske yazın ve PDFNet çalışma zamanını kapatın.

```csharp
    // Save the resulting PDF
    doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
    Console.WriteLine("PDF created: output.pdf");
}

// Shut down PDFNet (optional but good practice)
PDFNet.Terminate();
```

Programı çalıştırdığınızda iki‑sayfalı bir PDF (`output.pdf`) oluşur. Adobe Acrobat Reader’da açın, sayfa 1’deki metin kutusuna tıklayın, bir şeyler yazın, ardından sayfa 2’ye geçin – aynı metin anında görünür. Bu, kopyalanmış bir alanla **create pdf textbox field** örneğinin tam işlevsel bir gösterimidir.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
// Program.cs
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;

class Program
{
    static void Main()
    {
        PDFNet.Initialize();

        using (PDFDoc doc = new PDFDoc())
        {
            // Create two pages
            Page sourcePage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(sourcePage);
            Page targetPage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(targetPage);

            // Get the form (creates one if missing)
            Form form = doc.GetForm();

            // Step 1: Create a text box field on the first page
            TextBoxField textBoxField = new TextBoxField(sourcePage,
                new Rect(100, 500, 300, 520))
            {
                Value = "Sample"
            };

            // Step 2: Add the field to the form
            form.Add(textBoxField, "multiBox");

            // Step 3: Clone the widget so it appears on page 2
            Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

            // Step 4: Attach the cloned widget to the second page
            targetPage.Annotations.Add(clonedWidget);

            // Save the file
            doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
            Console.WriteLine("PDF created: output.pdf");
        }

        PDFNet.Terminate();
    }
}
```

**Beklenen çıktı:** `output.pdf` adlı dosya iki sayfa içerir. Her iki sayfada da “Sample” etiketiyle aynı düzenlenebilir metin kutusu gösterilir. Birini düzenlemek diğerini anında günceller.

---

## Yaygın Sorular & Kenar Durumları

### Alanı *iki* sayfadan **daha fazla** sayfada kullanmam gerekirse?

Her ek sayfa için klon‑ve‑ekle adımlarını tekrarlayın. Temel veri nesnesi aynı kalır, bu yüzden tüm widget'lar senkronizedir.

```csharp
Widget anotherClone = textBoxField.CreateWidgetAnnotation();
thirdPage.Annotations.Add(anotherClone);
```

### Görünümü (yazı tipi, kenarlık, arka plan) nasıl değiştiririm?

Her `Widget` için `SetBorderColor`, `SetBorderWidth` ve `SetBackgroundColor` metodları bulunur. Ayrıca yazı tipi ve boyutu kontrol etmek için varsayılan görünüm dizesi (`DA`) atayabilirsiniz.

```csharp
textBoxField.SetBorderColor(new ColorPt(0, 0, 1), 3); // blue border
textBoxField.SetBackgroundColor(new ColorPt(0.9, 0.9, 0.9), 3); // light gray fill
textBoxField.SetDefaultAppearance("Helvetica 12 Tf 0 g");
```

### Kullanıcı doldurduktan sonra alanı sadece‑okunur (read‑only) yapabilir miyim?

Evet. Veriyi topladıktan sonra alanın `ReadOnly` bayrağını ayarlayın veya iş akışınıza göre dinamik olarak değiştirin.

```csharp
textBoxField.SetFlag(Field.Flag.e_readonly, true);
```

### Zaten bir form içeren PDF'ler nasıl ele alınır?

Belge zaten bir AcroForm içeriyorsa, `doc.GetForm()` sadece onu döndürür. Yeni alanlar ekleyebilir, mevcutları bozmadan çalışabilirsiniz. Tekil alan adları kullanmaya özen gösterin.

---

## Gerçek Dünya Projeleri İçin İpuçları

- **Adlandırma konvansiyonu:** Çakışmaları önlemek için alan adlarını sayfa veya bölüm ile önekleyin (ör. `invoice_customer_name`).  
- **Doğrulama:** İstemci‑tarafı doğrulama gerekiyorsa JavaScript eylemleri ekleyin (`field.SetAction(Field.Action.e_keystroke, "event.rc = /^[A-Za-z]+$/.test(event.change);")`).  
- **Performans:** Büyük PDF'lerle çalışırken toplu işlemlerden önce `doc.Lock()` çağırarak I/O yükünü azaltın.  
- **Erişilebilirlik:** Ekran okuyucuların alanı tanımlaması için `AlternateName` özelliğini ayarlayın.

---

## Sonuç

Şimdi **PDF textbox field** oluşturduk, **duplicate PDF form field**'ı sayfalar arasında nasıl çoğaltacağımızı gösterdik ve C# kullanarak **add textbox to PDF form** işlemini en basit şekilde uyguladık. Tam, çalıştırılabilir kod yukarıda yer alıyor; stil, doğrulama veya ek sayfalar ekleyerek genişletebilirsiniz.

Bir sonraki adım için hazır mısınız? Bir açılır menü (`ChoiceField`) veya imza widget'ı eklemeyi deneyin, ya da veri girişi sonrası formu arşiv amaçlı düzleştirmeyi (flatten) keşfedin. PDFTron SDK (veya benzer bir kütüphane) size yapı taşlarını sunar—son şekli hayal gücünüz belirler.

Bir sorunla karşılaşırsanız, aşağıya yorum bırakın ya da kütüphanenin resmi dokümantasyonuna göz atın; burada ele aldıklarımızı tamamlayan çok sayıda örnek bulacaksınız. Kodlamanın tadını çıkarın, formlarınız her zaman senkronize olsun!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımları keşfetmeniz için adım‑adım açıklamalı tam çalışan kod örnekleri içerir.

- [Aspose ile PDF Oluşturma – Form Alanı ve Sayfalar Ekleme](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Java ile PDF Belgesine Form Alanı Ekleme](/pdf/english/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)
- [Java ile PDF Belgesine Form Alanı Ekleme (Almanca)](/pdf/german/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}