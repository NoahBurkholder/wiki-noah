#### [< Back to Index](readme.md)

# :coffee: Code

Game programming rewards creativity in code, and games are systemically different enough that you'll often run into problems that don't have precedented soltutions. You will constantly run into challenges which don't have a concrete answer.

You don't need to know much math, or crazy algorithms. You don't need to know system architectures. It's mostly just creative problem-solving and creative problem-creating. The problem-creating part is also kind of unique to games, since typically games don't have a point besides (usually) fun - they are self-contained, and the technical challenges within are motivated by you, the designer.

The aim of this page isn't to teach the basics. This is relatively advanced techniques for making competitive code. **If you can use these, you can already compete with many of game developer professionals I know.**

## :notes: C#

This is what every Unity programmer I know unquestionably uses. Even if they have other favourite languages, they know C# because it is the common language of Unity devs.

Writing in C# in Unity is a lot like writing music with a score. It is a toolset which looks and operates objectively, but is used (at least in our context) to create subjective things. It needs to be flexible enough to let programmers get away with creative but sloppy prototyping, yet robust enough to enforce technical efficiency. Perfect for game development.

**If you know Java**, C# is basically just Java but a little *less* confusingly arbitrary and noisy. It also is developed by Microsoft so it has good integration with Windows. Very easy to interface with the OS.

Great language! Any Unity code snippets you find online will probably use C# as the basis.

Anyways - on to some actual code information:

## General Practice

### Code Intuition

Most of the time it's really hard to know for sure the **cost** of lines of code. Here's some rules of thumb for choosing the best variable types and discerning the computation cost of methods:

1. **Bools** are the lightest, always. However, they suffer from scalability problems.
    1. Ex. If you have two game states, playing and not playing, you might consider using an integer anyways, so that if you ever create a third game state, you don't have to restructure any code.
2. **Integers** are the gold standard for *performance **and** scalability*. They are super damn light, but still have a lot of flexibility due to the min and max values they can contain. (In our case, +/- 2,147,483,647).
3. **Floats** aren't actually very slow for modern machines. You can use them willynilly and it shouldn't be an issue unless you're really misusing them. The main thing to watch out for is expending extra resources to round numbers, or do approximations as a limitation born of the variable type.

4. **Chars** are reasonably light, but typically they're only used in the context of their big brother...
5. **Strings**. These are perhaps the least-responsibly used of all the native C# data types.

#### A Quick Rant About Strings

Humans love strings because they are familiar. We spend our whole life dealing with strings. *Unfortunately*, although both humans and computers can use strings - they do so in completely different ways.

**Computers** look at strings as ordered arrays of single-character data. Their toolsets parse strings as just that:  
`Strings` are arrays of `characters`, and computers process them using `indices`.  

Example:

```c#

    // This single string...
    string someString = "Banana";

    // ...is more-or-less equal to these 6 characters in an array (as far as the computer is concerned).
    char[] sameString = new char[] { 'B', 'a', 'n', 'a', 'n', 'a' };

    // 1. The string is totally arbitrary.
    // 2. There is no symbolic meaning.
    // 3. The string "Banana" is no more special meaning than "bbbbbb" to the computer.
    // 4. Every string is read on a character-by-character basis.

```

This is not how humans think about strings.

**Humans** use strings as holistic symbols or identifiers, because we're pattern-based creatures.  
`Strings` are `words` or `sentences` which inherently represent things we have memory of using our `alphabet`, and we process them on a `word` basis.  

Example:

`"Banana" is a single thing - a word - which I recognize, and it inherently represents this object over here.`

This introduces a **language barrier** between how humans and computers think about the same data type. Humans will often wrongly structure their code to use strings as identifying tokens, because we have a linguistic bias. Logically they contain way too much data for this task, and computers get stuck with a very unwieldy, bloated data type post-compilation. Computers would use an integer to the same end.

