---
category: general
date: 2026-03-03
description: Как проверить установку пакета NuGet в PowerShell. Узнайте, как запустить
  PowerShell от имени администратора, установить конкретную версию и эффективно управлять
  пакетами.
draft: false
keywords:
- how to verify installation
- install specific version
- run powershell as admin
- install nuget package powershell
- powershell package management
language: ru
og_description: Как проверить установку пакета NuGet в PowerShell. Это пошаговое руководство
  покажет, как запустить PowerShell от имени администратора, установить конкретную
  версию и убедиться, что пакет присутствует.
og_title: Как проверить установку пакета NuGet с помощью PowerShell
tags:
- PowerShell
- NuGet
- Package Management
title: Как проверить установку пакета NuGet с помощью PowerShell
url: /ru/net/getting-started/how-to-verify-installation-of-a-nuget-package-with-powershel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как проверить установку пакета NuGet с помощью PowerShell

Проверка установки пакета NuGet в PowerShell — распространённая задача для администраторов Windows. Если вы когда‑нибудь задавались вопросом, действительно ли пакет оказался в вашей системе, это руководство покажет, как точно проверить установку — без догадок.  

В течение нескольких минут мы пройдём процесс запуска PowerShell от имени администратора, загрузки конкретной версии пакета и окончательной проверки, что пакет существует на вашем компьютере. Вы также узнаете несколько советов по повседневному **PowerShell package management**, которые помогут поддерживать чистоту вашей среды.  

Прежде чем мы начнём, убедитесь, что у вас есть компьютер с Windows и PowerShell 7 (или Windows PowerShell 5.1), а также подключение к интернету. Дополнительные инструменты не требуются; всё работает напрямую через встроенного провайдера PackageManagement.

---

![Скриншот повышенного окна PowerShell с командой Get-Package](/images/verify-installation.png "Скриншот, показывающий, как проверить установку в повышенном окне PowerShell")

## Шаг 1: Запустить PowerShell от администратора  

Запуск PowerShell с правами администратора — первая линия защиты от проблем, связанных с разрешениями. Когда вы **запускаете PowerShell от администратора**, команда `Install-Package` может записывать в папку Program Files и регистрировать пакет в системном каталоге.

```powershell
# Open an elevated session (manual step)
# Right‑click the PowerShell icon → Run as administrator
```

> **Pro tip:** Прикрепите ярлык «Windows PowerShell (Admin)» к панели задач. Один клик — и вы готовы работать.

### Почему важны права администратора  

Без повышения прав `Install-Package` может тихо перейти в пользовательскую область, что позже может запутать `Get-Package`, поскольку по умолчанию он ищет в системной области. Повышение гарантирует, что пакет окажется там, где ожидают его большинство скриптов.

---

## Шаг 2: Установить конкретную версию пакета NuGet  

Часто вам нужна не последняя версия, а проверенная версия, с которой ваш проект уже тестировался. Шаблон **установки конкретной версии** прост с флагом `-Version`.

```powershell
# Install Aspose.PDF version 25.3 from the PowerShell Gallery
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Scope AllUsers -Force
```

### Разбор команды  

| Параметр | Что делает | Зачем нужен |
|-----------|------------|--------------|
| `-Version 25.3` | Фиксирует точный номер сборки | Гарантирует воспроизводимые сборки |
| `-ProviderName NuGet` | Указывает PowerShell, какой провайдер использовать | Избегает неоднозначности, если зарегистрировано несколько провайдеров |
| `-Scope AllUsers` | Устанавливает для всех учетных записей на машине | Работает с системными запросами `Get-Package` |
| `-Force` | Подавляет запросы (полезно в скриптах) | Обеспечивает плавную автоматизацию |

> **Watch out:** Если опустить `-Version`, PowerShell загрузит новейший пакет, что может привести к несовместимым изменениям.

---

## Шаг 3: Проверить установку  

Настал момент истины: **как проверить установку**. Самый прямой способ — запросить у PowerShell только что установленный пакет.

```powershell
# Retrieve the package info
Get-Package -Name Aspose.PDF -ProviderName NuGet
```

Вы должны увидеть вывод, похожий на:

