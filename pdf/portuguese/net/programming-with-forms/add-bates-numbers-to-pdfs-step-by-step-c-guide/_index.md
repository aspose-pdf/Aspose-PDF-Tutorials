---
category: general
date: 2026-02-12
description: Adicione números Bates a arquivos PDF rapidamente. Aprenda como adicionar
  campo de texto PDF, adicionar campo de formulário PDF e adicionar números de página
  PDF usando Aspose.PDF.
draft: false
keywords:
- add bates numbers
- add text field pdf
- add form field pdf
- add page numbers pdf
- how to add bates
language: pt
og_description: Adicione números Bates a documentos PDF em C#. Este guia mostra como
  adicionar campo de texto PDF, campo de formulário PDF e números de página PDF com
  Aspose.PDF.
og_title: Adicionar Números Bates a PDFs – Tutorial Completo de C#
tags:
- PDF
- C#
- Aspose.PDF
title: Adicionar Números Bates a PDFs – Guia passo a passo em C#
url: /pt/net/programming-with-forms/add-bates-numbers-to-pdfs-step-by-step-c-guide/
---


{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adicionar Números Bates a PDFs – Guia Completo em C#

Já precisou **add bates numbers** a um conjunto de PDFs jurídicos, mas não sabia por onde começar? Você não está sozinho. Em muitos escritórios de advocacia e projetos de e‑discovery, carimbar cada página com um identificador único é uma tarefa diária, e fazer isso manualmente é um pesadelo.  

A boa notícia? Com algumas linhas de C# e Aspose.PDF você pode automatizar tudo. Neste tutorial vamos percorrer **how to add bates** numbers, espalhar um campo de texto em cada página e salvar um PDF limpo e pesquisável — tudo sem suar.

> **O que você receberá:** um exemplo de código totalmente executável, explicações sobre por que cada linha importa, dicas para casos de borda e uma lista rápida para verificar sua saída.  

Também abordaremos tarefas relacionadas como **add text field pdf**, **add form field pdf** e **add page numbers pdf**, para que você tenha uma caixa de ferramentas pronta para qualquer desafio de automação de documentos.

---

## Prerequisites

- .NET 6.0 ou superior (o código também funciona com .NET Framework 4.6+)  
- Visual Studio 2022 (ou qualquer IDE de sua preferência)  
- Uma licença válida do Aspose.PDF for .NET (a versão de avaliação gratuita serve para testes)  
- Um PDF de origem chamado `source.pdf` colocado em uma pasta que você possa referenciar  

Se algum desses itens lhe for desconhecido, pause e instale o que falta antes de prosseguir. Os passos abaixo assumem que você já adicionou o pacote NuGet Aspose.PDF:

```bash
dotnet add package Aspose.Pdf
```

---

## How to add bates numbers to a PDF with Aspose.PDF

A seguir está o programa completo, pronto para copiar‑e‑colar. Ele carrega um PDF, cria um **text box field** em cada página, grava um número Bates formatado e, por fim, salva o arquivo modificado.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 👉 Step 1: Load the source PDF document
        using (var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf"))
        {
            // 👉 Step 2: Add a Bates number text field to each page
            for (int pageNumber = 1; pageNumber <= pdfDocument.Pages.Count; pageNumber++)
            {
                // Define the rectangle where the field will appear (10,10) = lower‑left corner
                var fieldRect = new Rectangle(10, 10, 150, 30);

                // Create the TextBoxField – this is the “add text field pdf” part
                var batesField = new TextBoxField(pdfDocument.Pages[pageNumber], fieldRect)
                {
                    // Format the number: BATES-00001, BATES-00002, …
                    Value = $"BATES-{pageNumber:D5}"
                };

                // Register the field with the form collection – “add form field pdf”
                pdfDocument.Form.Add(batesField, $"Bates_{pageNumber}", pageNumber);
            }

            // 👉 Step 3: Save the modified PDF with Bates numbers
            pdfDocument.Save(@"YOUR_DIRECTORY\bates.pdf");
        }

        Console.WriteLine("✅ Bates numbers added successfully!");
    }
}
```

### Why this works

- **`Document`** é o ponto de entrada; representa o PDF inteiro.  
- **`Rectangle`** define onde o campo ficará na página. Os números estão em pontos (1 pt ≈ 1/72 in). Ajuste as coordenadas se precisar do número em outro canto.  
- **`TextBoxField`** é um *form field* que pode conter qualquer string. Ao atribuir `Value` efetivamente **add page numbers pdf** com um prefixo customizado.  
- **`pdfDocument.Form.Add`** registra o campo no AcroForm do PDF, tornando‑o visível em visualizadores como o Adobe Acrobat.  

Se precisar mudar a aparência (fonte, cor, tamanho) você pode ajustar as propriedades do `TextBoxField` — veja a documentação da Aspose para `DefaultAppearance` e `Border`.

---

## Adding a text field to each PDF page (the “add text field pdf” step)

Às vezes você quer apenas um rótulo visível, não um campo de formulário interativo. Nesse caso, pode substituir o `TextBoxField` por um `TextFragment` e adicioná‑lo diretamente à coleção `Paragraphs` da página. Aqui está uma alternativa rápida:

```csharp
var fragment = new TextFragment($"BATES-{pageNumber:D5}")
{
    // Position the text using a TextState (font, size, color)
    TextState = new TextState
    {
        Font = FontRepository.FindFont("Arial"),
        FontSize = 12,
        ForegroundColor = Color.Black
    }
};