<details><summary>Additionally (and I'm gonna get a little bit technical here, so click to expand):</summary><br>
    
Humans will also underestimate the <i>power</i> of strings because we think in terms of words and the alphabet. We often neglect numerical and special characters in strings as ways to encrypt or compress data. And the seriality of strings means we can use them as a powerful way to record and read data, especially as a way to pass data <i>between languages</i>. They aren't necessarily as efficient as using serial binary data, but the added readability means every step of the way there is an ounce of understandability for the developer. 

Ex. Passing the data `"d*4L27*A*72##39a874AAA8749FF00@7847"` into your game from another program means you can identify there are - for instance - two `#`'s adjacent to each other, which may be helpful information for you, whereas if it were all 1s and 0s you'd maybe not recognize that pattern without some careful analysis. This is very comp-sci though, so I don't expect you'll find this relevant or interesting.
</details><br>
Use strings responsibly.

#### Applying Code Intuition

When you're thinking of ways to solve a problem, think about how you can cut down on complex data types and operations, while keeping your code's readability high, and the scalability high. In other words, identify where your code is weakest (performance, scalability, readability), and attempt to remedy that weakness.

[Enumerators](#enumerators) are a gold nugget for improving **all three aspects** with basically no drawbacks.

> Think about every line of code as having a cost (because it does), and hypothesize about what that cost might be. You'll begin to get an intuition about what good code is.

**As a programmer, you will often have to interface with others' code.** You can critique others' code very quickly just by looking at the data types they are using. This includes Unity's built-in methods.

#### Examples of Code Intuition

`GameObject.Find(string objectName)` inputs a string, telling us that this method is probably quite heavy. We can also infer that it might be navigating the scene hierarchy scouring for your GameObject. This is bad, and I'd be wary of using this method.

`gameObject.transform.GetChild(int index)` does a similar thing to above - however, it's an instanced method (it must be run on a specific instance - notice the lower-case 'g' on `gameObject`).  We can infer by the name of the method 'GetChild' that this search will be localized to the children of the gameObject instance this was run from. Additionally, we see it inputs an index instead of a name. This implies instead of comparing strings, it is merely going through the children sequentially as they are ordered in the hierarchy. No string comparison is happening. (Yay!)

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

Now, you can basically forget about needing to make a reference to your manager object constantly. Instead, without making a reference, you can just type `GameManager.instance.aNonStaticVariable`. This instance reference is static, but specific to a single instanced version of your manager. This means your variables/members inside the class can be used like any other, from any other place, with no issue.

## Coroutines

Okay hotshot. You like loops? Well, coroutines are about to be your new best friend. They are the polite cousin of the `Update` loops bundled with Unity. They are used in Unity by creating a method returning the IEnumerator class.

Coroutines can patiently wait durations of time, and will function asynchronously - kinda like a [pseudo thread](#threading) - so that if they get held up, the rest of your code will continue to fly by. They are perfect for sequencing events in cutscenes, or doing large tasks over a dilute period of time.

You can make a custom loop which only updates every 20 seconds if you wanted to, or simply mimic the Update loop without hurting the buttery smoothness of your Camera transforms thanks to asynchronicity! :100:

### And Before You Ask...

1. There is *no hard limit* to the number of coroutines you can have.
    1. Like the number of update loops running concurrently, your coroutines will scale nicely into the hundreds and even thousands.
    2. Like update loops, each coroutine has a small instance overhead to be aware of.
    3. *Fun fact: it's much more efficient to have a single update loop update 1000 objects than 1000 objects updating in their own loop.*
2. Coroutines are more efficient *90% of the time* when regular intervals are required.
    1. The only exception is looping *every* frame.
3. Coroutines are more efficient *100% of the time* when any irregular timing is involved.
    1. Coroutines are also more understandable to programmers 100% of the time when any irregular timing is involved.
4. If you want **synchronicity**, this is one of the only times you'll deliberately choose an update loop.

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

Amazing! Efficient. Easy to read. No confusing nesting at all. Additionally, this happens asynchronously, which - unless you're doing very graceful frame-dependent operations - is basically always wanted. And - amazingly - we're also not checking four conditionals every frame. *Conditionals can stack up if you're doing them every frame.*

### Custom Loops

Now, maybe you discover your `Update()` method is getting bogged down by a very heavy process every frame. One way to solve this issue is to take your heavy method and put it into an asynchronous and infrequent loop. This is another of coroutines' strengths.

```c#

private void Start() {

    // Start a coroutine!
    StartCoroutine(predictTsunamisInPacific());
}

// We can assume that this update loop shouldn't be used for heavy lifting, because...
private void Update() {

    // ...this needs to happen without a hitch.
    moveCamera();
    
    // We've commented this call out, here. It was slowing down Update() which meant our moveCamera() script was stuttering.
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

What happens if we forget to wait? If we forget to **limit**?


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
You've just froze Unity. The problem isn't necessarily the `(true)` - I've done many-a loops which need to persist unconditionally, and you can always call a `yield break` within the loop or a `StopAllCoroutines()` within the same Monobehaviour script to stop the loop.

More accurately, the issue is the lack of an appropriate `yield return` statement which necessitates the passage of time or frames. Your loop is essentially trying to compute an indefinite amount of work with no regard for any of its script friends. It will hog the CPU so intensely that every other Unity script within the application will freeze in fear.

The only reason this doesn't bluescreen Windows is because there are extensive layers of script-safety preventing memory allocation issues and a multitude of short-circuiting scripts. Basically Unity is self-contained and very high-level in comparison.

### Nesting

You can also wait for *other* coroutines.

```c#

private void Start() {

    // The coroutine below takes maybe 8-10 seconds to finish.
    StartCoroutine(BananaCutscene());
    
    // But since BananaCutscene() is merely sent rolling with a small push, Start() will continue onward instantly to this line.
    // BananaCutscene() will go at its own pace, and Start() isn't responsible for it anymore.
    Debug.Log("I play on the first frame! I - the Debug Log - have not waited for this terrible cutscene to finish!");
    
}

// Gets called on start.
private IEnumerator BananaCutscene() {

    // The 'yield return' below will play the entirety of a line-reading coroutine before continuing.
    yield return StartCoroutine(Wizard.SayLine("behold_my_great_golden_banana"));
    
    // Again, the below will play the whole clip before allowing the script to continue.
    yield return StartCoroutine(Monkey.SayLine("whatever_chump"));
    
    // This one doesn't have a 'yield return' so the BananaCutscene routine you're reading will *not* wait for this one to finish.
    StartCoroutine(Wizard.SayLine("curse_you_monkey_you_never_respect_my_magic"));
    
    // Instead this line will interrupt the Wizard line above.
    yield return StartCoroutine(Monkey.SayLine("im_leaving_to_go_find_babes"));
    
    // Even though the conversation was started by Start() before the first debug message, this line will log after it.
    Debug.Log("I play after like 8-10 seconds of terrible horrible dialogue!");
    
    // Exits the coroutine explicitly. Again. This is useful for the programmer mostly. It will exit regardless.
    // Typically 'yield break' is the first thing I write in a coroutine because if there aren't any yields it will throw an error.
    yield break; 
}
```

### Cache To Kill Garbage

You'll be using lots of `yield return new WaitForSeconds(float)` so it's good to - instead of creating a `new` return - cache one of them, and recycle it:  

```c#
// Create a reference to a single public Wait() object for each length of wait time you'll need. 
// Store this reference in the GameManager script. Accessible through GameManager.instance.myWait.
public WaitForSeconds myWait = new WaitForSeconds(1f);

// Coroutines throughout your project you can call
yield return GameManager.instance.myWait;
// To have the coroutine wait one second.
```
* This will cut down on memory and computation of having multiple parallel "WaitFor's", helping optimization.
* It targets the biggest drawback of these returns - garbage collection (GC), which can hurt framerates.
* Caching these yields works with `WaitForSeconds(float)`, `WaitForFixedUpdate()` (which waits for the Physics loop Fixed frame), and `WaitForNextFrame()` (which waits for the next normal `Update()` frame).

## Enumerators

Forget what we said about coroutines, Enumerators (Enums) are going to be your new *bester* friends.

They're essentially just numbers with names, which means you can make checks more clear and easy to understand. *Computationally they're just integers* (very light), but to your eyes they have nice word-names! (Wow!)

This means in the future you can avoid checking if an object exists on a layer with `LayerMask.NameToLayer("GrossString")`.

Okay. I'm just gonna stop for a second and be angry because this fucking method compares a compound data type with no regard for our performance. Don't use strings for identifying things ever again! Use Enumerators instead! They're just integers! But they're kinda not!

Here's an example of a perfect utilization - keeping track of the indices of your layers.

For those of you who don't know - [Unity](unity.md) keeps track of your game layers using integers, because it's very efficient. These indices - the first 7 of which are reserved - are tied to your layer, and the name of it which you assign and interface with as a designer in the inspector.

Let's start with a **bad** piece of code. I've commented the badness so you know how bad it is.

```c#
if (gameObject.layer == 10) // What is this???!!!! Might've been clear when you wrote it, but not after 3 months.
{
    // Do something but terribly.
}
```
Yikes. So I'm glad we're done with that. I'm looking at that code and I still don't know what that 10 is supposed to be. That could be any layer, and honestly I'm too lazy to check the Layer list in Unity. You probably are too! I always click the wrong dropdown item and get lost and confused.

Let's use an **enumerator** for this next bit. First let's define it:

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
And now instead of that *bad* chunk of code, we make this **good** chunk of code.

```c#
if (gameObject.layer == (int)Layer.Environment) // Oh, it's the Environment layer. Remember to cast to int! (Visual Studio will remind you.)
{
    // Do something but sexy.
}
```

It also has the added bonus that if your layer indexes get shifted, you only have to modify the Enumerator's definitions, and not every occurance throughout the project. Yay! You can even rename a given layer to something else and the index will stay the same. *If you did this using strings you'd have to change every occurance of the string. (!)*

## Threading

(Coming soon!) Regarding sending jobs to other threads on the CPU, and the limitations of game engines and synchronicity in this regard.

## Events and Delegates

(Coming soon!) Regarding the efficient utilization of events and delegating for rare callbacks which shouldn't be called every frame.

## Worthwhile Resources

* [Polymorphism](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/polymorphism)  
* [Delegates](https://unity3d.com/learn/tutorials/topics/scripting/delegates)  
* [Asynchronus tasks + Coroutines](https://docs.unity3d.com/Manual/Coroutines.html)

#### [< Back to Index](readme.md)
