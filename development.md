# :wrench: Development

Time to make a game!

Here's some tips for doing that.

## :coffee: Code

### Singleton Managers
Any script called [Blank]Manager - ex. GameManager, PlayerManager, LevelManager, AudioManager - should probably use this convenient and safe setup. It allows you to access an instance from anywhere in the project by ensuring that a static reference to a singleton exists at all times.

A singleton pattern is a code pattern designed to ensure only one instance and always one instance of the script are available. These scripts are designed from the ground up to self-police.

```c#
public class GameManager : MonoBehaviour
{
    private static GameManager _instance;

    public static GameManager instance
    {
        get
        {
            if (_instance == null)
            {
                _instance = (GameManager)FindObjectOfType(typeof(GameManager));

                if (_instance == null)
                {
                    Debug.LogError("An instance of " + typeof(GameManager) +
                        " is needed in the scene, but there is none.");
                }
            }

            return _instance;
        }
    }

    public void Awake()
    {

        // Check if instance already exists
        if (_instance == null)
        {
            // If not, set instance to this
            _instance = this;
        }
        // If instance already exists and it's not this:
        else if (_instance != this)
        {
            // Then destroy this. This enforces our singleton pattern.
            Destroy(gameObject);
        }
    }
}
```

### Coroutines

Coroutines are your new best friend. They are the polite cousin of the Update loops bundled with Unity. :two_hearts:  
Coroutines patiently wait durations of time, and will function asynchronously so that if they get held up, the rest of your code will continue to fly by.  
Perfect for sequencing events in cutscenes, or doing large tasks over a dilute period of time.  
You can make a custom loop which only updates every 20 seconds if you wanted to, or simply mimic the Update loop without hurting the buttery smoothness of your Camera transforms! :100:  

As you'll discover, using 'yield return' is one of coroutines' most powerful tools for sequencing and looping. You'll be using lots of 'yield return WaitForSeconds(float)' so it's good to optimize them nicely using the following:  

```c#
// Create a reference to a single public Wait() object for each length of wait time you'll need. 
// Store this refernce in the GameManager script. Accessible through GameManager.instance.myWait.
public WaitForSeconds myWait = new WaitForSeconds(1f);

// Coroutines throughout your project you can call
yield return GameManager.instance.myWait;
// To have the coroutine wait one second.
```
* This will cut down on memory and computation of having multiple parallel "WaitFor's", helping optimization.
* Caching these yields works with WaitForSeconds(), WaitForFixedUpdate() (which waits for the Physics loop Fixed frame), and WaitForNextFrame() (which waits for the next normal Update() frame).

### Enumerators

Forget what we said about coroutines, Enums are going to be your new **bester** friends. 
They're essentially just numbers with names, which means you can make checks more clear and easy to understand.  
Computationally they're just integers (very light), but to your eyes they have nice word-names!  
They should be called Enamerations... Or NameyNums! (<<< Tony came up with these, not me.)  
Avoid checking if an object exists on a layer by converting a string to an int with LayerMask.NameToLayer("GrossString"). Don't use strings for IDing things ever again! use Enums instead!

Here's an example of a perfect utilization - keeping track of the indices of your layers:

```c#
public enum Layer
{
    Default = 0,
    UI = 5,
    Projectile = 8,
    Enemies = 9,
    Environment = 10,
    Gun = 12
}
```
Used as:

```c#
if (gameObject.layer == (int)Layer.Environment) // Oh, it's the Environment layer. Remember to cast to int! (Visual Studio will remind you.)
{
    // Do something.
}
```

Rather than:

```c#
if (gameObject.layer == 10) // What is this???!!!! Might've been clear when you wrote it, but not after 3 months.
{
    // Do something but worse.
}
```
It also has the added bonus that if your layer indexes get shifted, you only have to modify the Enumerator's definitions, and not every occurance throughout the project. Yay!

### Worthwhile Resources

