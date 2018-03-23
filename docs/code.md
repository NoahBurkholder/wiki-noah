#### [< Back to Index](readme.md)

# :coffee: Code

Unlike hard computer-science software utility development, game programming is oddly creative, and is greatly unprecedented. You will constantly run into challenges which don't have a concrete answer.

You don't need to know much math. You don't need to know crazy algorithms. You don't need to know system architectures. It's mostly just creative problem-solving and creative problem-creating.

The aim of this page isn't to teach the basics. This is relatively advanced techniques for making highly efficient code. **If you can use these, you can already compete with the majority of game developer professionals I know.**

# :notes: C#

This is what every game programmer I know unquestionably uses. Even if they have other favourite languages, this is the standard.

Writing in C# in Unity is a lot like writing music with musical scores. It is a technical expression of typically pretty creative expressions. It is a toolset which looks and operates objectively, but is used (at least in our context) to solve subjective things.

It's basically Java but a little less confusingly arbitrary and noisy. It also is developed by Microsoft so it has amazing integration with Windows. Very easy to interface with the OS.

Great language! It's an almost impossible balance of stability, compatibility, understandability, and efficiency. Perfect for game programming. It's the default for most game developers of this age.

Any Unity code snippets you find online will probably use C# as the basis.

Anyways - on to some useful structures in C#:

## Singleton Managers

A singleton pattern is a code pattern designed to ensure only one instance and always one instance of the script are available. These scripts are designed from the ground up to self-police.

Any script called [Blank]Manager - ex. GameManager, PlayerManager, LevelManager, AudioManager - should probably use this convenient and safe setup. It allows you to access an instance from anywhere in the project by ensuring that a static reference to a singleton exists at all times.

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
I love it.

## Coroutines

Okay hotshot. Coroutines are your new best friend. They are the polite cousin of the Update loops bundled with Unity. They are used in Unity by creating a IEnumerator method.

Coroutines can patiently wait durations of time, and will function asynchronously - kinda like a pseudo thread - so that if they get held up, the rest of your code will continue to fly by. They are perfect for sequencing events in cutscenes, or doing large tasks over a dilute period of time.

You can make a custom loop which only updates every 20 seconds if you wanted to, or simply mimic the Update loop without hurting the buttery smoothness of your Camera transforms thanks to asynchronicity! :100:

As you'll discover, using `yield return` is one of coroutines' most powerful tools for sequencing and looping. The idea is that a `yield return` keyword will *wait* for whatever is to the right of it to finish, and then *it will continue from where it was yielding*. The implications of this are pretty neat...

### Custom Intervals

If you've ever had to do a complex piece of timing - perhaps a cutscene - without any use of animation events and keyframes, you'll know how much of a nightmare manual timing of events can be within an `Update()` or `FixedUpdate()` loop. 

<details><summary>It looks a little something like this. (Click to expand.)</summary><br>
    
```c#
float timer = 0;
int thingsDone = 0;
private void FixedUpdate() {
    // Iterate timer.
    timer += time.deltaTime;

    // Begin terrible complicated series of conditionals...
    if (thingsDone >= 4) return; // If the sequence is already done, don't do any more code.

    // Otherwise...

    if (thingsDone == 0) {
        if (timer > 2f) {
            doThing1();
            thingsDone++;
        }
    } else if (thingsDone == 1) {
        if (timer > 4f) {
            doThing2();
            thingsDone++;
        }
    } else if (thingsDone == 2) {
        if (timer > 5f) {
            doThing3();
            thingsDone++;
        }
    } else { // has done 3 things, and needs one more.
        if (timer > 5.5f) {
            doThing4();
            thingsDone++;
        }
    }
}

```
</details><br>

If you looked at the collapsed snippet above, you are probably dry heaving, so let's put a blanket on you and take a look at the much better coroutine alternative:

```c#

private void Start() {
    // Start it once.
    StartCoroutine(oddlySpecificWaitRoutine());
}

private IEnumerator oddlySpecificWaitRoutine() {

    Debug.Log("This happens instantly...")

    yield return new WaitForseconds(2f);
    doThing1();
    
    yield return new WaitForseconds(2f);
    doThing2();
    
    yield return new WaitForseconds(1f);
    doThing3();
    
    yield return new WaitForseconds(0.5f);
    doThing4();
    
    yield return new WaitForEndOfFrame();
    Debug.Log("This happens at 5.5 seconds + 1 frame...")
    
    yield break; // Exits the coroutine explicitly. (I do this a lot just to mentally mark the end of a coroutine and to explicitly ensure it ends.)
}
```

Amazing! Efficient. Easy to read. No confusing nesting at all. Additionally, this happens asynchronously, which - unless you're doing very graceful frame-dependent operations - is basically always wanted.

### Custom Loops

Now, maybe you discover your `Update()` method is getting bogged down by a very heavy process every frame. One way to solve this issue is to take your heavy method and put it into an asynchronous and infrequent loop. This is another of coroutines' strengths.

