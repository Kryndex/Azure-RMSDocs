---
# required metadata

title: File types supported by Azure Information Protection
description: Technical details about supported file types, file name extensions, and levels of protection for admins who are are responsible for the Azure Information Protection client for Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/15/2017
ms.topic: article
ms.prod:
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# File types supported by the Azure Information Protection client

>*Applies to: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 with SP1*

The Azure Information Protection client can apply the following to documents and emails:

- Classification only

- Classification and protection

- Protection only

Use the following information to check which file types are supported, the different levels of protection and how to change the default protection level, and which files are automatically excluded (skipped) from classification and protection.

## File types supported for classification only

Classification-only is supported for the following file types. Other file types support classification when they are also protected.

- **Adobe Portable Document Format**: .pdf​

- **Microsoft Visio**: .vsdx, .vsdm, .vssx, .vssm, .vsd, .vdw, .vst​

- **Microsoft Project**: .mpp, .mpt​

- **Microsoft Publisher**: .pub​

- **Microsoft Office 97, Office 2010, Office 2003**: .xls, .xlt, .doc, .dot, .ppt, .pps, .pot​
- **Microsoft XPS**: .xps .oxps​

- **Images**: .jpg, .jpe, .jpeg, .jif, .jfif, .jfi.png, .tif, .tiff​

- **SolidWorks**: .sldprt, .slddrw, .sldasm​

- **Autodesk Design Review 2013**: .dwfx​

- **Adobe Photoshop**: .psd​

- **Digital Negative**: .dng

## File types supported for protection

The Azure Information Protection client supports protection at two different levels, as described in the following table.