* [Polymorphism](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/polymorphism)  
* [Delegates](https://unity3d.com/learn/tutorials/topics/scripting/delegates)  
* [Asynchronus tasks + Coroutines](https://docs.unity3d.com/Manual/Coroutines.html)

## :game_die: Unity

### Unity Timesavers
* Use Shift + Spacebar to quickly toggle fullscreening of any Unity window/panel.
* If you want to keep one GameObject or Asset active in the inspector while being able to select other objects in the hierarchy, press the tiny dark grey padlock icon at the extreme top-right of the Inspector panel.


### Reference IDs

There are a couple ways to keep track of objects and scripts. They both piggyback on one of Unity's **most powerful** features - reference IDs. These are basically hashed codes (a bunch of gibberish) like `bd966ac2849d6f3488fa20b0ae654ce5` which Unity has a look-up database keeping track of where they are in the hierarchy. In essence Unity has a big spreadsheet with every known reference ID, and where they are at all times. Each file within the Assets folder has an associated .meta file.

The two most-used ways of finding references are as follows:

1. Drag-and-dropping references into public variables in the inspector before runtime.
2. Getting references in runtime through code using `GetComponent<Component>`, `GameObject.Find("Object")` and other such methods.

Basically, directly dragging references into the inspector saves on computation in run-time, making loads faster, but it also risks us losing our references from a metadata issue - Git related or otherwise. It's essentially entrusting prefabs that they will not forget all its reference IDs, and entrusting each .meta file in the project not to change, or at least to 'ping' Unity's database to let them know they're changing their number. Unity is usually pretty good about this, and a changed .meta file will go "Hey I got a new phone my number is 6e2559ca1e833764ebdbdfebcc9ee23c."

The alternative to pre-referenced references is using `GetComponent<Component>()` or `GameObject.Find()`, but the downside is that this can accumulate into major performance issues in loadtime and runtime. Depending on the number of scripts and objects being located, it can be an invisible overhead, or a game-shattering hangup/stutter.

**My solution** is to use a little Editor-side scripting to get the best of both worlds. It goes as follows:

1. Make a public reference in your class (MyClass), using the drag-and-drop in the inspector. We will rely on Unity's reference ID system for the high performance it provides.
2. Make a new script and class (MyPopulator) with the tag `[ExecuteInEditMode]` before the class block.
2. In MyPopulator, we will put `#if UNITY_EDITOR`to start a block of editor-specific code.
3. Put `if (myClass.myReference == null) { /* Find reference of MyClass using Find() or GetComponent() */ }` within the `UNITY_EDITOR` block.
4. Then any time you notice your dragged references have lost their connection, disable and re-enable your MyPopulator script and it should repopulate the references using various `GetComponent<Component>()` and `GameObject.Find("Object")` calls.
5. Because nothing in the `UNITY_EDITOR` block will compile in builds, you don't have to worry about expensive Find methods slowing down your build.

Example code snippet (untested):

MyClass.cs
```c#
public class MyClass {

    // Pre-assigned in inspector.
    public GameObject playerObject;
    public Player playerScript;
    
    private void Start() {
        
        // Hopefully these aren't null!
        playerObject.transform.position = banana.transform.position;
        playerScript.EatBanana(ravenously);
    }

}
```

MyPopulator.cs
```c#
[ExecuteInEditMode]
public class MyPopulator {

    
    private void OnEnable() // Disabling and re-enabling this script in the inspector will call this.
    {
#if UNITY_EDITOR
        MyClass instance = GetComponent<MyClass>(); // In this case I assume these two scripts are on the same GameObject.
        if (instance.playerObject == null) instance.playerObject = GameObject.FindGameObjectWithTag("Player");
        if (instance.playerScript == null) instance.playerScript = instance.playerObject.GetComponent<Player>();
#endif
    
    }
}
```


### Know the Costs of Unity Methods
Examples:
* GameObject.Find() - This thing basically scans your whole game world until it finds something. Lots of unnecessary and clunky computation which bogs down your game.
* GetComponent() - It's really hard not to use this, and sometimes it's the best option. You might consider making a public reference and dragging it into the script via the Inspector panel. This will make it load the component reference it needs BEFORE runtime, without needing to 'search'.
* RayCasting - Raycasting is indeed wonderful especially for AR swipe and tap input, but in large volumes or frequencies, it will be one of the heaviest operations in your game. Use sparingly, have a [short length, and mask your collision layers.](https://docs.unity3d.com/ScriptReference/Physics.Raycast.html)
* Instantiate() - very expensive, so load them at startup, and keep them inactive or hidden until they need to be used. Recycle them, and only spawn the max that will ever conceivably be on-screen.

### Take Update Loops Seriously
* Keep Update() free of anything not related to Input or Camera movement
* Updating visual elements within FixedUpdate() or similar loops (custom fixed-frame coroutines) will introduce noticable judder. This is because the Fixed Framerate uses a lower refresh rate. This is modifiable so it's equal to the target visual framerate, but since Update varies depending on performance, there is no guarantee FixedUpdate and Update will sync up.
* Input events which are done outside of Update() will often not register or will have noticable lag, which is :thumbsdown:
* Offload as many functions as possible into less-frequently-updated asynchronous loops. For instance, checking for new hardware on the system can be done every 2 seconds instead of every frame 

## :space_invader: Game Design

As a developer in a small company like Virtro, you'll often have to make calls about design decisions when Steven is away for lunch. The basics of game design are more-or-less as follows:

### The Basics of Fun

1. Games are greater than the sum of their parts. 
    * If something isn't feeling good, add sound, animation principles, visual polish, agency, responsiveness, cinematography, tone, etc...
    * Good game developers can use the full spectrum of the medium to add flare and satisfaction to a part of a game.
    * GREAT game developers can make something look and feel good using only a couple of the aforementioned components.
2. Player input needs to be responsive.
    * It needs have have punch and it needs to feel good. 
    * If you need to slow the responsiveness of something down, use [animation principles](https://en.wikipedia.org/wiki/12_basic_principles_of_animation) to give it physicality. 
    * Dark Souls does this really well. Attacks don't happen instantly, but have anticipation, windup, followthrough, and there is a noticable secondary impact motion on the enemies which helps communicate your power.
3. Design toward an experience. Design by subtraction.
    * Everything in your game should bring it closer to a particular experiential aesthetic. Decide on that aesthetic early, and tailor EVERYTHING towards it.
    * Often the best way to make something better is to take something out of it. We make assumptions constantly about what 'should' be in a game. In the example of Zombie Donuts we let the player move around the environment, and due to the limitations of the Gear VR players didn't like the control scheme and felt sick because of it. Players had more fun by standing still.
    * If you want a great example of design by subtraction take a look at one of my favourite game designers of all time - Fumito Ueda's [Shadow of the Colossus](http://www.thesaint-online.com/2017/03/fumito-ueda-design-by-subtraction/) and [Ico.](https://www.youtube.com/watch?v=AmSBIyT0ih0)
4. Fuck tutorials.
    * If you can make a game entirely without tutorials, do it. 
    * In addition to forcing you to make a terrible bastardization of your gameplay loop, players hate them. 
    * Players hate reading, feeling patronized, and having the discovery of mechanics spoiled for them.
5. Teach the player without them noticing.
    * Use light or colour :rainbow: to guide the eye to important gameplay elements. 
    * Use sound to cue the player to look in a direction. Use framing to focus the player on important elements. 
    * Use visual weight (notice how the rainbow emoji draws your eye because it has a bolder visual presence than the rest of the text) to draw attention. 
    * Force the player using psychology to teach themselves how to play the game. It's hard but when it's done right it's phenomenal.

### XR-Specific
1. Make interactions kinetic! (Give them physicality and weight.)
    * Have the player directly influence items in the game world or on the phone screen. 
    * Don't rely on buttons and floating UI.
2. Avoid unmotivated movement, perspective shifts of any sort, and even movement in general if you can.
3. Make intuitive or charming environmental interactions instead of buttons. 
    * Ex. Toggle the music by having the player shoot a jukebox.

If you must do movement, try some of the following options:

1. Fade/blink to an indicated location.
2. **Slow** movement using conventional control schemes. Must be a decent controller.
3. Constant and linear movement. (See Run Dorothy Run)
4. Deliberate physical movement.
    * Using motion controllers to swim or push off objects in space. 
    * Needs to be tuned to feel physically true-to-life, make sure there are no physics glitches that will make you instantly barf. :mask: