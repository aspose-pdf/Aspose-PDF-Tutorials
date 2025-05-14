---
"date": "2025-04-14"
"description": "Java için Aspose.PDF'yi kullanarak PDF belgelerinde erişilebilir etiketli tabloların nasıl oluşturulacağını ve yapılandırılacağını öğrenin. Adım adım kılavuzla belge erişilebilirliğini geliştirin."
"title": "Java için Aspose.PDF Kullanarak PDF'lerde Erişilebilir Etiketli Tablolar Oluşturun"
"url": "/tr/java/tables-lists/create-tagged-table-aspose-pdf-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Java için Aspose.PDF Kullanarak PDF'lerde Erişilebilir Etiketli Tablolar Oluşturun

Erişilebilir belgeler oluşturmak, tüm kullanıcıların, yetenekleri ne olursa olsun, içeriğinizle etkili bir şekilde etkileşime girebilmelerini sağlamak için çok önemlidir. Bu eğitim, güçlü Aspose.PDF for Java kitaplığını kullanarak etiketli PDF'lerde tablolar oluşturma ve yapılandırma konusunda size rehberlik edecektir. Bu adımları izleyerek, Aspose.PDF'nin sağlam özelliklerinden yararlanırken belge erişilebilirliğini nasıl artıracağınızı öğreneceksiniz.

## Ne Öğreneceksiniz

- Java için Aspose.PDF nasıl kurulur ve başlatılır
- PDF belgesi içerisinde etiketli bir tablo oluşturma süreci
- Tablo başlıklarını, gövdelerini ve altbilgilerini yapılandırma teknikleri
- Kullanılabilirliği artırmak için erişilebilir niteliklerin eklenmesi
- Büyük belgelerle çalışırken performansı optimize etmeye yönelik en iyi uygulamalar

Başlamadan önce ihtiyaç duyacağınız ön koşullara bir göz atalım.

## Ön koşullar

Bu eğitimi takip edebilmek için şunlara sahip olduğunuzdan emin olun:

- Sisteminizde Java Development Kit (JDK) yüklü.
- IntelliJ IDEA veya Eclipse gibi Entegre Geliştirme Ortamı (IDE).
- Temel Java programlama bilgisi ve PDF kavramlarına aşinalık.

Java için Aspose.PDF'yi de kullanacağız. Proje ortamınızda gerekli kütüphanelerin ve bağımlılıkların kurulu olduğundan emin olun.

## Java için Aspose.PDF Kurulumu

### Kurulum

Aspose.PDF for Java'yı Maven veya Gradle kullanarak projenize kolayca entegre edebilirsiniz. Aşağıda her iki derleme sistemi için bağımlılık yapılandırmaları verilmiştir:

**Usta**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### Lisans Edinimi

Java için Aspose.PDF'yi kullanmak için ücretsiz deneme lisansı edinebilir veya tam sürümü satın alabilirsiniz. Başlamak için şu adımları izleyin:

- **Ücretsiz Deneme**: Geçici bir lisans indirin [Aspose Ücretsiz Deneme](https://releases.aspose.com/pdf/java/).
- **Satın almak**: Ticari kullanım için tam lisans satın almayı düşünün [Aspose Satın Alma](https://purchase.aspose.com/buy).

### Temel Başlatma

Aspose.PDF projenizi, bir örneğini oluşturarak başlatın `Document` sınıf. Bu, PDF belgeleriyle çalışmak için giriş noktası görevi görür.

```java
import com.aspose.pdf.Document;

// Yeni bir Belge Başlat
Document document = new Document();
```

## Uygulama Kılavuzu

Bu bölümde, Aspose.PDF kullanarak PDF belgenizde etiketli bir tablo oluşturma ve yapılandırma sürecini mantıksal adımlara ayıracağız.

### 1. Temel Yapının Oluşturulması

Etiketli PDF belgenizin temel yapısını ayarlayarak başlayın:

```java
import com.aspose.pdf.ITaggedContent;
import com.aspose.pdf.tagged.logicalstructure.elements.TableElement;

// Etiketli İçeriği Başlat
ITaggedContent taggedContent = document.getTaggedContent();
taggedContent.setTitle("Example Table in a Tagged PDF");
taggedContent.setLanguage("en-US");

// Kök yapı öğesini alın ve yeni bir TableElement oluşturun
StructureElement rootElement = taggedContent.getRootElement();
TableElement tableElement = taggedContent.createTableElement();
rootElement.appendChild(tableElement);
```

### 2. Tablo Kenarlıklarını Yapılandırma

Görsel netliği artırmak için tablonuzun sınırlarını belirleyin:

```java
import com.aspose.pdf.BorderInfo;
import com.aspose.pdf.BorderSide;

// Tüm tablo için sınır belirleyin
tableElement.setBorder(new BorderInfo(BorderSide.All, 1.2F, Color.getDarkBlue()));
```

### 3. Tablo Başlığını Ayarlama (THead)

Sütun başlıklarını görüntülemek için tablo başlığınızı oluşturun ve yapılandırın:

```java
import com.aspose.pdf.tagged.logicalstructure.elements.TableTHeadElement;
import com.aspose.pdf.tagged.logicalstructure.elements.TableTHElement;

TableTHeadElement tableTHeadElement = tableElement.createTHead();
TableTRElement headTrElement = tableTHeadElement.createTR();
headTrElement.setAlternativeText("Header Row");
headTrElement.setBackgroundColor(Color.getLightGray());

int colCount = 4;
for (int colIndex = 0; colIndex < colCount; colIndex++) {
    TableTHElement thElement = headTrElement.createTH();
    thElement.setText(String.format("Header %s", colIndex));
    thElement.setBackgroundColor(Color.getGreenYellow());
    thElement.setBorder(new BorderInfo(BorderSide.All, 4.0F, Color.getLightGray()));
    thElement.setMargin(new MarginInfo(16.0, 2.0, 8.0, 2.0));
    thElement.setAlignment(HorizontalAlignment.Right);
}
```

### 4. Tablo Gövdesini (TBody) Yapılandırma

Tablonuzun gövdesini verilerle doldurun:

```java
import com.aspose.pdf.tagged.logicalstructure.elements.TableTBodyElement;
import com.aspose.pdf.tagged.logicalstructure.elements.TableTDElement;

TableTBodyElement tableTBodyElement = tableElement.createTBody();
int rowCount = 50;
for (int rowIndex = 0; rowIndex < rowCount; rowIndex++) {
    TableTRElement trElement = tableTBodyElement.createTR();
    trElement.setAlternativeText(String.format("Data Row %s", rowIndex));

    for (int colIndex = 0; colIndex < colCount; colIndex++) {
        int colSpan = 1;
        int rowSpan = 1;

        if (colIndex == 1 && rowIndex == 1) {
            colSpan = 2;
            rowSpan = 2;
        } else if (colIndex == 2 && (rowIndex == 1 || rowIndex == 2)) {
            continue;
        } else if (rowIndex == 2 && (colIndex == 1 || colIndex == 2)) {
            continue;
        }

        TableTDElement tdElement = trElement.createTD();
        tdElement.setText(String.format("Cell [%s, %s]", rowIndex, colIndex));
        tdElement.setBackgroundColor(Color.getYellow());
        tdElement.setBorder(new BorderInfo(BorderSide.All, 4.0F, Color.getGray()));
        tdElement.setMargin(new MarginInfo(8.0, 2.0, 8.0, 2.0));
        tdElement.setAlignment(HorizontalAlignment.Center);

        // Hücre içeriği için metin durumunu yapılandırın
        TextState cellTextState = new TextState();
        cellTextState.setForegroundColor(Color.getDarkBlue());
        cellTextState.setFontSize(7.5F);
        cellTextState.setFontStyle(FontStyles.Bold);
        cellTextState.setFont(FontRepository.findFont("Arial"));
        tdElement.setDefaultCellTextState(cellTextState);

        tdElement.isWordWrapped();
        tdElement.setVerticalAlignment(VerticalAlignment.Center);
        tdElement.setColSpan(colSpan);
        tdElement.setRowSpan(rowSpan);
    }
}
```

### 5. Tablo Altbilgisini (TFoot) Ayarlama

Özetleme veya ek bilgi için tablonuza bir altbilgi ekleyin:

```java
import com.aspose.pdf.tagged.logicalstructure.elements.TableTFootElement;

TableTFootElement tableTFootElement = tableElement.createTFoot();
TableTRElement footTrElement = tableTFootElement.createTR();
footTrElement.setAlternativeText("Footer Row");
footTrElement.setBackgroundColor(Color.getLightSeaGreen());

for (int colIndex = 0; colIndex < colCount; colIndex++) {
    TableTDElement tdElement = footTrElement.createTD();
    tdElement.setText(String.format("Footer %s", colIndex));
    tdElement.setAlignment(HorizontalAlignment.Center);
    tdElement.getStructureTextState().setFontSize(7F);
    tdElement.getStructureTextState().setFontStyle(FontStyles.Bold);
}
```

### 6. Erişilebilirlik Niteliklerinin Eklenmesi

Tablonuza özet niteliği ekleyerek erişilebilirliği artırın:

```java
import com.aspose.pdf.tagged.logicalstructure.StructureAttributes;
import com.aspose.pdf.tagged.logicalstructure.StructureAttribute;
import com.aspose.pdf.tagged.logicalstructure.elements.TaggedPdfElements;

// Erişilebilirlik için bir açıklama ekleme
StructureAttributes attributes = new StructureAttributes();
attributes.setLang("en-US");
taggedContent.setTagProperties(attributes);

// Tabloya bir özet ekleyin
TableElement taggedTable = (TableElement) taggedContent.getTaggedPdfElements().get(TaggedPdfElements.Table);
taggedTable.setTitleAlternativeText("Summary of Data");
```

### 7. Belgenizi Kaydetme

Son olarak belgenizi kaydedin:

```java
document.save("AccessibleTaggedTable.pdf");
```

## Çözüm

Bu öğreticiyi takip ederek, Java için Aspose.PDF kullanarak PDF'lerde erişilebilir etiketli tabloların nasıl oluşturulacağını öğrendiniz. Bu süreç yalnızca belgelerinizin kullanılabilirliğini artırmakla kalmaz, aynı zamanda erişilebilirlik standartlarına uyumu da sağlar.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}