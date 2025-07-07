---
title: Extracting google earth data.
date: 2025-07-07
categories: journey
---
## Journey
I needed the model of our city for a new game. After some research, I found out that best way to do this is using RenderDoc program, it is made by Baldur Karlsson.

Going through many versions of RenderDoc, Blender and browsers, I found exact versions and browser that work for me. I am making this tutorial for same versions that worked for me.
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

 ![creation of shortcut]({{site.baseurl}}/assets/images/create_shortcut.png)
 
And paste location from up above:

 ![creation of shortcut]({{site.baseurl}}/assets/images/shortcut_location.png)
 ![creation of shortcut]({{site.baseurl}}/assets/images/shortcut_name.png)

> If you made shortcut this way, it is going to have icon of cmd.exe.
> If you make shortcut from microsoft edge exe file, and edit its properties, it is going to have microsft edge icon. Not relevant to our objective, but so you don't get confused by the icon. 

### 2. Open RenderDoc, do the setup
First, we need to enable process injection.

You are going to do this by going to tools and settings:

 ![creation of shortcut]({{site.baseurl}}/assets/images/renderdoc_settings.png)

Check this option on general tab:

 ![creation of shortcut]({{site.baseurl}}/assets/images/renderdoc_injection.png)

**And restart the program**
### 3. Injection to Microsoft Edge process

Open you microsoft edge shortcut:

 ![creation of shortcut]({{site.baseurl}}/assets/images/edge_icon.png)

And you are going to get white window, alongside small window with some number:

 ![creation of shortcut]({{site.baseurl}}/assets/images/edge_popup.png)

Dont close it, yet.

Go back to RenderDoc and go to File, Inject to process

 ![creation of shortcut]({{site.baseurl}}/assets/images/renderdoc_injectWindow.png)

In the filter box type your number (pid) you got eariler from opening microsoft edge, click refresh:

 ![creation of shortcut]({{site.baseurl}}/assets/images/renderdoc_injectWindow2.png)
Select msedge.exe with your number (pid), Correct Window Title is Microsoft Edge Gpu.

Click the inject button:

 ![creation of shortcut]({{site.baseurl}}/assets/images/renderdoc_injectButton.png)

You can now close small microsoft edge popup from earlier.
### 4. Choosing location

In your previously opened Microsoft Edge, open google earth:

[https://earth.google.com/](https://earth.google.com/)


Pick your location and move to it.

For this example we are goint to Zürich, Switzerland:

![zurich picture]({{site.baseurl}}/assets/images/zurich.png)

In my experience, closer you zoom in, more details you get. But you will get less area in your extracted model.

After some research, I found out a little trick for getting more details without zooming so much, so you can get more area:
	When using Microsoft Edge, you can click three dots in top right corner, and set zoom to 25%. This will load more details, like when you get closer.

### 5. Extracting 3d data

Go back to RenderDoc, and you will see this section:

![capture options]({{site.baseurl}}/assets/images/capture_options.png)

There is multiple ways to capture data using RenderDoc. In my experience most reliable way is to use "Trigger after delay option". Set it to 5-10 seconds (More if you need more time).

You are going to click "Trigger after delay" button, and capture will happen after amount of time that is previously set.

Click the button and switch window to Microsoft Edge, after previously set time passed, you can switch window back to RenderDoc. You will see capture, looking simillar to this:

![capture example]({{site.baseurl}}/assets/images/capture_example.png)

If your file is a lot smaller size, there is possibility that there is no actual 3d (polygon) data. In my experience it happens sometimes, **but you can try moving your map after clicking "Trigger after delay", and stopping before actual capture happens.**

> Previously to realizing that capture can happen without catching 3d data, I tought problem was in this combination of program versions. I tought there was problem in this version of RenderDoc. After that I tought problem was in MapsModelsImporter or Blender version, because I get error when importing capture to Blender. But sometimes, capture doesn't contain important part of data. (When file size is too small, that can give you a hint). Also you can use Texture Viewer tab to be sure, but that is a little bit more advanced.

### 6. Saving capture to computer
Right click on your capture, and click save:

![capture save]({{site.baseurl}}/assets/images/capture_save.png)

Save it to folder of your choice. (I am not sure if specific file location can be problematic for blender extention accessing file). File extension will be **.rdc**

### 7. Installing Blender add-on

Open Blender that you previously installed, and open new empty general file.

Find edit section and click "Preferences"

![edit preference]({{site.baseurl}}/assets/images/edit_pref.png)

Click on add-ons section on the left side of newly opened window. After that, click install button on top right of the window.

![addon install]({{site.baseurl}}/assets/images/addon_install.png)

Find your MapsModelsImporter download, it should have **.zip** extension. Click install add-on.

![addon downloaded]({{site.baseurl}}/assets/images/addon_downloaded.png)

To easier find you newly installed add-on in Blender, you can use search option.

Activate add-on by clicking on checkbox.

![addon check]({{site.baseurl}}/assets/images/addon_check.png)

You have now installed add-on. You can close "Preferences window".
#### Footnotes
---
[^1]: You can download exact version of RenderDoc from their website:
	
	[https://renderdoc.org/builds](https://renderdoc.org/builds)
	
	Or you can use direct link from their website (1.19 64bit)
	
	[https://renderdoc.org/stable/1.19/RenderDoc_1.19_64.msi](https://renderdoc.org/stable/1.19/RenderDoc_1.19_64.msi)
	
	You can also use portable version of this program

[^2]: You can download exact version of Blender from their website:
	
	[https://download.blender.org/release/](https://download.blender.org/release/)
	
	Or you can use direct link from their website (2.93.0)
	
	[https://download.blender.org/release/Blender2.93/](https://download.blender.org/release/Blender2.93/)
	
	You will need this on Windows 64 bit system:
	
	**blender-2.93.0-windows-x64.msi**

[^3]: You can download exact Microsoft Edge version on bottom of this page:
	
	[https://www.microsoft.com/en-us/edge/business/download?form=MA13FJ](https://www.microsoft.com/en-us/edge/business/download?form=MA13FJ)
	
	Version used is the latest version at the moment I am writing at, and it is the version that worked. There is possibility that version of Microsoft Edge is not important.
	
	Previously I tried using Google Chrome, but it didn't work.