```c#

private void Start() {

    // Start a coroutine!
    StartCoroutine(predictTsunamisInPacific());
}

// This update loop shouldn't be used for heavy lifting.
private void Update() {

    // This needs to happen without a hitch.
    moveCamera();
    
    // We've commented this out here.
    // predictTsunamisInPacific(); 
}

// Instead move it to a coroutine.
private IEnumerator tsunamiPredictionLoop() {
    while (tryingToSaveLives) {
        
        // This will take however long it needs, and won't hitch our moveCamera() method.
        predictTsunamisInPacific();
        
        // And you can even make it wait 20 seconds between loop iterations.
        yield return new WaitForSeconds(20f);
    }
}
```

The key here is to inject a `while` loop into your coroutine, and then **limit** this coroutine by forcing it to Wait before returning to the beginning of the loop.

What happens if we forget to wait?


```c#
private void Start() {
    // Uh oh...
    StartCoroutine(terribleIdea());
}

private IEnumerator terribleIdea() {
    while (true) {
        // Literally anything.
    }
}

```
You've just froze Unity. The problem isn't necessarily the `(true)` - I've done a few loops which need to persist unconditionally, and you can always call a `yield break` within the loop or a `StopAllCoroutines()` within the same Monobehaviour script to stop the loop.

More accurately, the issue is the lack of an appropriate `yield return` statement which necessitates the passage of time or frames. Your loop is essentially trying to compute an indefinite amount of work with no regard for any of its script friends. It will hog the CPU so intensely that every other Unity script within the application will freeze in fear.

### Nesting

You can also wait for *other* coroutines.

```c#

private void Start() {
    StartCoroutine(BananaCutscene()); // Takes maybe 8-10 seconds to finish.
    Debug.Log("I play on the first frame!"); // But since Start is a normal function, it will continue onward instantly to this line.
}

// Gets called on start.
private IEnumerator BananaCutscene() {

    // Plays entirety of line before continuing.
    yield return StartCoroutine(Wizard.SayLine("thanks_for_banana"));
    
    // Again, plays whole clip before continuing.
    yield return StartCoroutine(Monkey.SayLine("whatever"));
    
    // This one doesn't have a 'yield return' so the BananaCutscene routine will *not* wait for this one to finish.
    StartCoroutine(Wizard.SayLine("its_a_very_sweet_juicy_banana"));
    
    // Instead this line will interrupt Wizard.
    yield return StartCoroutine(Monkey.SayLine("ok_bye_creep"));
    
    // Even though the conversation was started by Start() before the first debug message, this line will log after it.
    Debug.Log("I play after like 8-10 seconds of dialogue!");
    
    yield break; // Exits the coroutine explicitly.
}
```

You'll be using lots of `yield return WaitForSeconds(float)` so it's good to optimize them nicely using the following resource saver:  

```c#
// Create a reference to a single public Wait() object for each length of wait time you'll need. 
// Store this reference in the GameManager script. Accessible through GameManager.instance.myWait.
public WaitForSeconds myWait = new WaitForSeconds(1f);

// Coroutines throughout your project you can call
yield return GameManager.instance.myWait;
// To have the coroutine wait one second.
```
* This will cut down on memory and computation of having multiple parallel "WaitFor's", helping optimization.
* Caching these yields works with `WaitForSeconds(float)`, `WaitForFixedUpdate()` (which waits for the Physics loop Fixed frame), and `WaitForNextFrame()` (which waits for the next normal `Update()` frame).

## Enumerators

Forget what we said about coroutines, Enums are going to be your new **bester** friends.

They're essentially just numbers with names, which means you can make checks more clear and easy to understand. *Computationally they're just integers* (very light), but to your eyes they have nice word-names! (Wow!)

This means in the future you can avoid checking if an object exists on a layer with `LayerMask.NameToLayer("GrossString")`. This fucking method compares a complex data type with no regard for our performance. Don't use strings for IDing things ever again! use Enums instead! They're just integers! But they're kinda not!

Here's an example of a perfect utilization - keeping track of the indices of your layers.

Let's start with a BAD piece of code. I've commented the badness so you know how bad it is.

```c#
if (gameObject.layer == 10) // What is this???!!!! Might've been clear when you wrote it, but not after 3 months.
{
    // Do something but terribly.
}
```
Yikes. So I'm glad we're done with that code. I don't know what that 10 is supposed to be. That could be any layer, and honestly I'm too lazy to check the Layer list in Unity.

Let's use our **enumerator** for this next bit. First let's define it:

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
And now instead of that BAD chunk of code, we make this GOOD chunk of code.

```c#
if (gameObject.layer == (int)Layer.Environment) // Oh, it's the Environment layer. Remember to cast to int! (Visual Studio will remind you.)
{
    // Do something but sexy.
}
```

It also has the added bonus that if your layer indexes get shifted, you only have to modify the Enumerator's definitions, and not every occurance throughout the project. Yay! You can even rename a given layer to something else and the index will stay the same. *If you did this using strings you'd have to change every occurance of the string. (!)*

### Worthwhile Resources

* [Polymorphism](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/polymorphism)  
* [Delegates](https://unity3d.com/learn/tutorials/topics/scripting/delegates)  
* [Asynchronus tasks + Coroutines](https://docs.unity3d.com/Manual/Coroutines.html)

#### [< Back to Index](readme.md)
