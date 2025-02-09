## Overview

When creating a CVM, you can configure an instance by specifying **custom data**. During the **first launch** of the CVM, the custom data will be passed into the CVM in text format and be executed. If you purchase multiple CVMs at a time, the custom data text will be executed on all CVMs during their first launch.

This document describes an example in which a PowerShell script is passed during the first launch of a Windows CVM.

## Supports and Limits

- Windows operating systems that support custom data include:
 - Windows Server 2019 IDC 64-bit Chinese/English version
 - Windows Server 2016 IDC 64-bit Chinese/English version
 - Windows Server 2012 R2 IDC 64-bit Chinese/English version
- A command can be executed by passing text only when a CVM is launched for the first time.
- Before Base64 encoding, the size of the custom data cannot exceed 16 KB.
- Custom data is Base64 encoded and then passed. If you directly copy a non-Base64 script file, do not select “The entry is Base64-encoded text”.
- During launch, executing specified tasks in custom data will increase the amount of time it takes to launch the CVM. We recommend that you wait for a few minutes, and after the tasks are completed, test whether the tasks have been successfully executed.
- In this example, specify the Windows PowerShell script by using the PowerShell label, for example, the &lt;powershell&gt;&lt;/powershell&gt; label.

## Directions

### Preparing text

Prepare text based on your actual requirements:


#### PowerShell script[](id:PowerShellScript)
Use the PowerShell label to prepare a PowerShell script.
For example, if you need to create a “tencentcloud.txt” file with the content of “Hello Tencent Cloud.” in the C drive (C:), use the PowerShell label to prepare the following content:
```shell
<powershell>
"Hello Tencent Cloud." | Out-File  C:\tencentcloud.txt
</powershell>
```


#### Base64 encoded script[](id:Base64Script)

1. Run the following command to create a PowerShell script named “script_text.ps1”.
```shell
vi script_text.ps1
```
2. Press **i** to switch to the editing mode, refer to the following content, write it into the file, and save the “script_text.ps1” script.
```shell
<powershell>
"Hello Tencent Cloud." | Out-File  C:\tencentcloud.txt
</powershell>
```
3. Run the following command to perform the Base64 encoding operation on the “script_text.ps1” script.
```shell
base64 script_text.ps1
```
The following information is returned:
```shell
PHBvd2Vyc2hlbGw+CiJIZWxsbyBUZW5jZW50IENsb3VkLiIgfCBPdXQtRmlsZSAgQzpcdGVuY2VudGNsb3VkLnR4dAo8L3Bvd2Vyc2hlbGw+Cg==
```

### Passing text

We provide multiple methods to launch an instance, and here we introduce two of them. Choose a method according to your requirements:

<dx-tabs>
::: Console[](id:Consoletrans)

1. Refer to [Creating an Instance](https://intl.cloud.tencent.com/document/product/213/4855) to purchase an instance, and click **Advanced settings** in **2. Complete configuration**.
![](https://qcloudimg.tencent-cloud.cn/raw/283fb3e0e1400d4ba5725c8b6a1ea279.png)
2. In **Advanced settings**, enter the text content you have prepared in the **Custom data** text box.
 - PowerShell script: Directly enter [PowerShell script](#PowerShellScript).
 - Base64 encoded script: First select “The entry is Base64-encoded text”, and enter [Base64 encoded text](#Base64Script).
 ![](https://main.qcloudimg.com/raw/0b6b594f174568ca7d3312821c0571ed.png)
3. Follow the prompts on the interface to complete CVM creation.
:::
::: API[](id:APItrans)
When creating a CVM by using API, you can pass the text by assigning the value of the encoded result returned in [Base64 encoded script](#Base64Script) to the UserData parameter of the RunInstances API.
The following is an sample CVM creation request with UserData:
```shell
https://cvm.tencentcloudapi.com/?Action=RunInstances
&Version=2017-03-12
&Placement.Zone=ap-guangzhou-2
&ImageId=img-pmqg1cw7
&UserData=PHBvd2Vyc2hlbGw+CiJIZWxsbyBUZW5jZW50IENsb3VkLiIgfCBPdXQtRmlsZSAuXHRlbmNlbnRjbG91ZC50go=
&<Common Request Parameters>
```
:::
</dx-tabs>



### Verifying custom data configuration

1. Log in to your CVM.
2. On the operating system interface, open the C drive (C:\), and check whether the `tencentcloud.txt` text file exists.
If the `tencentcloud.txt` text file exists, the configuration is successful, as shown in the following figure:
![](https://main.qcloudimg.com/raw/9f94ec922111734a489b9730d66168c3.png)


### Viewing execution logs
You can view the `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\log\cloudbase-init.log` file to get the execution logs of the script.

