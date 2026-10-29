---
title: Criptografar PDF com Permissão de Não‑Impressão Usando Aspose.PDF para .NET
weight: 101
limit:
description: Aprenda como criptografar um PDF com AES‑256 e desativar a impressão usando Aspose.PDF para .NET.
keywords: [Aspose.PDF for .NET, pdf encryption aes-256, disable pdf printing, pdf password protection, no print permission pdf]
url: /net/security-permissions/encrypt-pdf-no-print/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Aprenda como criptografar um PDF com AES‑256 e desativar a impressão
    usando Aspose.PDF para .NET.
  headline: Criptografar PDF com Permissão de Não‑Impressão Usando Aspose.PDF para
    .NET
  type: TechArticle
- description: Aprenda como criptografar um PDF com AES‑256 e desativar a impressão
    usando Aspose.PDF para .NET.
  name: Criptografar PDF com Permissão de Não‑Impressão Usando Aspose.PDF para .NET
  steps:
  - name: Defina o caminho do PDF de origem, o nome do arquivo protegido de saída
      e as senhas de visualização e proprietário.
    text: Defina o caminho do PDF de origem, o nome do arquivo protegido de saída
      e as senhas de visualização e proprietário.
  - name: Verifique se o arquivo de origem existe e interrompa com uma mensagem de
      erro se estiver ausente.
    text: Verifique se o arquivo de origem existe e interrompa com uma mensagem de
      erro se estiver ausente.
  - name: Abra o PDF original, defina nenhuma permissão, criptografe-o com AES‑256
      usando as senhas especificadas e salve o arquivo protegido.
    text: Abra o PDF original, defina nenhuma permissão, criptografe-o com AES‑256
      usando as senhas especificadas e salve o arquivo protegido.
  - name: Reabra o PDF criptografado com a senha de visualização e escreva sua flag
      IsEncrypted no console para confirmar a proteção.
    text: Reabra o PDF criptografado com a senha de visualização e escreva sua flag
      IsEncrypted no console para confirmar a proteção.
  - name: Exiba uma mensagem final indicando que a criptografia está concluída e o
      nome do arquivo de saída.
    text: Exiba uma mensagem final indicando que a criptografia está concluída e o
      nome do arquivo de saída.
  type: HowTo
- questions:
  - answer: '`Permissions` é um enum de flags; atribuir `0` significa que nenhum bit
      de permissão está definido, portanto Aspose.Pdf não concede o direito PrintDocument
      e o visualizador não pode imprimir o PDF.'
    question: Por que definir `Permissions rights = 0;` desativa a impressão?
  - answer: Sim, substitua `CryptoAlgorithm.AESx256` por `CryptoAlgorithm.AESx128`
      (ou outro valor de enum suportado) na chamada `pdfDoc.Encrypt`; o restante do
      código permanece inalterado.
    question: Posso usar um algoritmo de criptografia diferente, como AES‑128, com
      o mesmo código?
  - answer: Aspose.Pdf aceitará senhas idênticas, mas a senha do proprietário não
      fornecerá privilégios adicionais; o PDF ainda será criptografado, e as permissões
      que você especificou (nenhuma) serão aplicadas.
    question: O que acontece se a senha de visualização e a senha mestra (do proprietário)
      forem iguais?
  - answer: Abra o arquivo protegido com a senha de visualização (`new Document(securedFile,
      viewerPwd)`) e tente imprimir a partir de um visualizador de PDF; como nenhuma
      permissão PrintDocument foi definida, o visualizador recusará o comando de impressão.
    question: Como posso confirmar que a impressão está realmente bloqueada após a
      criptografia?
  - answer: O código verifica `File.Exists(sourceFile)` e grava um erro em `Console.Error`
      antes de retornar, evitando que uma `FileNotFoundException` seja lançada pelo
      construtor `Document`.
    question: Qual erro é lançado se `original.pdf` não existir, e como devo tratá‑lo?
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-no-print/og-image.png
og_title: Criptografar PDF e Bloquear Impressão
og_description: Proteja seu PDF com criptografia AES‑256 e garanta que ele não possa ser impresso — guia passo a passo.
og_image_alt: Captura de tela mostrando código Aspose.PDF para .NET que criptografa um PDF e desativa a impressão.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Criptografar PDF com Permissão de Não‑Impressão Usando Aspose.PDF para .NET
Este tutorial mostra como abrir um PDF existente com Aspose.PDF para .NET, aplicar criptografia AES‑256 concedendo nenhuma permissão — desativando efetivamente a impressão — salvar o documento protegido e confirmar a proteção abrindo-o com a senha de visualização. Siga o código passo a passo para garantir que seu PDF não possa ser impresso após a criptografia.

---

{{< tutorial-widget sourcePath="pdf/net/security-permissions/encrypt-pdf-no-print" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: Por que definir `Permissions rights = 0;` desativa a impressão?**  
A: `Permissions` é um enum de flags; atribuir `0` significa que nenhum bit de permissão está definido, portanto Aspose.Pdf não concede o direito PrintDocument e o visualizador não pode imprimir o PDF.

**Q: Posso usar um algoritmo de criptografia diferente, como AES‑128, com o mesmo código?**  
A: Sim, substitua `CryptoAlgorithm.AESx256` por `CryptoAlgorithm.AESx128` (ou outro valor de enum suportado) na chamada `pdfDoc.Encrypt`; o restante do código permanece inalterado.

**Q: O que acontece se a senha de visualização e a senha mestra (do proprietário) forem iguais?**  
A: Aspose.Pdf aceitará senhas idênticas, mas a senha do proprietário não fornecerá privilégios adicionais; o PDF ainda será criptografado, e as permissões que você especificou (nenhuma) serão aplicadas.

**Q: Como posso confirmar que a impressão está realmente bloqueada após a criptografia?**  
A: Abra o arquivo protegido com a senha de visualização (`new Document(securedFile, viewerPwd)`) e tente imprimir a partir de um visualizador de PDF; como nenhuma permissão PrintDocument foi definida, o visualizador recusará o comando de impressão.

**Q: Qual erro é lançado se `original.pdf` não existir, e como devo tratá‑lo?**  
A: O código verifica `File.Exists(sourceFile)` e grava um erro em `Console.Error` antes de retornar, evitando que uma `FileNotFoundException` seja lançada pelo construtor `Document`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}