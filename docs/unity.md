#### [< Back to Index](readme.md)

# :game_die: Unity

And here we have it - one of the biggest driving forces behind the industry and especially the indiestry.

The indiestry, or indies-try - so-called because *unlike many big companies, we try* - is the most exciting place to be in games, and also the most dangerous.

So let's jump in and talk about why Unity is pretty revolutionary.

## :octopus: What Makes Unity Great

Unity is an Octopus. It is fast, fits into any project, has a surprising amount of power, and a surprising amount of legs. It's also approachable as hell, just like an Octopus, which is definitely approachable.

I'd boil it down into 3 parts, each with many justifications:

1. Flexibility
    1. Full support for 2D and 3D systems/visuals.
    2. Deep support for animation systems.
    3. Good and approachable support for audio and mixing.
    4. Active community which can solve anything you throw at them.
    5. Incredible native physics engine framework.
    6. In-engine support for NVidia's shader language [CG](shaders.md)
    7. Great native support for file types of all sorts.
    8. Modularity and customizability of the Editor.
2. Accessibility
    1. It's easy to learn.
    2. Well documented.
    3. It's surprisingly fun?
    4. It has a nice collaboration feature for small teams!
    5. It's decently priced if you ever want to upgrade it.
3. An Infernal and Increasing Storm of Power on The Horizon
    1. It has steadily been attaining a frankly scary amount of power for how much flexibility it has.
    2. Watching the Unity Engine development is like watching the fires of Mordor kindle.
    3. Presently it can render nearly [movie-ready computer graphics in real time](https://www.youtube.com/watch?v=5cvi4TVkUdU) on a good computer.
    4. Its balance of relative logical and graphical efficiency means it can compete with engines like Unreal.

### Live Updates

Let me start by saying **only make changes out of Play Mode**, with *few exceptions.* All changes will be lost upon un-hitting the play button. You can experiment with values, on the fly, but you don't want try to make permanent changes in Play Mode.

I just saved you a couple hours. Most common mistake in the book.

I actually recommend going into `Edit > Preferences` and giving the editor a colour overlay when you're in play more, to give you a visual reminder.

But this leads right into one of the most powerful parts of Unity, its ability to test your game directly within the editor. Perfect for blazingly fast iterative testing, and you actually have room to experiment during the gameplay. 

You have two views of your game world:

**The Game View**

This one just acts as a porthole into what the player is going to see. You can even play the game from this window. If you have multiple cameras in the scene, the one in Game View will be the camera tagged "Main Camera".

**The Scene View**

This camera is a perspective-flexible developer camera which can be used both in Play and Editor mode. It can see debug lines you may be casting, invisible to the player. It shows developer icons for game objects and components, and has a bunch of rendering modes which help you visualize wireframes, UVs, lightmaps, overdraws, and other weird technical stuff.

### Inspector Gadget

(Coming Soon) Everything you need to know about the Inspector.

### The Profiler

(Coming Soon) A light introduction to a powerful advanced tool. Consider this an entry to optimization.

### Reference IDs

There are a couple ways to keep track of objects and scripts. They both piggyback on one of Unity's **most powerful** features - reference IDs. These are basically hashed codes (a bunch of gibberish) like `bd966ac2849d6f3488fa20b0ae654ce5` which Unity has a look-up database keeping track of where they are in the hierarchy. In essence Unity has a big spreadsheet with every known reference ID, and where they are at all times. Each file within the Assets folder has an associated .meta file.

The two most-used ways of finding references are as follows:

1. Drag-and-dropping references into public variables in the inspector before runtime.
2. Getting references in runtime through code using `GetComponent<Component>`, `GameObject.Find("Object")` and other such methods.

Basically, directly dragging references into the inspector saves on computation in run-time, making loads faster, but it also risks us losing our references from a metadata issue - Git related or otherwise. It's essentially entrusting prefabs that they will not forget all its reference IDs, and entrusting each .meta file in the project not to change, or at least to 'ping' Unity's database to let them know they're changing their number. Unity is usually pretty good about this, and a changed .meta file will typically go *"Hey I got a new phone my number is 6e2559ca1e833764ebdbdfebcc9ee23c."*

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
### Multiplatform as Hell

(Coming Soon) Unity can make things for most big devices and OS's.

#### [< Back to Index](readme.md)

## :violin: Best Practices

Here's just some pro tips relating to the specifics Unity provides. Things to save time, or things to watch out for.

### Know the Costs of Unity Methods
Examples:
* `GameObject.Find()` - This thing basically scans your whole game world until it finds something. Lots of unnecessary and clunky computation which bogs down your game.
* `GetComponent()` - It's really hard not to use this, and sometimes it's the best option. You might consider making a public reference and dragging it into the script via the Inspector panel. This will make it load the component reference it needs BEFORE runtime, without needing to 'search'.
* RayCasting - Raycasting is indeed wonderful especially for AR swipe and tap input, but in large volumes or frequencies, it will be one of the heaviest operations in your game. Use sparingly, have a [short length, and mask your collision layers.](https://docs.unity3d.com/ScriptReference/Physics.Raycast.html)
* `Instantiate()` - very expensive, so load them at startup, and keep them inactive or hidden until they need to be used. Recycle them, and only spawn the max that will ever conceivably be on-screen.

### Take Update Loops Seriously
* Keep `Update()` free of anything not related to Input or Camera movement
* Updating visual elements within `FixedUpdate()` or similar loops (custom fixed-frame coroutines) will introduce noticable judder. This is because the Fixed Framerate uses a lower refresh rate. This is modifiable so it's equal to the target visual framerate, but since Update varies depending on performance, there is no guarantee FixedUpdate and Update will sync up.
* Input events which are done outside of `Update()` will often not register or will have noticable lag, which is :thumbsdown:
* Offload as many functions as possible into less-frequently-updated asynchronous loops. For instance, checking for new hardware on the system can be done every 2 seconds instead of every frame 

### Unity Timesavers
* Use Shift + Spacebar to quickly toggle fullscreening of any Unity window/panel.
* If you want to keep one GameObject or Asset active in the inspector while being able to select other objects in the hierarchy, press the tiny dark grey padlock icon at the extreme top-right of the Inspector panel.

#### [< Back to Index](readme.md)