|Type of protection|Native|Generic|
|----------------------|----------|-----------|
|Description|For text, image, Microsoft Office (Word, Excel, PowerPoint) files, .pdf files, and other application file types that support a Rights Management service, native protection provides a strong level of protection that includes both encryption and enforcement of rights (permissions).|For all other applications and file types, generic protection provides a level of protection that includes both file encapsulation using the .pfile file type and authentication to verify if a user is authorized to open the file.|
|Protection|Files are fully encrypted and protection is enforced in the following ways:<br /><br />- Before protected content is rendered, successful authentication must occur for those who receive the file through email or are given access to it through file or share permissions.<br /><br />- Additionally, usage rights and policy set by the content owner when files are protected are fully enforced when the content is rendered in either the Azure Information Protection viewer (for protected text and image files) or the associated application (for all other supported file types).|File protection is enforced in the following ways:<br /><br />- Before protected content is rendered, successful authentication must occur for those who are authorized to open the file and given access to it. If authorization fails, the file does not open.<br /><br />- Usage rights and policy set by the content owner are displayed to inform authorized users of the intended usage policy.<br /><br />- Audit logging of authorized users opening and accessing files occurs, however, no usage rights are enforced by non-supporting applications.|
|Default for file types|This is the default level of protection for the following file types:<br /><br />- Text and image files<br /><br />- Microsoft Office (Word, Excel, PowerPoint) files<br /><br />- Portable document format (.pdf)<br /><br />For more information, see the following section, [Supported file types and file name extensions](#supported-file-types-for-protection-and-their-file-name-extensions).|This is the default protection for all other file types (such as .vsdx, .rtf, and so on) that are not supported by full protection.|

You can change the default protection level that the Azure Information Protection client applies. You can change the default level of native to generic, from generic to native, and even prevent the Azure Information Protection client from applying protection. For more information, see the [Changing the default protection level of files](#changing-the-default-protection-level-of-files) section in this article.

The data protection can be applied automatically when a user selects a label that an administrator has configured, or users can specify their own custom protection settings by using [permission levels](../deploy-use/configure-usage-rights.md#rights-included-in-permissions-levels). 

### Supported file types for protection and their file name extensions
The following table lists file types that are natively supported by the Azure Information Protection client. For these file types, the original file name extension is changed when native protected is applied, and these files become read-only.

For files that are generically protected, the original file name extension is always changed to .pfile.

> [!WARNING]
> If you have firewalls, web proxies, or security software that inspect and take action according to file name extensions, you might need to reconfigure these to support these new file name extensions.

|Original file name extension|Protected file name extension|
|--------------------------------|-------------------------------------|
|.txt|.ptxt|
|.xml|.pxml|
|.jpg|.pjpg|
|.jpeg|.ppng|
|.pdf|.ppdf|
|.png|.ppng|
|.tif|.ptif|
|.tiff|.ptiff|
|.bmp|.pbmp|
|.gif|.pgif|
|.jpe|.pjpe|
|.jfif|.pjfif|
|.jt|.pjt|


The following table lists the file types that the Azure Information Protection client natively supports for Microsoft Office apps. For these files, the file name extension remains the same after the file is protected by a Rights Management service.

|File types supported by Office|File types supported by Office|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm|.pptx<br /><br />.thmx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

### Changing the default protection level of files
You can change how the Azure Information Protection client protects files by editing the registry. For example, you can force files that support native protection to be generically protected by the Azure Information Protection client.

Reasons for why you might want to do this:

-   To ensure that all users can open the file if they don’t have an application that supports native protection.

-   To accommodate security systems that take action on files by their file name extension and can be reconfigured to accommodate the .pfile file name extension but cannot be reconfigured to accommodate multiple file name extensions for native protection.

Similarly, you can force the Azure Information Protection client to apply native protection to files that by default, would have generic protection applied. This might be appropriate if you have an application that supports the RMS APIs – for example, a line-of-business application written by your internal developers or an application purchased from an independent software vendor (ISV).

You can also force the Azure Information Protection client to block the protection of files (not apply native protection or generic protection). For example, this might be required if you have an automated application or service that must be able to open a specific file to process its contents. When you block protection for a file type, users cannot use the Azure Information Protection client to protect a file that has that file type. When they try, they see a message that the administrator has prevented protection and they must cancel their action to protect the file.

To configure the Azure Information Protection client to apply generic protection to all files that by default, would have native protection applied, make the following registry edits. Note if the FileProtection key does not exist, you must manually create it.

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection**: Create a new key named *.

    This setting denotes files with any file name extension.

2.  In the newly added key of HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\\\*, create a new string value (REG_SZ) named **Encryption** that has the data value of **Pfile**.

    This setting results in the Azure Information Protection client applying generic protection.

These two settings result in the Azure Information Protection client applying generic protection to all files that have a file name extension. If this is your goal, no further configuration is required. However, you can define exceptions for specific file types, so that they are still natively protected. To do this, you must make three additional registry edits for each file type:

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection**: Add a new key that has the name of the file name extension (without the preceding period).

    For example, for files that have a .docx file name extension, create a key named **DOCX**.

2.  In the newly added file type key (for example, **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**), create a new DWORD Value named **AllowPFILEEncryption** that has a value of **0**.

3.  In the newly added file type key (for example, **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**), create a new String Value named **Encryption** that has a value of **Native**.

As a result of these settings, all files are generically protected except files that have a .docx file name extension, which are natively protected by the Azure Information Protection client.

Repeat these three steps for other file types that you want to define as exceptions because they support native protection and you do not want them to be generically protected by the Azure Information Protection client.

You can make similar registry edits for other scenarios by changing the value of the **Encryption** string that supports the following values:

-   **Pfile**: Generic protection

-   **Native**: Native protection

-   **Off**: Block protection

For additional information, see [File API configuration](../develop/file-api-configuration.md) from the developer guidance. In this documentation for developers, generic protection is referred to as "PFile". 

## File types that are excluded from classification and protection by the Azure Information Protection client

To help prevent users from changing files that are critical for computer operations, some file types and folders are automatically excluded from classification and protection. If users try to classify or protect these files, they see a message that they are excluded.

- **Excluded file types**: .lnk, .exe, .com, .cmd, .bat, .dll, .ini, .pst, .sca, .drm, .sys, .cpl, .inf, .drv, .dat, .tmp, .msp, .msi, .pdb, .jar

- **Excluded folders**: 
    - Windows
    - Program Files (\Program Files and \Program Files (x86))
    - \ProgramData 
    - \AppData (for all users)




## Next steps
Now that you've identified the file types supported by the Azure Information Protection client, see the following for additional information that you might need to support this client:

- [Client files and usage logging](client-admin-guide-files-and-logging.md)

- [Document tracking](client-admin-guide-document-tracking.md)

- [PowerShell commands](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
