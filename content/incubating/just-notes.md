---
title: "Mini Notes"
date: 2020-09-09T15:00:18-07:00
weight: 10
---

#### Looking for Screen Capture

Python - PIL - ImageGrab.py
  * On Darwin, invokes `screencapture` utility (`screencapture -x filename.bmp`) (`x` is do not play sound.)
  * On windows, invokes `PyImaging_GrabScreenWin32`, which is in .../Pillow/src/Tk/displays.c
    * Does `CreateCompatibleDC`, and all those ilk.
  * PIL Docs:  https://pillow.readthedocs.io/en/2.9.0/index.html

AutoHotKey
  * Search in AHK code for 'Screen' - you will find things like GetScreenDPI(), which is part of it.
  * .../source/globaldata.cpp
  * https://github.com/Lexikos/AutoHotkey_L
  * Apparently, the above fn quit working in Win8, so use implementation from Linear Spoon:
    * https://autohotkey.com/board/topic/121619-screencaptureahk-broken-capturescreen-function-win-81-x64/

From a 2020 Article on 6 OpenSource RPA tools. (https://enterprisersproject.com/article/2020/4/rpa-robotic-process-automation-6-open-source-tools)
  * TagUI: https://github.com/kelaberetiv/TagUI
  * RPA for Python (was TagUI for Python): https://github.com/tebelorg/RPA-Python
  * Robocorp: https://robocorp.com/
  * Robot Framework: https://github.com/robotframework/robotframework , http://robotframework.org/
  * Automagica (freemium): https://github.com/automagica/automagica , https://automagica.com/
  * Taskt: https://github.com/saucepleez/taskt , http://www.taskt.net/

GoLang

#### Other Possibilities

Python
* https://pypi.org/project/pyscreenshot/

C#
* https://github.com/gavinkendall/autoscreen

Java
* https://sourceforge.net/projects/capturedit/
* https://sourceforge.net/projects/jscreenrecorder/
* https://github.com/amiraslanaslani/java-screen-capture
  * Uses AWT, like the snippet below. Is used by nodejs-screen-capture

Nodejs
* https://github.com/soulehshaikh99/win-screenshot
* https://github.com/amiraslanaslani/node-screen-capture
* https://www.npmjs.com/package/screenshot-desktop
* https://github.com/uiur/node-screencapture

PowerShell
* https://gallery.technet.microsoft.com/scriptcenter/eeff544a-f690-4f6b-a586-11eea6fc5eb8




#### Examples

* PIL.ImageGrab.grab():
  * https://www.programcreek.com/python/example/89032/PIL.ImageGrab.grab
* Code Bullet: Storm-the-house-auto-clicker
  * https://github.com/Code-Bullet/Storm-The-House-Auto-Clicker


#### Source for Others

From https://github.com/siyanda-zama/java-ScreenShot

```java
import java.awt.AWTException;
import java.awt.Rectangle;
import java.awt.Robot;
import java.awt.Toolkit;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;
import javax.imageio.ImageIO;

public class ScreenshotExample
{
	public static void main(String[] args)
	{
		try
		{
			Robot robot = new Robot();
			Rectangle rectangle = new Rectangle(Toolkit.getDefaultToolkit().getScreenSize());
			BufferedImage bufferedImage = robot.createScreenCapture(rectangle);
			File file=new File("screenshot.png");
			boolean status = ImageIO.write(bufferedImage, "png",file);
			System.out.println("Screenshot captured!" + status + "File path: "+file.getAbsolutePath());
		}
		catch(AWTException | IOException ex)
		{
			System.out.println(ex.toString());
		}
	}
}
```

