---
title: Extracting google earth data.
date: 2025-07-07
categories: journey
---
## Journey
I needed the model of our city for a new game. After some research, I found out that best way to do this is using RenderDoc program, it is made by Baldur Karlsson.

Going through many versions of RenderDoc, Blender and browsers, I found exact versions and browser that work.
## Requirements
To extract 3d data we are going to need following:
- RenderDoc v1.19[^1]
- Blender v2.93.0[^2]
- Microsoft edge v138.0.3351.65[^3]
## Steps
### 1. Create microsoft edge shortcut
You need to make shortcut of microsoft edge with some specific parameters, we are going to assume you have microsoft edge on default windows location:

```bash
C:\Windows\System32\cmd.exe /c "SET RENDERDOC_HOOK_EGL=0 && START "" ^"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe^" --disable-gpu-sandbox --disable_direct_composition=1 --gpu-startup-dialog"
```

You can do this by creating shortcut on you desktop:

 ![creation of shortcut]({site.baseurl}/assets/images/create_shortcut.png)
 
And paste location from up above:
![[Pasted image 20250707210744.png]]
![[Pasted image 20250707211304.png]]

> [!NOTE]
> If you made shortcut this way, it is going to have icon of cmd.exe.
> If you make shortcut from microsoft edge exe file, and edit its properties, it is going to have microsft edge icon. Not relevant to our objective, but so you don't get confused by the icon. 

### 2. Open RenderDoc, setup it
First, we need to enable process injection.
You are going to do this by going to tools and settings:
![[Pasted image 20250707211816.png]]
Check this option on general tab:
![[Pasted image 20250707211845.png]]
**And restart the program**
### 3. Injection to Microsoft Edge process
Open you microsoft edge shortcut:
![[Pasted image 20250707212035.png]]

And you are going to get white windows, alongside small window with some number:
![[Pasted image 20250707212128.png]]
Dont close it, yet.

Go back to RenderDoc and go to File, Inject to process
![[Pasted image 20250707212350.png]]

In the filter box type your number (pid) you got eariler from opening microsoft edge, click refresh:
![[Pasted image 20250707212430.png]]
Select msedge.exe with your number (pid), Correct Window Title is Microsoft Edge Gpu.

Click the inject button:
![[Pasted image 20250707213100.png]]

You can now close small microsoft edge popup from earlier.
### 4. Extracting google earth data
yey

[^1]: You can download exact version of RenderDoc from their website:
	[https://renderdoc.org/builds](https://renderdoc.org/builds)
	
	Or you can use direct link from their website (1.19 64bit)
	
	https://renderdoc.org/stable/1.19/RenderDoc_1.19_64.msi
	
	You can also use portable version of this program

[^2]: You can download exact version of blender from their website:
	https://download.blender.org/release/
	Or you can use direct link from their website (2.93.0)
	https://download.blender.org/release/Blender2.93/
	You will need this on windows 64 bit system:
	**blender-2.93.0-windows-x64.msi**

[^3]: You can download exact microsoft edge version on bottom of this page:
	https://www.microsoft.com/en-us/edge/business/download?form=MA13FJ
	This is the latest version at the moment I am writing at, and it is the version that worked. There is possibilty that version of microsoft edge is not important.
	
	Previously I tried using google chrome, but it didn't work.