// Set the fragment’s rectangle (same coordinates as before)
fragment.Position = new Position(10, 10);
pdfDocument.Pages[pageNumber].Paragraphs.Add(fragment);
```

A abordagem **add text field pdf** é útil quando o documento final será somente leitura, enquanto o método **add form field pdf** mantém os números editáveis posteriormente.

---

## Saving the PDF with Bates numbers (the “add page numbers pdf” moment)

Depois que o loop termina, chamar `pdfDocument.Save` grava tudo no disco. Se precisar preservar o arquivo original, basta mudar o caminho de saída ou usar as sobrecargas de `pdfDocument.Save` para transmitir o resultado diretamente a uma resposta em uma API web.

```csharp
// Example: stream to HTTP response (ASP.NET Core)
Response.ContentType = "application/pdf";
pdfDocument.Save(Response.Body);
```

Essa é a parte elegante — sem arquivos temporários, sem bibliotecas extras, apenas o Aspose fazendo o trabalho pesado.

---

## Expected Result & Quick Verification

Abra `bates.pdf` em qualquer visualizador de PDF. Você deverá ver uma pequena caixa no canto inferior‑esquerdo de cada página contendo:

```
BATES-00001
BATES-00002
…
```

Se inspecionar as propriedades do documento, notará um AcroForm contendo campos nomeados `Bates_1`, `Bates_2`, etc. Isso confirma que a etapa **add form field pdf** foi bem‑sucedida.

---

## Common Pitfalls & Pro Tips

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| Numbers appear off‑center | Rectangle coordinates are relative to the page’s lower‑left corner. | Flip the Y‑value (`pageHeight - marginTop`) or use `page.PageInfo.Height` to calculate a top‑margin placement. |
| Fields are invisible in Adobe Reader | The default border is set to “No”. | Set `batesField.Border = new Border { Width = 0.5f, Color = Color.Black };` |
| Large PDFs cause memory pressure | `using` disposes the document only after the loop finishes. | Process pages in chunks or use `pdfDocument.Save` with `SaveOptions` that enable streaming. |
| License not applied | Aspose prints a watermark on the first page. | Register your license early: `License lic = new License(); lic.SetLicense("Aspose.Pdf.lic");` |

---

## Extending the Solution

- **Custom prefixes:** Replace `"BATES-"` with any string (`"DOC-"`, `"CASE-"`, …).  
- **Zero‑padding length:** Change `{pageNumber:D5}` to `{pageNumber:D3}` for three digits.  
- **Dynamic placement:** Use `pdfDocument.Pages[pageNumber].PageInfo.Width` to position the field on the right‑hand side.  
- **Conditional numbering:** Skip blank pages by checking `pdfDocument.Pages[pageNumber].IsBlank`.

Todas essas variações mantêm o padrão central de **add bates numbers**, **add text field pdf** e **add form field pdf** intacto.

---

## Full Working Example (All‑in‑One)

Abaixo está o programa final, pronto‑para‑executar, que incorpora as dicas acima. Copie‑o para um novo aplicativo console e pressione F5.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;

class AddBatesNumbers
{
    static void Main()
    {
        // Register your license here (optional for trial)
        // var license = new License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        using (var pdfDocument = new Document(inputPath))
        {
            int totalPages = pdfDocument.Pages.Count;

            for (int i = 1; i <= totalPages; i++)
            {
                // Position the field 10 pts from left and 10 pts from bottom
                var rect = new Rectangle(10, 10, 150, 30);

                var batesField = new TextBoxField(pdfDocument.Pages[i], rect)
                {
                    Value = $"BATES-{i:D5}"
                };

                // Optional: make the field look nicer
                batesField.Border = new Border
                {
                    Width = 0.5f,
                    Color = Color.Gray
                };
                batesField.DefaultAppearance = new DefaultAppearance
                {
                    Font = FontRepository.FindFont("Arial"),
                    FontSize = 10,
                    ForegroundColor = Color.DarkBlue
                };

                pdfDocument.Form.Add(batesField, $"Bates_{i}", i);
            }

            pdfDocument.Save(outputPath);
        }

        Console.WriteLine($"✅ Finished! Bates numbers saved to: {outputPath}");
    }
}
```

Execute, abra o resultado e você verá um identificador com aparência profissional em cada página — exatamente o que um especialista em suporte a litígios esperaria.

---

## Conclusion

Acabamos de demonstrar **how to add bates numbers** a qualquer PDF usando C# e Aspose.PDF. Ao criar um **text box field** em cada página, simultaneamente **add text field pdf**, **add form field pdf** e **add page numbers pdf** em uma única passagem. A abordagem é rápida, escalável e fácil de ajustar para prefixos personalizados, layouts diferentes ou lógica condicional.

Pronto para o próximo desafio? Experimente incorporar um QR code que linka ao arquivo original do caso, ou gerar uma página de índice separada que liste todos os números Bates com seus respectivos títulos de página. A mesma API permite mesclar PDFs, extrair páginas e até redigir dados sensíveis — o céu é o limite.

Se encontrar algum problema, deixe um comentário abaixo ou consulte a documentação oficial da Aspose para aprofundamentos. Feliz codificação, e que seus PDFs estejam sempre perfeitamente numerados!  

---  

![add bates numbers screenshot](https://example.com/images/add-bates-numbers.png "add bates numbers example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}