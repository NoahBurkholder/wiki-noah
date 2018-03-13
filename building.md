# :factory: Building

## The Basics

### Version Number Rules

You'll typically want to use the format ```A:B:C``` where A is the 'Major Release' number, B is the "Minor Release' number and C is the 'Build' number.

* A will start at 0, and will be incremented by 1 every time you have a build which is ready to be sent off to the store.
* B will start at 0, and will be incremented by 1 every time you reach a milestone in the development process (ie a big new feature is fully implemeneted, or a patch for an existing release is uploaded to the store).
* C will start at 1, and will be incremented by 1 every time you build (after #2 rolls over, this will start at 0)

Note: The build number can never exceed 99 (you'll see why below) so if it ever gets that high, just roll over the Minor Release number.

So some example versions are:

```
0.0.1 - First ever build
0.1.0 - First build which contains all the core gameplay
0.2.3 - Third build after implementing a cool new game changing feature
1.0.0 - First build ready to be sent off to the app store
1.0.1 - First build working on a patch for the initital release
1.1.0 - First patch applied to game
```

### Bundle Version Code Rules

All Bundle Version Codes are just integers for computers to be able to check quickly which is higher, and so which should be installed (higher bundle code = newer build file).

We get our Bundle Version Code number by manipulating the Version Number following the rule below:

```
(Major Release * 10,000) + (Minor Release * 100) + Build Number
```
Which might seem complicated but isn't.  
Examples: 
```
0.0.1 = 1
0.2.3 = 203
1.0.2 = 10002
2.3.54 = 20354
```

## The Output

### What files in my `Project/Assets` folder are included in my build?
Aka. 'So, you built your Tetris clone, and the file size is 1.6Gb (!?)'

Here's the hard and fast rule for what files get included in your builds:

1. **All scripts are included.**
2. Any asset which has a [referenced ID](README.md#referencing-gameobjects-and-components) in the project.
3. Any asset which is located in the `Assets/Resources` folder. (These are included but **not pre-loaded** on startup.)
4. Any asset which is located in the `Assets/StreamingAssets` folder. (These are included **and pre-loaded** on startup.)

Hopefully your Tetris clone is back down to 2Mb. (Or it would be if an empty Unity project wasn't already 40Mb.)

## Building for Android

Your inital development builds can be done without any extra steps, but once you want to release the game you'll need a keystore and key. [To attain these follow this guide.](http://www.technoreply.com/creating-an-android-keystore-on-unity/)

Then once you have your keystore set up, do the following:

1. When you build for release go to 'Publishing Settings' in the Player Settings panel  
2. Check 'Use existing keystore' and then click 'browse for keystore'.
3. When you find and select it, type *the password* for it.
4. Under the 'Key' heading select 'Create new key' from the 'Alias' dropdown and create a new key within that dialog.

### Android Builds Require OSIG Files

In order to be able to run an .apk file on your phone, you must first include a special developer-device-specific OSIG file in your project.

The official guide for obtaining these signature files is found [right here.](https://developer.oculus.com/documentation/mobilesdk/latest/concepts/mobile-submission-sig-file/)

Once you've made your OSIG files, the location for these files must be the `Assets/Plugins/Android/Assets` folder which is automatically included if you downloaded the 'Oculus Integration' asset from the Asset Store, or downloaded the equivalent APIs directly from Oculus.

`Important Note: If you want to show a colleague your game on their device, you will need to obtain a similar OSIG for their exact phone.`

### Identification and Package Names

Under the 'Other Settings' section fo the player settings panel you can find the 'Package Name' field. This should look roughly like: `ca.company.nameofgame` or `com.company.nameofgame` depending on if you want to be Canadian. Changing this will functionally change the current app ID, so you'll be installing a second app on the phone instead of merely updating it.

### Version Numbers and Bundle Versions Codes

Under the 'Other Settings' section of the player settings panel, you can find the 'Version' and 'Bundle Version Code' fields.  
These help keep track of which builds are most recent, and so no two builds should ever have the same ones.  
ie. every time you're about to build, increment them!

The Versions numbers are the human readable numbers which track versions for *us*. The bundle version codes however are for machines. They tell whether the build file their trying to install should overwrite a version of the game they already have installed,  
or if this is an older version of the game which they should ignore.

