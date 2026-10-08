---
category: general
date: 2026-02-20
description: Learn how to install nuget packages using PowerShell, run powershell
  as admin, list installed packages and verify installed package in minutes.
draft: false
keywords:
- how to install nuget
- run powershell as admin
- list installed packages
- how to verify package
- verify installed package
language: en
og_description: how to install nuget packages using PowerShell, run powershell as
  admin, list installed packages and verify installed package—complete walkthrough.
og_title: how to install nuget packages via PowerShell – quick guide
tags:
- PowerShell
- NuGet
- Package Management
title: how to install nuget packages via PowerShell – step by step
url: /net/getting-started/how-to-install-nuget-packages-via-powershell-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to install nuget packages via PowerShell – step by step

Ever wondered **how to install nuget** packages without opening Visual Studio? You’re not alone. In many CI pipelines or on fresh machines the fastest route is to drop into PowerShell—preferably *run powershell as admin*—and let the package manager do its thing.

In this tutorial we’ll walk through the entire process: opening the right console, pulling down a specific version of a library, and finally confirming that the package really landed on your system. By the end you’ll be able to **list installed packages**, know **how to verify package** integrity, and feel confident that the **verify installed package** step succeeded every time.

## What you’ll learn

- How to launch PowerShell with the correct privileges.  
- The exact `Install-Package` command syntax for NuGet.  
- Ways to **list installed packages** and confirm version numbers.  
- Common pitfalls (missing admin rights, version mismatches) and how to avoid them.  

No prior experience with NuGet is required, just a working Windows machine and a bit of curiosity.

---

## How to Install NuGet Packages Using PowerShell

> **Pro tip:** If you frequently add the same packages, consider adding them to a script file and running it with `-File`. It saves you from typing the same line over and over.

### Step 1: Open PowerShell with the necessary permissions

The very first thing you need to do is **run powershell as admin**. Without elevated rights the `Install-Package` cmdlet may silently fail or ask for confirmation you don’t want to deal with.

1. Click the Start button.  
2. Type **PowerShell**.  
3. Right‑click *Windows PowerShell* and choose **Run as administrator**.  

You’ll see a UAC prompt; click **Yes**. Now you have a privileged session ready for package installation.

> *Why admin?*  
> NuGet writes files to the global packages folder (`C:\Program Files\PackageManagement\NuGet\Packages` by default). That location is protected, so only an elevated process can write there.

### Step 2: Install the desired NuGet package and version

With the console open, the core command is straightforward:

```powershell
# Install the Aspose.PDF library, version 25.3
Install-Package Aspose.PDF -Version 25.3
```

- `Install-Package` is the PowerShell wrapper around NuGet’s client.  
- `-Version` pins the exact build you need, preventing accidental upgrades.  

If you omit `-Version`, PowerShell will pull the latest stable release—sometimes that’s fine, sometimes you want the exact version you tested against.

#### What happens under the hood?

PowerShell contacts the configured package source (by default `https://www.nuget.org/api/v2`) and downloads the `.nupkg` file. It then extracts the DLLs into the global packages folder and registers the package with the local package provider. The whole process usually finishes in a few seconds unless you’re on a slow network.

### Step 3: Verify that the package was installed successfully

Now that the package is on disk, you’ll probably ask, **“How do I verify the package?”** The answer lives in a simple query:

```powershell
# List all installed NuGet packages
Get-Package -Name Aspose.PDF
```

Running this returns something like:

```
Name        Version   Source
----        -------   ------
Aspose.PDF  25.3      nuget.org
```

That output confirms two things:

1. The package **Aspose.PDF** is present.  
2. Its version matches the one you asked for, satisfying the **verify installed package** requirement.

If you want to see *every* package on the machine, drop the `-Name` filter:

```powershell
Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}
```

This **list installed packages** view is handy for audits or when you need to clean up old libraries.

### Step 4: Optional – handling edge cases

#### a) Package not found or version mismatch

If PowerShell replies with *“Package not found”* or *“Version not available”*, double‑check the spelling and version number. NuGet is case‑insensitive, but a stray space will break the command.

```powershell
# Search the NuGet feed for available versions
Find-Package Aspose.PDF -AllVersions
```

#### b) Running without admin rights

Should you forget to **run powershell as admin**, the cmdlet will throw a permission error. The fix is simply to close the window and reopen it with elevated rights—no need to reinstall anything.

#### c) Using a custom source

In corporate environments you might have an internal NuGet feed:

```powershell
Install-Package MyCompany.Logging -Source https://nuget.mycompany.local/api/v2
```

The verification step stays the same; just remember to include `-Source` when you install.

---

## Quick reference table

| Action                              | PowerShell command                                          | Why it matters |
|-------------------------------------|-------------------------------------------------------------|----------------|
| Open elevated console               | *Run PowerShell as Administrator*                           | Needed for global install |
| Install a specific version          | `Install-Package <pkg> -Version <x.y.z>`                    | Guarantees reproducible builds |
| List a single package               | `Get-Package -Name <pkg>`                                    | Confirms **how to verify package** |
| List all NuGet packages             | `Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}`| Useful for **list installed packages** |
| Search available versions           | `Find-Package <pkg> -AllVersions`                           | Helps when version is unknown |

---

## Conclusion

We’ve covered **how to install nuget** packages using PowerShell from start to finish—opening the console **run powershell as admin**, pulling down a specific version, and finally **list installed packages** to **verify installed package**. With these commands in your toolbox you can automate library management on any Windows machine, whether you’re scripting a CI pipeline or just fixing a missing DLL on your dev box.

Next steps? Try adding multiple packages to a single script, explore the `-Scope` parameter to install locally for a project, or combine these commands with `Invoke-Expression` to build a lightweight installer for your team. And if you hit a snag, remember the **how to verify package** step—seeing the version in `Get-Package` is often the fastest way to spot a problem.

Happy PowerShelling! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}