```
Name           Version   Source   Summary
----           -------   ------   -------
Aspose.PDF    25.3      NuGet    .NET PDF library from Aspose
```

Если команда ничего не вернёт, попробуйте запрос в пользовательской области:

```powershell
Get-Package -Name Aspose.PDF -ProviderName NuGet -Scope CurrentUser
```

### Альтернативные методы проверки  

1. **Проверьте папку модуля** – Пакеты хранятся в `C:\Program Files\PackageManagement\Packages\`. Ищите папку с именем `Aspose.PDF.25.3`.  
2. **Используйте `Find-Package`** – Этот запрос ищет в репозитории и может подтвердить наличие версии:  

   ```powershell
   Find-Package -Name Aspose.PDF -ProviderName NuGet | Where-Object { $_.Version -eq '25.3' }
   ```

3. **Проверьте с помощью .NET** – Загрузите сборку в PowerShell, чтобы убедиться, что DLL можно загрузить:  

   ```powershell
   Add-Type -Path "C:\Program Files\PackageManagement\Packages\Aspose.PDF.25.3\lib\netstandard2.0\Aspose.Pdf.dll"
   [Aspose.Pdf.License] | Get-Member
   ```

Если любой из этих проверок прошёл успешно, вы успешно **проверили установку**.

---

## Распространённые подводные камни и как их избежать  

- **Отсутствует провайдер NuGet** – Сначала выполните `Install-PackageProvider -Name NuGet -Force`.  
- **Блокировки ExecutionPolicy** – Временно установите `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` для текущей сессии.  
- **Проблемы с сетевым прокси** – Используйте параметры `-Proxy` и `-ProxyCredential`, если ваша среда находится за корпоративным прокси.  
- **Конфликты версий** – Когда существует несколько версий, укажите `-RequiredVersion` в `Get-Package` для уточнения.

---

## Сводим всё вместе — полный скрипт  

Ниже представлен готовый к запуску скрипт, который объединяет три шага, включает обработку ошибок и выводит дружелюбное сообщение об успехе.

```powershell
<# 
.SYNOPSIS
    Installs a specific version of a NuGet package and verifies the installation.
.DESCRIPTION
    Demonstrates how to run PowerShell as admin, install a specific version, 
    and confirm that the package is present using Get-Package.
#>

# Ensure we are running elevated
if (-not ([Security.Principal.WindowsPrincipal] `
        [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole(`
        [Security.Principal.WindowsBuiltInRole]::Administrator)) {
    Write-Warning "Please run this script in an elevated PowerShell session."
    exit 1
}

$packageName = 'Aspose.PDF'
$packageVersion = '25.3'

try {
    Write-Host "Installing $packageName version $packageVersion..."
    Install-Package $packageName -Version $packageVersion `
        -ProviderName NuGet -Scope AllUsers -Force -ErrorAction Stop

    Write-Host "Installation completed. Verifying..."
    $pkg = Get-Package -Name $packageName -ProviderName NuGet -ErrorAction Stop

    if ($pkg.Version -eq $packageVersion) {
        Write-Host "`n✅ Successfully verified installation of $packageName $packageVersion."
    } else {
        Write-Error "Version mismatch: Expected $packageVersion but got $($pkg.Version)."
    }
}
catch {
    Write-Error "An error occurred: $_"
}
```

Запуск скрипта выдаёт чёткую строку «✅ Successfully verified installation…», подтверждая, что **как проверить установку** работает от начала до конца.

---

## Заключение  

Теперь вы знаете **как проверить установку** любого пакета NuGet с помощью PowerShell, начиная с запуска повышенной сессии, установки целевой версии и заканчивая подтверждением наличия пакета. Овладение этими шагами даёт уверенность в вашем процессе **PowerShell package management** и предотвращает головные боли «пакет выглядит установленным, но не установлен», которые часто мучают разработчиков Windows.

Что дальше? Попробуйте заменить `Aspose.PDF` на другую библиотеку, поэкспериментировать с `-Scope CurrentUser` или написать скрипт массовой установки нескольких пакетов для новой рабочей станции. И если столкнётесь с особенностями, вспомните приведённые выше советы по устранению неполадок — особенно проверки провайдера и политики выполнения.

Удачного скриптования, и пусть ваши установки всегда можно будет проверить!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}