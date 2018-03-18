# Screenshots

* Import ScreenshotScripts.unitypackage (Ico / Util C# Scripts) into your project

## Basic Screenshots

* Set the dimensions of your game window to the dimensions required by the store you are uploading to

```
Google Play Store    : 3840 x 2160
Google Daydream Apps : 3840 x 2160
Appple App Store     :
Oculus (Rift/Gear)   :
Steam Store (Vive)   : 
Sony Playstation VR  :
```
* Open the screenshot tool under the 'Tools' menu
* Stage shots by pausing the game and manually moving things around the scene
* When you have a good frame, press the Take Screenshot button!

## 360 Screenshots

* These only work in Unity version ***2018.1.0b7*** and later
* Attach the Capture360Sphere script to the main camera in your scene
* In the inspector on the script set the filename to whatever you want (**DON'T** include an extension)
* Create a custom Render Texture with dimension = cube, 4096x4096 and drag it into the script in the inspector (cubemap)
* Create a render texture with dimension = 2d, 4096x4096 and drag it into the script in the inspector (equirect)
* Wherever you handle player input in your game, add a check for some keypress, and have that check call the method

```c#
//For example: 
if (Input.GetButtonDown("s"))
{
    Capture360Sphere.CaptureSphere();
}
```
* Play your game in the editor, and when ever you're ready you can press your key to capture a 360 photo!
** NOTE : it seems to always crash whem you try to take a second one, so be careful!

